---
title: Laravel: un marco PHP para el desarrollo de back-end
description: 
published: true
date: 2023-02-04T13:17:28.869Z
tags: 
editor: markdown
dateCreated: 2023-02-04T13:17:23.556Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Laravel: A PHP Framework for Backend Development***English** document is available*](/en/Knowledge-base/Backend/laravel-a-php-framework-for-backend-development)
{.links-list}


# Laravel: un marco PHP para el desarrollo de back-end

Laravel es un marco PHP de código abierto popular para crear aplicaciones web. Este marco es conocido por su sintaxis expresiva y elegante y su capacidad para facilitar las tareas complejas de desarrollo web.

Laravel es popular entre los desarrolladores de back-end por su amplia gama de funciones y su creciente comunidad. En este artículo, veremos algunas de las características de Laravel que lo convierten en una opción popular para el desarrollo de back-end.

## Enrutamiento

El sistema de enrutamiento de Laravel es una de sus características más poderosas. Le permite definir rutas para su aplicación y asignarlas a las acciones del controlador. Esto facilita mantener organizada la lógica de su aplicación.

Aquí hay un ejemplo de cómo definir una ruta en Laravel:

```php
// routes/web.php

Route::get('/users', 'UserController@index');
```

En este ejemplo, estamos definiendo una ruta para la URL `/usuarios`. Esta ruta será manejada por la acción `index` del `UserController`.

## ORM elocuente

El ORM Eloquent de Laravel es otra característica poderosa. Proporciona una manera fácil de trabajar con los datos de su aplicación.

Aquí hay un ejemplo de cómo usar Eloquent ORM para consultar registros:

```php
// app/User.php

<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    //
}
```

```php
// routes/web.php

Route::get('/users', function () {
    $users = App\User::all();

    return view('users.index', compact('users'));
});
```

En este ejemplo, estamos usando el método `todos` del modelo `Usuario` para recuperar todos los usuarios de la base de datos. Luego estamos pasando la variable `$users` a la vista `index`.

## Plantillas de hojas

El lenguaje de plantillas Blade de Laravel es otra gran característica. Blade facilita la creación de vistas para su aplicación.

Aquí hay un ejemplo de cómo usar Blade para crear una vista:

```php
// resources/views/users/index.blade.php

@foreach ($users as $user)
    <p>{{ $user->name }}</p>
@endforeach
```

En este ejemplo, estamos usando la directiva `@foreach` de Blade para recorrer la variable `$users` y mostrar el nombre de cada usuario.

## Seguridad

Laravel se toma la seguridad en serio. Proporciona funciones como hash de contraseña y protección CSRF listas para usar.

Aquí hay un ejemplo de cómo usar la función de hash de contraseña de Laravel:

```php
// app/Http/Controllers/Auth/RegisterController.php

<?php

namespace App\Http\Controllers\Auth;

use App\Http\Controllers\Controller;
use App\User;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\Validator;

class RegisterController extends Controller
{
    /**
     * Create a new user instance after a valid registration.
     *
     * @param  array  $data
     * @return \App\User
     */
    protected function create(array $data)
    {
        return User::create([
            'name' => $data['name'],
            'email' => $data['email'],
            'password' => Hash::make($data['password']),
        ]);
    }
}
```

En este ejemplo, estamos utilizando el método `make` de la fachada `Hash` para codificar la contraseña del usuario antes de almacenarla en la base de datos.

## Documentación

La documentación de Laravel es otra gran característica. Es completo y fácil de leer.

## Comunidad

Laravel tiene una comunidad en crecimiento. Hay muchos recursos disponibles para ayudarte a aprender Laravel.

## Conclusión

Laravel es un marco PHP de código abierto popular para crear aplicaciones web. Este marco es conocido por su sintaxis expresiva y elegante y su capacidad para facilitar las tareas complejas de desarrollo web.

Laravel es popular entre los desarrolladores de back-end por su amplia gama de funciones y su creciente comunidad. En este artículo, hemos echado un vistazo a algunas de las características de Laravel que lo convierten en una opción popular para el desarrollo de back-end.