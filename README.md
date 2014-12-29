# BILoggerFactory


## Overview

a **BILoggerFactory** which you can use to get interface based BiLoggers and case class based BiLoggers.

### Migration from CFLogger

Declare a bean in your spring config which returns your interface and use the the BILoggerFactory to retrieve the interface.

```scala

@Bean def htmlRendererBILog: HtmlRendererBILog = {
    return BILoggerFactory.aBILoggerFor(classOf[HtmlRendererBILog])
  }
```
```java
@Bean
public EditorLog editorLog() {
    return BILoggerFactory.aBILoggerFor(EditorLog.class);
}

```
