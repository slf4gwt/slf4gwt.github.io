---
layout: default
title: Introduction
nav_order: 1
---

# Introduction

slf4gwt is a slf4j emulation for GWT. This project makes it possible to use the slf4j API on the 
GWT client side. So you can use slf4j on server AND client code.

## Motivation
On server code it is a common practice to use slf4j to hide the used logging framework. On GWT client side slf4j cannot 
be used and so it is up to the developer to keep an eye on her code and check where it runs. Especially the shared code is a problem here. The solution for this problem is slf4gwt.

Like the well-known slf4j, sl4fgwt uses a logging framework to write the log messages. GWT provides a <code>java.util.logging</code> implementation, and we use this implementation to write the messages to the right appender/handler.

## Inspiration
slf4gwt is inspired by some other open source projects. The most important one is
[gwt-log](https://github.com/fredsa/gwt-log) the former number one logging framework for GWT. With GWT 2.1 and the JUL emulation it lost it state and is nowadays in archived mode on Github. Next we like [slf4j-gwt](https://github.com/FinamTrade/slf4j-gwt) a lot, but the work on it stopped some years ago, and slf4gwt tries to bridge the gap and provide a state of the art version, that can be used with the current GWT releases.