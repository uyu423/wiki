---
title: Estudio de caso: desarrollo y lanzamiento de un servicio de comercio electrónico simple en AWS
description: 
published: true
date: 2023-02-04T11:18:08.701Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:18:07.048Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Case Study: Developing and Launching a Simple e-Commerce Service on AWS***English** document is available*](/en/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-e-commerce-service-on-aws)
{.links-list}


# Estudio de caso: desarrollo y lanzamiento de un servicio de comercio electrónico simple en AWS

En este caso de estudio, le mostraremos cómo desarrollar y lanzar un servicio de comercio electrónico simple en AWS. Repasaremos la arquitectura del servicio y los diferentes servicios de AWS que se utilizan. También proporcionaremos algunos ejemplos de código para ayudarlo a comenzar.

## La arquitectura

El servicio de comercio electrónico que desarrollaremos es simple y consiste en un front-end web y una base de datos back-end. El front-end web se desarrollará utilizando el lenguaje de programación PHP y la base de datos back-end será MySQL.

![Arquitectura de servicios de comercio electrónico](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/architecture.png)

El front-end web se alojará en una instancia de Amazon EC2 y se accederá a él a través de una distribución de Amazon CloudFront. CloudFront es una red de entrega de contenido (CDN) que almacenará en caché el contenido estático del sitio web (como imágenes, CSS y archivos JavaScript) y lo entregará a los usuarios con baja latencia.

La base de datos de back-end se alojará en Amazon RDS y se utilizará para almacenar los datos de productos y pedidos. RDS es un servicio de base de datos relacional administrado que facilita la configuración, el funcionamiento y el escalado de una base de datos relacional en la nube.

## Los servicios de AWS utilizados

Los siguientes servicios de AWS se utilizarán en este estudio de caso:

-Amazon EC2
-Amazon CloudFront
-Amazon RDS
-Amazon S3

## Configuración de la base de datos de back-end

Comenzaremos configurando la base de datos back-end. Usaremos Amazon RDS para MySQL.

Primero, crearemos una nueva instancia de RDS. Elegiremos el motor MySQL y la clase de instancia db.t2.micro.

![Creando una nueva instancia de RDS](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-01.png)

A continuación, configuraremos los ajustes para la instancia. Le daremos un nombre a la instancia, elegiremos el motor de base de datos MySQL 5.6.x y seleccionaremos la clase de instancia db.t2.micro.

![Configuración de la instancia de RDS](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-02.png)

A continuación, crearemos una nueva base de datos. Le daremos un nombre a la base de datos y elegiremos el motor de base de datos MySQL 5.6.x.

![Creando una nueva base de datos](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-03.png)

Ahora que se ha creado la base de datos, necesitaremos crear un usuario y otorgarle acceso a la base de datos. Crearemos un usuario con el nombre de usuario "ecommerce" y la contraseña "password".

![Creando un nuevo usuario](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-04.png)

A continuación, otorgaremos al usuario acceso a la base de datos. Seleccionaremos la base de datos "ecommerce" y el usuario "ecommerce" y haremos clic en el botón "Add".

![Concesión de acceso a la base de datos](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-05.png)

## Configuración del front-end web

Ahora que se ha configurado la base de datos de back-end, necesitaremos configurar el front-end web. Usaremos Amazon EC2 para esto.

Primero, crearemos una nueva instancia EC2. Elegiremos la AMI de Amazon Linux y el tipo de instancia t2.micro.

![Creando una nueva instancia EC2](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-01.png)

A continuación, configuraremos los ajustes para la instancia. Le daremos un nombre a la instancia, elegiremos la AMI de Amazon Linux y seleccionaremos el tipo de instancia t2.micro.

![Configuración de la instancia EC2](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-02.png)

Ahora que se ha creado la instancia, necesitaremos SSH en la instancia. Usaremos la clave privada que descargamos cuando creamos la instancia.

![SSH en la instancia EC2](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-03.png)

Una vez que hayamos iniciado sesión en la instancia, necesitaremos instalar el servidor web Apache, PHP y el cliente MySQL. Haremos esto usando el administrador de paquetes yum.

```bash
$ sudo yum install -y httpd24 php70 mysql56-client
```

A continuación, iniciaremos el servidor web Apache.

```bash
$ sudo service httpd start
```

Ahora que el servidor web está funcionando, necesitaremos crear un nuevo archivo PHP. Llamaremos a este archivo "index.php" y lo colocaremos en el directorio "/var/www/html".

```php
<?php
  echo "Hello, world!";
?>
```

Ahora, necesitaremos editar el archivo "/etc/httpd/conf/httpd.conf" y descomentar la siguiente línea:

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

A continuación, reiniciaremos el servidor web Apache.

```bash
$ sudo service httpd restart
```

Ahora, necesitaremos crear un nuevo usuario de MySQL. Usaremos el usuario de "comercio electrónico" que creamos anteriormente. Concederemos al usuario acceso a la base de datos de "comercio electrónico".

