---
title: 094: Integración de Spring Boot con Apache Storm para procesamiento en tiempo real
description: 
published: true
date: 2023-02-05T23:33:00.044Z
tags: 
editor: markdown
dateCreated: 2023-02-05T23:32:54.580Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [094: Integrating Spring Boot with Apache Storm for Real-Time Processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/094-integrating-spring-boot-with-apache-storm-for-real-time-processing)
{.links-list}


# 094: Integrando Spring Boot con Apache Storm para procesamiento en tiempo real

En esta publicación, mostraremos cómo integrar Spring Boot con Apache Storm para el procesamiento en tiempo real.

Storm es un marco de procesamiento de flujo distribuido que permite un procesamiento fácil y confiable de datos de transmisión. Es una opción popular para procesar datos en tiempo real, como fuentes de redes sociales, datos financieros y datos de sensores.

Spring Boot es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

La integración de Storm con Spring Boot le permite aprovechar los beneficios de ambos marcos. Storm proporciona la potencia de procesamiento y la confiabilidad necesarias para el procesamiento de datos en tiempo real, mientras que Spring Boot facilita la creación e implementación de su aplicación.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

- Un entorno de desarrollo Java
- Apache Experto
- Tormenta apache

## Configurando tu proyecto

Comencemos creando un nuevo proyecto Maven. Llamaremos a nuestro proyecto "storm-spring-boot-example".

En el archivo pom.xml del proyecto, necesitaremos agregar las siguientes dependencias:

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

Apache Storm proporciona las dependencias storm-core y storm-kafka. Spring Boot proporciona la dependencia spring-boot-starter-web.

## Configuración de la tormenta

Ahora que tenemos nuestro proyecto configurado, configuremos Storm.

Comenzaremos creando un nuevo archivo llamado "storm.yaml" en el directorio src/main/resources del proyecto. En este archivo, agregaremos la siguiente configuración:

```yaml
storm.zookeeper.servers:
    - "localhost"
nimbus.seeds: ["localhost"]
storm.local.dir: "target/storm-data"
ui.port: 8080
logging.level: "INFO"
```

Esta configuración le dice a Storm que use un servidor ZooKeeper local y que almacene datos en el directorio target/storm-data. También establece el puerto de la interfaz de usuario en 8080.

## Crear una topología

Ahora que tenemos Storm configurado, creemos una topología. Una topología es un gráfico de componentes de procesamiento de flujo que reciben datos, los procesan y emiten nuevos datos.

Comenzaremos creando un nuevo archivo llamado "Topology.java" en el directorio src/main/java/com/example del proyecto. En este archivo, agregaremos el siguiente código:

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

En este código, comenzamos creando un TopologyBuilder. Este constructor se utilizará para construir nuestra topología.

A continuación, colocamos el pico. Un spout es un componente que lee datos de una fuente externa. En este caso, usamos un KafkaSpout para leer datos de Kafka. Configuraremos el surtidor de Kafka en un momento.

Después del pico, colocamos los pernos. Los pernos son componentes que procesan datos. En esta topología, tenemos dos tornillos. El primer perno simplemente pasa los datos al segundo perno. El segundo perno imprime los datos en la consola.

Finalmente, presentamos la topología. Si estamos ejecutando en modo local, usaremos un LocalCluster. Si estamos ejecutando en modo clúster, usaremos un StormSubmitter.

## Creando el caño Kafka

Ahora echemos un vistazo a la configuración del surtidor de Kafka. Comenzamos creando un mapa de parámetros de Kafka. Estos parámetros se utilizarán para configurar el surtidor de Kafka.

A continuación, creamos un KafkaSpoutConfig. Esta configuración le dice al canal de Kafka cómo conectarse a Kafka y de qué tema leer.

## Creando los tornillos

Ahora echemos un vistazo a los pernos. Comenzamos creando una clase Bolt1. Este perno simplemente pasa los datos al siguiente perno en la topología.

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

A continuación, creamos una clase Bolt2. Este perno simplemente imprime los datos en la consola.

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

## Ejecutar la topología

Ahora que tenemos nuestra topología creada, vamos a ejecutarla.

Si estamos ejecutando en modo local, simplemente podemos ejecutar la topología desde nuestro IDE. Storm iniciará un clúster local y enviará la topología.

Si estamos ejecutando en modo de clúster, necesitaremos empaquetar nuestra topología en un archivo jar y enviarlo al clúster. Esto lo podemos hacer usando el siguiente comando:

```
mvn package
storm jar storm-spring-boot-example-0.0.1-SNAPSHOT.jar com.example.Topology storm-topology
```

## Conclusión

En esta publicación, mostramos cómo integrar Spring Boot con Apache Storm para el procesamiento en tiempo real. Hemos creado una topología que lee datos de Kafka, los procesa y los imprime en la consola.

La integración de Storm con Spring Boot es una excelente manera de aprovechar los beneficios de ambos marcos. Storm proporciona la potencia de procesamiento y la confiabilidad necesarias para el procesamiento de datos en tiempo real, mientras que Spring Boot facilita la creación e implementación de su aplicación.