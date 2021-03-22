---
layout: default
title: Remote logging
nav_order: 5
---

# Configuration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Remote logging

GWT provides with java.util.logging a remote logging handler. This means you can log a message in the browser
and this message is transferred to the webserver. There you have a special logging servlet and the message is 
there logged to the server-side java.util.logging framework.

You can log a `warn` or `error` message from the client straight to the server to take care of further analysis.
Depending on the way the GWT application is rolled out, this may be the only way to get information about 
client problems.

The current GWT implementation loggs every browser log message directly to the server, as soon as the handler is
enabled. So you have two problems: first every log message is a new server call and second you have to choose the
browser log level wisely because on the loglevel Fine/Debug you can fill the bandwith up with debug log messages and
the whole application slows down.

## Remote logging improved

slf4gwt provides a new way to send log messages to the server. The remote log handler can filter the messages that find
their way down to the servlet and the bandwidth is not wasted. And the handler tries to collect batches of log messages before they are sent. With this you save some addtional bandwith and reduce the amount of server calls alot.

## Use the Remote Batch Logger

The Remote Batch logger is available within an extra JAR and you can even use it without using slf4gwt at all. 
Like all other our jars, you have to add the jar to your pom.xml or add it to your dependency management like any
other dependency.

```xml
<dependency>
    <groupId>org.slf4gwt</groupId>
    <artifactId>slf4gwt-remote</artifactId>
    <version>1.4</version>
</dependency>
```

Now you have to add the library to your `application.gwt.xml` file and configure the loglevel filter (if you like). If you don't define a filter minimum level, all log messages go via network to the servlet. Depending on your configuration, this can result in high network taffic.

```xml
<inherits name="org.slf4gwt.remote.batching.Enable" />
<!-- optional minium log level filter - possible values are TRACE, DEBUG, INFO, WARN, ERROR -->
<!-- default value is TRACE -->
<set-property name="slf4gwt.log.remote.batch.minLogLevel" value="WARN"/>
```

Then you should add the logging servlet _or_ your own servlet, that implements our interface (`org.slf4gwt.remote.batching.shared.RemoteBatchLoggingService`), to your web.xml with the path `remote_logging`. 

