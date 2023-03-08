---
title: 094: Integrating Spring Boot with Apache Storm for Real-Time Processing
description: 
published: true
date: 2023-02-05T23:32:56.309Z
tags: 
editor: markdown
dateCreated: 2023-02-05T23:32:54.583Z
---

- [094: Integración de Spring Boot con Apache Storm para procesamiento en tiempo real***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/094-integrating-spring-boot-with-apache-storm-for-real-time-processing)
{.links-list}
- [094：将 Spring Boot 与 Apache Storm 集成以进行实时处理***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/094-integrating-spring-boot-with-apache-storm-for-real-time-processing)
{.links-list}
- [094: 실시간 처리를 위해 Apache Storm과 Spring Boot 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/094-integrating-spring-boot-with-apache-storm-for-real-time-processing)
{.links-list}


# 094: Integrating Spring Boot with Apache Storm for Real-Time Processing

In this post, we'll show how to integrate Spring Boot with Apache Storm for real-time processing.

Storm is a distributed stream processing framework that allows for easy and reliable processing of streaming data. It's a popular choice for processing real-time data, such as social media feeds, financial data, and sensor data.

Spring Boot is a popular Java framework that makes it easy to create stand-alone, production-grade Spring-based applications.

Integrating Storm with Spring Boot allows you to take advantage of the benefits of both frameworks. Storm provides the processing power and reliability needed for real-time data processing, while Spring Boot makes it easy to create and deploy your application.

## Prerequisites

Before we get started, there are a few things you'll need:

- A Java development environment
- Apache Maven
- Apache Storm

## Setting up your project

Let's start by creating a new Maven project. We'll name our project "storm-spring-boot-example".

In the project's pom.xml file, we'll need to add the following dependencies:

```xml
<dependencies>
	<dependency>
		<groupId>org.apache.storm</groupId>
		<artifactId>storm-core</artifactId>
		<version>1.1.1</version>
		<scope>provided</scope>
	</dependency>
	<dependency>
		<groupId>org.apache.storm</groupId>
		<artifactId>storm-kafka</artifactId>
		<version>1.1.1</version>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
</dependencies>
```

The storm-core and storm-kafka dependencies are provided by Apache Storm. The spring-boot-starter-web dependency is provided by Spring Boot.

## Configuring Storm

Now that we have our project set up, let's configure Storm.

We'll start by creating a new file named "storm.yaml" in the project's src/main/resources directory. In this file, we'll add the following configuration:

```yaml
storm.zookeeper.servers:
    - "localhost"
nimbus.seeds: ["localhost"]
storm.local.dir: "target/storm-data"
ui.port: 8080
logging.level: "INFO"
```

This configuration tells Storm to use a local ZooKeeper server and to store data in the target/storm-data directory. It also sets the UI port to 8080.

## Creating a topology

Now that we have Storm configured, let's create a topology. A topology is a graph of stream processing components that take in data, process it, and emit new data.

We'll start by creating a new file named "Topology.java" in the project's src/main/java/com/example directory. In this file, we'll add the following code:

