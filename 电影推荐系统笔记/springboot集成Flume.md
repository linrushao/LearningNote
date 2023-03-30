## springboot 集成 Flume

### 1 spring boot项目

springboot 2.3.7.RELEASE 和flume 1.9.0版本

再springboot项目中导入以下依赖：

```pom
 <!--flume日志采集的依赖-->
        <dependency>
            <groupId>org.apache.flume</groupId>
            <artifactId>flume-ng-sdk</artifactId>
            <version>1.9.0</version>
        </dependency>
        <!-- 引入logback-flume的依赖 -->
        <dependency>
            <groupId>com.teambytes.logback</groupId>
            <artifactId>logback-flume-appender_2.10</artifactId>
            <version>0.0.9</version>
        </dependency>
```

在resouce资源目录下创建logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true" scanPeriod="60 seconds" debug="false">

    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender" >
        <encoder>
            <pattern>%d{yyy MMM dd HH:mm:ss.SSS} [%thread] %-5level %logger{36}:%L- %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>

<!--此处为flume日志采集的配置-->
    <appender name="flume" class="com.teambytes.logback.flume.FlumeLogstashV1Appender">
        <flumeAgents>
<!--配置flume所在服务器的ip地址以及端口号。如果配置了主机名映射，可以填写主机名.-->
            hadoop201:44444
        </flumeAgents>
        <flumeProperties>
            connect-timeout=4000;
            request-timeout=8000
        </flumeProperties>
        <batchSize>1</batchSize>
        <reportingWindow>1</reportingWindow>
        <additionalAvroHeaders>
            myHeader=myValue
        </additionalAvroHeaders>
        <application>BusinessServerApplication</application>
        <layout class="ch.qos.logback.classic.PatternLayout">
            <!--这里可以自定义，定义为我们想要采集的内容即可-->
            <pattern>%msg%n</pattern>
        </layout>
    </appender>

    <!-- 控制台输出日志级别 -->
    <root level="INFO">
        <appender-ref ref="STDOUT" />
    </root>
    <!--这是你需要在项目中采集日志的全类名，我的日志信息是由此类产生的-->
    <logger name="com.linrushao.businessserver.controller.UserRatingController" level="INFO">
        <!--配置完成之后一定要在此处引入flume配置组件，不然flume接收不到发送的日志。-->
        <appender-ref ref="flume" />
    </logger>

</configuration>

```

### 2 flume配置

①在Linux中，flume是解压即用，自行下载解压

②在flume的conf目录下（其他目录也行）创建movielog.conf 配置文件，用来配置flume从哪里采集的信息发送到哪里去

```xml
# 声明基本组件 Source Channel Sink example2.properties
a1.sources = s1
a1.sinks = sk1
a1.channels = c1
# 配置Source组件,从Socket中接收本数据
a1.sources.s1.type = avro
<!--你的flume服务器IP地址或主机名-->
a1.sources.s1.bind = hadoop201
<!--flume 端口号，默认为44444，在配置文件中可以自行修改-->
a1.sources.s1.port = 44444
# 配置Sink组件,将接收数据输出到对应kafka
<!--以什么类型的数据发送-->
a1.sinks.sk1.type = org.apache.flume.sink.kafka.KafkaSink
<!--Kafka集群-->
a1.sinks.sk1.kafka.bootstrap.servers = hadoop201:9092
a1.sinks.sk1.kafka.topic = log
a1.sinks.sk1.kafka.flumeBatchSize = 20
a1.sinks.sk1.kafka.producer.acks = 1
a1.sinks.sk1.kafka.producer.linger.ms = 1
a1.sinks.sk1.kafka.producer.compression.type = snappy
a1.sinks.sk1.serializer.class=kafka.serializer.StringEncoder
a1.sinks.sk1.custom.encoding=UTF-8
# 配置Channel通道，主要负责数据缓冲
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100
# 进组件间的绑定
a1.sources.s1.channels = c1
a1.sinks.sk1.channel = c1
```

flume的启动命令:

```sh
bin/flume-ng agent --name a1 --conf-file conf/movielog.conf -Dflume.root.logger=INFO,console
```

### 3 kafka

利用Kafka测试

创建一个Kafka ==topic==和你flume文件中的topic一直

```
bin/kafka-topics.sh --create --zookeeper hadoop201:2181/kafka --replication-factor 3 --partitions 3 --topic log
```



启动Kafka消费者

```
bin/kafka-console-consumer.sh --bootstrap-server hadoop201:9092 --topic log
```

测试结果

![image-20221016150953211](springboot%E9%9B%86%E6%88%90Flume.assets/image-20221016150953211.png)