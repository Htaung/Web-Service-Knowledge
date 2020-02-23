# Web-Service-Knowledge

The man's future depends on what he was doing on his leisure time in daily life

Web Service
Protocol Stack => TCP IP
-Transport Layer => HTTP
-Encoding Layer => XML
-Messaging layer => sOAP
-Service Description Layer: WSDL
-Service Discovery Layer; UDDI => directory of service

SOAP => simple object access protocol => 

JAX-RPC
Client <=> Stub    <=>	  Skeleton(tied) <=> Service

https://www.youtube.com/playlist?list=PLOxOmO43E6JsMCqjhxDtEKIX00Xr8aWeR

https://www.youtube.com/watch?v=S0zdMGNrxr0&index=8&list=PLqq-6Pq4lTTZTYpk_1DOowOGWJMIH5T39#t=4.622539

https://www.youtube.com/watch?v=Ir5KjU_exG8&list=PLd3UqWTnYXOkofdmEC1VB42cX8ZUwNEB7&index=6


Another nice feature of the MessageDispatcherServlet (or more correctly the WsdlDefinitionHandlerAdapter) is that it is able to transform the value of the 'location' of all the WSDL that it exposes to reflect the URL of the incoming request. 
<servlet>
    <servlet-name>spring-ws</servlet-name>
    <servlet-class>org.springframework.ws.transport.http.MessageDispatcherServlet</servlet-class>
    <init-param>
      <param-name>transformWsdlLocations</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>

static-wsdl(SimpleWsdl11Definition)	=>	Spring Web Services can also generate a WSDL from an XSD schema.
in stixCloud => web=>  WS2ServletConfig(spring-ws=> defined in web.xml) have defined all web service config of
com/stixcloud/webservice/wsdl/stixV0.wsdl



DefaultWsdl11Definition =>  builds a WSDL from a XSD schema by using conventions
in stixCloud => web=>  WS2ServletConfig(spring-be=> defined in web.xml) have defined all web service config of
com/stixcloud/stixwebservice/wsdl/stixV0.wsdl

SEI => service end point interface
From client to web serice SEI is used to convert obj to soap message in and out

wsimport http://www.webservicex.com/globalweather.asmx?wsdl -d D:\sei

wsimport http://www.webservicex.net/geoipservice.asmx?WSDL -d D:\sei

-d <dir> => specify where to place generated output file
-s <dir> => specify where to place generated source file
-clientjar <jarfile>
-p package
-vervose //detail


web service stub generation
wsimport http://www.webservicex.net/geoipservice.asmx?WSDL -d D:\sei
wsimport http://www.webservicex.com/globalweather.asmx?wsdl -d D:\sei
wsimport -keep  -s D:\sei\src http://www.webservicex.net/geoipservice.asmx?WSDL  

wsimport -keep -s D:\mkyong http://localhost:9999/ws/hello?wsdl
wsimport http://localhost:9999/ws/hello?wsdl -d D:\mkyong
wsimport -b binding_file.xml wsdl // binding xsd or xml to java


https://www.mkyong.com/webservices/jax-ws/jax-ws-hello-world-example-document-style/
//wsgen command
Document style requires extra classes to run,
 you can use “wsgen” to generate all necessary Java artifacts (mapping classes, wsdl or xsd schema). T
he “wsgen” command is required to read a service endpoint implementation class :
wsgen -verbose -keep -cp . com.mkyong.ws.HelloWorldImpl
wsgen -keep -cp . com.mkyong.ws.HelloWorldImpl


http://www.mkyong.com/webservices/jax-ws/jax-ws-hello-world-example/
http://www.mkyong.com/webservices/jax-ws/how-to-trace-soap-message-in-eclipse-ide/

https://stackoverflow.com/questions/6776421/display-the-tomcat-manager-application

changing the service name changes the default WSDL url

When RPC style is used, no schema gets generated for types.
13

soapui.org=> download free soapUi
soapui.org/IDE-Plugins/eclipse-plugin.html

metro bundle inside glassfish do all the work for webservice

With spring-ws, you receive a representation of the raw XML at EndPoint

http://theopentutorials.com/examples/java/jaxb/generate-xml-schema-from-java-class-in-eclipse-ide/
https://wiki.eclipse.org/Introduction_to_the_XSD_Editor

by referencing locationuri  => can get the wsdl by


One of the core interfaces of Spring Web Services is the WebServiceMessage. 
This interface represents a protocol-agnostic XML message.
 The interface contains methods that provide access to the payload of the message, 
in the form of a javax.xml.transform.Source or a javax.xml.transform.Result.
 Source and Result are tagging interfaces that represent an abstraction over XML input and output.
in stixcloud => user SaajSoapMessageFactory
//For larger SOAP messages, 
//this may not be very performant. In that case, the AxiomSoapMessageFactory might be more applicable. 
The SaajSoapMessageFactory uses the SOAP with Attachments API for Java to create SoapMessage implementations. 
SAAJ is part of J2EE 1.4, so it should be supported under most modern application servers.
//Note
SAAJ is based on DOM, the Document Object Model. 
This means that all SOAP messages are stored in memory. For larger SOAP messages, 
this may not be very performant. In that case, the AxiomSoapMessageFactory might be more applicable. 
the best version to use is  SOAP 1.1(safest bet)

3.6.2 Routing the Message to the Endpoint
As part of writing the endpoint, we also used the @PayloadRoot annotation to indicate which sort of messages can be handled by the handleHolidayRequest method
Here we route messages based on their content, by using a PayloadRootAnnotationMethodEndpointMapping
@PayloadRoot(namespace = "http://mycompany.com/hr/schemas", localPart = "HolidayRequest")
basically means that whenever an XML message is received with the namespace 
http://mycompany.com/hr/schemas and the HolidayRequest local name, it will be routed to the handleHolidayRequest method.


4.1 Web service messages
One of the core interfaces of Spring Web Services is the WebServiceMessage
The interface contains methods that provide access to the payload of the message, in the form of a javax.xml.transform.Source or a javax.xml.transform.Resul