```java
public class Topology {
	public static void main(String[] args) throws Exception {
		// Create a topology builder
		TopologyBuilder builder = new TopologyBuilder();
		
		// Set the spout
		builder.setSpout("kafka-spout", new KafkaSpout<>(getKafkaSpoutConfig()));
		
		// Set the bolts
		builder.setBolt("bolt1", new Bolt1()).shuffleGrouping("kafka-spout");
		builder.setBolt("bolt2", new Bolt2()).shuffleGrouping("bolt1");
		
		// Submit the topology
		Config config = new Config();
		config.setDebug(true);
		
		StormTopology topology = builder.createTopology();
		
		if (args.length == 0) {
			LocalCluster cluster = new LocalCluster();
			cluster.submitTopology("storm-spring-boot-example", config, topology);
		}
		else {
			StormSubmitter.submitTopology(args[0], config, topology);
		}
	}
	
	private static KafkaSpoutConfig<String, String> getKafkaSpoutConfig() {
		// Configure Kafka
		Map<String, Object> kafkaParams = new HashMap<>();
		kafkaParams.put("bootstrap.servers", "localhost:9092");
		kafkaParams.put("key.deserializer", StringDeserializer.class);
		kafkaParams.put("value.deserializer", StringDeserializer.class);
		kafkaParams.put("group.id", "storm-spring-boot-example");
		kafkaParams.put("auto.offset.reset", "latest");
		kafkaParams.put("enable.auto.commit", false);
		
		// Configure the Kafka spout
		KafkaSpoutConfig<String, String> kafkaSpoutConfig = KafkaSpoutConfig.builder(kafkaParams, getTopicMap())
			.setOffsetCommitPeriodMs(10_000)
			.setFirstPollOffsetStrategy(FirstPollOffsetStrategy.EARLIEST)
			.build();
		
		return kafkaSpoutConfig;
	}
	
	private static Map<String, List<String>> getTopicMap() {
		Map<String, List<String>> topicMap = new HashMap<>();
		topicMap.put("storm-topic", Collections.singletonList("storm-partition"));
		
		return topicMap;
	}
}
```

In this code, we start by creating a TopologyBuilder. This builder will be used to construct our topology.

Next, we set the spout. A spout is a component that reads data from an external source. In this case, we're using a KafkaSpout to read data from Kafka. We'll configure the Kafka spout in a moment.

After the spout, we set the bolts. Bolts are components that process data. In this topology, we have two bolts. The first bolt simply passes the data to the second bolt. The second bolt prints the data to the console.

Finally, we submit the topology. If we're running in local mode, we'll use a LocalCluster. If we're running in cluster mode, we'll use a StormSubmitter.

## Creating the Kafka spout

Now let's take a look at the Kafka spout configuration. We start by creating a Map of Kafka parameters. These parameters will be used to configure the Kafka spout.

Next, we create a KafkaSpoutConfig. This config tells the Kafka spout how to connect to Kafka and which topic to read from.

## Creating the bolts

Now let's take a look at the bolts. We start by creating a Bolt1 class. This bolt simply passes the data to the next bolt in the topology.

```java
public class Bolt1 extends BaseRichBolt {
	private OutputCollector collector;
	
	@Override
	public void prepare(Map<String, Object> config, TopologyContext context, OutputCollector collector) {
		this.collector = collector;
	}
	
	@Override
	public void execute(Tuple tuple) {
		collector.emit(tuple, new Values(tuple.getValue()));
		collector.ack(tuple);
	}
	
	@Override
	public void declareOutputFields(OutputFieldsDeclarer declarer) {
		declarer.declare(new Fields("value"));
	}
}
```

Next, we create a Bolt2 class. This bolt simply prints the data to the console.

```java
public class Bolt2 extends BaseRichBolt {
	private OutputCollector collector;
	
	@Override
	public void prepare(Map<String, Object> config, TopologyContext context, OutputCollector collector) {
		this.collector = collector;
	}
	
	@Override
	public void execute(Tuple tuple) {
		System.out.println(tuple.getValue());
		collector.ack(tuple);
	}
	
	@Override
	public void declareOutputFields(OutputFieldsDeclarer declarer) {
		// This bolt does not emit any data
	}
}
```

## Running the topology

Now that we have our topology created, let's run it.

If we're running in local mode, we can simply run the topology from our IDE. Storm will start a local cluster and submit the topology.

If we're running in cluster mode, we'll need to package our topology into a jar file and submit it to the cluster. We can do this using the following command:

```
mvn package
storm jar storm-spring-boot-example-0.0.1-SNAPSHOT.jar com.example.Topology storm-topology
```

## Conclusion

In this post, we've shown how to integrate Spring Boot with Apache Storm for real-time processing. We've created a topology that reads data from Kafka, processes it, and prints it to the console.

Integrating Storm with Spring Boot is a great way to take advantage of the benefits of both frameworks. Storm provides the processing power and reliability needed for real-time data processing, while Spring Boot makes it easy to create and deploy your application.