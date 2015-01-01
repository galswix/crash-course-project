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

### Interface Based BILogger

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
val logger = BILoggerFactory.aBILoggerFor(classOf[HtmlRendererBILog])
```
