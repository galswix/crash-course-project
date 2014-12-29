# BILoggerFactory


## Overview

a **BILoggerFactory** which you can use to get interface based BILoggers and case class based BILoggers.

### Migration from CFLogger

1. Remove @CFLogger from your logging class (where you declare your @BiEvent)

2. Declare a bean in your spring config which returns your interface and use the the BILoggerFactory to retrieve the interface.

3. Retrieve your logger with @Resource

```scala

@Bean 
def htmlRendererBILog: HtmlRendererBILog = BILoggerFactory.aBILoggerFor(classOf[HtmlRendererBILog]) //HtmlRendererBILog is a class that has @BiEvent(s)
```
```java
@Bean
public HtmlRendererBILog htmlRendererBILog() {
    return BILoggerFactory.aBILoggerFor(HtmlRendererBILog.class);
}

```
