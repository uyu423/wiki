---
title: Validación Spring Boot con API de validación de Bean
description: 
published: true
date: 2023-02-07T18:32:46.600Z
tags: 
editor: markdown
dateCreated: 2023-02-07T18:32:44.569Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Validation with Bean Validation API***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-validation-with-bean-validation-api)
{.links-list}


# Spring Boot Validation con Bean Validation API

La validación de la entrada del usuario es una parte importante de cualquier aplicación. En este artículo, veremos cómo usar la API de validación de Bean para validar la entrada del usuario en una aplicación Spring Boot.

## ¿Qué es la validación de frijoles?

Bean Validation es una especificación de Java para validar las restricciones de las propiedades de Java Bean. Es parte de Java Enterprise Edition (Java EE) y está disponible como una biblioteca independiente para su uso en aplicaciones Java SE.

## ¿Qué es la API de validación de Bean?

La API de Bean Validation es un conjunto de interfaces y clases que definen los contratos para implementar un proveedor de Bean Validation. Un proveedor de Bean Validation es una implementación de estos contratos que se puede conectar a una aplicación Java EE o Java SE para proporcionar servicios de validación.

## ¿Cómo funciona la validación de beans?

Bean Validation define un conjunto de anotaciones que se pueden usar para anotar las propiedades de Java Bean. Estas anotaciones se pueden utilizar para especificar las restricciones que se deben aplicar a la propiedad.

Cuando una propiedad se anota con una anotación de restricción, el proveedor de validación de Bean validará la propiedad contra la restricción. Si la propiedad es válida, el proveedor no hará nada. Si la propiedad no es válida, el proveedor generará una ConstraintViolationException.

## Configuración de la validación de beans en Spring Boot

Para usar Bean Validation en una aplicación Spring Boot, debemos agregar la dependencia de Hibernate Validator a nuestro proyecto. Hibernate Validator es la implementación de referencia de Bean Validation API.

```xml
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>6.0.17.Final</version>
</dependency>
```

Una vez que hayamos agregado la dependencia, podemos comenzar a usar Bean Validation en nuestra aplicación.

## Validación de la entrada del usuario

Digamos que tenemos un formulario de registro de usuario con los siguientes campos:

-   Nombre de usuario
-   Contraseña
-   Confirmar Contraseña
-   Correo electrónico

Podemos validar el formulario usando las siguientes anotaciones:

- @NotNull: el campo no puede ser nulo.
- @NotEmpty: el campo no puede estar vacío.
- @Size: el campo debe estar entre el tamaño especificado.
- @Email: el campo debe ser una dirección de correo electrónico válida.

Podemos anotar los campos del formulario con estas anotaciones:

```java
public class RegistrationForm {

    @NotNull
    @Size(min = 3, max = 20)
    private String username;

    @NotNull
    @Size(min = 6, max = 40)
    private String password;

    @NotNull
    @Size(min = 6, max = 40)
    private String confirmPassword;

    @NotNull
    @Email
    private String email;
    
    //Getters and setters
}
```

Ahora, digamos que tenemos un controlador con un método que maneja el envío del formulario:

```java
@PostMapping("/register")
public String register(@Valid RegistrationForm form, BindingResult bindingResult) {
    //Validate form
    if (bindingResult.hasErrors()) {
        return "register";
    }
    
    //Register user
    return "redirect:/login";
}
```

La anotación @Valid le dice a Spring que valide el formulario. BindingResult contiene el resultado de la validación. Si el formulario no es válido, el método hasErrors() devolverá verdadero y podemos devolver el formulario al usuario con los mensajes de error.

## Restricciones personalizadas

Además de las restricciones integradas, podemos definir nuestras propias restricciones personalizadas. Para hacer esto, necesitamos crear una anotación y una clase de validación.

Digamos que queremos crear una restricción personalizada para verificar si los campos de contraseña y confirmación de contraseña coinciden. Podemos crear una anotación personalizada como esta:

```java
@Documented
@Constraint(validatedBy = PasswordMatchesValidator.class)
@Target({ TYPE, FIELD, ANNOTATION_TYPE })
@Retention(RUNTIME)
public @interface PasswordMatches {
    String message() default "Passwords do not match";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```

Y una clase de validador como esta:

```java
public class PasswordMatchesValidator implements ConstraintValidator<PasswordMatches, Object> {

    @Override
    public void initialize(PasswordMatches constraintAnnotation) {       
    }

    @Override
    public boolean isValid(Object obj, ConstraintValidatorContext context){   
        User user = (User) obj;
        return user.getPassword().equals(user.getConfirmPassword());
    }     
}
```

Luego podemos anotar el campo de confirmación de contraseña con la anotación @PasswordMatches:

```java
public class RegistrationForm {

    //...    

    @NotNull
    @Size(min = 6, max = 40)
    @PasswordMatches
    private String confirmPassword;

    //...
}
```

## Conclusión

En este artículo, hemos visto cómo usar la API de validación de Bean para validar la entrada del usuario en una aplicación Spring Boot. También hemos visto cómo crear restricciones personalizadas.