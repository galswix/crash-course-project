# BILoggerFactory


## Overview

a **BILoggerFactory** which you can use to get interface based BILoggers and case class based BILoggers.

### Migration from CFLogger

* Remove @CFLogger from your logging class (where you declare your @BiEvent)

* Declare a bean in your spring config which returns your interface and use the the BILoggerFactory to retrieve the interface.

```scala

@Bean def htmlRendererBILog: HtmlRendererBILog = {
    return BILoggerFactory.aBILoggerFor(classOf[HtmlRendererBILog]) //HtmlRendererBILog is a class that has @BiEvent(s)
  }
```
```java
@Bean
public HtmlRendererBILog htmlRendererBILog() {
    return BILoggerFactory.aBILoggerFor(HtmlRendererBILog.class);
}

```

* Retrieve your logger with @Resource

### General usage

Please check the [tests](https://github.com/wix/wix-framework/blob/master/wix-bi-reporting/src/test/scala/com/wixpress/framework/bi/BIContractTest.scala) for usages example


