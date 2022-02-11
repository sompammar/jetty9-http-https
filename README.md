# Jetty Configuration for http to https
## jetty9-http-https

- Download jetty from https://www.eclipse.org/jetty/download.php
- unzip/untar

## Initialization of jetty-base
```
mkdir my-base
export JETTY_HOME=~/jetty
cd my-base
      
java -jar $JETTY_HOME/start.jar --create-startd
java -jar $JETTY_HOME/start.jar --add-to-start=http,https,deploy


java -jar $JETTY_HOME/start.jar --add-to-start=http,deploy
```

## Configuration
- Uncomment following line from start.d/deploy.ini 
```
jetty.deploy.defaultsDescriptorPath=${jetty.base}/etc/webdefault.xml
```
- Add following entries to etc/webdefault.xml. A sample webdefault.xml file can be copied from {jetty.home}/etc/

```

 <security-constraint>

 <web-resource-collection>

 <web-resource-name>Everything</web-resource-name>

 <url-pattern>/*</url-pattern>

 </web-resource-collection>

 <user-data-constraint>

 <transport-guarantee>CONFIDENTIAL</transport-guarantee>

 </user-data-constraint>

 </security-constraint>

  

 <security-constraint>

 <web-resource-collection>

 <web-resource-name>Internal Info</web-resource-name>

 <url-pattern>/internal/info</url-pattern>

 </web-resource-collection>

 </security-constraint>

  

 <security-constraint>

 <web-resource-collection>

 <web-resource-name>Actuator Info</web-resource-name>

 <url-pattern>/actuator/*</url-pattern>

 </web-resource-collection>

 </security-constraint>

  
 
 ```
 
 This configuration redirects all the requests except health endpoints (e.g. /actuator/ or internal/info) etc.
