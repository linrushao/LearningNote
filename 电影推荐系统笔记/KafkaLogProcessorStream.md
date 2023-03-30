## KafkaLogProcessorStream

### 1 依赖引入

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>recommender</artifactId>
        <groupId>org.example</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <artifactId>KafkaLogProcessorStream</artifactId>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>
    <dependencies>
        <!-- 用来连接Kafka的工具类 -->
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
            <version>0.10.2.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-streams</artifactId>
            <version>0.10.2.1</version>
        </dependency>
    </dependencies>

    <build>
        <finalName>kafkastream</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-assembly-plugin</artifactId>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>com.linrushao.Application</mainClass>
                        </manifest>
                    </archive>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                </configuration>
                <executions>
                    <execution>
                        <id>make-assembly</id>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

### 2 编写Java日志程序

设置日志过滤，过滤出我们想要的数据。直接实现Java中Processor封装的方法

```java
 @Override
    public void process(byte[] dummy, byte[] line) {
        // 把收集到的日志信息用string表示
        String input = new String(line);
        // 根据前缀MOVIE_RATING_PREFIX:从日志信息中提取评分数据
        if( input.contains("MOVIE_RATING_PREFIX:") ){
            System.out.println("movie rating data coming!>>>>>>>>>>>" + input);
            input = input.split("MOVIE_RATING_PREFIX:")[1].trim();
            context.forward( "logProcessor".getBytes(), input.getBytes() );
        }
    }
```

### 3 日志过滤

日志由生产者传到消费者中，直接通过程序连成一个通道

```java

builder.addSource("SOURCE", from)
    .addProcessor("PROCESS", () -> new LogProcessor(), "SOURCE")
    .addSink("SINK", to, "PROCESS");
```

- from：生产者
- 中间件：经过我们重写Processor的方法，将日志从生产者提取出来传到消费者中
- to：消费者

### 4 LogProcessor整体代码

```java
package com.linrushao;

import org.apache.kafka.streams.processor.Processor;
import org.apache.kafka.streams.processor.ProcessorContext;

/**
 * @Author LRS
 * @Date 2022/9/19 10:03
 * Desc
 */
public class LogProcessor implements Processor<byte[], byte[]> {
    //上下文
    private ProcessorContext context;
    @Override
    public void init(ProcessorContext processorContext) {
        this.context = processorContext;
    }
    @Override
    public void process(byte[] dummy, byte[] line) {
        // 把收集到的日志信息用string表示
        String input = new String(line);
        // 根据前缀MOVIE_RATING_PREFIX:从日志信息中提取评分数据
        if( input.contains("MOVIE_RATING_PREFIX:") ){
            System.out.println("movie rating data coming!>>>>>>>>>>>" + input);
            input = input.split("MOVIE_RATING_PREFIX:")[1].trim();
            context.forward( "logProcessor".getBytes(), input.getBytes() );
        }
    }
    @Override
    public void punctuate(long l) {

    }

    @Override
    public void close() {

    }
}
```

### 5 Application整体代码

```java
package com.linrushao;

import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.processor.TopologyBuilder;
import java.util.Properties;
import java.util.logging.Logger;
/**
 * @Author LRS
 * @Date 2022/9/19 10:01
 * Desc 主运行程序,kafka过滤程序
 */

public class Application {

    public static void main(String[] args) {
        String brokers = "hadoop201:9092";
        String zookeepers = "hadoop201:2181";

        // 输入和输出的topic
        String from = "log";//product
        String to = "recommender";//consume

        // 定义kafka streaming的配置
        Properties settings = new Properties();
        settings.put(StreamsConfig.APPLICATION_ID_CONFIG, "logFilter");
        settings.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, brokers);
        settings.put(StreamsConfig.ZOOKEEPER_CONNECT_CONFIG, zookeepers);
        // 创建 kafka stream 配置对象
        StreamsConfig config = new StreamsConfig(settings);
        // 创建一个拓扑建构器
        TopologyBuilder builder = new TopologyBuilder();

        // 定义流处理的拓扑结构
        builder.addSource("SOURCE", from)
                .addProcessor("PROCESS", () -> new LogProcessor(), "SOURCE")
                .addSink("SINK", to, "PROCESS");

        KafkaStreams streams = new KafkaStreams(builder, config);
        streams.start();

        System.out.println("Kafka stream started!>>>>>>>>>>>");
    }
}
```

