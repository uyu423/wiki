---
title: Procesamiento Spring Boot XML con JAXB
description: 
published: true
date: 2023-02-03T05:58:44.967Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:58:43.290Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot XML Processing with JAXB***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-xml-processing-with-jaxb)
{.links-list}


# Procesamiento Spring Boot XML con JAXB

Java Architecture for XML Binding (JAXB) es una tecnología que permite a los desarrolladores de Java asignar objetos Java a representaciones XML. JAXB proporciona dos funciones principales: la capacidad de convertir objetos Java en XML y la capacidad de convertir XML nuevamente en objetos Java.

En este artículo, veremos cómo usar JAXB con Spring Boot para procesar archivos XML. Comenzaremos con una breve descripción general de JAXB y luego profundizaremos en algunos ejemplos de código.

## ¿Qué es JAXB?

Como mencionamos anteriormente, JAXB le permite asignar objetos Java a representaciones XML y viceversa. JAXB proporciona anotaciones que puede usar para asignar objetos Java a elementos XML. Una vez que haya anotado sus clases Java, puede usar la API JAXB para clasificarlas (o convertirlas) en XML. También puede usar la API JAXB para descomponer (o convertir) XML nuevamente en objetos Java.

JAXB es una tecnología estándar que forma parte de la plataforma Java SE. JAXB también se incluye en las plataformas Java EE. JAXB existe desde hace mucho tiempo y es una tecnología probada y ampliamente utilizada.

## Uso de JAXB con Spring Boot

Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar". Usaremos Spring Boot en este artículo para facilitar la puesta en marcha con nuestro ejemplo de procesamiento XML.

Para usar JAXB con Spring Boot, debe agregar la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
   <groupId>com.sun.xml.bind</groupId>
   <artifactId>jaxb-impl</artifactId>
   <version>2.2.11</version>
</dependency>
```

Con esta dependencia en su lugar, ahora podemos crear una aplicación Spring Boot que use JAXB para procesar XML.

## Creación de una aplicación Spring Boot

Comenzaremos creando una aplicación Spring Boot simple que use JAXB para clasificar y desclasificar XML. Para hacer esto, usaremos la dependencia `spring-boot-starter-jaxb`. Esta dependencia extraerá todas las dependencias que necesitamos para usar JAXB con Spring Boot.

Aquí está el archivo `pom.xml` para nuestro proyecto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-jaxb-example</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>spring-boot-jaxb-example</name>
    <description>Example project for Spring Boot</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-jaxb</artifactId>
        </dependency>

        <dependency>
            <groupId>javax.xml.bind</groupId>
            <artifactId>jaxb-api</artifactId>
            <version>2.3.0</version>
        </dependency>

        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-impl</artifactId>
            <version>2.3.0</version>
        </dependency>

        <dependency>
            <groupId>com.sun.xml.bind</groupId>
            <artifactId>jaxb-core</artifactId>
            <version>2.3.0</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>


</project>

```

Tenga en cuenta que hemos incluido las dependencias `jaxb-api`, `jaxb-impl` y `jaxb-core` además de la dependencia `spring-boot-starter-jaxb`. Estas dependencias son necesarias para que nuestra aplicación compile.

Ahora que tenemos nuestras dependencias en su lugar, creemos una aplicación Spring Boot simple que use JAXB para clasificar y desclasificar XML.

## Marshalling y Unmarshaling XML con JAXB

Comenzaremos creando una aplicación Spring Boot simple que use JAXB para clasificar y desclasificar XML. Para hacer esto, crearemos una clase `Person` que podemos usar para representar a una persona en XML. Anotaremos esta clase con anotaciones JAXB para que podamos ordenarla en XML.

Aquí está la clase `Persona`:

```java
package com.example.xml;

import javax.xml.bind.annotation.XmlAccessType;
import javax.xml.bind.annotation.XmlAccessorType;
import javax.xml.bind.annotation.XmlAttribute;
import javax.xml.bind.annotation.XmlRootElement;

@XmlRootElement(name = "person")
@XmlAccessorType(XmlAccessType.FIELD)
public class Person {

    @XmlAttribute
    private String firstName;

    @XmlAttribute
    private String lastName;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

}
```

Como puede ver, hemos anotado esta clase con las anotaciones `@XmlRootElement` y `@XmlAccessorType`. También hemos anotado los campos `firstName` y `lastName` con la anotación `@XmlAttribute`. Estas anotaciones le dicen a JAXB cómo mapear la clase `Person` a XML.

Ahora que tenemos nuestra clase `Person`, escribamos una aplicación Spring Boot simple que use JAXB para clasificar y desclasificar XML.

Aquí está la clase `Aplicación`:

```java
package com.example.xml;

import java.io.StringReader;

import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Marshaller;
import javax.xml.bind.Unmarshaller;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

	public static void main(String[] args) throws JAXBException {
		SpringApplication.run(Application.class, args);
		
		JAXBContext jaxbContext = JAXBContext.newInstance(Person.class);
		Marshaller marshaller = jaxbContext.createMarshaller();
		marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, true);
		
		Person person = new Person();
		person.setFirstName("John");
		person.setLastName("Doe");
		
		marshaller.marshal(person, System.out);
		
		String xml = "<person firstName=\"Jane\" lastName=\"Doe\"/>";
		
		Unmarshaller unmarshaller = jaxbContext.createUnmarshaller();
		Person person2 = (Person) unmarshaller.unmarshal(new StringReader(xml));
		
		System.out.println(person2.getFirstName());
		System.out.println(person2.getLastName());
	}

}
```

En esta clase, hemos creado un método `principal` que utiliza la API JAXB para clasificar y desclasificar XML. Primero, creamos un `JAXBContext` y lo usamos para crear un `Marshaller`. Establecemos la propiedad `JAXB_FORMATTED_OUTPUT` en `true` para que el XML tenga un buen formato cuando se ordene.

A continuación, creamos un objeto `Person` y configuramos los campos `firstName` y `lastName`. Luego, clasificamos el objeto `Person` en XML y lo imprimimos en la consola.

Finalmente, creamos una cadena XML que representa una `Persona`. Luego usamos el 'JAXBContext' para crear un 'Unmarshaller' y lo usamos para desarmar la cadena XML de nuevo en un objeto 'Persona'. Imprimimos los campos `firstName` y `lastName` del objeto `Person` en la consola para verificar que se desmarcó correctamente.

Si ejecutamos esta aplicación, deberíamos ver el siguiente resultado:

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<person firstName="John" lastName="Doe"/>
Jane
Doe
```

Como podemos ver, el XML se ordenó y desarmó correctamente.

## Conclusión

En este artículo, analizamos cómo usar JAXB con Spring Boot para procesar archivos XML. Comenzamos con una breve descripción general de JAXB y luego profundizamos en algunos ejemplos de código.

JAXB es una tecnología bien establecida que se usa ampliamente para procesar XML en aplicaciones Java. JAXB proporciona una forma sencilla de asignar objetos Java a XML y viceversa. Spring Boot facilita el uso de JAXB en sus aplicaciones con algunas dependencias simples.

Esta es solo una breve introducción al uso de JAXB con Spring Boot. Si está interesado en obtener más información, consulte los siguientes recursos:

* [Tutorial de Spring Boot y XML](https://spring.io/blog/2013/12/19/building-a-restful-web-service-with-xml-payloads)
* [Tutorial JAXB](https://www.javatpoint.com/jaxb-tutorial)
* [Procesamiento Java XML con JAXB](https://www.baeldung.com/jaxb-tutorial)