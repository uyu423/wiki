---
title: 094: 실시간 처리를 위해 Apache Storm과 Spring Boot 통합
description: 
published: true
date: 2023-02-05T23:33:00.044Z
tags: 
editor: markdown
dateCreated: 2023-02-05T23:32:54.576Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [094: Integrating Spring Boot with Apache Storm for Real-Time Processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/094-integrating-spring-boot-with-apache-storm-for-real-time-processing)
{.links-list}


# 094: 실시간 처리를 위해 Spring Boot와 Apache Storm 통합

이 게시물에서는 실시간 처리를 위해 Spring Boot를 Apache Storm과 통합하는 방법을 보여줍니다.

Storm은 스트리밍 데이터를 쉽고 안정적으로 처리할 수 있는 분산 스트림 처리 프레임워크입니다. 소셜 미디어 피드, 금융 데이터 및 센서 데이터와 같은 실시간 데이터를 처리하는 데 널리 사용되는 선택입니다.

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 인기 있는 Java 프레임워크입니다.

Storm을 Spring Boot와 통합하면 두 프레임워크의 이점을 모두 활용할 수 있습니다. Storm은 실시간 데이터 처리에 필요한 처리 능력과 안정성을 제공하는 반면 Spring Boot는 애플리케이션을 쉽게 만들고 배포할 수 있도록 합니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- 자바 개발 환경
- 아파치 메이븐
- 아파치 스톰

## 프로젝트 설정

새로운 Maven 프로젝트를 생성하여 시작하겠습니다. 프로젝트 이름을 "storm-spring-boot-example"로 지정합니다.

프로젝트의 pom.xml 파일에서 다음 종속성을 추가해야 합니다.

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

storm-core 및 storm-kafka 종속성은 Apache Storm에서 제공됩니다. spring-boot-starter-web 종속성은 Spring Boot에서 제공합니다.

## 스톰 구성

이제 프로젝트가 설정되었으므로 Storm을 구성하겠습니다.

프로젝트의 src/main/resources 디렉터리에 "storm.yaml"이라는 새 파일을 생성하여 시작하겠습니다. 이 파일에서 다음 구성을 추가합니다.

```yaml
storm.zookeeper.servers:
    - "localhost"
nimbus.seeds: ["localhost"]
storm.local.dir: "target/storm-data"
ui.port: 8080
logging.level: "INFO"
```

이 구성은 Storm에게 로컬 ZooKeeper 서버를 사용하고 target/storm-data 디렉터리에 데이터를 저장하도록 지시합니다. 또한 UI 포트를 8080으로 설정합니다.

## 토폴로지 만들기

이제 Storm을 구성했으므로 토폴로지를 생성해 보겠습니다. 토폴로지는 데이터를 받아 처리하고 새 데이터를 내보내는 스트림 처리 구성 요소의 그래프입니다.

프로젝트의 src/main/java/com/example 디렉토리에 "Topology.java"라는 새 파일을 생성하는 것으로 시작하겠습니다. 이 파일에 다음 코드를 추가합니다.

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

이 코드에서는 TopologyBuilder를 만드는 것으로 시작합니다. 이 빌더는 토폴로지를 구성하는 데 사용됩니다.

다음으로 주둥이를 설정합니다. 스파우트는 외부 소스에서 데이터를 읽는 구성 요소입니다. 이 경우 KafkaSpout을 사용하여 Kafka에서 데이터를 읽습니다. 잠시 후 Kafka 스파우트를 구성합니다.

주둥이 후에 볼트를 설정합니다. 볼트는 데이터를 처리하는 부품입니다. 이 토폴로지에는 두 개의 볼트가 있습니다. 첫 번째 볼트는 단순히 데이터를 두 번째 볼트로 전달합니다. 두 번째 볼트는 데이터를 콘솔에 인쇄합니다.

마지막으로 토폴로지를 제출합니다. 로컬 모드에서 실행 중인 경우 LocalCluster를 사용합니다. 클러스터 모드에서 실행 중인 경우 StormSubmitter를 사용합니다.

## Kafka 스파우트 만들기

이제 Kafka spout 구성을 살펴보겠습니다. Kafka 매개변수의 맵을 생성하여 시작합니다. 이 매개변수는 Kafka 스파우트를 구성하는 데 사용됩니다.

다음으로 KafkaSpoutConfig를 만듭니다. 이 구성은 Kafka spout에 Kafka에 연결하는 방법과 읽을 주제를 알려줍니다.

## 볼트 만들기

이제 볼트를 살펴보겠습니다. 먼저 Bolt1 클래스를 생성합니다. 이 볼트는 단순히 데이터를 토폴로지의 다음 볼트로 전달합니다.

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

다음으로 Bolt2 클래스를 생성합니다. 이 볼트는 단순히 데이터를 콘솔에 인쇄합니다.

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

## 토폴로지 실행

이제 토폴로지가 생성되었으므로 실행해 보겠습니다.

로컬 모드에서 실행 중인 경우 IDE에서 간단히 토폴로지를 실행할 수 있습니다. Storm은 로컬 클러스터를 시작하고 토폴로지를 제출합니다.

클러스터 모드에서 실행 중인 경우 토폴로지를 jar 파일로 패키징하고 클러스터에 제출해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
mvn package
storm jar storm-spring-boot-example-0.0.1-SNAPSHOT.jar com.example.Topology storm-topology
```

## 결론

이 게시물에서는 실시간 처리를 위해 Spring Boot를 Apache Storm과 통합하는 방법을 보여주었습니다. Kafka에서 데이터를 읽고 처리하고 콘솔에 출력하는 토폴로지를 만들었습니다.

Storm을 Spring Boot와 통합하는 것은 두 프레임워크의 이점을 모두 활용할 수 있는 좋은 방법입니다. Storm은 실시간 데이터 처리에 필요한 처리 능력과 안정성을 제공하는 반면 Spring Boot는 애플리케이션을 쉽게 만들고 배포할 수 있도록 합니다.