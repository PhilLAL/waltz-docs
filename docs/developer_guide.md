We shall start this developer guide with a super short introduction to the basic web technologies which are used in Waltz. 
If you don't need this, please, skip this part and go directly to the Waltz description.

## Short introduction to the basics of Web
Let's start with Client-Server architecture which looks like this at the first glance.

![devGuide_intro_client-serv_1](images/devGuide_intro_client-serv_1.png)

In our case we consider Browser as a Client and if we deep a bit, we get:
![devGuide_intro_client-serv_2](images/devGuide_intro_client-serv_2.png)

Browser via sends HTTP request to a specific URL. 
Server returns HTTP response that represents static/dynamic data on a local server system.

For example, Request URL “http:localhost:8080/jsTangORB/” means jsTangORB folder on the Server which returns as response index.html 
![devGuide_intro_client-serv_3](images/devGuide_intro_client-serv_3.png)

_Apache Tomcat_ (a Java HTTP web server environment) and _Servlet_ (a Java program that extends the capabilities of a server) 
are both middleware. Apache Tomcat binds itself to HTTP port and Servlet transforms API, 
so you don't need to keep in mind socets and ports.
![devGuide_intro_Apache_Tomcat-Servlet_engine](images/devGuide_intro_Apache_Tomcat-Servlet_engine.png)

_REST API_ is philosophy, a set of constraints.

It uses structured requests:
* http://{host}/{app}/{api}/{version}/{collection} e.g. http://localhost:8080/my-app/users
* http://{host}/{app}/{api}/{version}/{collection}/{item} e.g. http://localhost:8080/my-app/users/123
* http://{host}/{app}/{api}/{version}/{collection}/{item}/{sub-collection}

It adds semantic to HTTP methods:
* GET → get resource
* POST → create new resource
* PUT → update resource
* DELETE → remove resource


JAX-RS –  is a Java programming language API specification for server/client side REST implementation. 
Using previous diagrams JAX-RS will take the following place (note annotations on the code):
![devGuide_intro_rest](images/devGuide_intro_rest.png)

**Tango REST API is a RESTful view on Tango Controls.** It is just a SPECIFICATION!!!
http://{host}/{app}/{api}/{version}/{collection}/{item}/{sub-collection} → http://host/tango/rest/rc4/hosts/tango_host/10000/devices

So putting it all together, we get the following diagram:
![devGuide_intro_putting_all_together](images/devGuide_intro_putting_all_together.png)


# Waltz platform

## mTangoREST.server
[mTangoREST.server](https://github.com/ingvord/mtangorest.server) - is a Java implementation of a Tango Controls REST API specification. If you need C++ version, please, visit [RestDS](http://tangodevel.jinr.ru/git/tango/web/RestDS) page.

mTangoREST.server has [two distributions](https://github.com/Ingvord/mtangorest.server/releases): .jar and .zip

The difference is shown in the following diagram:
![mTangoREST.server_jar-zip](images/mTangoREST.server_jar-zip.png)

**.jar**
* For development/small production deployment
* Standalone Tango device 
* Integration with standard Tango tools (Astor)
* Using launch script
* Dokerized

**.war**
* For production deployment:
    - Allows fine Tomcat tuning
    - High load (1K-10K users)
    - Standard enterprise infrastructure
* Embedded Tango device 
    - Configuration in WEB-INF/web.xml


Pipeline of the mTangoREST.server request can be presented like this:
![mTangoREST.server_request_pipeline](images/mTangoREST.server_request_pipeline.png)
Where 
* org.tango.web.server.filters; 

** org.tango.web.server.providers;

*** org.tango.web.server.resolvers, org.tango.web.server.interceptors.

Tango JAX-RS resources - Tango entities (aka device, attribute, commands etc) in mTangoREST.server.
The examples of code structure and Device class are below:
![mTangoREST.server_JAX-RS_resources](images/mTangoREST.server_JAX-RS_resources.png)

If you debug Device.java class, you will see 
![mTangoREST.server_device_class_debug](images/mTangoREST.server_device_class_debug.png)



## Waltz

