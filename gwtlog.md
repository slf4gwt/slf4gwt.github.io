---
layout: default
title: gwt-log compatibility layer
nav_order: 4
---

# Configuration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What's gwt-log?
Back in the early days of GWT, there was no logging framework and so gwt-log was introduced.
Old projects may still stay on gwt-log, because it takes much time to migrate to another framework.
Slf4GWT likes to make the transition much more easy and so we implemented a compatibiliy layer.

The idea is to add our gwtlog jar to your project and configure slf4gwt. Then your old gwt-log calls work
as before, but use the new slf4gwt framework. Then you can move one class after another to slf4gwt and
remove the gwtlog compatibility layer in the end. 

## Dependency

```xml
<dependency>
    <groupId>org.slf4gwt</groupId>
    <artifactId>slf4gwt-gwtlog</artifactId>
    <version>1.4</version>
</dependency>
```

## Connect it with our application

Normally you should already have the `gwt-log.jar` file in our classpath and to connect our compatibility 
layer with your application, you have to remove the gwt-log jar first. Additionally you can comment out the
old gwt-log configuration in your gwt.xml file.

Your IDE should show you many errors, because the gwt-log Log class is missing in our classpath.

Now you can connect the compatibility layer by putting one `inherit` line to our gwt.xml file.

```xml
<inherits name="com.allen_sauer.gwt.log.gwt-log"/>
```

After the changes, your IDE should go back to a almost normal state. Maybe there are some minor issue, like the
UncaughtExceptionHandler, but this can be fixed easily.

After these changes you are ready to switch all logging to slf4gwt and can still have some old gwt-log log messages
in our code.