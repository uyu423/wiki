---
title: Plantillas de proyectos de inicio de Spring Boot
description: 
published: true
date: 2023-02-01T18:57:50.191Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:57:48.593Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [Spring Boot Starter Project Templates***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-starter-project-templates)
{.links-list}


# Plantillas de proyectos de inicio de Spring Boot

Desarrollar una aplicación Spring Boot puede ser una tarea abrumadora. Hay muchas partes móviles y puede ser difícil saber por dónde empezar. Aquí es donde entran en juego las plantillas de proyectos iniciales de Spring Boot.

Una plantilla de proyecto inicial es una aplicación Spring Boot preconfigurada que puede usar como punto de partida para su propia aplicación. Estas plantillas pueden ser una excelente manera de ponerse en marcha rápidamente con un mínimo de complicaciones.

En este artículo, echaremos un vistazo a algunas de las plantillas de proyectos de inicio más populares y veremos cómo pueden ayudarlo a poner en marcha su aplicación Spring Boot.

## Iniciador web Spring Boot

Spring Boot Web Starter es la plantilla de proyecto de inicio más popular. Proporciona todo lo que necesita para poner en funcionamiento una aplicación web Spring Boot básica.

Web Starter incluye las siguientes dependencias:

- spring-boot-arrancador-web
- primavera-arranque-arrancador-tomcat
- primavera-arranque-arrancador-hoja de tomillo

También incluye las siguientes características clave:

- Tomcat integrado
- Soporte para plantillas Thymeleaf
- Configuración automática para Spring MVC

Comenzar con Web Starter es simple. Puede crear un nuevo proyecto utilizando Spring Initializr y seleccionando Web Starter de la lista de iniciadores.

Una vez que haya configurado su proyecto, puede agregar un controlador para manejar las solicitudes a su aplicación. Por ejemplo, el siguiente controlador asignaría solicitudes a la ruta `/` a una plantilla de Thymeleaf llamada `index.html`:

```java
@Controller
public class IndexController {

    @RequestMapping("/")
    public String index() {
        return "index";
    }

}
```

Luego puede agregar su plantilla `index.html` al directorio `src/main/resources/templates`. Web Starter configurará automáticamente Thymeleaf y podrá acceder a su plantilla en `http://localhost:8080/`.

## Datos de arranque de Spring JPA Starter

Spring Boot Data JPA Starter es otra plantilla de proyecto de inicio popular. Proporciona todo lo que necesita para comenzar con Spring Data JPA.

Data JPA Starter incluye las siguientes dependencias:

- spring-boot-arrancador-datos-jpa
- primavera-arranque-arrancador-aop
- spring-boot-iniciador-jdbc

También incluye las siguientes características clave:

- Configuración automática para Spring Data JPA
- Soporte para transacciones
- Apoyo a la auditoría

Comenzar con Data JPA Starter es tan simple como Web Starter. Puede crear un nuevo proyecto utilizando Spring Initializr y seleccionando Data JPA Starter de la lista de iniciadores.

Una vez que haya configurado su proyecto, puede agregar una entidad JPA para representar sus datos. Por ejemplo, la siguiente entidad representa a un usuario:

```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String email;

    // Getters and setters...

}
```

Luego puede agregar una interfaz de repositorio para acceder a sus datos. El siguiente repositorio proporcionaría métodos para encontrar usuarios por su identificación o correo electrónico:

```java
public interface UserRepository extends JpaRepository<User, Long> {

    User findById(Long id);

    User findByEmail(String email);

}
```

Spring Data JPA implementará automáticamente esta interfaz por usted. Luego puede inyectar el repositorio en sus controladores y usarlo para acceder a sus datos.

## Iniciador de seguridad Spring Boot

Spring Boot Security Starter es un excelente punto de partida para las aplicaciones que necesitan proporcionar autenticación y autorización.

Security Starter incluye las siguientes dependencias:

- spring-boot-arrancador-seguridad
- primavera-seguridad-config

También incluye las siguientes características clave:

- Configuración automática para Spring Security
- Soporte para autenticación basada en formularios
- Seguridad para recursos estáticos

Comenzar con el Security Starter es tan simple como los otros starters. Puede crear un nuevo proyecto utilizando Spring Initializr y seleccionando Security Starter de la lista de iniciadores.

Una vez que haya configurado su proyecto, puede agregar una configuración de seguridad a su aplicación. Por ejemplo, la siguiente configuración protegería todas las URL con la ruta `/admin`:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().permitAll()
            .and()
            .formLogin()
                .loginPage("/login")
                .permitAll();
    }

}
```

Esta configuración protegería todas las URL con la ruta `/admin` y requeriría que el usuario se autentique con el rol `ADMIN`. También proporcionaría una página de inicio de sesión en `/login` que permitiría a los usuarios autenticarse.

## Arrancador de actuador de bota de resorte

Spring Boot Actuator Starter es un gran punto de partida para aplicaciones que necesitan proporcionar capacidades de supervisión y gestión.

El actuador de arranque incluye las siguientes dependencias:

- resorte-bota-arrancador-actuador

También incluye las siguientes características clave:

- Configuración automática para Spring Boot Actuator
- Puntos finales para la supervisión y gestión de aplicaciones

Comenzar con el arrancador de actuador es tan simple como con los otros arrancadores. Puede crear un nuevo proyecto utilizando Spring Initializr y seleccionando Actuator Starter de la lista de iniciadores.

Una vez que haya configurado su proyecto, puede agregar puntos finales de actuador a su aplicación. Por ejemplo, la siguiente configuración habilitaría los puntos finales `info` y `health`:

```java
@Configuration
@EnableWebSecurity
public class ActuatorConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/actuator/**").permitAll()
                .anyRequest().authenticated()
            .and()
            .httpBasic();
    }

}
```

Esta configuración habilitaría los puntos finales `info` y `health`. Estos puntos finales proporcionan información sobre la aplicación y su estado.

## Conclusión

Las plantillas de proyecto de inicio son una excelente manera de comenzar a trabajar rápidamente con un mínimo de complicaciones. Pueden proporcionar un excelente punto de partida para su aplicación y pueden ahorrarle mucho tiempo y esfuerzo.

En este artículo, hemos analizado algunas de las plantillas de proyectos de inicio más populares y hemos visto cómo pueden ayudarlo a poner en marcha su aplicación Spring Boot.