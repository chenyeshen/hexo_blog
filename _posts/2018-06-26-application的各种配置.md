---
layout:     post
title:      application的各种配置
subtitle:   个人代码
date:       2018-06-26
author:     chenyeshen
header-img: img/bg25.jpg
catalog: true
tags:
    - Java
    - Springboot
    - Config 配置
---

## application的各种配置

### application-center-dev.yml

```
spring:
  profiles:
    include: [center]
  ####### database Config #######
  datasource:
    druid:
      connection-init-sqls: set names utf8mb4
      driver-class-name: com.mysql.jdbc.Driver
    type: com.alibaba.druid.pool.DruidDataSource
    url: jdbc:mysql://localhost:3306/yeshenblog?useUnicode=true&characterEncoding=utf-8&autoReconnect=true&zeroDateTimeBehavior=convertToNull&allowMultiQueries=true&useSSL=false&allowPublicKeyRetrieval=true
    username: root
    password: root
  ####### Redis Config #######
  redis:
    database: 6
    # Redis服务器地址
    host: 127.0.0.1
    # Redis服务器连接端口
    port: 6379
    # Redis服务器连接密码（默认为空）
    password: 123456

  ####### redis缓存服务配置 #######
  session:
    store-type: redis

  ####### 自定义配置 #######

  ####### 自定义配置 #######
```

### application.yml

```
# Server settings
server:
    port: 8086
    # HTTP请求和响应头的最大量，以字节为单位，默认值为4096字节,超过此长度的部分不予处理,一般8K。解决java.io.EOFException: null问题
    max-http-header-size: 8192
    use-forward-headers: true
    compression:
        enabled: true
        min-response-size: 1024
        mime-types: text/plain,text/css,text/xml,text/javascript,application/json,application/javascript,application/xml,application/xml+rss,application/x-javascript,application/x-httpd-php,image/jpeg,image/gif,image/png
    tomcat:
        remote-ip-header: X-Forwarded-for
        protocol-header: X-Forwarded-Proto
        port-header: X-Forwarded-Port
        uri-encoding: UTF-8
# SPRING PROFILES
spring:
    profiles:
        active: '@profileActive@'
    application:
        name: blog-admin
    freemarker:
        allow-request-override: false
        allow-session-override: false
        cache: false
        charset: UTF-8
        check-template-location: true
        content-type: text/html
        enabled: true
        expose-request-attributes: false
        expose-session-attributes: false
        expose-spring-macro-helpers: true
        prefer-file-system-access: true
        suffix: .ftl
        template-loader-path: classpath:/templates/
        settings:
            template_update_delay: 0
            default_encoding: UTF-8
            classic_compatible: true
    # HTTP ENCODING
    servlet:
        multipart:
            max-file-size: 50MB
            max-request-size: 50MB
    http:
        encoding:
            enabled: true
            charset: UTF-8
            force: true
    messages:
        encoding: UTF-8
    jmx:
        enabled: true
        default-domain: agentservice
    resources:
        chain:
            strategy:
                content:
                    enabled: true
                    paths: /**
    banner:
        charset: UTF-8
# MyBatis
mybatis:
    type-aliases-package: com.zyd.blog.persistence.beans
    mapper-locations: classpath:/mybatis/*.xml
# mapper
mapper:
    mappers:
        - com.zyd.blog.plugin.BaseMapper
    not-empty: false
    identity: MYSQL
# pagehelper
pagehelper:
    helper-dialect: mysql
    reasonable: true
    support-methods-arguments: true
    params: count=countSql
```

### application-dev.yml

```
# Server settings
server:
    tomcat:
        basedir: /var/tmp/website-blog-admin
# SPRING PROFILES
spring:
    profiles:
        include: [center-dev]
    # 指定默认MimeMessage的编码，默认为: UTF-8
    mail:
        default-encoding: UTF-8
        # 指定SMTP server使用的协议，默认为: smtp
        protocol: smtp
        # 指定SMTP server host.
        host: xxx
        port: 465
        # 指定SMTP server的用户名.
        username: xxx
        # 指定SMTP server登录密码:
        password: xxx
        # 指定是否在启动时测试邮件服务器连接，默认为false
        test-connection: false
        properties:
            mail.smtp.auth: true
            # 腾讯企业邮箱 下两个配置必须！！！
            mail.smtp.ssl.enable: true
            mail.smtp.socketFactory.class: javax.net.ssl.SSLSocketFactory
            mail.smtp.socketFactory.port: 465
            mail.smtp.starttls.enable: true
            mail.smtp.starttls.required: true
            mail.smtp.connectiontimeout: 50000
            mail.smtp.timeout: 30000
            mail.smtp.writetimeout: 50000
    # Redis数据库索引（默认为0）
    redis:
        jedis:

            pool:
                # 连接池最大连接数（使用负值表示没有限制）
                max-active: 8
                # 连接池最大阻塞等待时间（使用负值表示没有限制）
                max-wait: -1ms
                # 连接池中的最大空闲连接
                max-idle: 8
                # 连接池中的最小空闲连接
                min-idle: 0
        # 连接超时时间（毫秒）
        timeout: 5000ms
        # 默认的数据过期时间，主要用于shiro权限管理
        expire: 2592000

# logging settings
logging:
  path: /var/tmp/website-blog-admin
####################################自定义配置##########################################
app:
    # 是否启用kaptcha验证码
    enableKaptcha: false
    # shiro配置项
    shiro:
        loginUrl: "/passport/login/"
        successUrl: "/"
        unauthorizedUrl: "/error/403"
####################################自定义配置##########################################
```