4.1.2 SoapMessage
The SoapMessage is a subclass of WebServiceMessage. It contains SOAP-specific methods, such as getting SOAP Headers, SOAP Faults,
. Generally, your code should not be dependent on SoapMessage, 
because the content of the SOAP Body (the payload of the message) can be obtained via getPayloadSource() and getPayloadResult() in the WebServiceMessage.
 Only when it is necessary to perform SOAP-specific actions, such as adding a header, getting an attachment, etc.,
 should you need to cast WebServiceMessage to SoapMessage.


4.1.3 Message Factories
Concrete message implementations are created by a WebServiceMessageFactory. 
This factory can create an empty message, or read a message based on an input stream.
 There are two concrete implementations of WebServiceMessageFactory; one is based on SAAJ, 
the SOAP with Attachments API for Java, the other based on Axis 2's AXIOM, the AXis Object Model. 

SaajSoapMessageFactory
The SaajSoapMessageFactory uses the SOAP with Attachments API for Java to create SoapMessage implementations. 
SAAJ is part of J2EE 1.4, so it should be supported under most modern application servers. 
Here is an overview of the SAAJ versions supplied by common application servers: 

 Additionally, Java SE 6 includes SAAJ 1.3. You wire up a SaajSoapMessageFactory like so:
<bean id="messageFactory" class="org.springframework.ws.soap.saaj.SaajSoapMessageFactory" />
[Note]	Note
SAAJ is based on DOM, the Document Object Model. This means that all SOAP messages are stored in memory. 
For larger SOAP messages, this may not be very performant. In that case, the AxiomSoapMessageFactory might be more applicable. 

AxiomSoapMessageFactory
AxiomSoapMessageFactory uses the AXis 2 Object Model to create SoapMessage implementations.
 AXIOM is based on StAX, the Streaming API for XML. StAX provides a pull-based mechanism for reading XML messages, which can be more efficient for larger messages. 
 To increase reading performance on the AxiomSoapMessageFactory, you can set the payloadCaching property to false (default is true). 
This will read the contents of the SOAP body directly from the socket stream. 
When this setting is enabled, the payload can only be read once. This means that you have to make sure that any pre-processing (logging etc.) of 
the message does not consume it.
You use the AxiomSoapMessageFactory as follows:

<bean id="messageFactory" class="org.springframework.ws.soap.axiom.AxiomSoapMessageFactory">
    <property name="payloadCaching" value="true"/>
</bean>
 In addition to payload caching, AXIOM also supports full streaming messages, as defined in the StreamingWebServiceMessage. 
This means that the payload can be directly set on the response message, rather than being written to a DOM tree or buffer.
Full streaming for AXIOM is used when a handler method returns a JAXB2-supported object.
 It will automatically set this marshalled object into the response message, and write it out to the outgoing socket stream when the response is going out. 

SOAP 1.1 or 1.2
SaajSoapMessageFactory and the AxiomSoapMessageFactory have a soapVersion property, where you can inject a SoapVersion constant.
 <bean id="messageFactory" class="org.springframework.ws.soap.saaj.SaajSoapMessageFactory">
        <property name="soapVersion">
            <util:constant static-field="org.springframework.ws.soap.SoapVersion.SOAP_12"/>
        </property>
Version 1.2 might become more popular in the future, but currently 1.1 is the safest bet. 


//4.1.4 MessageContext
Typically, messages come in pairs: a request and a response
In Spring Web Services, such a conversation is contained in a MessageContext, 
which has properties to get request and response messages. 
On the client-side, the message context is created by the WebServiceTemplate.
 On the server-side, the message context is read from the transport-specific input stream. 
For example, in HTTP, it is read from the HttpServletRequest and the response is written back to the HttpServletResponse. 


IN stixCloud => webservice config is in Ws2ServletConfig.java and WsServletConfig.java

4.2 TransportContext
One of the key properties of the SOAP protocol is that it tries to be transport-agnostic. 
This is why, for instance, Spring-WS does not support mapping messages to endpoints by HTTP request URL, but rather by mesage content. 

4.3 Handling XML With XPath
One of the best ways to handle XML is to use XPath. 
XPath is a fourth generation declarative language that allows you to specify which nodes you want to process without specifying exactly how the processor is supposed to navigate to those nodes.
 XPath's data model is very well designed to support exactly what almost all developers want from XML.
In practice, XPath expressions tend to be much more robust against unexpected but perhaps insignificant changes in the input document. 


4.3.1 XPathExpression
The XPathExpression is an abstraction over a compiled XPath expression, such as the Java 5 javax.xml.xpath.XPathExpression, or the Jaxen XPath class.
 To construct an expression in an application context, there is the XPathExpressionFactoryBean. Here is an example which uses this factory bean:
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans-2.0.xsd">

    <bean id="nameExpression" class="org.springframework.xml.xpath.XPathExpressionFactoryBean">
        <property name="expression" value="/Contacts/Contact/Name"/>
    </bean>

    <bean id="myEndpoint" class="sample.MyXPathClass">
        <constructor-arg ref="nameExpression"/>
    </bean>
</beans>

bean myEndPoint can be expressed in java class by extending  org.springframework.ws.config.annotation.WsConfigurerAdapter
use @Bean to represent id="myEndpoint" 

4.4 Message Logging and Tracing
When developing or debugging a Web service, it can be quite useful to look at the content of a (SOAP) message when it arrives, or just before it is sent. 
Spring Web Services offer this functionality, via the standard Commons Logging interface. 


5. Creating a Web service with Spring-WS
5.1 Introduction
Spring-WS's server-side support is designed around a MessageDispatcher that dispatches incoming messages to endpoints, 
with configurable endpoint mappings, response generation, and endpoint interception.
Endpoints are typically annotated with the @Endpoint annotation, and have one or more handling methods
These methods handle incoming XML request messages by inspecting parts of the message (typically the payload), and create some sort of response. 
 You annotate the method with another annotation, typically @PayloadRoot, to indicate what sort of messages it can handle. 

