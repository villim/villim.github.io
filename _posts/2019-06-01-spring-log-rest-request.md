---
title: Log REST Request in SpringBoot2
layout: post
---

When building REST APIs, if we are able to see incoming request, the raw headers and payload info will help to solve integration testing. 

What I'm tring to do, is printing the raw request, to see what client is sending.

## Background

I'm working with: 

* SpringBoot 2.0.1.RELEASE
* Spring 5.0.5.RELEASE
* Spring WS 2.4.3.RELEASE.

Unlike Spring SOAP APIs, to view original request, we can simply change logger level to **TRACE** in Log4j.

```xml
<Logger name="org.springframework.ws.client.MessageTracing.sent" level="trace" />
<Logger name="org.springframework.ws.client.MessageTracing.received" level="trace" />
<Logger name="org.springframework.ws.server.MessageTracing.sent" level="trace" />
<Logger name="org.springframework.ws.server.MessageTracing.received" level="trace" />
```

## Try print Client Sent Raw Request

REST implementation is a little tricky. As mentioned before, we can't simply configure Log4j, we have to print it by ourself.

Where can we get request information? First object come to mind is **HttpServletRequest**! But unlucky, it only contains headers information, no payload data. So just add it to method parameter, can't satisfy our requirement.

```java
@RestController
public class DemoRestController {
		...
    @RequestMapping(method = RequestMethod.POST, value = "/v1/foo", consumes = "application/json", produces = "application/json")
    public FooResponse postFooMessage(HttpServletRequest httpRequest, @Valid @RequestBody FooRequest fooRequest) {
        FooResponse fooResponse = new SmsResponse();
        ...
        return smsResponse;
    }
		...
}
``` 

After debugging we can see, Spring won't read payload, until it trying to convert payload to FooRequest object.  This converting happens in RequestResponseBodyMethodProcessor.java

```
public class RequestResponseBodyMethodProcessor extends AbstractMessageConverterMethodProcessor {
...
	@Override
	public Object resolveArgument(MethodParameter parameter, @Nullable ModelAndViewContainer mavContainer,
			NativeWebRequest webRequest, @Nullable WebDataBinderFactory binderFactory) throws Exception {
		parameter = parameter.nestedIfOptional();
		Object arg = readWithMessageConverters(webRequest, parameter, parameter.getNestedGenericParameterType());
	  //  We can print payload here
	  //  LOG.debug("Origin Raw Payload is [{}]", arg.toString());
    
		...
		}
}
```

So if we can customize our own **RequestResponseBodyMethodProcessor**, and inject it back to **RequestMappingHandlerAdapter**, then problem solved.

And **RequestMappingHandlerAdapter** do allow to customize argument resolvers with **setCustomArgumentResolvers** method.

```java 
public class RequestMappingHandlerAdapter extends AbstractHandlerMethodAdapter
		implements BeanFactoryAware, InitializingBean {
	/**
	 * Provide resolvers for custom argument types. Custom resolvers are ordered
	 * after built-in ones. To override the built-in support for argument
	 * resolution use {@link #setArgumentResolvers} instead.
	 */
	public void setCustomArgumentResolvers(@Nullable List<HandlerMethodArgumentResolver> argumentResolvers) {
		this.customArgumentResolvers = argumentResolvers;
	}
 ...
}
```  

But unfortunately, it would not change default resolvers, it only append our customized resolver at the end of list. Just as the document in WebMvcConfigurer says, if we want to change default resolvers, we have to directly replace **RequestMappingHandlerAdapter**.

```java
public interface WebMvcConfigurer {
	/**
	 * Add resolvers to support custom controller method argument types.
	 * <p>This does not override the built-in support for resolving handler
	 * method arguments. To customize the built-in support for argument
	 * resolution, configure {@link RequestMappingHandlerAdapter} directly.
	 * @param resolvers initially an empty list
	 */
	default void addArgumentResolvers(List<HandlerMethodArgumentResolver> resolvers) {
	}
}
```

Solution is clear now, however, customize **RequestMappingHandlerAdapter** is not that easy. 

Omit Detailed trials, in a word, you will find, to do it, we have to change quite many Spring code, no just **RequestMappingHandlerAdapter** itself. Caused by **protected** method, we have to customize quite a lot Spring classes.

That made me uncomfortable at all. If we doing this way, it will be not easy to upgrade Spring version in the future, and have to spend quite many time to maintain these customized code. Noooo ~

