# Concept to use an embedded Tomcat as a transport in CXF

## Possible classes needed for an embedded Tomcat

Based on our study of Jetty and Undertow as a transport in CXF, we believe that the following classes will have to be implemented for our projects' proof of concept:

* Interface ServerEngine
* Class TomcatHTTPServerEngine extends ServerEngine
* Class TomcatHTTPServerEngineFactory
* Class TomcatDestinationFactory
* Class TomcatHTTPDestination
* Class TomcatHTTPHandler
* Class ThreadingParameters

Furthermore, we hope that it will be possible to reuse certain implementations from the other implementations.
For example for the interface ServerEngine (
[Jetty](https://github.com/gcorsini/cxf/blob/master/rt/transports/http-jetty/src/main/java/org/apache/cxf/transport/http_jetty/ServerEngine.java) 
or 
[Undertow](https://github.com/gcorsini/cxf/blob/master/rt/transports/http-undertow/src/main/java/org/apache/cxf/transport/http_undertow/ServerEngine.java)
) or for the class ThreadingParameters (
[Jetty](https://github.com/gcorsini/cxf/blob/master/rt/transports/http-jetty/src/main/java/org/apache/cxf/transport/http_jetty/ThreadingParameters.java) 
or 
[Undertow](https://github.com/gcorsini/cxf/blob/master/rt/transports/http-undertow/src/main/java/org/apache/cxf/transport/http_undertow/ThreadingParameters.java)
).

As explained in our previous presentation, we will first write tests that will ensure that every part is working as expected (TDD).

