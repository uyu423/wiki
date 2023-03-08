---
title: 013: Integración con sistemas externos usando Spring Boot y REST
description: 
published: true
date: 2023-02-01T21:36:36.734Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:36:31.845Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [013: Integrating with external systems using Spring Boot and REST***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/013-integrating-with-external-systems-using-spring-boot-and-rest)
{.links-list}


# Introducción

En esta publicación, veremos cómo integrar Spring Boot con sistemas externos usando REST. Usaremos un ejemplo simple para ilustrar cómo se puede hacer esto.

# ¿Qué es DESCANSO?

REST es un acrónimo de Transferencia de Estado Representacional. Es un estilo de arquitectura de software que define un conjunto de restricciones que se utilizarán para crear servicios web. Los servicios web que se ajustan al estilo arquitectónico REST se denominan servicios web RESTful.

# ¿Por qué usar REST?

Los servicios web RESTful son fáciles de construir y son muy adecuados para admitir sistemas distribuidos y escalables. Los servicios web RESTful se pueden construir en cualquier plataforma y pueden ser consumidos por cualquier cliente que admita el protocolo HTTP.

# ¿Cómo crear un servicio web RESTful?

Hay dos formas de crear un servicio web RESTful:

1. Usando JAX-RS y Jersey
2. Usando Spring Boot

En esta publicación, nos centraremos en cómo crear un servicio web RESTful usando Spring Boot.

# ¿Qué es Spring Boot?

Spring Boot es un marco que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción. Proporciona un enfoque obstinado para configurar y crear aplicaciones basadas en Spring.

# ¿Por qué usar Spring Boot?

Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción. Proporciona una amplia gama de funciones que se pueden usar para crear, probar e implementar aplicaciones basadas en Spring.

# ¿Cómo crear un servicio web RESTful usando Spring Boot?

Usaremos las siguientes herramientas y tecnologías para crear nuestro servicio web RESTful basado en Spring Boot:

1.Java 8
2. Experto 3.3.9
3. Arranque de resorte 1.5.4.LIBERAR
4. Eclipse de neón.3

# Creando el Proyecto

Usaremos Spring Initializr para generar nuestro proyecto Spring Boot. Usaremos los siguientes ajustes:

1. Grupo: com.ejemplo
2. Artefacto: resorte-reposa-botas
3. Nombre: DESCANSO de arranque de primavera
4. Descripción: Ejemplo REST de Spring Boot
5. Nombre del paquete: com.example.springbootrest
6. Embalaje: Tarro
7. Versión Java: 1.8
8. Seleccione las siguientes dependencias: Web, JPA, H2

# Configurando el Proyecto

Usaremos H2 como nuestra base de datos. Configuraremos H2 en el archivo application.properties:

spring.h2.console.enabled=true
primavera.h2.console.path=/h2

# Creando la Entidad

Crearemos una entidad simple llamada Empleado:

@Entidad
Empleado de clase pública {

    @Identificación
    @ValorGenerado
    identificación larga privada;

    cadena privada nombre;

    función de cadena privada;

    // Getters y setters
}

# Creando el Repositorio

Crearemos una interfaz JpaRepository simple para nuestra entidad Empleado:

interfaz pública EmployeeRepository extiende JpaRepository<Employee, Long> {

}

# Creando el Servicio

Crearemos una interfaz de EmployeeService simple:

interfaz pública EmployeeService {

    Guardar empleado (empleado empleado);

    List<Empleado> findAll();

    Empleado findOne (ID largo);

    anular eliminar (identificación larga);
}

# Creación de la implementación del servicio

Crearemos una clase simple EmployeeServiceImpl:

@Servicio
public class EmployeeServiceImpl implementa EmployeeService {

    @autocableado
    empleadoRepositorio privado empleadoRepositorio;

    @Anular
    ahorro de empleado público (empleado empleado) {
        return employeeRepository.save(empleado);
    }

    @Anular
    public List<Empleado> findAll() {
        volver empleadoRepository.findAll();
    }

    @Anular
    empleado público findOne (identificación larga) {
        return employeeRepository.findOne(id);
    }

    @Anular
    eliminación de vacío público (identificación larga) {
        empleadoRepository.delete(id);
    }
}

# Creando el controlador REST

Crearemos una clase EmployeeController simple:

@RestController
@RequestMapping("/empleados")
clase pública EmployeeController {

    @autocableado
    servicio de empleado privado servicio de empleado;

    @RequestMapping(método = RequestMethod.GET)
    public List<Empleado> findAll() {
        return servicioempleado.findAll();
    }

    @RequestMapping(método = RequestMethod.POST)
    guardar empleado público(@RequestBody empleado empleado) {
        return employeeService.save(empleado);
    }

    @RequestMapping(método = RequestMethod.GET, valor = "/{id}")
    empleado público findOne(@PathVariable Long id) {
        return employeeService.findOne(id);
    }

    @RequestMapping(método = RequestMethod.DELETE, valor = "/{id}")
    eliminación de vacío público(@PathVariable Long id) {
        servicioempleado.delete(id);
    }
}

# Prueba del controlador REST

Usaremos los siguientes comandos curl para probar nuestro EmployeeController:

Para salvar a un empleado:

curl -X POST -H "Content-Type: application/json" -d '{"name":"John Smith","role":"Developer"}' http://localhost:8080/employees

Para encontrar a todos los empleados:

curl -X OBTENER http://localhost:8080/empleados

Para encontrar un empleado con id 1:

curl -X OBTENER http://localhost:8080/employees/1

Para eliminar un empleado con id 1:

curl -X ELIMINAR http://localhost:8080/empleados/1

# Conclusión

En esta publicación, vimos cómo crear un servicio web RESTful usando Spring Boot. Vimos cómo crear el proyecto, configurar el proyecto, crear la entidad, crear el repositorio, crear el servicio, crear la implementación del servicio, crear el controlador REST y probar el controlador REST.