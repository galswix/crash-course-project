# BILoggerFactory


## Overview

a **BILoggerFactory** which you can use to get interface based BILoggers and case class based BILoggers.

##Migration
### Migration from CFLogger

* Remove @CFLogger from your logging class (where you declare your @BiEvent)

* Declare a bean in your spring config which returns your interface and use the the BILoggerFactory to retrieve the interface.

```scala

@Bean def htmlRendererBILog: HtmlRendererBILog = {
     BILoggerFactory.aBILoggerFor(classOf[HtmlRendererBILog]) //HtmlRendererBILog is a class that has @BiEvent(s)
  }
```
```java
@Bean
public HtmlRendererBILog htmlRendererBILog() {
    return BILoggerFactory.aBILoggerFor(HtmlRendererBILog.class);
}

```

* Retrieve a logger with @Resource

##Usage

### Interface based BILogger

* Create a logging interface and declare your @BiEvent(s)
```java
public interface HtmlRendererBILog {
    
    public static final String RENDERING_HTML_SITE = "Rendering HTML Site";
    public static final String HTML_SITE_NOT_FOUND = "Html Site not Found";
    public static final int RENDERING_HTML_SITE_ID = 4100;
    public static final int HTML_SITE_NOT_FOUND_ID = 4101;

    @BiEvent(biEvent = RENDERING_HTML_SITE, biEventId = RENDERING_HTML_SITE_ID)
    void renderingHtmlSite(@ParamName("renderer") String renderer,
                           @ParamName("baseUri") String baseUri,
                           @ParamName("applicationId") String applicationId,
                           @ParamName("domain") String domain,
                           @ParamName("documentType") DocumentType documentType,
                           @ParamName("path") String path,
                           @ParamName("rendererResult") ProcessorResult result);

    @BiEvent(biEvent = HTML_SITE_NOT_FOUND, biEventId = HTML_SITE_NOT_FOUND_ID)
    void htmlSiteNotFound(@ParamName("renderer") String renderer,
                          @ParamName("baseUri") String baseUri,
                          @ParamName("applicationId") String applicationId,
                          @ParamName("documentType") DocumentType documentType,
                          @ParamName("path") String path);
}
```
* Retrieve a logger

```scala
val biLog = BILoggerFactory.aBILoggerFor(classOf[HtmlRendererBILog])
```
(Or through @Bean and @Resource or )

* Log BiEvents

```scala
biLog.renderingHtmlSite("name", "/baseUri", "appId","domain", "docType", "path", result);
```

### Case class based BILogger

* Create a logger
```scala
val exampleSource = 28
val logger = BILoggerFactory.aBILogger(eventSource = exampleSource, markerName = "name")
```

* Create case class based BiEvent
```scala
case class MyEvent(user: String) extends BIEvent(32)
```

* Log BiEvent
```scala
logger.log(MyEvent("gals"))
```

##One more thing...

As always, start with checking out the [tests](https://github.com/wix/wix-framework/blob/master/wix-bi-reporting/src/test/scala/com/wixpress/framework/bi/BIContractTest.scala)
