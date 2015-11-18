**API Developer Guide version 1**

> **Important Information about this version**

> *Razuna 1.5 features a new improved version of the API! For legacy issues, we still leave this version of the API around, but developers should [develop against version 2 of the API!](/api/)*

___

**Web Service Overview**

*Web Services can be defined as software designed to support interoperable Machine-to-Machine interaction over a network. Web Services are frequently Web APIs that can be accessed over the Internet and executed on a remote system hosting the requested services. The definition encompasses many different systems, but in common usage and throughout this document the term refers to clients and servers that communicate using XML messages that follow the SOAP or REST standards. Common in both the field and the terminology is the assumption that there is also a machine readable description of the operations supported by the server, often referred to as a Web Services Description Language (WSDL). The latter is not a requirement of SOAP endpoint, but it is a prerequisite for automated client-side code generation in the mainstream Java and .NET SOAP frameworks. Some industry organizations, such as the WS-I, mandate both SOAP and WSDL in their definition of a Web service.*

*The specifications that define Web Services are intentionally modular, and as a result there is no one document that contains them all. Additionally, there is neither a single, nor a stable set of specifications. There are a few "core" specifications that are supplemented by others as the circumstances and technologies dictate, including:*

*SOAP: An XML-based, extensible message envelope format, with "bindings" to underlying protocols. The primary protocols are HTTP and HTTPS, although bindings for others, including SMTP and XMPP, have been written.*

*WSDL: An XML document that allows service interfaces to be described, along with the details of their bindings to specific protocols. Typically used to generate server and client code, and for configuration.*

*Most of these core specifications have come from W3C, including XML, SOAP, and WSDL.*

___

**Calling Razuna Web Services**

*The SOAP and REST protocols are used for transmission of the data and methods in this document. The SOAP protocol allows for simple integration with most languages and development systems. You can learn more about SOAP at [http://en.wikipedia.org/wiki/SOAP](http://en.wikipedia.org/wiki/SOAP). For more information about REST you can visit [http://en.wikipedia.org/wiki/Representational_State_Transfer](http://en.wikipedia.org/wiki/Representational_State_Transfer).*

> **Razuna SaaS Platform** : *The URL for Razuna API's is: api.razuna.com. You can also use the host name of the account. Example: If your hostname is "demo" the URL would be demo.razuna.com*

___

**SOAP**

*To call our web service your client must be able to consume our WSDL file. Most programming and scripting languages have tools that facilitate consuming a web service. Generally, when your developer toolkit inspects the WSDL file it will auto-generate programming code that interfaces with the Web Services.*

*Sample Call:*

```
Authentication auth = new Authentication();
string sessionToken = auth.Login(appKey, userName, password);
```

*Sample CFML Call:*

```
<cfinvoke webservice ="http://api.razuna.com/global/api/authentication.cfc?wsdl"
method="login"
hostid="1"
user="admin"
pass="admin"
returnVariable="xml">
```
*When an API method is called, a response is returned to the caller in XML format. The content type of the response will be "text/xml".*

___

**REST**

*API Method Request Format: API methods are encapsulated by web pages within the API web site. To call a method, make a POST or GET request to the web page corresponding to the method you want to execute.*

*Sample URL:*

```
http://api.razuna.com/global/api/authentication.cfc?method=login&hostid=1&user=admin&pass=admin
```

*Sample CFML Call:*

```
<cfhttp url="http://api.razuna.com/global/api/authentication.cfc">
 <cfhttpparam name="method" value="login" type="url">
 <cfhttpparam name="hostid" value="1" type="url">
 <cfhttpparam name="user" value="admin" type="url">
 <cfhttpparam name="pass" value="admin" type="url">
</cfhttp>
```
*When an API method is called, a response is returned to the caller in XML format. The content type of the response will be "text/xml". Specifically, the response will be a WDDX packet. You can read up on the WDDX at Wikipedia.*

___

**Available API Calls**

The following API sections are available:

 * [Authentication API1](/api old/Authentication API1)
 * [Folder API1](/api old/Folder API1)
 * [Collection API1](/api old/Collection API1)
 * [Search API1](/api old/Search API1)
 * [Upload API1](/api old/Upload API1)
 * [Hosts API1](/api old/Hosts API1)
 * [User API1](/api old/User API1)
 * [Asset API1](/api old/Asset API1)

___

**API Requests**

*Requests to extend the Razuna API are welcomed. Please submit your request over at our public Request system at [http://issues.razuna.com](http://issues.razuna.com).*