An endpoint can choose from a large amount of XML handling libraries supported by Spring-WS, 
including the DOM family (W3C DOM, JDOM, dom4j, and XOM), SAX or StAX for faster performance, XPath to extract information from the message, 
or even marshalling techniques (JAXB, Castor, XMLBeans, JiBX, or XStream) to convert the XML to objects and vice-versa. 

5.2 The MessageDispatcher
The server-side of Spring-WS is designed around a central class that dispatches incoming XML messages to endpoints. 
Spring-WS's MessageDispatcher is extremely flexible, allowing you to use any sort of class as an endpoint, as long as it can be configured in the Spring IoC container. 
In a way, the message dispatcher resembles Spring's DispatcherServlet, the “Front Controller” used in Spring Web MVC. 

MessageDispatcher take dispatch request from client then called to  => getEndPoint(request) from EndpoingMapping 
MessageDispatcher After get endpoint from EndpointMapping => support(Endpoint) to EndpointAdapter => EndpointAdapter return to MessageDispatcher
MessageDispatcher invoke(request,endpoint) to EndpointAdapter => EndpointAdapter => invoke(request) to Endpoint  --- Endpoint give response to Endpoint Adapter
MessageDispatcher get the response from EndpointAdapter and then reurn the response back to client

When a MessageDispatcher is set up for use and a request comes in for that specific dispatcher, said MessageDispatcher starts processing the request. 
The list below describes the complete process a request goes through when handled by a MessageDispatcher:

1.An appropriate endpoint is searched for using the configured EndpointMapping(s). 
If an endpoint is found, the invocation chain associated with the endpoint (pre-processors, post-processors, and endpoints) 
will be executed in order to create a response.

2.An appropriate adapter is searched for the endpoint. The MessageDispatcher delegates to this adapter to invoke the endpoint.

3.If a response is returned, it is sent on its way. If no response is returned (which could be due to a pre- or post-processor intercepting the request, for example, for security reasons), no response is sent.
The message dispatcher operates on a message context, and not transport-specific input stream and output stream.
 As a result, transport specific requests need to read into a MessageContext. For HTTP, this is done with a WebServiceMessageReceiverHandlerAdapter, which is a Spring Web HandlerInterceptor, so that the MessageDispatcher can be wired in a standard DispatcherServlet

5.3 Transports
Spring Web Services supports multiple transport protocols. The most common is the HTTP transport, for which a custom servlet is supplied,
 but it is also possible to send messages over JMS, and even email. 

5.3.1 MessageDispatcherServlet
The MessageDispatcherServlet is a standard Servlet which conveniently extends from the standard Spring Web DispatcherServlet, and wraps a MessageDispatcher.
 As such, it combines the attributes of these into one: as a MessageDispatcher, it follows the same request handling flow as described in the previous section.
 As a servlet, the MessageDispatcherServlet is configured in the web.xml of your web application. 


Automatic WSDL exposure

http://localhost:8081/holidayService/holiday.wsdl
http://localhost:8081/holidayService/holidayService/orders.wsdl

