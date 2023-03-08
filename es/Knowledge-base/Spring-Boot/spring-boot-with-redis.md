---
title: Bota Primavera con Redis
description: 
published: true
date: 2023-02-07T11:32:59.252Z
tags: 
editor: markdown
dateCreated: 2023-02-07T11:32:53.565Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot with Redis***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-with-redis)
{.links-list}


# Bota de primavera con Redis

Redis es un almacén de estructura de datos en memoria de código abierto que se utiliza como base de datos, caché y agente de mensajes. Admite estructuras de datos como cadenas, hashes, listas, conjuntos, conjuntos ordenados con consultas de rango, mapas de bits, hiperloglogs e índices geoespaciales con consultas de radio.

En este artículo, le mostraremos cómo usar Spring Boot con Redis.

## ¿Qué es Redis?

Redis es un almacén de estructura de datos en memoria de código abierto (con licencia BSD), que se utiliza como base de datos, caché y agente de mensajes. Admite estructuras de datos como cadenas, hashes, listas, conjuntos, conjuntos ordenados con consultas de rango, mapas de bits, hiperloglogs e índices geoespaciales con consultas de radio.

Redis tiene replicación integrada, secuencias de comandos Lua, desalojo de LRU, transacciones y diferentes niveles de persistencia en disco, y proporciona alta disponibilidad a través de Redis Sentinel y partición automática con Redis Cluster.

## Bota de primavera con Redis

Spring Boot proporciona soporte de primera clase para Redis. En esta sección, le mostraremos cómo usar Spring Boot con Redis.

Usaremos la biblioteca [lettuce](https://github.com/lettuce-io/lettuce-core) para comunicarnos con Redis. Lettuce es un cliente Redis totalmente sin bloqueo basado en Netty para manejar conexiones Redis y Spring Data para el mapeo de objetos.

### Dependencias Maven

Primero, necesitamos agregar las siguientes dependencias a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-redis</artifactId>
</dependency>
```

### Configuración de Redis

De forma predeterminada, Spring Boot buscará un servidor Redis en `localhost:6379`. Podemos cambiar esto configurando las propiedades `spring.redis.host` y `spring.redis.port` en nuestro archivo application.properties:

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

También podemos especificar una contraseña para Redis si está protegido por contraseña:

```properties
spring.redis.password=secret
```

### Redis de datos de primavera

Spring Data Redis es la implementación específica de Redis de Spring Data. Proporciona las abstracciones de los clientes Redis [Jedis](https://github.com/xetorthio/jedis) y [Lettuce](https://github.com/lettuce-io/lettuce-core) y proporciona un objeto unificado -Interfaz de mapeador para Redis.

#### Plantilla Redis

RedisTemplate es la clase central en Spring Data Redis. Define operaciones Redis de alto nivel contra los tipos de datos utilizados en las aplicaciones Spring.

Podemos configurar un RedisTemplate en nuestro contexto de aplicación Spring:

```java
@Bean
public RedisTemplate<String, Object> redisTemplate(
        RedisConnectionFactory factory) {
    RedisTemplate<String, Object> template = new RedisTemplate<>();
    template.setConnectionFactory(factory);
    return template;
}
```

#### StringRedisTemplate

StringRedisTemplate es una RedisTemplate especializada que está diseñada para manejar datos basados en cadenas en Redis.

Podemos configurar un StringRedisTemplate en nuestro contexto de aplicación Spring:

```java
@Bean
public StringRedisTemplate stringRedisTemplate(
        RedisConnectionFactory factory) {
    StringRedisTemplate template = new StringRedisTemplate();
    template.setConnectionFactory(factory);
    return template;
}
```

### Repositorios Redis

Spring Data Redis proporciona una abstracción de repositorio específica de Redis. Podemos usar esta abstracción para crear repositorios de Redis.

Primero, necesitamos crear una interfaz específica de Redis que amplíe la interfaz del Repositorio:

```java
public interface PersonRepository extends Repository<Person, String> {

    Person findById(String id);

    List<Person> findAll();

    Person save(Person person);

    void delete(Person person);
}
```

A continuación, necesitamos crear una implementación de nuestra interfaz PersonRepository:

```java
@Service
public class PersonRepositoryImpl implements PersonRepository {

    private final RedisTemplate<String, Person> redisTemplate;

    @Autowired
    public PersonRepositoryImpl(RedisTemplate<String, Person> redisTemplate) {
        this.redisTemplate = redisTemplate;
    }

    @Override
    public Person findById(String id) {
        return redisTemplate.opsForValue().get(id);
    }

    @Override
    public List<Person> findAll() {
        return redisTemplate.opsForValue().multiGet(redisTemplate.keys("*"));
    }

    @Override
    public Person save(Person person) {
        redisTemplate.opsForValue().set(person.getId(), person);
        return person;
    }

    @Override
    public void delete(Person person) {
        redisTemplate.delete(person.getId());
    }
}
```

En el ejemplo anterior, estamos usando RedisTemplate para interactuar con Redis.

### Datos de primavera Redis y Jackson

Spring Data Redis usa Jackson para serializar y deserializar objetos hacia y desde JSON. De forma predeterminada, Jackson está configurado para usar el introspector de anotaciones JAXB.

Podemos configurar Jackson para usar el introspector de anotaciones Jackson en lugar del introspector de anotaciones JAXB configurando la propiedad `spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS` en `true` en nuestro archivo application.properties:

```properties
spring.jackson.deserialization.USE_JACKSON_ANNOTATIONS=true
```

También podemos configurar Jackson para usar el introspector de anotaciones de Jackson usando un ObjectMapper personalizado:

```java
@Bean
public ObjectMapper objectMapper() {
    ObjectMapper mapper = new ObjectMapper();
    mapper.configure(DeserializationFeature.USE_JACKSON_ANNOTATIONS, true);
    return mapper;
}
```

## Conclusión

En este artículo, le mostramos cómo usar Spring Boot con Redis.