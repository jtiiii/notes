# Spring-boot

SpringBoot就是为了简化各类与spring框架结合的重复与繁琐的配置而出现的框架。

> 官方解释：
>
> Takes an opinionated view of building production-ready Spring applications. Spring Boot favors convention over configuration and is designed to get you up and running as quickly as possible.
>
> 对于构建用Spring构建的应用程序，SpringBoot 提出了自己的约定观点配置，来简化构建的操作，让您尽快的启动运行项目
>
> Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run". We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.
>
> Spring boot 能轻松建立基于Spring的生产级应用程序，你仅仅只需要运行即可。对于Spring平台与其他第三方依赖程序，我们有着自己的看法。对于此配置，您可以忽略或者不必在意。大多数SpringBoot项目仅仅需要很少的配置文件即可。



## Features 特性

- Create stand-alone Spring applications

  用于创建一个独立的Spring应用程序

- Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)

  直接支持Tomcat,Jetty或者Undertow（不需要去部署war文件）

- Provide opinionated 'starter' POMs to simplify your Maven configuration

  提供一个约定的用于开始的pom文件来简化你的maven配置

- Automatically configure Spring whenever possible

  尽量使用默认的设定来配置Spring

- Provide production-ready features such as metrics, health checks and externalized configuration

  提供为上生产环境做的准备的功能，比如健康度检查，外部配置等。

- Absolutely **no code generation** and **no requirement for XML** configuration

  不会生成任何代码，不会需要任何XML配置文件