@Bean
public SimpleWsdl11Definition stix(){ //if bean name is stix => so wsdl is stix.wsdl //=> servername/warname/stix.wsdl

It is therefore recommended to only use <dynamic-wsdl> during the development stages of your project. 
Then, we recommend to use your browser to download the generated WSDL, store it in the project, and expose it with <static-wsdl>. 
This is the only way to be really sure that the WSDL does not change over time. 


SisticAppConfig defined all the common config
com.stixcloud.config.webservice.WSServletConfig defined external WebService config
com.stixcloud.config.webservice.WS2ServletConfig defined WebService config
com.stixcloud.config.webservice.BookingEngineServletConfig defined booking engine WebService config
com.stixcloud.config.web.DispatcherServletConfig defined all SpringMVC Config


5.3.3 JMS transport
Spring Web Services supports server-side JMS handling through the JMS functionality provided in the Spring framework.
 Spring Web Services provides the WebServiceMessageListener to plug in to a MessageListenerContainer.
 This message listener requires a WebServiceMessageFactory to and MessageDispatcher to operate. 

5.4 Endpoints
Endpoints are the central concept in Spring-WS's server-side support. 
Endpoints provide access to the application behavior which is typically defined by a business service interface. 
An endpoint interprets the XML request message and uses that input to invoke a method on the business service (typically).
 The result of that service invocation is represented as a response message

@Endpoint                                                                                                              (1)
public class AnnotationOrderEndpoint {

  private final OrderService orderService;

  @Autowired                                                                                                           (2)
  public AnnotationOrderEndpoint(OrderService orderService) {
      this.orderService = orderService;
  }

  @PayloadRoot(localPart = "order", namespace = "http://samples")                                                      (5)
  public void order(@RequestPayload Element orderElement) {	(3)
    Order order = createOrder(orderElement);
    orderService.createOrder(order);
  }

  @PayloadRoot(localPart = "orderRequest", namespace = "http://samples")                                               (5)
  @ResponsePayload
  public Order getOrder(@RequestPayload OrderRequest orderRequest, SoapHeader header) {                                (4)
    checkSoapHeaderForSomething(header);
    return orderService.getOrder(orderRequest.getId());
  }


3=>	@RequestPayload => payload of the message => DOM Element
The order method takes a Element as a parameter, annotated with @RequestPayload. 
This means that the payload of the message is passed on this method as a DOM element.
 The method has a void return type, indicating that no response message is sent. 

4=> same as Stix => SaleEndpoint in stix also used FetchTransactionsV2 => is is annotated with @XmlRootElement (unmarshalled object)
The getOrder method takes a OrderRequest as a parameter, annotated with @RequestPayload as well.
 This parameter is a JAXB2-supported object (it is annotated with @XmlRootElement).
 This means that the payload of the message is passed on to this method as a unmarshalled object. 
The SoapHeader type is also given as a parameter. On invocation, this parameter will contain the SOAP header of the request message. 
The method is also annotated with @ResponsePayload, indicating that the return value (the Order) is used as the payload of the response message. 


 To enable the support for @Endpoint and related Spring-WS annotations, you will need to add the following to your Spring application context:

<beans xmlns="http://www.springframework.org/schema/beans"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:sws="http://www.springframework.org/schema/web-services"
  xsi:schemaLocation="http://www.springframework.org/schema/beans
      http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/web-services
      http://www.springframework.org/schema/web-services/web-services.xsd">

  <sws:annotation-driven />

</beans>

Or, if you are using @Configuration classes instead of Spring XML, you can annotate your configuration class with @EnableWs, like so:

@EnableWs
@Configuration
public class EchoConfig {

    // @Bean definitions go here

}

To customize the @EnableWs configuration, you can implement WsConfigurer, or better yet extend the WsConfigurerAdapter. For instance:

@Configuration
@EnableWs
@ComponentScan(basePackageClasses = { MyConfiguration.class })
public class MyConfiguration extends WsConfigurerAdapter {

  @Override
  public void addInterceptors(List<EndpointInterceptor> interceptors) {
    interceptors.add(new MyInterceptor());
  }

  @Override
  public void addArgumentResolvers(List<MethodArgumentResolver> argumentResolvers) {
    argumentResolvers.add(new MyArgumentResolver());
  }

  // More overridden methods ...
}


Note

Endpoints, like any other Spring Bean, are scoped as a singleton by default, i.e. one instance of the bean definition is created per container. Being a singleton implies that more than one thread can use it at the same time, so the endpoint has to be thread safe. If you want to use a different scope, such as prototype, refer to the Spring Reference documentation.

Note that all abstract base classes provided in Spring-WS are thread safe, unless otherwise indicated in the class-level Javadoc. 

5.4.1 @Endpoint handling methods
the method is typically annotated with either the @PayloadRoot or @SoapAction annotation.
 Here is an example of a handling method:

@PayloadRoot(localPart = "order", namespace = "http://samples")
public void order(@RequestPayload Element orderElement) {
  Order order = createOrder(orderElement);
  orderService.createOrder(order);
}

The order method takes a Element as a parameter, annotated with @RequestPayload. 
This means that the payload of the message is passed on this method as a DOM element.
 The method has a void return type, indicating that no response message is sent. 

Handling method parameters
org.springframework.ws.context.MessageContext => in phaseInInterceptor of stix => it is  Enabled by default.
@Override
public boolean handleResponse(MessageContext messageContext, Object endpoint) throws Exception {



Here are some examples of possible method signatures:

    public void handle(@RequestPayload Element element)

    This method will be invoked with the payload of the request message as a DOM org.w3c.dom.Element.

    public void handle(@RequestPayload DOMSource domSource, SoapHeader header)

    This method will be invoked with the payload of the request message as a javax.xml.transform.dom.DOMSource. 
    The header parameter will be bound to the SOAP header of the request message.

    public void handle(@RequestPayload MyJaxb2Object requestObject, @RequestPayload Element element, Message messageContext)

    This method will be invoked with the payload of the request message unmarshalled into a MyJaxb2Object (which is annotated with @XmlRootElement). 
    The payload of the message is also given as a DOM Element. The whole message context is passed on as the third parameter.

in stix *.xsl used to add namespace, serialized, deserialized request and response message 


Handling method return types =>  @ResponsePayload annotation. => To map the return value to the payload of the response message,
To send a response message, the handling needs to specify a return type. If no response message is required, the method can simply declare a void return type.
Most commonly, the return type is used to create the payload of the response message, but it is also possible to map to other parts of the response message. 

To map the return value to the payload of the response message, you will need to annotate the method with the @ResponsePayload annotation.
 This annotation tells Spring-WS that the return value needs to be bound to the response payload. 

@ResponsePayload Default Return type => W3C DOM	org.w3c.dom.Element

5.5 Endpoint mappings
The endpoint mapping is responsible for mapping incoming messages to appropriate endpoints.
The concept of configurable endpoint mappings that can optionally contain interceptors (which can manipulate the request or the response, or both) is extremely powerful
An EndpointMapping delivers a EndpointInvocationChain, which contains the endpoint that matches the incoming request, and may also contain a list of endpoint interceptors that will be applied to the request and response. 
When a request comes in, the MessageDispatcher will hand it over to the endpoint mapping to let it inspect the request and come up with an appropriate EndpointInvocationChain. 
Then the MessageDispatcher will invoke the endpoint and any interceptors in the chain.

@Endpoint style allows you to handle multiple requests in one endpoint class. This is the responsibility of the MethodEndpointMapping. This mapping determines which method is to be invoked for an incoming request message. 
There are two endpoint mappings that can direct requests to methods: the PayloadRootAnnotationMethodEndpointMapping and the SoapActionAnnotationMethodEndpointMapping, both of which are enabled by using <sws:annotation-driven/> in your application context. 

The PayloadRootAnnotationMethodEndpointMapping uses the @PayloadRoot annotation, with the localPart and namespace elements, 
to mark methods with a particular qualified name. Whenever a message comes in which has this qualified name for the payload root element, the method will be invoked.

Alternatively, the SoapActionAnnotationMethodEndpointMapping uses the @SoapAction annotation to mark methods with a particular SOAP Action. 
Whenever a message comes in which has this SOAPAction header, the method will be invoked. 

5.5.1 WS-Addressing
WS-Addressing specifies a transport-neutral routing mechanism. 
It is based on a To and Action SOAP header, which indicate the destination and intent of the SOAP message

In Spring Web Services, WS-Addressing is implemented as an endpoint mapping. 
Using this mapping, you associate WS-Addressing actions with endpoints, similar to the SoapActionAnnotationMethodEndpointMapping described above. 

AnnotationActionEndpointMapping
The AnnotationActionEndpointMapping is similar to the SoapActionAnnotationMethodEndpointMapping,
 but uses WS-Addressing headers instead of the SOAP Action transport header
To use the AnnotationActionEndpointMapping, annotate the handling methods with the @Action annotation, similar to the @PayloadRoot and @SoapAction annotations

@Endpoint
public class AnnotationOrderEndpoint {
    private final OrderService orderService;

    public AnnotationOrderEndpoint(OrderService orderService) {
        this.orderService = orderService;
    }

    @Action("http://samples/RequestOrder")
    public Order getOrder(OrderRequest orderRequest) {
        return orderService.getOrder(orderRequest.getId());
    }

    @Action("http://samples/CreateOrder")
    public void order(Order order) {
        orderService.createOrder(order);
    }

}
The mapping above routes requests which have a WS-Addressing Action of http://samples/RequestOrder to the getOrder method. 
Requests with http://samples/CreateOrder will be routed to the order method.. 

messageSenders property, which is required for sending response messages to non-anonymous, out-of-bound addresses. 
You can set MessageSender implementations in this property, the same as you would on the WebServiceTemplate.

5.5.2 Intercepting requests - the EndpointInterceptor interface
The endpoint mapping mechanism has the notion of endpoint interceptors. These can be extremely useful
 when you want to apply specific functionality to certain requests,
 for example, dealing with security-related SOAP headers, or the logging of request and response message. 

 Endpoint interceptors are typically defined by using a <sws:interceptors> element in your application context. In this element, you can simply define endpoint interceptor beans that apply to all endpoints defined in that application context. Alternatively, you can use <sws:payloadRoot> or <sws:soapAction> elements to specify for which payload root name or SOAP action the interceptor should apply. For example:

<sws:interceptors>
  <bean class="samples.MyGlobalInterceptor"/> //Global Interceptor
  <sws:payloadRoot namespaceUri="http://www.example.com">
    <bean class="samples.MyPayloadRootInterceptor"/>
  </sws:payloadRoot>
  <sws:soapAction value="http://www.example.com/SoapAction">
    <bean class="samples.MySoapActionInterceptor1"/>
    <ref bean="mySoapActionInterceptor2"/>
  </sws:soapAction>
</sws:interceptors>

<bean id="mySoapActionInterceptor2" class="samples.MySoapActionInterceptor2"/>

When using @Configuration classes, you can extend from WsConfigurerAdapter to add interceptors. Like so:
 //In stix there have the two interceptors in WS2ServletConfig.java  under 
 // PhaseInInterceptor and PayloadExceptionThrowingValidatingInterceptor
@Configuration
@EnableWs
public class MyWsConfiguration extends WsConfigurerAdapter {

  @Override
  public void addInterceptors(List<EndpointInterceptor> interceptors) {
    interceptors.add(new MyPayloadRootInterceptor());
  }
}

Interceptors must implement the EndpointInterceptor interface from the org.springframework.ws.server package.
 This interface defines three methods, one that can be used 
	for handling the request message before the actual endpoint will be executed,
 one that can be used 
	for handling a normal response message, and 
 one that can be used 
	for handling fault messages,
	both of which will be called after the endpoint
 is executed. These three methods should provide enough flexibility to do all kinds of pre- and post-processing. 

The handleRequest(..) method on the interceptor returns a boolean value. You can use this method to interrupt or continue the processing of the invocation chain. 
When this method returns true, 
	the endpoint execution chain will continue, 
when it returns false, 
	the MessageDispatcher interprets this to mean that the interceptor itself has taken care of things and does not continue executing the other interceptors and the actual endpoint in the invocation chain

The handleResponse(..) and handleFault(..) methods also have a boolean return value. 
	When these methods return false,
		 the response will not be sent back to the client.

PayloadLoggingInterceptor and SoapEnvelopeLoggingInterceptor
It can be useful to log the incoming and outgoing XML messages. SWS facilitates this with the PayloadLoggingInterceptor and SoapEnvelopeLoggingInterceptor classes. The former logs just the payload of the message to the Commons Logging Log; the latter logs the entire SOAP envelope, including SOAP headers. The following example shows you how to define them in an endpoint mapping:

  <sws:interceptors>
    <bean class="org.springframework.ws.server.endpoint.interceptor.PayloadLoggingInterceptor"/>
  </sws:interceptors>

Both of these interceptors have two properties: 'logRequest' and 'logResponse', which can be set to false to disable logging for either request or response messages

PayloadValidatingInterceptor
One of the benefits of using a contract-first development style is that we can use the schema to validate incoming and outgoing XML messages. 
Spring-WS facilitates this with the PayloadValidatingInterceptor. This interceptor requires a reference to one or more W3C XML or RELAX NG schemas, and can be set to validate requests or responses, or both. 

Note=>
	request validation	=>  good idea => resulting Web service very strict
	Usually, it is not really important whether the request validates, only if the endpoint can get sufficient information to fullfill a request
	Validating the response => a good idea, because the endpoint should adhere to its schema. Remember Postel's Law: “Be conservative in what you do; be liberal in what you accept from others.”

	 in this example, we use the schema in /WEB-INF/orders.xsd to validate the response, but not the request. 
	Note that the PayloadValidatingInterceptor can also accept multiple schemas using the schemas property. 
<bean id="validatingInterceptor"
        class="org.springframework.ws.soap.server.endpoint.interceptor.PayloadValidatingInterceptor">
    <property name="schema" value="/WEB-INF/orders.xsd"/>
    <property name="validateRequest" value="false"/>
    <property name="validateResponse" value="true"/>
</bean>

==> in stix => 	 WS2ServletConfig.java
	@Bean
	public PayloadExceptionThrowingValidatingInterceptor validatingInterceptor(){
		PayloadExceptionThrowingValidatingInterceptor pi=new PayloadExceptionThrowingValidatingInterceptor();
		pi.setSchema(new ClassPathResource("com/stixcloud/webservice/xsd/sisticV0.xsd"));
		pi.setValidateRequest(true);
		pi.setValidateResponse(true);
		return pi;
	}


PayloadTransformingInterceptor
 To transform the payload to another XML format, Spring Web Services offers the PayloadTransformingInterceptor. This endpoint interceptor is based on XSLT style sheets, and is especially useful when supporting multiple versions of a Web service: you can transform the older message format to the newer format. Here is an example to use the PayloadTransformingInterceptor:

<bean id="transformingInterceptor"
        class="org.springframework.ws.server.endpoint.interceptor.PayloadTransformingInterceptor">
    <property name="requestXslt" value="/WEB-INF/oldRequests.xslt"/>
    <property name="responseXslt" value="/WEB-INF/oldResponses.xslt"/>
</bean>

 To transform the payload to another XML format, Spring Web Services offers the PayloadTransformingInterceptor. This endpoint interceptor is based on XSLT style sheets, and is especially useful when supporting multiple versions of a Web service: you can transform the older message format to the newer format. Here is an example to use the PayloadTransformingInterceptor:

<bean id="transformingInterceptor"
        class="org.springframework.ws.server.endpoint.interceptor.PayloadTransformingInterceptor">
    <property name="requestXslt" value="/WEB-INF/oldRequests.xslt"/>
    <property name="responseXslt" value="/WEB-INF/oldResponses.xslt"/>
</bean>

5.6 Handling Exceptions => in stix it use com.stixcloud.webservice.SoapExceptionResolver, that are extending AbstractEndpointExceptionResolver,
				 as bean injecting into WsConfigurerAdapter => 
Spring-WS provides EndpointExceptionResolvers to ease the pain of unexpected exceptions occurring while your message is being processed 
by an endpoint which matched the request.
Endpoint exception resolvers are automatically picked up by the MessageDispatcher, so no explicit configuration is necessary. 
Besides implementing the EndpointExceptionResolver interface, which is only a matter of implementing the resolveException(MessageContext, endpoint, Exception) method, you may also use one of the provided implementations. The simplest implementation is the SimpleSoapExceptionResolver, which just creates a SOAP 1.1 Server or SOAP 1.2 Receiver Fault, and uses the exception message as the fault string. The SimpleSoapExceptionResolver is the default, but it can be overriden by explicitly adding another resolver.



5.6.1 SoapFaultMappingExceptionResolver
The SoapFaultMappingExceptionResolver is a more sophisticated implementation. This resolver enables you to take the class name of any exception that might be thrown and map it to a SOAP

Fault, like so:

<beans>
    <bean id="exceptionResolver"
        class="org.springframework.ws.soap.server.endpoint.SoapFaultMappingExceptionResolver">
        <property name="defaultFault" value="SERVER"/>
        <property name="exceptionMappings">
            <value>
                org.springframework.oxm.ValidationFailureException=CLIENT,Invalid request
            </value>
        </property>
    </bean>
</beans>

 The key values and default endpoint use the format faultCode,faultString,locale, where only the fault code is required. If the fault string is not set, it will default to the exception message. If the language is not set, it will default to English. The above configuration will map exceptions of type ValidationFailureException to a client-side SOAP Fault with a fault string "Invalid request", as can be seen in the following response:

<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
    <SOAP-ENV:Body>
       <SOAP-ENV:Fault>
           <faultcode>SOAP-ENV:Client</faultcode>
           <faultstring>Invalid request</faultstring>
       </SOAP-ENV:Fault>
    </SOAP-ENV:Body>
</SOAP-ENV:Envelope>


6. Using Spring Web Services on the Client
6.1 Introduction
Spring-WS provides a client-side Web service API that allows for consistent, XML-driven access to Web services. 
It also caters for the use of marshallers and unmarshallers so that your service tier code can deal exclusively with Java objects. 
The org.springframework.ws.client.core package provides the core functionality for using the client-side access API.
 It contains template classes that simplify the use of Web services,
he design principle common to Spring template classes is to provide helper methods to perform common operations, and
 for more sophisticated usage, delegate to user implemented callback interfaces. The Web service template follows the same design. 
The classes offer various convenience methods for the sending and receiving of XML messages, marshalling objects to XML before sending, and allows 
for multiple transport options. 

6.2 Using the client-side API
6.2.1 WebServiceTemplate
The WebServiceTemplate is the core class for client-side Web service access in Spring-WS. 
It contains methods for sending Source objects, and receiving response messages as either Source or Result. 
Additionally, it can marshal objects to XML before sending them across a transport, and unmarshal any response XML into an object again.


URIs and Transports	==> in stix => com.stixcloud.config.webservice.WS2ServletConfig => used WebServiceTemplate and set it Marshaller and Unmarshaller as jaxbMarshaller and defaulturi => http://localhost:7080/spring-ws2-exemplary/getSquare
The WebServiceTemplate class uses an URI as the message destination. 
You can either set a defaultUri property on the template itself, or supply an URI explicitly when calling a method on the template. 
The URI will be resolved into a WebServiceMessageSender, which is responsible for sending the XML message across a transport layer. 
You can set one or more message senders using the messageSender or messageSenders properties of ===> the WebServiceTemplate class.  


HTTP transports
There are two implementations of the WebServiceMessageSender interface for sending messages via HTTP.
The default implementation is the HttpUrlConnectionMessageSender, which uses the facilities provided by Java itself. 
The alternative is the HttpComponentsMessageSender, which uses the Apache HttpComponents HttpClient. 
Use the latter if you need more advanced and easy-to-use functionality (such as authentication, HTTP connection pooling, and so forth).

To use the HTTP transport, either set the defaultUri to something like http://example.com/services, or supply the uri parameter for one of the methods.
The following example shows how the default configuration can be used for HTTP transports:

<beans>

    <bean id="messageFactory" class="org.springframework.ws.soap.saaj.SaajSoapMessageFactory"/>

    <bean id="webServiceTemplate" class="org.springframework.ws.client.core.WebServiceTemplate">
        <constructor-arg ref="messageFactory"/>
        <property name="defaultUri" value="http://example.com/WebService"/>
    </bean>

</beans>

// ==> in stix => com.stixcloud.config.webservice.WS2ServletConfig => that use HttpComponentsMessageSender messageSender() 
=> to use the user and password authentication
The following example shows how override the default configuration, and to use Apache HttpClient to authenticate using HTTP authentication:
<bean id="webServiceTemplate" class="org.springframework.ws.client.core.WebServiceTemplate">
    <constructor-arg ref="messageFactory"/>
    <property name="messageSender">
        <bean class="org.springframework.ws.transport.http.HttpComponentsMessageSender">
            <property name="credentials">
                <bean class="org.apache.http.auth.UsernamePasswordCredentials">
                    <constructor-arg value="john:secret"/>
                </bean>
            </property>
        </bean>
    </property>
    <property name="defaultUri" value="http://example.com/WebService"/>
</bean>

JMS transport
For sending messages over JMS, Spring Web Services provides the JmsMessageSender. This class uses the facilities of the Spring framework to transform the WebServiceMessage into a JMS Message, send it on its way on 
a Queue or Topic, and receive a response (if any). 


Email transport
Spring Web Services also provides an email transport, which can be used to send web service messages via SMTP, 
and retrieve them via either POP3 or IMAP. The client-side email functionality is contained in the MailMessageSender class.
 This class creates an email message from the request WebServiceMessage, and sends it via SMTP. 
It then waits for a response message to arrive in the incoming POP3 or IMAP server. 

XMPP transport
Spring Web Services 2.0 introduced an XMPP (Jabber) transport, which can be used to send and receive web service messages via  XMPP. 
The client-side XMPP functionality is contained in the XmppMessageSender class. 
This class creates an XMPP message from the request WebServiceMessage, and sends it via XMPP. It then listens for a response message to arrive. 

To use the XmppMessageSender, set the defaultUri or uri parameter to a xmpp URI, for example xmpp:johndoe@jabber.org. 
The sender also requires an XMPPConnection to work, which can be conveniently created using the org.springframework.ws.transport.xmpp.support.XmppConnectionFactoryBean.
The following example shows how to use the xmpp transport:

<beans>
    <bean id="messageFactory" class="org.springframework.ws.soap.saaj.SaajSoapMessageFactory"/>
    <bean id="connection" class="org.springframework.ws.transport.xmpp.support.XmppConnectionFactoryBean">
        <property name="host" value="jabber.org"/>
        <property name="username" value="username"/>
        <property name="password" value="password"/>
    </bean>
    <bean id="webServiceTemplate" class="org.springframework.ws.client.core.WebServiceTemplate">
        <constructor-arg ref="messageFactory"/>
        <property name="messageSender">
            <bean class="org.springframework.ws.transport.xmpp.XmppMessageSender">
                <property name="connection" ref="connection"/>
            </bean>
        </property>
        <property name="defaultUri" value="xmpp:user@jabber.org"/>
    </bean>
</beans>

Message factories
In addition to a message sender, the WebServiceTemplate requires a Web service message factory. 
There are two message factories for SOAP: SaajSoapMessageFactory and AxiomSoapMessageFactory. 
If no message factory is specified (via the messageFactory property), Spring-WS will use the SaajSoapMessageFactory by default. 


6.2.2 Sending and receiving a WebServiceMessage
The WebServiceTemplate contains many convenience methods to send and receive web service messages. 
There are methods that accept and return a Source and those that return a Result. 
Additionally, there are methods which marshal and unmarshal objects to XML. Here is an example that sends a simple XML message to a Web service. 


import java.io.StringReader;
import javax.xml.transform.stream.StreamResult;
import javax.xml.transform.stream.StreamSource;

import org.springframework.ws.WebServiceMessageFactory;
import org.springframework.ws.client.core.WebServiceTemplate;
import org.springframework.ws.transport.WebServiceMessageSender;
public class WebServiceClient {

    private static final String MESSAGE =
        "<message xmlns=\"http://tempuri.org\">Hello Web Service World</message>";

    private final WebServiceTemplate webServiceTemplate = new WebServiceTemplate();

    public void setDefaultUri(String defaultUri) {
        webServiceTemplate.setDefaultUri(defaultUri);
    }

    // send to the configured default URI
    public void simpleSendAndReceive() {
        StreamSource source = new StreamSource(new StringReader(MESSAGE));
        StreamResult result = new StreamResult(System.out);
        webServiceTemplate.sendSourceAndReceiveToResult(source, result);
    }

    // send to an explicit URI
    public void customSendAndReceive() {
        StreamSource source = new StreamSource(new StringReader(MESSAGE));
        StreamResult result = new StreamResult(System.out);
        webServiceTemplate.sendSourceAndReceiveToResult("http://localhost:8080/AnotherWebService",
            source, result);
    }

}

<beans xmlns="http://www.springframework.org/schema/beans">

    <bean id="webServiceClient" class="WebServiceClient">
        <property name="defaultUri" value="http://localhost:8080/WebService"/>
    </bean>

</beans>


 The above example uses the WebServiceTemplate to send a hello world message to the web service located at 
http://localhost:8080/WebService (in the case of the simpleSendAndReceive() method), and writes the result to the console. 
The WebServiceTemplate is injected with the default URI, which is used because no URI was supplied explicitly in the Java code.

Please note that the WebServiceTemplate class is thread-safe once configured (assuming that all of it's dependencies are thread-safe too, 
which is the case for all of the dependencies that ship with Spring-WS), and so multiple objects can use the same shared WebServiceTemplate instance if so desired. 
The WebServiceTemplate exposes a zero argument constructor and messageFactory/messageSender bean properties which can be used for constructing the instance 
(using a Spring container or plain Java code). Alternatively, consider deriving from Spring-WS's WebServiceGatewaySupport convenience base class, 
which exposes convenient bean properties to enable easy configuration. (You do not have to extend this base class... it is provided as a convenience class only.) 


6.2.4  WebServiceMessageCallback
 To accommodate the setting of SOAP headers and other settings on the message, the WebServiceMessageCallback interface gives you access to the message after it has been created, but before it is sent. The example below demonstrates how to set the SOAP Action header on a message that is created by marshalling an object.

public void marshalWithSoapActionHeader(MyObject o) {

    webServiceTemplate.marshalSendAndReceive(o, new WebServiceMessageCallback() {

        public void doWithMessage(WebServiceMessage message) {
            ((SoapMessage)message).setSoapAction("http://tempuri.org/Action");
        }
    });
}

[Note]	Note
Note that you can also use the org.springframework.ws.soap.client.core.SoapActionCallback to set the SOAP Action header. 

WS-Addressing => skip 

6.2.5  WebServiceMessageExtractor
 The WebServiceMessageExtractor interface is a low-level callback interface that allows you to have full control over the process to extract an Object from a received WebServiceMessage. The WebServiceTemplate will invoke the extractData(..) method on a supplied WebServiceMessageExtractor while the underlying connection to the serving resource is still open. The following example illustrates the WebServiceMessageExtractor in action:
public void marshalWithSoapActionHeader(final Source s) {
    final Transformer transformer = transformerFactory.newTransformer();
    webServiceTemplate.sendAndReceive(new WebServiceMessageCallback() {
        public void doWithMessage(WebServiceMessage message) {
            transformer.transform(s, message.getPayloadResult());
        },
        new WebServiceMessageExtractor() {
            public Object extractData(WebServiceMessage message) throws IOException
                // do your own transforms with message.getPayloadResult()
                //     or message.getPayloadSource()
            }
        });
}


7. Securing your Web services with Spring-WS
7.1 Introduction
This chapter explains how to add WS-Security aspects to your Web services. We will focus on the three different areas of WS-Security, namely:

Authentication.  This is the process of determining whether a principal is who they claim to be. In this context, a "principal" generally means a user, device or some other system which can perform an action in your application.

Digital signatures.  The digital signature of a message is a piece of information based on both the document and the signer's private key. It is created through the use of a hash function and a private signing function (encrypting with the signer's private key).

Encryption and Decryption.  Encryption is the process of transforming data into a form that is impossible to read without the appropriate key. It is mainly used to keep information hidden from anyone for whom it is not intended. Decryption is the reverse of encryption; it is the process of transforming of encrypted data back into an readable form.

All of these three areas are implemented using the XwsSecurityInterceptor or Wss4jSecurityInterceptor, which we will describe in Section 7.2, “ XwsSecurityInterceptor ” and Section 7.3, “ Wss4jSecurityInterceptor ”, respectively
[Note]	Note

Note that WS-Security (especially encryption and signing) requires substantial amounts of memory, and will also decrease performance. If performance is important to you, you might want to consider not using WS-Security, or simply use HTTP-based security. 


import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;

http://briansjavablog.blogspot.com/2013/01/spring-web-services-tutorial.html

Convert from xml to xsd via cmd =>	C:\Program Files\Microsoft SDKs\Windows\v6.0A\Bin\xsd.exe
https://docs.microsoft.com/en-us/dotnet/framework/serialization/xml-schema-definition-tool-xsd-exe
xsd file.xml /o:[outputDirectory]






<xs:extension base="hayman:wsResponse"> => inherit

complex types=> contains other elements
simple types=> do not contain other elements.
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"  => define xml schema instance that will be use prefix xsi => example => <xs:element name="Request">

xmlns:xs="http://www.w3.org/2001/XMLSchema"
indicates that the elements and data types used in the schema come from the "http://www.w3.org/2001/XMLSchema" namespace.
 It also specifies that the elements and data types that come from the 
"http://www.w3.org/2001/XMLSchema" namespace should be prefixed with xs:

targetNamespace="http://endpoint.webservices.sistic.com/"
indicates that the elements defined by this schema (note, to, from, heading, body.) come from the targetNamespace="http://endpoint.webservices.sistic.com/"

elementFormDefault="qualified"
indicates that any elements used by the XML instance document which were declared in this schema must be namespace qualified.e 

Simple Elemnet => may have the name type and default
<xs:element name="color" type="xs:string" default="red"/> 

Simple elements cannot have attributes. If an element has attributes, it is considered to be of a complex type.
<xs:attribute name="lang" type="xs:string" default="EN"/> 
<xs:attribute name="lang" type="xs:string" fixed="EN"/> 

Optional and Required Attributes
Attributes are optional by default. To specify that the attribute is required, use the "use" attribute:
<xs:attribute name="lang" type="xs:string" use="required"/> 

Restrictions on Content
When an XML element or attribute has a data type defined, it puts restrictions on the element's or attribute's content.
If an XML element is of type "xs:date" and contains a string like "Hello World", the element will not validate.
With XML Schemas, you can also add your own restrictions to your XML elements and attributes. 
These restrictions are called facets. You can read more about facets in the next chapter.
Restrictions on XML elements are called facets.

<xs:element name="car" type="carType"/>

<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType> 
 In this case the type "carType" can be used by other elements because it is not a part of the "car" element.

element type annonymous => come out annonymous elementtype => from that add sequences and elements 
element can set multiplicity => like 0..1 or 1..1 etc

elements can set base type like inheritance =>
if elements is list => so list' type is complex type and from that complex type have seq and elements ==> from that elements => type is complex type ==>
							==>from that complex type have seq and elements

Indicators

There are seven indicators:

Order indicators:

    All
    Choice
    Sequence

Occurrence indicators:

    maxOccurs
    minOccurs

Group indicators:

    Group name
    attributeGroup name

The <all> indicator specifies that the child elements can appear in any order, and that each child element must occur only once: 
The <sequence> indicator specifies that the child elements must appear in a specific order:
The <choice> indicator specifies that either one child element or another can occur:
Group indicators are used to define related sets of elements.


<xs:group name="persongroup">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
    <xs:element name="birthday" type="xs:date"/>
  </xs:sequence>
</xs:group>

<xs:element name="person" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:group ref="persongroup"/>
    <xs:element name="country" type="xs:string"/>
  </xs:sequence>
</xs:complexType> 



<xs:attributeGroup name="personattrgroup">
  <xs:attribute name="firstname" type="xs:string"/>
  <xs:attribute name="lastname" type="xs:string"/>
  <xs:attribute name="birthday" type="xs:date"/>
</xs:attributeGroup>

<xs:element name="person">
  <xs:complexType>
    <xs:attributeGroup ref="personattrgroup"/>
  </xs:complexType>
</xs:element> 

The <any> element enables us to extend the XML document with elements not specified by the schema!

USER_SESSIONS_LOG
ACTIVE_USER_SESSIONS
AuthSuccessHandler
CommonRabbitMQConfig


