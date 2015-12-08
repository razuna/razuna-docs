**Monitoring Razuna (CF Server) with Nagios**

___

**Monitoring of ColdFusion with Nagios**

**For Windows**:

First, you will need to install the [NRPENT daemon](http://www.miwi-dv.com/nrpent/) on each of the Windows servers you have running CF. Follow the instructions within the zip to install. It just works.

**Add Coldfusion host to hosts.cfg**

If your CF servers are not already among the hosts you are monitoring, add them to hosts.cfg. A typical host definition looks similar to the one below.

```
define host {
     use                   generic-host
     host_name             cfserver1
     alias                 main coldfusion server
     address               172.16.3.129
     parents               Internet_Zone
     check_command         check-host-alive
     max_check_attempts    3
     notification_interval 60
     notification_period   24x7
     notification_options  d,u,r
}
```

**Add host groups for your Coldfusion server**

Assuming all your CF servers are running the same CF version, you can make a Nagios host group for those servers. This is much less work than adding individual servers to the service check (detailed below). If you have servers running disparate CF versions, set up a host group for each. Add your host group defintion to hostgroups.cfg. A typical host group definition looks similar to the one below.

```
define hostgroup {
     hostgroup_name cfmxservers
     alias          MCT ColdFusion MX Servers
     contact_groups webdev online
     members        cfserver1, cfserver2, cfserver3
}
```

**Add Coldfusion commands to checkcommands.cfg**

In a default Nagios installation, checkcommands.cfg contains all the definitions of the commands Nagios uses to inspect services running on the hosts it monitors. The following list of command definitions should cover ColdFusion 7 (and will likely also cover other versions (not checked)). Add the following lines to checkcommands.cfg.

```
define command {
   command_name    check_coldfusion5
   command_line    $USER1$/check_nt -H $HOSTADDRESS$ -p 1248 -v SERVICESTATE -l "Cold Fusion Application Server"
}
 
define command {
   command_name    check_coldfusionjrun
   command_line    $USER1$/check_nt -H $HOSTADDRESS$ -p 1248 -v SERVICESTATE -l "Macromedia JRun CFusion Server"
}
 
define command {
   command_name    check_coldfusionmx
   command_line    $USER1$/check_nt -H $HOSTADDRESS$ -p 1248 -v SERVICESTATE -l "ColdFusion MX Application Server"
}
 
define command {
   command_name    check_coldfusionmx_process
   command_line    $USER1$/check_nt -H $HOSTADDRESS$ -p 1248 -v COUNTER -l "\\Process(jrun)\\Private Bytes","JRun is using %.f bytes" -w 891289600 -c 1073741824
#   comment    Warning 850Mb, Critical 1024Mb (1Gb) YMMV
}
 
define command {
   command_name    check_coldfusionmx_threads
   command_line    $USER1$/check_nt -H $HOSTADDRESS$ -p 1248 -v COUNTER -l "\\Process(jrun)\\Thread Count","JRun is using %.f Threads" -w 90 -c 110
#   comment    Warning 90 threads, Critical 110 threads YMMV
}
```

The last two commands in the above listing check actual CF processes running on the server. Note the comments. The values we use may well be very different in your environment. The easiest way to check is to have a look at what your servers are doing and make an educated guess at the needed levels in your setup. No harm done if you use these values, you just may end up getting copious notifications from Nagios that you do not need (or conversely, no notifications at all). Test and tweak.

**Adding CF-??related services to services.cfg**

Nagios monitoring model is centered on the concept of services, so this step is perhaps one of the most important. You need to add service definitions to services.cfg for each of the command definitions you built earlier. A couple of sample service definitions are shown below.

```
define service {
    use                   NM-HTTP
    hostgroup_name        cfmxservers
    service_description   Check ColdFusion MX
    contact_groups        online,webdev
    check_period          24x7
    notification_interval 60
    notification_options  w,u,c,r
    notification_period   24x7
    check_command         check_coldfusionmx
    max_check_attempts    3
    normal_check_interval 1
    retry_check_interval  1
#   comment    Check if ColdFusion MX Server is responsive
}
 
define service {
    use                   NM-HTTP
    hostgroup_name        cfmxservers
    service_description   Check ColdFusion MX Process Threads
    contact_groups        webdev online
    check_period          24x7
    notification_interval 60
    notification_options  w,u,c,r
    notification_period   24x7
    check_command         check_coldfusionmx_threads
    max_check_attempts    3
    normal_check_interval 1
    retry_check_interval  1
}
```

**Restart Nagios**

At this point, Nagios should be ready, willing and able to monitor CF on your Windows-??based CF servers. Restart Nagios by whichever method you use. After restarting, if you log into the Nagios web interface, you should be able to see the CF services you set up being monitored.

**ColdFusion installed on Linux**

The above works good for Coldfusion installed on Windows. The below steps should help to get it going when Coldfusion is installed on Linux, but has not been tested!

Use "pstree" command in bash script: 

```
/usr/local/bin/coldfusion-threads-snmp.sh
```

This will print a CFChildren variable like:

```
CFChildren='/usr/bin/pstree | grep -e cfmx7.*cfmx7.*cfmx | sed -e 's/\*\[cfmx7\]$//' -e 's/? *..cfmx7.*.cfmx7...//''
```

and the results of the script can be exported within snmp; an entry in snmpd.conf like:

exec .1.3.6.1.4.1.2021.500 coldfusion-??threads /usr/local/bin/coldfusion-threads-snmp.sh will do it. 

