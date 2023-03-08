---
title: 082: Integración de Spring Boot con Apache Kafka para transmisión de datos
description: 
published: true
date: 2023-02-02T22:24:15.444Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:24:13.691Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [082: Integrating Spring Boot with Apache Kafka for Streaming Data***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/082-integrating-spring-boot-with-apache-kafka-for-streaming-data)
{.links-list}


# 082: Integrando Spring Boot con Apache Kafka para transmisión de datos

En esta publicación, veremos cómo integrar Spring Boot con Apache Kafka para la transmisión de datos. Apache Kafka es una popular plataforma de transmisión de código abierto que se puede usar para crear aplicaciones de transmisión escalables, de alto rendimiento y de baja latencia. Spring Boot es un marco popular basado en Java que se puede usar para crear aplicaciones basadas en Spring independientes y de grado de producción.

La integración de Spring Boot con Apache Kafka puede proporcionar varios beneficios, entre ellos:

- La capacidad de procesar grandes cantidades de datos de manera escalable y eficiente
- La capacidad de crear aplicaciones basadas en eventos
- La capacidad de integrarse con otros sistemas y servicios de forma débilmente acoplada

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará para seguir esta publicación:

- Un entorno de desarrollo Java
- Apache Experto
- Un entorno de desarrollo Apache Kafka

## Configuración de un proyecto Spring Boot

Lo primero que debemos hacer es configurar un proyecto Spring Boot. Podemos hacer esto usando Spring Initializr. Para esta publicación, usaremos la siguiente configuración:

- Proyecto: Proyecto Maven
- Idioma: Java
- Arranque de primavera: 2.1.0
- Grupo: com.ejemplo
- Artefacto: kafka-streams
- Nombre: kafka-streams
- Descripción: Un ejemplo de Kafka Streams
- Nombre del paquete: com.example.kafka.streams
- Envase: Tarro
- Versión Java: 1.8
- Dependencias: Web, Lombok, Apache Kafka Streams

Una vez que haya configurado el proyecto, debería tener una estructura de directorios similar a esta:

```
kafka-streams
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── kafka
        │               └── streams
        │                   └── KafkaStreamsApplication.java
        └── resources
            └── application.properties
```

## Configuración de Spring Boot para Apache Kafka

Ahora que tenemos un proyecto Spring Boot configurado, debemos configurarlo para que funcione con Apache Kafka. Podemos hacer esto agregando las siguientes propiedades al archivo `application.properties`:

```
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.streams.properties.application.id=streams-demo
spring.kafka.streams.properties.commit.interval.ms=1000
spring.kafka.streams.properties.default.key.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
spring.kafka.streams.properties.default.value.serde=org.apache.kafka.common.serialization.Serdes$StringSerde
```

Echemos un vistazo a lo que hace cada una de estas propiedades:

- `spring.kafka.bootstrap-servers`: esta propiedad se utiliza para configurar los agentes de Kafka a los que se conectará la aplicación.
- `spring.kafka.streams.properties.application.id`: esta propiedad se usa para configurar el identificador único para la aplicación Kafka Streams.
- `spring.kafka.streams.properties.commit.interval.ms`: esta propiedad se usa para configurar la frecuencia con la que Kafka Streams confirmará las compensaciones.
- `spring.kafka.streams.properties.default.key.serde`: esta propiedad se usa para configurar la clave predeterminada para Kafka Streams.
- `spring.kafka.streams.properties.default.value.serde`: esta propiedad se usa para configurar el valor predeterminado serde para Kafka Streams.

## Creación de una aplicación de secuencias de Kafka

Ahora que nuestro proyecto está instalado y configurado, podemos comenzar a escribir nuestra aplicación Kafka Streams. Comenzaremos creando una nueva clase llamada `KafkaStreamsApplication`. Esta clase extenderá la clase `org.springframework.boot.SpringApplication` y la anotará con la anotación `@SpringBootApplication`:

```java
package com.example.kafka.streams;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class KafkaStreamsApplication {

    public static void main(String[] args) {
        SpringApplication.run(KafkaStreamsApplication.class, args);
    }

}
```

La anotación `@SpringBootApplication` es una anotación conveniente que se usa para configurar una aplicación Spring Boot. Es equivalente a usar las siguientes anotaciones:

- `@Configuration`: esta anotación se usa para indicar que una clase contiene una configuración de Spring Boot.
- `@EnableAutoConfiguration`: esta anotación se usa para habilitar la función de configuración automática de Spring Boot.
- `@ComponentScan`: esta anotación se usa para habilitar el escaneo de componentes de Spring.

## Creación de una topología de secuencias de Kafka

Ahora que tenemos configurada nuestra clase `KafkaStreamsApplication`, podemos comenzar a escribir nuestra topología de Kafka Streams. Una topología de Kafka Streams es un gráfico dirigido de nodos de procesamiento de flujo. En nuestra topología, tendremos dos nodos: un nodo fuente y un nodo sumidero.

El nodo fuente leerá los datos de un tema de entrada y el nodo sumidero escribirá los datos en un tema de salida. Podemos crear nuestra topología anotando la clase `KafkaStreamsApplication` con la anotación `@EnableKafkaStreams`:

```java
package com.example.kafka.streams;

import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.kstream.KStream;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.kafka.annotation.EnableKafkaStreams;
import org.springframework.kafka.annotation.StreamsBuilderFactoryBean;
import org.springframework.kafka.config.StreamsBuilderFactoryBeanCustomizer;

@SpringBootApplication
@EnableKafkaStreams
public class KafkaStreamsApplication {

    @Value("${spring.kafka.bootstrap-servers}")
    private String bootstrapServers;

    @Value("${spring.kafka.streams.properties.application.id}")
    private String applicationId;

    @Value("${spring.kafka.streams.properties.commit.interval.ms}")
    private String commitIntervalMs;

    @Value("${spring.kafka.streams.properties.default.key.serde}")
    private String defaultKeySerde;

    @Value("${spring.kafka.streams.properties.default.value.serde}")
    private String defaultValueSerde;

    public static void main(String[] args) {
        SpringApplication.run(KafkaStreamsApplication.class, args);
    }

    @Bean
    public StreamsBuilderFactoryBeanCustomizer streamsBuilderFactoryBeanCustomizer() {
        return new StreamsBuilderFactoryBeanCustomizer() {
            @Override
            public void customize(StreamsBuilderFactoryBean streamsBuilderFactoryBean) {
                streamsBuilderFactoryBean.setBootstrapServers(bootstrapServers);
                streamsBuilderFactoryBean.setApplicationId(applicationId);
                streamsBuilderFactoryBean.setCommitInterval(Long.parseLong(commitIntervalMs));
                streamsBuilderFactoryBean.setDefaultKeySerde(Serdes.String());
                streamsBuilderFactoryBean.setDefaultValueSerde(Serdes.String());
            }
        };
    }

    @Bean
    public KStream<String, String> kStream(StreamsBuilder kStreamBuilder) {
        KStream<String, String> stream = kStreamBuilder.stream("input-topic");
        stream.to("output-topic");
        return stream;
    }

}
```

Echemos un vistazo a lo que hace cada una de estas anotaciones y métodos:

- `@EnableKafkaStreams`: esta anotación se usa para habilitar Kafka Streams en una aplicación Spring Boot.
- `@Value("${spring.kafka.bootstrap-servers}")`: esta anotación se usa para inyectar la propiedad `spring.kafka.bootstrap-servers` en el campo `bootstrapServers`.
- `@Value("${spring.kafka.streams.properties.application.id}")`: esta anotación se usa para inyectar la propiedad `spring.kafka.streams.properties.application.id` en `applicationId` campo.
- `@Value("${spring.kafka.streams.properties.commit.interval.ms}")`: esta anotación se usa para inyectar la propiedad `spring.kafka.streams.properties.commit.interval.ms` en el campo `commitIntervalMs`.
- `@Value("${spring.kafka.streams.properties.default.key.serde}")`: esta anotación se usa para inyectar la propiedad `spring.kafka.streams.properties.default.key.serde` en el campo `defaultKeySerde`.
- `@Value("${spring.kafka.streams.properties.default.value.serde}")`: esta anotación se usa para inyectar la propiedad `spring.kafka.streams.properties.default.value.serde` en el campo `defaultValueSerde`.
- `public static void main(String[] args)`: Este es el método principal de la clase `KafkaStreamsApplication`. Este método se utiliza para iniciar la aplicación Spring Boot.
- `@Bean`: esta anotación se usa para indicar que un método produce un bean que se puede inyectar en otros beans administrados por Spring.
- `StreamsBuilderFactoryBeanCustomizer streamsBuilderFactoryBeanCustomizer()`: este método se utiliza para crear un bean `StreamsBuilderFactoryBeanCustomizer`. Este bean se utiliza para personalizar `StreamsBuilderFactoryBean`.
- `public void customize(StreamsBuilderFactoryBean streamsBuilderFactoryBean)`: Este es el método `customize` de la interfaz `StreamsBuilderFactoryBeanCustomizer`. Este método se utiliza para personalizar `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setBootstrapServers(bootstrapServers);`: esta línea se usa para configurar los servidores de arranque para `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setApplicationId(applicationId);`: esta línea se usa para establecer la identificación de la aplicación para `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setCommitInterval(Long.parseLong(commitIntervalMs));`: esta línea se usa para establecer el intervalo de confirmación para `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setDefaultKeySerde(Serdes.String());`: esta línea se usa para establecer la clave predeterminada serde para `StreamsBuilderFactoryBean`.
- `streamsBuilderFactoryBean.setDefaultValueSerde(Serdes.String());`: esta línea se usa para establecer el valor predeterminado serde para `StreamsBuilderFactoryBean`.
- `@Bean`: esta anotación se usa para indicar que un método produce un bean que se puede inyectar en otros beans administrados por Spring.
- `KStream<String, String> kStream(StreamsBuilder kStreamBuilder)`: Este método se usa para crear un bean `KStream`. Este bean se utiliza para representar la topología de procesamiento de flujo.
- `KStream<String, String> stream = kStreamBuilder.stream("input-topic");`: esta línea se usa para crear un `KStream` a partir del tema de entrada.
- `stream.to("output-topic");`: esta línea se utiliza para escribir los datos de `KStream` en el tema de salida.
- `return stream;`: Esta línea se utiliza para devolver el `KStream`.

## Creación y ejecución de la aplicación

Ahora que tenemos nuestra aplicación escrita, podemos compilarla y ejecutarla. Esto lo podemos hacer ejecutando el siguiente comando:

```
mvn spring-boot:run
```

Una vez que la aplicación está en funcionamiento, podemos comenzar a producir y consumir mensajes de los temas de entrada y salida.

## Conclusión

En esta publicación, analizamos cómo integrar Spring Boot con Apache Kafka para la transmisión de datos. También vimos cómo crear una topología de Kafka Streams y ejecutarla en una aplicación Spring Boot.