P.S. If trying to customize **RequestMappingHandlerAdapter**, need know this issue [Issue: Unable to have custom RequestMappingHandlerMapping](https://github.com/spring-projects/spring-boot/issues/5004)


SO if we not able to print RAW incoming request with headers and payload, we can do 2 things to make error more visible.

### Solution 1: Log4j

Althought Spring won't print REST raw request info, we are still able to see error when encounter payload converting error.

```xml
<Logger name="org.springframework.web.servlet.mvc.method.annotation" level="debug"/>
```

### Solution 2: Jetty Log

Embedded Jetty can print all incoming request, no matter it is valid or not, like following format:

```
123.4.5.6 - - [20/Jul/2016:10:16:17 +0000]
  "GET /jetty/tut/XmlConfiguration.html HTTP/1.1"
  200 76793 "http://localhost:8080/jetty/tut/logging.html"
  "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.6) Gecko/20040614 Firefox/0.8" 342
```

Read more: [Configuring Jetty Request Logs](http://www.eclipse.org/jetty/documentation/current/configuring-jetty-request-logs.html)

Ofcourse, not exactly what we want, just a way to record every client invoke.

```java
@Component
public class EnableRequestLog implements WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> {

    private static final JettyServerCustomizer USE_SLF4J_REQUEST_LOG = server -> server.setRequestLog(new Slf4jRequestLog());

    @Override
    public void customize(ConfigurableServletWebServerFactory factory) {
        ((JettyServletWebServerFactory) factory).addServerCustomizers(USE_SLF4J_REQUEST_LOG);
    }
}
```

### Solution 3: Tcpdump

If do need check raw request, we can working in debug mode locally.

And Tcpdump can help when working on Servers.

## Print Request & Response for valid Request

When it's aleady comming into our method, it seems not that usefully to print request now. We already have that java object.

But from monitoring perspective, it's still quite useful when problem happened on Product Servers. It will be much easier to annalyse issues.

There're 2 ways to do it:

### 1. Use Interceptor to log for all APIs

This way will print request for all APIs.

First, change request to **ContentCachingRequestWrapper** which able to read origin payload:

```java
public class LoggableDispatcherServlet extends DispatcherServlet {

    private static final long serialVersionUID = 3916978888100594239L;

    @Override
    protected void doDispatch(HttpServletRequest request, HttpServletResponse response) throws Exception {

        if (!(request instanceof ContentCachingRequestWrapper)) {
            request = new ContentCachingRequestWrapper(request);
        }

        super.doDispatch(request, response);
    }

}

```

Second, create our customize interceptor to log payload:

```java
public class RawRequestLoggerInterceptor implements HandlerInterceptor {

    private Logger LOG = LoggerFactory.getLogger(RawRequestLoggerInterceptor.class);

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        ContentCachingRequestWrapper contentCachingRequest = (ContentCachingRequestWrapper) request;
        String rawRequest = this.getRequestBody(contentCachingRequest);
        LOG.debug("Raw Request Payload is: [{}]", rawRequest);
        return true;
    }

    private String getRequestBody(final ContentCachingRequestWrapper wrapper) {
        String payload = null;
        if (wrapper != null) {
            byte[] buf = wrapper.getContentAsByteArray();
            if (buf.length > 0) {
                try {
                    int maxLength = buf.length > 500 ? 500 : buf.length;
                    payload = new String(buf, 0, maxLength, wrapper.getCharacterEncoding());
                } catch (UnsupportedEncodingException e) {
                    LOG.error("UnsupportedEncoding.", e);
                }
            }
        }
        return payload;
    }

}
```

Third, inject our customized interceptor:

```java
@EnableWebSecurity
@SpringBootApplication
public class ServiceRestApplication {

		... ...
		
    @Bean(name = DispatcherServletAutoConfiguration.DEFAULT_DISPATCHER_SERVLET_BEAN_NAME)
    public DispatcherServlet dispatcherServlet() {
        return new LoggableDispatcherServlet();
    }

    @Bean
    public ACSRequestMappingHandlerAdapter requestMappingHandlerAdapter() {
        return new ACSRequestMappingHandlerAdapter();
    }

    @Bean
    public WebMvcConfigurer webMvcConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addInterceptors(InterceptorRegistry registry) {
                registry.addInterceptor(rawRequestLoggerInterceptor).addPathPatterns("/**");
            }

        };
    }

}
```

### 2. Use annotaiton to log for specified APIs

There is an other more elegant way to do it. It will only print the request for APIs we need monitoring.

Create a customized annotation, then we can log only for the APIs that needed : [Logging Spring REST APIs with Annotation](https://dzone.com/articles/logging-spring-rest-apis).  



