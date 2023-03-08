---
title: Validación de datos de usuario por seguridad
description: 
published: true
date: 2023-02-10T04:17:36.552Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:17:34.948Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Validating User Data for Security***English** document is available*](/en/Knowledge-base/Backend/validating-user-data-for-security)
{.links-list}


# Validación de datos de usuario por seguridad

Como desarrollador de aplicaciones, usted es responsable de garantizar que los datos que ingresan sus usuarios sean válidos y seguros. Esta puede ser una tarea difícil, ya que hay muchas formas en que los usuarios pueden ingresar datos no válidos y muchos riesgos de seguridad a considerar. En este artículo, discutiremos algunas de las mejores prácticas para validar los datos del usuario y ofreceremos algunos ejemplos de código en PHP.

## Desinfectar la entrada del usuario

El primer paso para validar la entrada del usuario es asegurarse de que los datos estén limpios o "desinfectados". Esto significa eliminar cualquier carácter especial que pueda usarse para inyectar código malicioso en su aplicación. Por ejemplo, si espera que un usuario ingrese su nombre, querrá eliminar los caracteres que no sean letras, como números, puntuación o espacios en blanco.

Una forma de desinfectar la entrada del usuario es usar la función de PHP ```filter_var()```. Esta función toma dos argumentos: el valor a filtrar y el filtro a aplicar. Por ejemplo, para filtrar un campo de nombre, puede usar el filtro ```FILTER_SANITIZE_STRING```, que elimina cualquier etiqueta o carácter especial.

```php
$name = "John Smith";

$sanitized_name = filter_var($name, FILTER_SANITIZE_STRING);

echo $sanitized_name; // John Smith
```

Es importante tener en cuenta que ```filter_var()``` no valida los datos, solo los limpia. Esto significa que si un usuario ingresa un nombre no válido, como "123456", la función ```filter_var()``` devolverá "123456", que aún no es válido.

## Validación de la entrada del usuario

Una vez que haya desinfectado la entrada del usuario, puede validarla para asegurarse de que esté en el formato correcto. Por ejemplo, si espera un campo de nombre, querrá asegurarse de que los datos estén en orden alfabético.

Una forma de validar la entrada del usuario es usar la función PHP ```filter_var()```, con los filtros ```FILTER_VALIDATE_*```. Estos filtros validan los datos según el formato especificado. Por ejemplo, para validar un campo de nombre, puede usar el filtro ```FILTER_VALIDATE_REGEXP```, con una expresión regular que solo permite caracteres alfabéticos.

```php
$name = "John Smith";

$validated_name = filter_var($name, FILTER_VALIDATE_REGEXP, array("options"=>array("regexp"=>"/^[a-zA-Z]+$/")));

if($validated_name === false) {
  echo "Invalid name";
} else {
  echo "Valid name";
}
```

Si los datos son válidos, ```filter_var()``` devolverá los datos. Si los datos no son válidos, ```filter_var()``` devolverá ```false```.

## Consideraciones de seguridad

Al validar la entrada del usuario, es importante tener en cuenta los riesgos de seguridad. Por ejemplo, si espera una dirección de correo electrónico, querrá asegurarse de que los datos estén en un formato de correo electrónico válido. Sin embargo, también desea asegurarse de que la dirección de correo electrónico no contenga ningún código malicioso.

Una forma de validar la entrada del usuario y al mismo tiempo considerar los riesgos de seguridad es usar la función PHP ```filter_var()```, con los filtros ```FILTER_SANITIZE_EMAIL``` y ```FILTER_VALIDATE_EMAIL```. El filtro ```FILTER_SANITIZE_EMAIL``` eliminará los caracteres no válidos de los datos, y el filtro ```FILTER_VALIDATE_EMAIL``` validará los datos según el formato del correo electrónico.

```php
$email = "john.smith@example.com";

$sanitized_email = filter_var($email, FILTER_SANITIZE_EMAIL);
$validated_email = filter_var($sanitized_email, FILTER_VALIDATE_EMAIL);

if($validated_email === false) {
  echo "Invalid email";
} else {
  echo "Valid email";
}
```

## Conclusión

La validación de la entrada del usuario es una parte fundamental para garantizar la seguridad de su aplicación. Al desinfectar y validar los datos de los usuarios, puede ayudar a proteger su aplicación de la inyección de código malicioso y otros riesgos de seguridad.