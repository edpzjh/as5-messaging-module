# JBoss Messaging module for AS 7
This project assembles a JBoss AS7 module containing the jars required to commuicated with JBoss Messaging running
on a JBoss 5.0.0.GA server.

# Building

    mvn install

# Installing to AS7
    
    unzip target/jboss-messaging-client-AS5.0.0.GA-module.zip -d $AS7_HOME/modules
    
# Client configuration
The client deployment (EAR, EJB, WAR) will be required to declare a dependency to this module so that it has
access to the correct versions of the jars. 
This can be done by specifying MANIFEST headers or by providing a _jboss-deployment-structure.xml_ in the META-INF
directory. 

Example of _jboss-deployment-strucuture.xml_:
```xml
        <jboss-deployment-structure>
            <deployment>
                <exclusions>
                    <module name="javax.jms.api"/>
                </exclusions>
                <dependencies>
                    <module name="org.jboss.as5.messaging.client"/>
                </dependencies>
            </deployment>
        </jboss-deployment-structure>
```        
Above we are declaring an explicit exclusion for _javax_jms_api_ which is otherwise an [implicit dependency](https://docs.jboss.org/author/display/AS71/Implicit+module+dependencies+for+deployments).    
And the explicit dependency is for the module that this project produces.