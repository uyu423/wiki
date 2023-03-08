---
title: Desarrollo de software 010: Ruby on Rails
description: 
published: true
date: 2023-02-07T20:56:08.685Z
tags: 
editor: markdown
dateCreated: 2023-02-07T20:56:06.913Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 010: Ruby on Rails***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-010-ruby-on-rails)
{.links-list}


# Desarrollo de software 010: Ruby on Rails

En esta publicación, analizaremos de manera integral y práctica Ruby on Rails, un popular marco de desarrollo web escrito en el lenguaje de programación Ruby.

Cubriremos los siguientes temas:

* ¿Qué es Ruby on Rails?
* Rieles MVC
* Instalación de Ruby on Rails
* Estructura de directorio de rieles
* Rutas de Ferrocarriles
* Controladores de rieles
* Modelos de Rieles
* Vistas de rieles
* Ayudantes de Rieles
* Diseños de rieles
* Activos ferroviarios
* Sobres de rieles
* Carriles ActiveRecord
* Rieles ActionPack
* Rieles ActionView
* Rieles ActionMailer
* Soporte activo de rieles
* Canalización de activos de Rails

## ¿Qué es Ruby on Rails?

Ruby on Rails es un marco de desarrollo web escrito en el lenguaje de programación Ruby. Está diseñado para hacer que el desarrollo de aplicaciones web sea más fácil y rápido al proporcionar una forma estándar de construirlas e implementarlas.

Rails se usa a menudo con el marco Ruby on Rails, que proporciona un conjunto de herramientas y bibliotecas que facilitan el desarrollo de aplicaciones web.

## Rieles MVC

Ruby on Rails se basa en el patrón arquitectónico Model View Controller (MVC). Este es un patrón de diseño común para aplicaciones web que ayuda a mantener el código organizado y fácil de mantener.

El patrón MVC se compone de tres partes:

* El **Modelo** es responsable de almacenar y recuperar datos.
* La **Vista** se encarga de mostrar los datos al usuario.
* El **Controlador** es responsable de manejar las entradas y las interacciones del usuario.

## Instalación de Ruby on Rails

Antes de que pueda comenzar a desarrollar con Ruby on Rails, deberá instalarlo en su computadora.

Hay algunas formas diferentes de instalar Ruby on Rails, pero usaremos el paquete RubyInstaller.