```sql
GRANT ALL ON ecommerce.* TO 'ecommerce'@'localhost' IDENTIFIED BY 'password';
```

Ahora que se ha creado el usuario, necesitaremos importar los datos a la base de datos. Usaremos el archivo "products.sql" que se incluye en el repositorio de GitHub.

```bash
$ mysql -u ecommerce -p ecommerce < products.sql
```

## Prueba de la aplicación

Ahora que la aplicación está configurada, debemos probarla para asegurarnos de que todo funcione como se esperaba. Comenzaremos accediendo a la aplicación a través de un navegador web.

![Probando la aplicación](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-01.png)

Como podemos ver, la aplicación está funcionando como se esperaba. Podemos ver la lista de productos y podemos añadir artículos al carrito de la compra.

![Probando la aplicación](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-02.png)

## Lanzamiento de la aplicación

Ahora que la aplicación está en funcionamiento, debemos iniciarla. Lo haremos creando una distribución de Amazon CloudFront.

Primero, crearemos una nueva distribución de CloudFront. Elegiremos el método de entrega "Web" y el método HTTP "Obtener".

![Crear una nueva distribución de CloudFront](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-01.png)

A continuación, configuraremos los ajustes para la distribución. Le daremos un nombre a la distribución, seleccionaremos el método de entrega "Web" y elegiremos el método HTTP "Obtener".

![Configuración de la distribución de CloudFront](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-02.png)

Ahora, necesitaremos crear un nuevo origen. Seleccionaremos el tipo "Origen personalizado" e ingresaremos la URL para nuestra instancia EC2.

![Creando un nuevo origen](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-03.png)

A continuación, configuraremos los ajustes para el origen. Le daremos un nombre al origen, seleccionaremos el tipo "Origen personalizado" e ingresaremos la URL para nuestra instancia EC2.

![Configuración del origen](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-04.png)

Ahora, necesitaremos crear un nuevo comportamiento de caché predeterminado. Seleccionaremos el patrón de ruta "Predeterminado (*)" y elegiremos la opción "Permitir todo" para los encabezados de reenvío.

![Creación de un nuevo comportamiento de caché predeterminado](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-05.png)

A continuación, configuraremos los ajustes para el comportamiento predeterminado de la memoria caché. Seleccionaremos el patrón de ruta "Predeterminado (*)" y elegiremos la opción "Permitir todo" para los encabezados de reenvío.

![Configuración del comportamiento de caché predeterminado](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-06.png)

Ahora, necesitaremos crear una nueva página de error. Seleccionaremos el código de error "404" e ingresaremos la URL de la página de error.

![Creando una nueva página de error](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-07.png)

A continuación, configuraremos los ajustes para la página de error. Seleccionaremos el código de error "404" e ingresaremos la URL de la página de error.

![Configuración de la página de error](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-08.png)

Ahora, necesitaremos crear un nuevo certificado SSL. Seleccionaremos la opción "Certificado personalizado" e ingresaremos el nombre de dominio de nuestro sitio web.

![Creando un nuevo certificado SSL](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-09.png)

A continuación, configuraremos los ajustes para el certificado SSL. Seleccionaremos la opción "Certificado personalizado" e ingresaremos el nombre de dominio de nuestro sitio web.

![Configuración del certificado SSL](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-10.png)

Ahora, necesitaremos crear una nueva distribución. Seleccionaremos el método de entrega "Web" y el método HTTP "Obtener".

![Creando una nueva distribución](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-11.png)

A continuación, configuraremos los ajustes para la distribución. Le daremos un nombre a la distribución, seleccionaremos el método de entrega "Web" y elegiremos el método HTTP "Obtener".

![Configuración de la distribución](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-12.png)

Ahora, necesitaremos crear un nuevo comportamiento de caché predeterminado. Seleccionaremos el patrón de ruta "Predeterminado (*)" y elegiremos la opción "Permitir todo" para los encabezados de reenvío.

![Creación de un nuevo comportamiento de caché predeterminado](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-13.png)

A continuación, configuraremos los ajustes para el comportamiento predeterminado de la memoria caché. Seleccionaremos el patrón de ruta "Predeterminado (*)" y elegiremos la opción "Permitir todo" para los encabezados de reenvío.

![Configuración del comportamiento de caché predeterminado](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-14.png)

Ahora, necesitaremos crear una nueva página de error. Seleccionaremos el código de error "404" e ingresaremos la URL de la página de error.

![Creando una nueva página de error](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-15.png)

A continuación, configuraremos los ajustes para la página de error. Seleccionaremos el código de error "404" e ingresaremos la URL de la página de error.

![Configuración de la página de error](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-16.png)

## Conclusión

En este estudio de caso, le mostramos cómo desarrollar y lanzar un servicio de comercio electrónico simple en AWS. Hemos repasado la arquitectura del servicio y los diferentes servicios de AWS que se utilizan. También proporcionamos algunos ejemplos de código para ayudarlo a comenzar.