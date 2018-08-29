# Installation and tutorial

## Prerequisites

1. Install OpenJDK-8 -- Java Development Kit. For Debian/Ubuntu:
```
$> sudo apt-get install openjdk-8-jdk
...
$> java -version
openjdk version "1.8.0_162"
OpenJDK Runtime Environment (build 1.8.0_162-8u162-b12-1~bpo8+1-b12)
OpenJDK 64-Bit Server VM (build 25.162-b12, mixed mode)
```

# I. mTangoREST.server installation guide

__If you use Windows__, visit Tango docs page with [Waltz (ex. TangoWebapp) installation tutorial](http://tango-controls.readthedocs.io/en/latest/tutorials-and-howtos/tutorials/install-tango-webapp.html)

__If you use Linux__, follow next steps.

1. Download [mTangoREST.server-rc4-2.7.jar](https://github.com/Ingvord/mtangorest.server/releases/download/mtangorest.server-rc4-2.7/mtangorest.server-rc4-2.7.jar). Save it in folder where you keep your Tango server executable files (possibly where Starter device can find it), e.g. /home/user/bin.
2. Next to the downloaded _.jar_ create a bash script with the name __TangoRestServer__ (this name is important for the future integration with Astor and other Tango tools) and put there

```bash
#!/bin/bash

echo "Using TANGO_HOST=$TANGO_HOST"

USERNAME=`whoami`
echo "Using USERNAME=$USERNAME"

#enable debug
JAVA_OPTS="-Xmx4G -Xshare:off -XX:+UseG1GC -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5009"
echo "Using JAVA_OPTS=$JAVA_OPTS"

/usr/bin/java -jar $JAVA_OPTS -DTANGO_HOST=$TANGO_HOST /home/$USERNAME/bin/mtangorest.server-rc4-2.7.jar -nodb -dlist test/rest/0
```

3. To make this file executable, in Terminal go to the folder and execute
```
$> chmod 777 TangoRestServer
```
4. Start Tango REST Server by
```
$> ./TangoRestServer
```
5. To test, open new Terminal and execute
```
curl -u "tango-cs:tango" http://localhost:10001/tango/rest/rc4
```



# II. Waltz (ex. TangoWebapp) installation guide

1. Download and extract [Apache Tomcat 8.5.31](https://tomcat.apache.org/download-80.cgi#8.5.31) (_.zip_ – for Windows, _.tar.gz_ – for Linux) in your folder with REST.

2. Download _.war_ file of [Waltz v0.4.2](https://github.com/tango-controls/tango-webapp/releases/download/v0.4.2/TangoWebapp.war) into /home/user/bin/apache-tomcat-8.5.31/webapps/

3. Start Tomcat in Terminal
```
$> cd apache-tomcat-8.5.31/bin/
$> ./startup.sh 
```
4. Open browser and go to http://localhost:8080/TangoWebapp
* login: tango-cs
* pass: tango

Get an error because have to connect to Tango Controls.

5. Set a valid Tango Host. In Waltz go to _Setting_ tab (1) -> _Tango hosts_ box -> put __your__ Tango host -> press "+" (2)

![installation_add tango host](images/installation_client_15.png)

# III. IDE Setup

This section describes how to setup [IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/download/download-thanks.html?platform=linux) for developing using Waltz (ex. TangoWebapp) platform. Setup for other IDEs should be the same in general.

1. Clone Waltz (ex. TangoWebapp):
```
$> git clone git@github.com:tango-controls/tango-webapp.git
```

OR using https (if you have no github account):

```
$> git clone https://github.com/tango-controls/tango-webapp.git
```

This will create **tango-webapp** folder in the current folder.

2. Open intelliJ IDEA and start a new project using existing source (_File_ -> _New_ -> _Project from existing source..._) and choose cloned tango-webapp folder.

3. Add an artifact to your project: _File_ -> _Project Structure..._

Add a new artifact "+" -> _Web Application: Exploded_ and add **tango-webapp** as _Directory content_ to the artifact:

![](images/installation_ide_3.png)

4. Once new project has been created let's setup Apache Tomcat. Select _Run_ -> _Edit configurations..._

Add a new local Tomcat run configuration:

![](images/installation_ide_1.png)

Setup a new Tomcat application server - just add Apache Tomcat base folder (the one you extracted in _I. mTangoREST.server installation guide_)

![](images/installation_ide_2.png)

Next you need to add TangoWebapp artifact to Tomcat: open _Deployment_ tab and add artifact:

![](images/installation_ide_4.png)

Set context - this is what defines URL at which Waltz will be accessible e.g. `http://localhost:8080/WaltzDev`:

![](images/installation_ide_6.png)

Finally switch back to _Server_ tab and choose _Update classes and resources_ on _Frame deactivation_:

![](images/installation_ide_5.png)

the later will allow source update on the fly i.e. changes to _.js_ files will be fetched by Tomcat automatically once you switch to the browser.

5. Finally set JavaScript language flavour to Nashorn: _File_ -> _Settings..._ -> put _javascript_ into search box -> _Languages & Frameworks_ -> _JavaScript_ -> select _Nashorn JS_ in the drop-down list

![](images/installation_ide_16.png)

Now IntelliJ IDEA is ready for development.




- - - - - - - - - - - - - - - - - -
## More information:

Tango Controls docs - [Tango REST API](http://tango-controls.readthedocs.io/en/latest/development/advanced/rest-api.html)