1. Descargue el paquete RubyInstaller del [sitio web de RubyInstaller] (https://rubyinstaller.org/).

2. Ejecute el instalador y siga las indicaciones. Asegúrese de seleccionar la opción "Agregar ejecutables de Ruby a su RUTA".

3. Una vez completada la instalación, abra una nueva ventana de terminal y escriba `ruby -v` para verificar que Ruby esté instalado. Debería ver algo como esto:

```
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin18]
```

4. Ahora necesitamos instalar Rails. Para hacer esto, usaremos el comando `gem`, que es un administrador de paquetes para Ruby. En la terminal, escribe `gem install rails`. Esto instalará la última versión de Rails.

5. Para verificar que Rails está instalado, escriba `rails -v`. Debería ver algo como esto:

```
Rails 5.2.3
```

## Estructura del directorio Rails

Ahora que tenemos Ruby on Rails instalado, echemos un vistazo a la estructura de directorios de una aplicación Rails.

Una aplicación Rails se compone de varias carpetas y archivos diferentes, cada uno con un propósito específico.

Aquí hay una lista de las carpetas y archivos más importantes:

* La carpeta `app` contiene el código de su aplicación.
* La carpeta `bin` contiene archivos ejecutables para su aplicación.
* La carpeta `config` contiene archivos de configuración para su aplicación.
* La carpeta `db` contiene los archivos de base de datos para su aplicación.
* La carpeta `lib` contiene archivos de biblioteca para su aplicación.
* La carpeta `log` contiene los archivos de registro de su aplicación.
* La carpeta `public` contiene archivos estáticos para su aplicación.
* La carpeta `test` contiene archivos de prueba para su aplicación.
* La carpeta `tmp` contiene archivos temporales para su aplicación.
* La carpeta `proveedor` contiene código de terceros para su aplicación.

## Rutas de rieles

Las rutas de Rails se utilizan para asignar direcciones URL a acciones de controlador. Se definen en el archivo `config/routes.rb`.

Por ejemplo, la siguiente ruta asignaría la URL `/artículos` a la acción `artículos# índice`:

```ruby
get '/articles', to: 'articles#index'
```

Rails también admite rutas comodín, que se pueden usar para asignar direcciones URL a acciones de controlador que toman argumentos.

Por ejemplo, la siguiente ruta asignaría la URL `/artículos/:id` a la acción `artículos# mostrar`:

```ruby
get '/articles/:id', to: 'articles#show'
```

## Controladores de rieles

Los controladores de Rails son responsables de manejar las entradas y las interacciones del usuario. Se definen en la carpeta `app/controllers`.

Cada controlador se compone de una serie de acciones, que son métodos que se encargan de manejar una solicitud específica.

Por ejemplo, el controlador `articles` podría tener una acción `index` para manejar las solicitudes de la URL `/articles` y una acción `show` para manejar las solicitudes de la URL `/articles/:id`.

## Modelos de rieles

Los modelos Rails son responsables de almacenar y recuperar datos. Se definen en la carpeta `app/models`.

Cada modelo representa un tipo de datos específico, como un 'Artículo' o un 'Usuario'. Los modelos se utilizan normalmente para almacenar datos en una base de datos, pero también se pueden utilizar para almacenar datos en otros formatos, como XML o JSON.

Los modelos también se pueden utilizar para realizar la validación de datos, como garantizar que un "Artículo" tenga un título y un cuerpo.

## Vistas de rieles

Las vistas de Rails son responsables de mostrar los datos al usuario. Se definen en la carpeta `app/views`.

Las vistas normalmente se escriben en HTML, pero también se pueden escribir en otros formatos, como XML o JSON.

Las vistas también pueden usar plantillas para SECAR su código. Por ejemplo, una vista que muestra una lista de artículos puede usar una plantilla que se encarga de mostrar un solo artículo.

## Ayudantes de rieles

Los ayudantes de Rails son módulos que proporcionan métodos de utilidad para usar en las vistas. Se definen en la carpeta `app/helpers`.

Los ayudantes se pueden usar para dar formato a los datos para su visualización, como convertir una fecha a un formato legible por humanos. También se pueden usar para generar marcado HTML, como enlaces o campos de formulario.

## Diseños de rieles

Los diseños de rieles se usan para SECAR el código de vista definiendo un diseño común para todas las vistas. Se definen en la carpeta `app/views/layouts`.

Los diseños normalmente se escriben en HTML, pero también se pueden escribir en otros formatos, como XML o JSON.

Los diseños también pueden usar plantillas para SECAR su código. Por ejemplo, un diseño que define un encabezado y un pie de página comunes para todas las vistas podría usar una plantilla responsable de mostrar el contenido de una vista.

## Activos de rieles

Los activos de Rails son archivos estáticos que utiliza su aplicación, como imágenes, archivos JavaScript o archivos CSS. Se almacenan en la carpeta `app/assets`.

Rails también proporciona una canalización de activos, que es un conjunto de herramientas que se pueden usar para procesar y comprimir activos.

## Sobres de rieles

Los anuncios publicitarios de Rails se utilizan para enviar correos electrónicos desde su aplicación. Se definen en la carpeta `app/mailers`.

Los anuncios publicitarios se pueden utilizar para enviar notificaciones a los usuarios, como instrucciones para restablecer la contraseña o notificaciones de nuevos artículos.

## Rieles ActiveRecord

Rails ActiveRecord es una biblioteca de mapeo relacional de objetos (ORM) que se utiliza para interactuar con bases de datos. Está definido en la gema `activerecord`.

ActiveRecord proporciona una serie de métodos que facilitan el trabajo con bases de datos, como "buscar" para recuperar datos y "guardar" para almacenar datos.

## Paquete de acción de rieles

Rails ActionPack es un conjunto de bibliotecas que se utilizan para crear aplicaciones web. Está definido en la gema `actionpack`.

ActionPack proporciona una serie de métodos y clases que facilitan el desarrollo de aplicaciones web, como `params` para acceder a los parámetros de solicitud y `render` para representar vistas.

## Vista de acción de rieles

Rails ActionView es una biblioteca que se utiliza para representar vistas. Se define en la gema `actionview`.

ActionView proporciona una serie de métodos y clases que facilitan la representación de vistas, como `render` para representar vistas y `parcial` para representar vistas parciales.

## Correo de acción sobre rieles

Rails ActionMailer es una biblioteca que se utiliza para enviar correos electrónicos desde su aplicación. Está definido en la gema `actionmailer`.

ActionMailer proporciona una serie de métodos y clases que facilitan el envío de correos electrónicos, como "correo" para enviar un correo electrónico y "archivos adjuntos" para agregar archivos adjuntos a un correo electrónico.

## Soporte activo de Rails

Rails ActiveSupport es un conjunto de clases y módulos de utilidad que utiliza Rails. Está definido en la gema `activesupport`.

ActiveSupport proporciona una serie de métodos y clases que facilitan el trabajo con objetos de Ruby, como `Inflector` para pluralizar y singularizar palabras, y `Time` para formatear fechas y horas.

## Canalización de activos de Rails

La canalización de activos de Rails es un conjunto de herramientas que se pueden usar para procesar y comprimir activos. Se define en la gema `sprockets`.

La canalización de activos proporciona una serie de métodos y clases que facilitan el trabajo con activos, como `uglifier` para comprimir archivos JavaScript y `sass` para compilar archivos Sass.

## Conclusión

En esta publicación, hemos dado una mirada integral y práctica a Ruby on Rails. Hemos cubierto mucho terreno, pero aún hay más que aprender sobre este popular marco de desarrollo web.

Si desea obtener más información sobre Ruby on Rails, consulte los siguientes recursos:

* Las [Guías de Ruby on Rails](https://guides.rubyonrails.org/)
* La [Documentación de la API de Ruby on Rails](https://api.rubyonrails.org/)
* El [Tutorial de Ruby on Rails](https://www.railstutorial.org/)