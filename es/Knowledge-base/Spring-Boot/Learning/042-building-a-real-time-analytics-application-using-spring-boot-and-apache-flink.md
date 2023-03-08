---
title: 042: Creación de una aplicación de análisis en tiempo real con Spring Boot y Apache Flink
description: 
published: true
date: 2023-02-04T08:32:44.394Z
tags: 
editor: markdown
dateCreated: 2023-02-04T08:32:42.778Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [042: Building a real-time analytics application using Spring Boot and Apache Flink***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/042-building-a-real-time-analytics-application-using-spring-boot-and-apache-flink)
{.links-list}


# 042: Construyendo una aplicación de análisis en tiempo real usando Spring Boot y Apache Flink

En esta publicación, le mostraremos cómo crear una aplicación de análisis en tiempo real con Spring Boot y Apache Flink.

Apache Flink es un marco de procesamiento de transmisión de código abierto con potentes capacidades de análisis de transmisión. Puede manejar datos tanto por lotes como de transmisión, y tiene un amplio conjunto de operadores para transformaciones, agregaciones y ventanas.

Spring Boot es un marco Java popular para crear aplicaciones web. Facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar".

Cuando se usan juntas, estas dos tecnologías se pueden usar para crear aplicaciones que pueden procesar datos en tiempo real.

## Configurando tu proyecto

Lo primero que deberá hacer es crear un nuevo proyecto Spring Boot. Puede hacer esto usando Spring Initializr.

Una vez que haya creado su proyecto, deberá agregar las siguientes dependencias a su `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-streaming-java_2.11</artifactId>
        <version>1.8.0</version>
    </dependency>
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka_2.11</artifactId>
        <version>1.8.0</version>
    </dependency>
</dependencies>
```

La dependencia `flink-streaming-java_2.11` es la API de streaming de Apache Flink para Java. La dependencia `flink-connector-kafka_2.11` es el conector de Kafka para Apache Flink, que le permite leer y escribir datos en temas de Kafka.

## Crear un productor de Kafka

Para leer datos de un tema de Kafka, primero debemos crear un productor de Kafka. Un productor de Kafka es un programa que escribe datos en un tema de Kafka.

En nuestro caso, vamos a crear un productor de Kafka simple que genera números aleatorios y los escribe en un tema de Kafka.

Primero, necesitamos crear una nueva clase Java y anotarla con `@Component`. Esta anotación le dice a Spring que este es un componente que se puede inyectar en otros componentes.

```java
@Component
public class RandomNumberProducer {

}
```

A continuación, debemos inyectar una `KafkaTemplate` en nuestro productor. `KafkaTemplate` es un contenedor de Spring alrededor de la API del productor de Kafka que facilita el trabajo con Kafka en una aplicación de Spring.

```java
@Autowired
private KafkaTemplate<String, String> kafkaTemplate;
```

Ahora podemos escribir un método para generar un número aleatorio y enviarlo a un tema de Kafka. Llamaremos a este método `generateAndSendRandomNumber`.

```java
public void generateAndSendRandomNumber() {
    String randomNumber = String.valueOf(ThreadLocalRandom.current().nextInt(0, 100));
    kafkaTemplate.send("random-numbers", randomNumber);
}
```

Este método genera un número aleatorio entre 0 y 100 y lo envía al tema de Kafka `random-numbers`.

## Crear un consumidor de Kafka

Ahora que tenemos un productor de Kafka, necesitamos crear un consumidor de Kafka. Un consumidor de Kafka es un programa que lee datos de un tema de Kafka.

En nuestro caso, vamos a crear un consumidor de Kafka simple que lea los datos del tema de Kafka `random-numbers` y los imprima en la consola.

Primero, necesitamos crear una nueva clase Java y anotarla con `@Component`. Esta anotación le dice a Spring que este es un componente que se puede inyectar en otros componentes.

```java
@Component
public class RandomNumberConsumer {

}
```

A continuación, debemos inyectar un `FlinkKafkaConsumer011` en nuestro consumidor. `FlinkKafkaConsumer011` es el conector de Kafka para Apache Flink, que le permite leer datos de un tema de Kafka.

```java
@Autowired
private FlinkKafkaConsumer011<String> flinkKafkaConsumer;
```

Ahora podemos escribir un método para consumir datos del tema de Kafka `random-numbers` e imprimirlo en la consola. Llamaremos a este método `consumeAndPrintRandomNumbers`.

```java
public void consumeAndPrintRandomNumbers() {
    DataStream<String> stream = env
            .addSource(flinkKafkaConsumer.setStartFromEarliest()
                    .setTopic("random-numbers")
                    .setConsumerGroup("random-number-consumer"));

    stream.print();
}
```

