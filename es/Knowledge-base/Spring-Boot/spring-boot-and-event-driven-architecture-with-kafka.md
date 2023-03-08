---
title: Spring Boot y arquitectura basada en eventos con Kafka
description: 
published: true
date: 2023-02-08T02:32:38.873Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:32:37.166Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and Event-Driven Architecture with Kafka***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-event-driven-architecture-with-kafka)
{.links-list}


# Spring Boot y arquitectura dirigida por eventos con Kafka

La arquitectura basada en eventos (EDA) es un patrón de diseño popular para crear aplicaciones escalables de alto rendimiento. En un sistema controlado por eventos, los eventos son generados por los usuarios o por los componentes del sistema a medida que ocurren. Estos eventos luego se propagan a los componentes que han registrado interés en ellos, para que puedan tomar las medidas adecuadas.

Kafka es una popular plataforma de transmisión de código abierto que se puede usar para crear arquitecturas basadas en eventos. Kafka es altamente escalable y tolerante a fallas, y ofrece alto rendimiento y baja latencia.

En este artículo, veremos cómo usar Spring Boot y Kafka para crear una arquitectura basada en eventos. También veremos cómo usar Spring Cloud Stream para simplificar el desarrollo de microservicios basados en eventos.

## Configuración de Kafka

Antes de que podamos comenzar a desarrollar nuestra arquitectura basada en eventos, debemos configurar un agente de Kafka. Kafka está disponible para descargar desde el [sitio web de Confluent] (https://www.confluent.io/download/).

Una vez que haya descargado y extraído Kafka, puede iniciar el intermediario ejecutando el siguiente comando:

```
bin/kafka-server-start.sh config/server.properties
```

## Creación de un proyecto Spring Boot

Usaremos Spring Boot para simplificar el desarrollo de nuestros microservicios. Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

Podemos usar [Spring Initializr](https://start.spring.io/) para crear un nuevo proyecto Spring Boot. Tendremos que seleccionar las siguientes dependencias:

- Internet
- Corriente de la nube
- Flujos de Kafka

![Inicializar resorte](https://i.imgur.com/RgC5koh.png)

Una vez que hayamos generado el proyecto, podemos importarlo a nuestro IDE de elección.

## Desarrollando al Productor

Nuestra arquitectura basada en eventos constará de un productor que genera eventos y un consumidor que procesa esos eventos. Comenzaremos por desarrollar el productor.

El productor será una aplicación Spring Boot simple que expone un punto final REST. Cuando se llama a este punto final, generará un evento y lo enviará a un tema de Kafka.

Primero, necesitaremos crear un nuevo tema de Kafka. Podemos hacer esto usando la CLI de Kafka:

```
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --topic events --partitions 1 --replication-factor 1
```

A continuación, crearemos un enlace Spring Cloud Stream que enviará eventos a nuestro tema de Kafka. Este enlace se definirá en el archivo `application.yml`:

```yaml
spring:
  cloud:
    stream:
      bindings:
        output:
          destination: events
          content-type: application/json
```

Ahora podemos crear nuestro controlador Spring Boot. Este controlador expondrá un punto final `/events` que se puede usar para generar eventos:

```java
@RestController
public class EventController {

    @Autowired
    private MessageChannel output;

    @PostMapping("/events")
    public void publishEvent(@RequestBody Event event) {
        output.send(MessageBuilder.withPayload(event).build());
    }
}
```

El controlador se anota con `@RestController` para indicar que expone puntos finales REST. También inyecta un bean `MessageChannel` que se utiliza para enviar mensajes al tema de Kafka.

Finalmente, necesitamos definir nuestra clase `Event`. Esta clase se utilizará para representar los eventos que genera el productor:

```java
public class Event {

    private String id;
    private String data;

    // Getters and setters
}
```

## Desarrollando al Consumidor

Ahora que hemos desarrollado al productor, podemos pasar al desarrollo del consumidor.

El consumidor será una aplicación Spring Cloud Stream que utiliza Kafka Streams para procesar los eventos que se envían al tema de Kafka.

Primero, crearemos un enlace Spring Cloud Stream que recibirá eventos del tema de Kafka. Este enlace se definirá en el archivo `application.yml`:

```yaml
spring:
  cloud:
    stream:
      bindings:
        input:
          destination: events
          content-type: application/json
```

A continuación, crearemos una topología de Kafka Streams que procesará los eventos. Esta topología se definirá en la clase `EventStreamsConfig`:

```java
@Configuration
public class EventStreamsConfig {

    @Bean
    public Topology buildTopology(StreamsBuilder builder) {
        // ...
    }
}
```

El método `buildTopology()` acepta `StreamsBuilder` como parámetro. Podemos usar este constructor para construir nuestra topología.

En nuestra topología, crearemos un flujo de eventos que se leen desde el tema de Kafka. Luego, procesaremos esta transmisión con un procesador Kafka Streams. Este procesador extraerá los datos de los eventos y los imprimirá en la consola:

```java
@Configuration
public class EventStreamsConfig {

    @Bean
    public Topology buildTopology(StreamsBuilder builder) {
        Stream<Event> stream = builder.stream("events", Consumed.with(Serdes.String(), new JsonSerde<>(Event.class)));
        stream.process(new ProcessorSupplier<String, Event>() {
            @Override
            public Processor<String, Event> get() {
                return new Processor<String, Event>() {
                    private ProcessorContext context;

                    @Override
                    public void init(ProcessorContext context) {
                        this.context = context;
                    }

                    @Override
                    public void process(String key, Event event) {
                        String data = event.getData();
                        System.out.println(data);
                    }

                    @Override
                    public void close() {
                    }
                };
            }
        });

        return builder.build();
    }
}
```

En esta topología, usamos `JsonSerde` para serializar y deserializar los eventos. Alternativamente, podríamos usar `StringSerde` si quisiéramos usar eventos de texto sin formato.

Ahora que hemos desarrollado el consumidor, podemos iniciarlo y probarlo enviando algunos eventos al tema de Kafka. Podemos usar la CLI de Kafka para producir eventos:

```
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic events
```

Y luego, en el productor, podemos ingresar algunos datos de eventos JSON:

```json
{"id":"1","data":"Hello, world!"}
```

Si revisamos los registros del consumidor, deberíamos ver los datos del evento que ingresamos:

```
Hello, world!
```

## Conclusión

En este artículo, hemos visto cómo usar Spring Boot y Kafka para construir una arquitectura basada en eventos. También hemos visto cómo usar Spring Cloud Stream para simplificar el desarrollo de microservicios basados en eventos.