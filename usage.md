---
layout: default
title: Usage
nav_order: 3
---

# Configuration
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## How to use with GWT

You simply have to use the slf4j imports, define a logger and use it the slf4j way. 

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class GwtClientObject {
   public static final Logger LOG = LoggerFactory.getLogger(GwtClientObject.class);
   
   Integer value;
   Integer oldValue;
 
   public void setValue(Integer newValue) {
     oldValue = value;        
     value = newValue;

     LOG.debug("Value set to {}. Old value was {}.", value, oldValue);

     if(value.intValue() > 50) {
       LOG.info("value is bigger than 50");
     }
   }
} 
```

## Use parameters

In a plain GWT log message, you have to create a string and log it afterwards. With slf4gwt, you can use parameters in your log message and define a list of objects, that replaces the parameters. This makes the log message more readable in the program code and you don't need to polute the code with "if-log-level-enabled" checks. This is done just before logging and so it is encapsulated on a better place. Nevertheless you can check the log level, when you need to do time-consuming operations for logging.

Some log examples are here:

```java
// we use the LOG object from the example above
LOG.debug("This is a simple debug message without any dynamic value");

LOG.info("We log the object {} here", stringObj);

LOG.warn("You can log several objects like {}, {} and {}", obj1, obj2, obj3);
```

## Log exception

Additional to parameters, you can use exceptions in you log message as last parameter. This is not handled as the average parameter and so, you don't need to add the special paranthese notation here. This looks like this:

```java
LOG.debug("Some message, with exception", ex);

LOG.error("Message with one object {} and a exception", obj, ex);
```