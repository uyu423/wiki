---
title: 021: Creación y prueba de una aplicación Spring Boot con Junit
description: 
published: true
date: 2023-02-03T13:34:18.757Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:34:17.069Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [021: Building and testing a Spring Boot application with Junit***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/021-building-and-testing-a-spring-boot-application-with-junit)
{.links-list}


# 021: Construyendo y probando una aplicación Spring Boot con Junit

Junit es un marco de prueba popular para aplicaciones Java. Spring Boot es un marco basado en Java que se utiliza para crear microservicios y aplicaciones web. En esta publicación, le mostraremos cómo compilar y probar una aplicación Spring Boot con Junit.

Usaremos las siguientes herramientas en este tutorial:

-Java8
- Experto 3.3.9
- Eclipse Neón.3
- Junio 4.12

## Crear una aplicación Spring Boot

Comenzaremos creando una aplicación Spring Boot. Para este tutorial, usaremos el sitio web de Spring Initializr para generar nuestro proyecto.

Vaya al sitio web de Spring Initializr (https://start.spring.io/) e ingrese la siguiente información:

- Grupo: com.ejemplo
- Artefacto: junit-tutorial
- Nombre: junit-tutorial
- Descripción: proyecto de demostración para el tutorial de Junit
- Nombre del paquete: com.example.junit.tutorial
- Envase: Tarro
- Versión Java: 1.8
- Seleccione las siguientes dependencias: Web, JPA, H2, Lombok

Haga clic en Generar proyecto para descargar el proyecto.

Extraiga el archivo zip e impórtelo a Eclipse como un proyecto de Maven.

## Escribiendo un caso de prueba

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a escribir nuestro caso de prueba. Probaremos el siguiente escenario:

- Dado un usuario con el nombre de usuario "johndoe" y la contraseña "password"
- Cuando el usuario intenta iniciar sesión
- Entonces el usuario debería poder iniciar sesión correctamente

Cree una nueva clase Java en el paquete com.example.junit.tutorial.service y asígnele el nombre LoginServiceTest.java. Agregue el siguiente código a la clase:

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class LoginServiceTest {

    @Autowired
    private LoginService loginService;

    @Test
    public void testLogin() {
        // given
        String username = "johndoe";
        String password = "password";

        // when
        boolean result = loginService.login(username, password);

        // then
        assertTrue(result);
    }
}
```

En el código anterior, usamos las anotaciones @RunWith y @SpringBootTest para ejecutar nuestro caso de prueba. También estamos inyectando LoginService en nuestro caso de prueba para que podamos probar el método login().

El método login() toma un nombre de usuario y una contraseña y devuelve un valor booleano que indica si el inicio de sesión fue exitoso o no. En nuestro caso de prueba, estamos pasando el nombre de usuario y la contraseña "johndoe" y "contraseña". Luego afirmamos que el resultado es verdadero, lo que significa que el inicio de sesión fue exitoso.

## Ejecutar el caso de prueba

Para ejecutar el caso de prueba, haga clic con el botón derecho en la clase LoginServiceTest.java y seleccione Ejecutar como > Prueba JUnit.

Debería ver el siguiente resultado en la consola:

```
. ____ _ __ _ _
 /\\ / ___'_ __ _ _(_)_ __ __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/ ___)| |_)| | | | | || (_| | ) ) ) )
  ' |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot :: (v2.0.3.RELEASE)

2018-07-26 12:21:06.469 INFO 6484 --- [principal] c.e.j.t.s.LoginServiceTest: Iniciar LoginServiceTest en PC-LAPTOP con PID 6484 (iniciado por John Doe en C:\junit-tutorial)
2018-07-26 12:21:06.470 INFO 6484 --- [principal] c.e.j.t.s.LoginServiceTest: No se ha establecido un perfil activo, recurriendo a los perfiles predeterminados: predeterminado
2018-07-26 12:21:06.526 INFO 6484 --- [principal] s.c.a.AnnotationConfigApplicationContext: Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@4a3a4df7: fecha de inicio [jue 26 de julio 12:21:06 EDT 2018]; raíz de la jerarquía de contexto
2018-07-26 12:21:07.067 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Registro de beans para exposición JMX al inicio
2018-07-26 12:21:07.068 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Bean con el nombre 'dataSource' se ha detectado automáticamente para exposición JMX
2018-07-26 12:21:07.069 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'dataSource': registrándose con el servidor JMX como MBean [com.zaxxer.hikari:name=dataSource,type=HikariDataSource]
2018-07-26 12:21:07.076 INFO 6484 --- [principal] o.s.b.a.h2.H2ConsoleAutoConfiguration: consola H2 disponible en '/h2-console'. Base de datos disponible en 'jdbc:h2:mem:testdb'
2018-07-26 12:21:07.094 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: MBean ubicado 'h2:name=MemoryManagerService': registrándose con el servidor JMX como MBean [org.h2.mvstore.db.H2Database:name= Servicio de administrador de memoria]
2018-07-26 12:21:07.095 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: MBean ubicado 'h2:name=DatabaseStatusMBean': registrándose con el servidor JMX como MBean [org.h2.engine.DatabaseStatusMBean]
2018-07-26 12:21:07.097 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: MBean ubicado 'h2:name=DeadlockDetector': registrándose con el servidor JMX como MBean [org.h2.engine.DeadlockDetector]
2018-07-26 12:21:07.098 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: MBean ubicado 'h2:name=ThreadPool': registrándose con el servidor JMX como MBean [org.h2.engine.ThreadPool]
2018-07-26 12:21:07.102 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'h2:name=SessionTracker': registrándose con el servidor JMX como MBean [org.h2.engine.SessionTracker]
2018-07-26 12:21:07.104 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'h2:name=WebServer': registrándose con el servidor JMX como MBean [org.h2.tools.Server]
2018-07-26 12:21:07.105 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: MBean ubicado 'h2:name=ConnectionPool': registrándose con el servidor JMX como MBean [org.h2.engine.ConnectionPool]
2018-07-26 12:21:07.106 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: MBean ubicado 'h2:name=StatementTracker': registrándose con el servidor JMX como MBean [org.h2.engine.StatementTracker]
2018-07-26 12:21:07.107 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'h2:name=SystemProperties': registrándose con el servidor JMX como MBean [org.h2.engine.SystemProperties]
2018-07-26 12:21:07.108 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'h2:name=Versions': registrándose con el servidor JMX como MBean [org.h2.engine.Versions]
2018-07-26 12:21:07.109 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'h2:name=ClusterSettings': registrándose con el servidor JMX como MBean [org.h2.cluster.settings.ClusterSettings]
2018-07-26 12:21:07.110 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Ubicado MBean 'h2:name=ServerInfo': registrándose con el servidor JMX como MBean [org.h2.engine.ServerInfo]
2018-07-26 12:21:07.115 INFO 6484 --- [principal] o.s.b.w.embedded.tomcat.TomcatWebServer: Tomcat inicializado con puerto(s): 8080 (http)
2018-07-26 12:21:07.118 INFO 6484 --- [principal] o.apache.catalina.core.StandardService: servicio de inicio [Tomcat]
2018-07-26 12:21:07.118 INFO 6484 --- [principal] org.apache.catalina.core.StandardEngine: motor de servlet de inicio: Apache Tomcat/8.5.27
2018-07-26 12:21:07.119 INFO 6484 --- [ost-startStop-1] o.a.catalina.core.AprLifecycleListener: la biblioteca nativa de Apache Tomcat basada en APR que permite un rendimiento óptimo en entornos de producción no se encontró en java. biblioteca.ruta: [C:\Archivos de programa\Java\jdk1.8.0_171\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:/Archivos de programa/Java /jdk1.8.0_171/jre/bin/server;C:/Archivos de programa/Java/jdk1.8.0_171/jre/bin;C:/Archivos de programa/Java/jdk1.8.0_171/jre/lib/amd64;C: \ProgramData\Oracle\Java\javapath;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Archivos de programa\ Git\cmd;C:\Program Files\nodejs\;C:\Program Files (x86)\Brackets\command;C:\Users\John Doe\AppData\Local\Microsoft\WindowsApps;;.]
2018-07-26 12:21:07.154 INFO 6484 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/] : Inicializando Spring Embed WebApplicationContext
2018-07-26 12:21:07.154 INFO 6484 --- [ost-startStop-1] o.s.web.context.ContextLoader: Root WebApplicationContext: inicialización completada en 350 ms
2018-07-26 12:21:07.295 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean: Servlet dispatcherServlet asignado a [/]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: Filtro de asignación: 'characterEncodingFilter' a: [/*]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: filtro de asignación: 'hiddenHttpMethodFilter' a: [/*]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: Filtro de asignación: 'httpPutFormContentFilter' a: [/*]
2018-07-26 12:21:07.296 INFO 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: filtro de asignación: 'requestContextFilter' a: [/*]
2018-07-26 12: 21: 07.363 INFO 6484 --- [principal] j.LocalContainerEntityManagerFactoryBean: construcción de contenedor JPA EntityManagerFactory para unidad de persistencia 'predeterminada'
2018-07-26 12:21:07.364 INFO 6484 --- [principal] o.hibernate.jpa.internal.util.LogHelper: HHH000204: Procesando PersistenceUnitInfo [
nombre: predeterminado
...]
2018-07-26 12:21:07.380 INFO 6484 --- [principal] org.hibernate.Version: HHH000412: Hibernate Core {5.2.17.Final}
2018-07-26 12:21:07.381 INFO 6484 --- [principal] org.hibernate.cfg.Environment: HHH000206: hibernate.properties no encontrado
2018-07-26 12:21:07.381 INFO 6484 --- [principal] org.hibernate.cfg.Environment: HHH000021: Nombre del proveedor de código de bytes: javassist
2018-07-26 12:21:07.402 INFO 6484 --- [principal] o.hibernate.annotations.common.Version: HCANN000001: Hibernate Commons Annotations {5.0.1.Final}
2018-07-26 12:21:07.445 INFO 6484 --- [principal] org.hibernate.dialect.Dialect: HHH000400: Uso del dialecto: org.hibernate.dialect.H2Dialect
2018-07-26 12:21:07.502 INFO 6484 --- [principal] o.h.e.j.e.i.LobCreatorBuilderImpl: HHH000424: Deshabilitar la creación de LOB contextual porque la conexión era nula
2018-07-26 12:21:07.504 INFO 6484 --- [principal] org.hibernate.type.BasicTypeRegistry: HHH000270: el registro de tipo [java.util.UUID] anula el anterior: org.hibernate.type.UUIDBinaryType@6e3c0c47
2018-07-26 12:21:07.620 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Registro de beans para exposición JMX al inicio
2018-07-26 12:21:07.621 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Bean con el nombre 'dataSource' se ha detectado automáticamente para exposición JMX
2018-07-26 12:21:07.621 INFO 6484 --- [principal] o.s.j.e.a.AnnotationMBeanExporter: Bean con el nombre 'entityManagerFactory' ha sido autodetectado para exposición JMX
2018-07-26 12:21:07.621 INFO 6484 --- [principal] o.s.j.e.a.An