# R&D Workshop 2019
Tomcat as a transport in CXF

## Status

**date: 03.04.2019**
We learned about the CXF structure and finally found an integration test for the embedded Jetty implementation called [EngineLifecycleTest](https://github.com/gcorsini/cxf/blob/master/systests/transports/src/test/java/org/apache/cxf/systest/http_jetty/EngineLifecycleTest.java#L88).

**date: 08.04.2019**
We compared the Jetty and Undertow implementation and studied the tests in more details.

**date: 15.04.2019**
We generated two class diagrams (of the existing Jetty and Undertow implementation) and a sequence diagram of the EngineLifecycleTest. We wrote short summaries of our findings: The [documentation](documentation/documentation.md) covers our findings about Jetty and Undertow and in [concept](concept/concept.md) we describe what we want to do in order to embed Tomcat.

**date: 22.04.2019**
Debugging how Jetty and Undertow work. (Especially integration test of Jetty.)

**date: 29.04.2019**
Finished [midpoint presentation](presentations%20and%20reports/MIDPOINT%20PRESENTATION_Apache%20Tomcat%20as%20a%20transport%20in%20CXF.pdf) with preparation. Debugging why the DestinationFactory bean loaded Jetty instead of Tomcat in our integration test. Solved this by moving the integration test to it's own directory: [systests/transport-tomcat/src/test/java/org/apache/cxf/systest/http_tomcat/TomcatEngineLifecycleTest.java](https://github.com/gcorsini/cxf/blob/transport_tomcat/systests/transport-tomcat/src/test/java/org/apache/cxf/systest/http_tomcat/TomcatEngineLifecycleTest.java)

**date: 06.05.2019**
While having the same code, we both got different errors. Therefore, one of us pulled the state again and importet the same project settings from the other. Adding a servlet creates a NullPointerException due to missing implementations in the core engine class.

**date: 14.05.2019**
The servlet still fails. We think it might have to do with the Handler instead of the Engine class. We will analyze how Jetty and Undertow handle this specific case and should be able to figure out what the issue is. If it is related to the Handler class, we might need some detailed information about Tomcat.

**date: 22.05.2019**
We believe that the issue appears, because the class [TomcatHTTPDestination](https://github.com/gcorsini/cxf/blob/transport_tomcat/rt/transports/http-tomcat/src/main/java/org/apache/cxf/transport/http_tomcat/TomcatHTTPDestination.java) is never instantiated and especially it's never being attached to the server in our code.

**date: 27.05.2019**
We were able to add a filter for a servlet and make it run with the embedded Tomcat server. We will now look into why the tests of [TomcatEngineLifecycleTest](https://github.com/gcorsini/cxf/blob/transport_tomcat/systests/transport-tomcat/src/test/java/org/apache/cxf/systest/http_tomcat/TomcatEngineLifecycleTest.java) aren't running yet.

**date: 03.06.2019**
We are trying to add multiple servlets to the tomcat server. Fixing errors in the engine class, for example removing servants correctly.

**date: 11.06.2019**
We are trying to add support for https. Additionally, we are working on a proof of concept / demo that uses an embedded Tomcat as a transport in CXF. Finally, we are also finishing the [final presentation](presentations%20and%20reports/FINAL%20PRESENTATION_Apache%20Tomcat%20as%20a%20transport%20in%20CXF.pdf) and [final report](presentations%20and%20reports/FINAL%20REPORT_Apache%20Tomcat%20as%20a%20transport%20in%20CXF.pdf)
