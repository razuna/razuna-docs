**Recommended MySQL Settings**

Depending of your MySQL Server setup (if it is a dedicated server or not) there are different my.cnf files you should deploy.

Since Razuna is using the InnoDB Engine for it databases you should apply some specific InnoDB settings to the MySQL Server. If you don't know InnoDB here is a short description;

> InnoDB provides MySQL with a transaction-safe (ACID compliant) storage engine that has commit, rollback, and crash recovery capabilities. InnoDB does locking on the row level and also provides an Oracle-style consistent non-locking read in SELECT statements. These features increase multi-user concurrency and performance.

You can find out more on [InnoDB at the official MySQL InooDB documentation](http://dev.mysql.com/doc/refman/5.0/en/innodb-overview.html).

___

**Adding specific InnoDB settings**

*For the best performance for Razuna you should add/modify the following settings to the my.cnf file:*

```
server_id                               = 1
log_bin                                 = mysql-bin
expire_logs_days                        = 10
max_binlog_size                         = 100M
binlog_do_db                            = include_database_name
binlog_ignore_db                        = include_database_name
sync_binlog                             = 1
innodb_open_files                       = 500
innodb_file_per_table
innodb_buffer_pool_size                 = 400M
innodb_flush_log_at_trx_commit          = 1
innodb_thread_concurrency               = 8
innodb_lock_wait_timeout                = 500
interactive_timeout                     = 300
back_log                                = 75
thread_cache                            = 32
wait_timeout                            = 300
connect_timeout                         = 10
innodb_flush_method                     = O_DIRECT
```

This ensures that the MySQL Server behaves the most efficient way in regards to InnoDB tables. We have run this settings at different production setups and have had very good feedback from customers.

Make sure that you restart the MySQL server to apply the above settings.





