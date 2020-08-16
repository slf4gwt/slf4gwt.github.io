---
layout: default
title: Configuration
nav_order: 2
---

# Configuration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Important information

slf4gwt is in beta state for now, the configuration and the behavior may change
{: .label .label-yellow }

## dependency managment

slf4gwt is listed on maven central and so you can simply add the library to your dependency management system as long as maven central is supported. Maven itself supports maven central directly and so you only hve to add these lines to your pom.xml. Please check mven central for other system syntax.

```xml
<dependency>
    <groupId>org.slf4gwt</groupId>
    <artifactId>slf4gwt</artifactId>
    <version>1.0</version>
</dependency>
```

## connect to your application

You can really simple use slf4gwt in your application and you only need to add this <code>inherits</code> line to your <code>gwt.xml</code> file.

```xml
<inherits name="org.slf4jgwt.logging.gwt.Logging"/>
```

## set the log level

The default log level for slf4gwt is INFO, but you can override it in your <code>gwt.xml</code> file by adding this line. Supported log levels are <code>TRACE</code>, <code>DEBUG</code>, <code>INFO</code>, <code>WARN</code> and <code>ERROR</code>.

```xml
<set-property name="slf4gwt.log.level" value="INFO"/>
```

## define your appenders/handlers

As with the originals slf4j, you can choose different appenders to which you pipe the log files to. But in contrast to slf4j, the selected appenders are addressed in parallel and the output can thus be influenced via the following configuration.

```xml
<set-property name="slf4gwt.log.handler.console" value="ENABLED" />
<set-property name="slf4gwt.log.handler.developmentMode" value="ENABLED" />
<set-property name="slf4gwt.log.handler.hasWidgets" value="DISABLED" />
<set-property name="slf4gwt.log.handler.system" value="DISABLED" />
<set-property name="slf4gwt.log.handler.simpleRemote" value="DISABLED" />
```

The shown example is the default configuration, <code>console</code> and <code>developmentMode</code> logging are enabled by default. Everything else is disabled. It's up to you, to select a suitable appender configuration.

## development and production mode

Normally the logging is enabled in development mode and disabled in production mode.
If you need to get logs on production mode, you have to enable the GWT logging as defined on the
[GWT logging manual](http://www.gwtproject.org/doc/latest/DevGuideLogging.html#Configuring_GWT_Logging). Or simply add this line to you *.gwt.xml file:

```xml
<set-property name="gwt.logging.enabled" value="TRUE"/>
```

Possible values are <code>TRUE</code>, <code>WARNING</code>, <code>SEVERE</code> and <code>FALSE</code> (if you don't need any logging at all).