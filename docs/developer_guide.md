We shall start this developer guide with a super short introduction to the basic web technologies which are used in Waltz. 
If you don't need this, please, skip this part and go directly to the Waltz description.

## Short introduction to the basics of Web
Let's start with Client-Server architecture which looks like this at the first glance.

![devGuide_intro_client-serv_1](images/devGuide_intro_client-serv_1.png)

In our case we consider Browser as a Client and if we deep a bit, we get:
![devGuide_intro_client-serv_2](images/devGuide_intro_client-serv_2.png)

Browser via sends http request to a specific URL. 
Server returns http response that represents static/dynamic data on a local server system.

For example, Request URL “http:localhost:8080/jsTangORB/” means jsTangORB folder on the Server which returns as response index.html 
![devGuide_intro_client-serv_3](images/devGuide_intro_client-serv_3.png)

Apache Tomcat (a Java HTTP web server environment) and Servlet (a Java program that extends the capabilities of a server) 
are both middleware. Apache Tomcat binds itself to http port and  Servlet transforms API, 
so you don't need to keep in mind socets and ports.
![devGuide_intro_Apache_Tomcat-Servlet_engine](images/devGuide_intro_Apache_Tomcat-Servlet_engine.png)


# Waltz
