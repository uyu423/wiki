---
title: Creación de aplicaciones reactivas con TypeScript y RxJS
description: 
published: true
date: 2023-02-13T11:18:10.233Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:18:08.598Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Reactive Applications with TypeScript and RxJS***English** document is available*](/en/Knowledge-base/TypeScript/building-reactive-applications-with-typescript-and-rxjs)
{.links-list}


# Creación de aplicaciones reactivas con TypeScript y RxJS

La programación reactiva es un paradigma de programación que se ocupa de los flujos de datos y la propagación del cambio. Es una técnica de programación asíncrona que utiliza observables para detectar y reaccionar ante cambios en los datos.

TypeScript es un superconjunto escrito de JavaScript que se compila en JavaScript simple. RxJS es una biblioteca para programación reactiva que proporciona una implementación del patrón de observables.

En este artículo, veremos cómo usar TypeScript y RxJS para crear aplicaciones reactivas. Comenzaremos creando un observable simple y luego veremos cómo usar operadores para transformar y combinar observables. Finalmente, veremos cómo usar RxJS con Angular para construir una aplicación del mundo real.

## Creando un observable

Comencemos por crear un observable simple que emita los números del 1 al 10.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
});
```

El operador `crear` toma una función que se ejecuta cuando se suscribe el observable. A esta función se le asigna un objeto observador que se utiliza para emitir valores. En este ejemplo, usamos el método `siguiente` para emitir los números del 1 al 10. También llamamos al método `completo` para indicar que el observable ha terminado de emitir valores.

Podemos suscribirnos al observable para empezar a recibir valores.

```typescript
observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

El método `subscribe` toma tres argumentos: una función para ejecutar cuando se emite un valor, una función para ejecutar cuando se produce un error y una función para ejecutar cuando se completa el observable.

## Transformando observables

Los operadores se utilizan para transformar y combinar observables. RxJS proporciona una amplia variedad de operadores para diferentes propósitos.

### Mapeo

Los operadores de mapeo se utilizan para transformar los valores emitidos por un observable.

Por ejemplo, podemos usar el operador `mapa` para transformar los números emitidos por nuestro observable en cadenas.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
}).pipe(
  map((value: number) => value.toString())
);

observable.subscribe(
  (value: string) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

El operador `mapa` toma una función que se aplica a cada valor emitido por el observable. En este ejemplo, usamos esta función para transformar cada número en una cadena.

También podemos usar el operador `mapa` para transformar los valores emitidos por un observable en un tipo diferente.

Por ejemplo, podemos usar el operador `mapa` para transformar las cadenas emitidas por nuestro observable en números.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<string>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i.toString());
  }
  observer.complete();
}).pipe(
  map((value: string) => parseInt(value))
);

observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

En este ejemplo, usamos el operador `mapa` para transformar las cadenas emitidas por nuestro observable en números.

### Filtrado

Los operadores de filtrado se utilizan para seleccionar un subconjunto de valores emitidos por un observable.

Por ejemplo, podemos usar el operador `filtro` para seleccionar solo los números pares emitidos por nuestro observable.

```typescript
const observable = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
}).pipe(
  filter((value: number) => value % 2 === 0)
);

observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

El operador `filtro` toma una función que se usa para probar cada valor emitido por el observable. En este ejemplo, usamos esta función para probar si cada valor es un número par.

### Combinando

Los operadores de combinación se utilizan para combinar los valores emitidos por múltiples observables.

Por ejemplo, podemos usar el operador `combinar` para combinar los valores emitidos por dos observables.

```typescript
const observable1 = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 1; i <= 10; i++) {
    observer.next(i);
  }
  observer.complete();
});

const observable2 = Rx.Observable.create((observer: Rx.Observer<number>) => {
  for (let i = 11; i <= 20; i++) {
    observer.next(i);
  }
  observer.complete();
});

const observable = Rx.Observable.merge(observable1, observable2);

observable.subscribe(
  (value: number) => console.log(value),
  (err: any) => console.log(err),
  () => console.log('complete')
);
```

En este ejemplo, usamos el operador `combinar` para combinar los valores emitidos por `observable1` y `observable2`.

## RxJS y Angular

RxJS se puede usar con Angular para crear aplicaciones reactivas. Angular proporciona un servicio `HttpClient` que se utiliza para realizar solicitudes HTTP. El servicio `HttpClient` es una API basada en observables que utiliza observables para devolver los resultados de las solicitudes HTTP.

Veamos cómo usar el servicio `HttpClient` para realizar una solicitud GET.

```typescript
@Injectable()
export class HttpService {
  constructor(private http: HttpClient) {}

  get(url: string) {
    return this.http.get(url);
  }
}
```

En este ejemplo, inyectamos el servicio `HttpClient` en nuestro `HttpService` y creamos un método `get` que utiliza el método `http.get` para realizar una solicitud GET.

Podemos suscribirnos al método `get` para recibir los resultados de la solicitud GET.

```typescript
this.httpService.get('/api/users').subscribe(
  (res: any) => console.log(res),
  (err: any) => console.log(err)
);
```

En este ejemplo, nos suscribimos al método `get` para recibir los resultados de la solicitud GET. El método `subscribe` toma dos argumentos: una función para ejecutar cuando la solicitud tiene éxito y una función para ejecutar cuando la solicitud falla.

También podemos usar operadores para transformar el observable devuelto por el método `get`.

Por ejemplo, podemos usar el operador `mapa` para transformar la respuesta JSON en una matriz de objetos `Usuario`.

```typescript
this.httpService.get('/api/users').pipe(
  map((res: any) => res.json())
).subscribe(
  (users: User[]) => console.log(users),
  (err: any) => console.log(err)
);
```

En este ejemplo, usamos el operador `mapa` para transformar la respuesta JSON en una matriz de objetos `Usuario`. Entonces podemos suscribirnos al observable para recibir la matriz de objetos `Usuario`.

## Conclusión

En este artículo, hemos visto cómo usar TypeScript y RxJS para crear aplicaciones reactivas. Hemos visto cómo crear observables y cómo usar operadores para transformar y combinar observables. También hemos visto cómo usar RxJS con Angular para crear una aplicación del mundo real.