### application.properties

```
# 激活环境
spring.profiles.active=dev

spring.mvc.view.prefix=/templates/
spring.mvc.view.suffix=.html
# mybatis配置
mybatis.mapper-locations=classpath:tech/wetech/myapp/modules/**/mapper/*.xml
mybatis.type-aliases-package=tech.wetech.myapp.modules.*.po
# 通用mapper配置
mapper.identity=MYSQL
mapper.mappers=tech.wetech.myapp.core.utils.MyMapper
mapper.not-empty=false
# 分页插件配置
pagehelper.helper-dialect=mysql
pagehelper.params=count=countSql
```

### application-dev.properties

```
debug=true
logging.level.root=debug
logging.level.tech.wetech.myapp.modules.*.mapper=trace

server.port=8887
server.servlet.context-path=/my-app

spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/consumer
spring.datasource.username=root
spring.datasource.password=root

spring.datasource.druid.initial-size=1
spring.datasource.druid.max-active=20
spring.datasource.druid.min-idle=1
spring.datasource.druid.stat-view-servlet.allow=true
spring.datasource.druid.test-on-borrow=true


spring.application.name=spirng-boot-rabbitmq

spring.rabbitmq.host=127.0.0.1
spring.rabbitmq.port=5672
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
```
### 最新配置

```
# log
logging.level.com.yeshen.xdvideo.mapper=debug


# Server settings
server:
    port: 8080
    # HTTP请求和响应头的最大量，以字节为单位，默认值为4096字节,超过此长度的部分不予处理,一般8K。解决java.io.EOFException: null问题
    max-http-header-size: 8192
    use-forward-headers: true
    compression:
        enabled: true
        min-response-size: 1024
        mime-types: text/plain,text/css,text/xml,text/javascript,application/json,application/javascript,application/xml,application/xml+rss,application/x-javascript,application/x-httpd-php,image/jpeg,image/gif,image/png
    tomcat:
        remote-ip-header: X-Forwarded-for
        protocol-header: X-Forwarded-Proto
        port-header: X-Forwarded-Port
        uri-encoding: UTF-8
        basedir: /var/tmp/website-app

################################### 数据源配置 ###################################
# SPRING PROFILES
spring:
    datasource:
        type: com.alibaba.druid.pool.DruidDataSource
        driver-class-name: com.mysql.jdbc.Driver
        url: jdbc:mysql://localhost:3306/xdvideo?useUnicode=true&characterEncoding=utf-8&autoReconnect=true&zeroDateTimeBehavior=convertToNull&allowMultiQueries=true&useSSL=false
        username: root
        password: root
    application:
        name: xdvideo
    # HTTP ENCODING
    http:
        multipart:
            max-file-size: 2MB
            max-request-size: 10MB
        encoding:
            enabled: true
            charset: UTF-8
            force: true
    messages:
        encoding: UTF-8
    jmx:
        enabled: true
        default-domain: agentservice
    resources:
        chain:
            strategy:
                content:
                    enabled: true
                    paths: /**
    # redis缓存服务配置
    session:
        store-type: redis
    # Redis数据库索引（默认为0）
#    redis:
#        database: 1
#        # Redis服务器地址
#        host: 127.0.0.1
#        # Redis服务器连接端口
#        port: 6379
#        # Redis服务器连接密码（默认为空）
#        password: 123456
#        # 连接池最大连接数（使用负值表示没有限制）
#        pool:
#            maxActive: 8
#            # 连接池最大阻塞等待时间（使用负值表示没有限制）
#            maxWait: -1
#            # 连接池中的最大空闲连接
#            maxIdle: 8
#            # 连接池中的最小空闲连接
#            minIdle: 0
#        # 连接超时时间（毫秒）
#        timeout: 0
#        # 默认的数据过期时间，主要用于shiro权限管理
#        expire: 2592000

# MyBatis
mybatis:

  configuration:
    map-underscore-to-camel-case: true
    cache-enabled: true
#    type-aliases-package: com.yeshen.xdvideo.domain
#    mapper-locations: classpath:/mapper/*.xml

# pagehelper
pagehelper:
    helper-dialect: mysql
    reasonable: true
    support-methods-arguments: true
    params: count=countSql

################################### 程序自定义配置 ###################################
yeshen:
    druid:
        # druid访问用户名（默认：zyd-druid）
        username: zyd-druid
        # druid访问密码（默认：zyd-druid）
        password: zyd-druid
        # druid访问地址（默认：/druid/*）
        servletPath: /druid/*
        # 启用重置功能（默认false）
        resetEnable: false
        # 白名单(非必填)， list
        allowIps[0]:
        # 黑名单(非必填)， list
        denyIps[0]:
```