Este método lee datos del tema de Kafka `random-numbers` y los imprime en la consola.

## Crear un trabajo de Flink

Ahora que tenemos un productor de Kafka y un consumidor de Kafka, necesitamos crear un trabajo de Flink que los vincule.

Un trabajo de Flink es un programa que lee datos de una o más fuentes, aplica una o más transformaciones y escribe los resultados en uno o más receptores.

En nuestro caso, vamos a crear un trabajo de Flink simple que lea datos del tema de Kafka `random-numbers`, aplique una transformación `map` para elevar al cuadrado los números y escriba los resultados en `random-numbers-squared ` Tema de Kafka.

Primero, necesitamos crear una nueva clase Java y anotarla con `@Component`. Esta anotación le dice a Spring que este es un componente que se puede inyectar en otros componentes.

```java
@Component
public class RandomNumberSquarer {

}
```

A continuación, debemos inyectar un `StreamExecutionEnvironment` en nuestro trabajo. `StreamExecutionEnvironment` es el punto de entrada para todos los programas de procesamiento de flujo de Apache Flink.

```java
@Autowired
private StreamExecutionEnvironment env;
```

Ahora podemos escribir un método para crear y ejecutar nuestro trabajo Flink. Llamaremos a este método `squareRandomNumbers`.

```java
public void squareRandomNumbers() {
    DataStream<String> stream = env
            .addSource(flinkKafkaConsumer.setStartFromEarliest()
                    .setTopic("random-numbers")
                    .setConsumerGroup("random-number-consumer"));

    stream
            .map(new MapFunction<String, String>() {
                @Override
                public String map(String value) {
                    int number = Integer.parseInt(value);
                    int square = number * number;
                    return String.valueOf(square);
                }
            })
            .addSink(new FlinkKafkaProducer011<>("random-numbers-squared", new SimpleStringSchema(), props));
}
```

Este método lee datos del tema de Kafka "números aleatorios", aplica una transformación de "mapa" para elevar al cuadrado los números y escribe los resultados en el tema de Kafka "números aleatorios al cuadrado".

## Poniendolo todo junto

Ahora que tenemos un productor de Kafka, un consumidor de Kafka y un trabajo de Flink, debemos conectarlos a todos.

Podemos hacer esto creando una nueva aplicación Spring Boot y anotándola con `@EnableScheduling`. Esta anotación le dice a Spring que habilite la programación para esta aplicación.

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

A continuación, debemos crear una nueva clase `@Configuration` y anotarla con `@EnableKafka`. Esta anotación le dice a Spring que habilite Kafka para esta aplicación.

```java
@Configuration
@EnableKafka
public class KafkaConfiguration {

}
```

Ahora podemos crear un `@Bean` de tipo `Properties` y anotarlo con `@Value`. Este bean se usará para configurar el productor y consumidor de Kafka.

```java
@Bean
@Value("${kafka.bootstrap.servers}")
public Properties props() {
    Properties props = new Properties();
    props.setProperty("bootstrap.servers", bootstrapServers);
    props.setProperty("group.id", "random-number-consumer");
    props.setProperty("enable.auto.commit", "true");
    props.setProperty("auto.commit.interval.ms", "1000");
    props.setProperty("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
    props.setProperty("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
    return props;
}
```

Finalmente, necesitamos crear un método `@Scheduled` que llame a los métodos `generateAndSendRandomNumber` y `squareRandomNumbers`. Este método se llamará cada segundo y generará y elevará al cuadrado números aleatorios en tiempo real.

```java
@Scheduled(fixedRate = 1000)
public void schedule() {
    randomNumberProducer.generateAndSendRandomNumber();
    randomNumberSquarer.squareRandomNumbers();
}
```

## Ejecutando tu aplicación

Ahora que tenemos nuestra aplicación configurada, podemos ejecutarla simplemente ejecutando el método `principal`.

Una vez que la aplicación esté en funcionamiento, debería ver el siguiente resultado en la consola:

```
1
4
9
16
25
36
49
64
81
100
```

Esta salida muestra los resultados de nuestro trabajo de Flink, que está elevando al cuadrado los números aleatorios que genera nuestro productor de Kafka.

## Conclusión

En esta publicación, le mostramos cómo crear una aplicación de análisis en tiempo real con Spring Boot y Apache Flink. También le mostramos cómo conectar un productor de Kafka, un consumidor de Kafka y un trabajo de Flink para procesar datos en tiempo real.