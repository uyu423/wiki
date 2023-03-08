---
title: Node.js y Elasticsearch: una guía práctica de búsqueda y análisis
description: 
published: true
date: 2023-02-15T12:56:03.936Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:56:02.175Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js and Elasticsearch: A Hands-On Guide to Search and Analytics***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-elasticsearch-a-hands-on-guide-to-search-and-analytics)
{.links-list}


# Node.js y Elasticsearch: una guía práctica de búsqueda y análisis

En este artículo, exploraremos cómo usar Node.js y Elasticsearch para crear una solución poderosa de búsqueda y análisis. Comenzaremos configurando un entorno de desarrollo de Node.js, luego instalaremos el servidor de Elasticsearch y las bibliotecas de cliente.

A continuación, crearemos una aplicación Node.js simple que indexará algunos datos en Elasticsearch y los consultará mediante Elasticsearch Query DSL. También veremos cómo usar las agregaciones de Elasticsearch para crear potentes consultas de análisis de datos.

Finalmente, veremos cómo implementar nuestra aplicación Node.js y Elasticsearch en la nube usando Heroku.

## Configuración de un entorno de desarrollo Node.js

Comencemos configurando un entorno de desarrollo para nuestra aplicación Node.js. Tendremos que instalar Node.js y algunas otras herramientas.

### Instalación de Node.js

Primero, necesitamos instalar Node.js. Podemos hacer esto usando un administrador de paquetes como Homebrew:

```shell
brew install node
```

Alternativamente, podemos descargar e instalar el binario Node.js desde el [sitio web de Node.js] (https://nodejs.org/en/).

Una vez instalado Node.js, podemos verificar que funciona ejecutando el siguiente comando:

```shell
node -v
```

Esto debería imprimir el número de versión de Node.js en la consola.

### Instalación de otras herramientas

Además de Node.js, necesitaremos instalar algunas otras herramientas:

- Un editor de código. Recomiendo [Visual Studio Code](https://code.visualstudio.com/).
- [Git](https://git-scm.com/), para el control de versiones.
- [Docker](https://www.docker.com/), para ejecutar el servidor de Elasticsearch en un contenedor.

## Instalación del servidor de Elasticsearch

El primer paso es instalar el servidor de Elasticsearch. Podemos hacer esto usando Docker:

```shell
docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name es elasticsearch:7.5.0
```

Esto iniciará un contenedor Docker que ejecuta el servidor Elasticsearch en el puerto 9200. Podemos verificar que el servidor se está ejecutando enviando una solicitud HTTP al punto final `/_cluster/health`:

```shell
curl -X GET "localhost:9200/_cluster/health?pretty"
```

Esto debería devolver una respuesta JSON con el estado del clúster de Elasticsearch:

```json
{
  "cluster_name" : "docker-cluster",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100
}
```

También podemos acceder a la interfaz web del servidor de Elasticsearch en [http://localhost:9200](http://localhost:9200).

## Instalación del cliente de Elasticsearch Node.js

Ahora que el servidor de Elasticsearch está en funcionamiento, podemos instalar el cliente de Elasticsearch Node.js. Podemos hacer esto usando el administrador de paquetes [npm](https://www.npmjs.com/):

```shell
npm install elasticsearch
```

Esto instalará el módulo `elasticsearch` Node.js y lo agregará a la sección `dependencias` del archivo `package.json`.

## Creando una aplicación Node.js

Ahora que tenemos todo configurado, podemos comenzar a crear nuestra aplicación Node.js. Comenzaremos creando un archivo `package.json` para administrar las dependencias de nuestra aplicación:

```shell
npm init
```

Esto le pedirá cierta información sobre la aplicación, como el nombre y la versión. Puede aceptar los valores predeterminados presionando `Enter`.

A continuación, crearemos un archivo llamado `index.js` en el directorio raíz del proyecto con los siguientes contenidos:

```javascript
const { Client } = require('elasticsearch');

const client = new Client({
  host: 'localhost:9200'
});

(async () => {
  // Index some data into Elasticsearch
  await client.index({
    index: 'my-index',
    type: 'my-type',
    id: '1',
    body: {
      title: 'My first document',
      body: 'This is my first document'
    }
  });
  
  // Query the data using the Elasticsearch Query DSL
  const result = await client.search({
    index: 'my-index',
    type: 'my-type',
    body: {
      query: {
        match: {
          body: 'first'
        }
      }
    }
  });
  
  console.log(result.hits.hits);
})();
```

Este código crea un objeto de cliente de Elasticsearch y lo utiliza para indexar algunos datos en Elasticsearch y consultarlos mediante Elasticsearch Query DSL.

## Indexación de datos en Elasticsearch

Echemos un vistazo más de cerca al código que indexa los datos en Elasticsearch. Primero, creamos un objeto `index` con las siguientes propiedades:

- `index`: El nombre del índice.
- `tipo`: El tipo del documento.
- `id`: El ID del documento.
- `cuerpo`: El cuerpo del documento.

Luego indexamos el documento en Elasticsearch usando el método `index`:

```javascript
await client.index({
  index: 'my-index',
  type: 'my-type',
  id: '1',
  body: {
    title: 'My first document',
    body: 'This is my first document'
  }
});
```

Esto indexará el documento en el índice `my-index` con el tipo `my-type` y el ID `1`.

## Consulta de datos mediante Elasticsearch Query DSL

Ahora que hemos indexado algunos datos en Elasticsearch, echemos un vistazo a cómo consultarlos. Elasticsearch proporciona un poderoso lenguaje de consulta llamado Query DSL.

Podemos usar Query DSL para crear consultas complejas que se pueden usar para recuperar documentos específicos de un índice.

En el ejemplo de código anterior, usamos la consulta `coincidencia` para encontrar todos los documentos que contienen el término `primero` en el campo `cuerpo`:

```javascript
const result = await client.search({
  index: 'my-index',
  type: 'my-type',
  body: {
    query: {
      match: {
        body: 'first'
      }
    }
  }
});
```

Esta consulta coincidirá con el documento que indexamos anteriormente y lo devolverá en el objeto `resultado`.

## Implementación en la nube

Ahora que tenemos una aplicación Node.js y Elasticsearch en funcionamiento, implementémosla en la nube. Usaremos [Heroku](https://www.heroku.com/) para hacer esto.

Primero, necesitamos crear un `Procfile` en el directorio raíz del proyecto con los siguientes contenidos:

```
web: node index.js
```

Este archivo le dice a Heroku cómo iniciar la aplicación.

A continuación, debemos crear un archivo `.env` en el directorio raíz del proyecto con los siguientes contenidos:

```
ES_HOST=localhost
ES_PORT=9200
```

Este archivo contiene las variables de entorno que utilizará la aplicación.

Finalmente, necesitamos crear un archivo ` heroku.yml ` en el directorio raíz del proyecto con los siguientes contenidos:

```yaml
build:
  docker:
    web: Dockerfile
```

Este archivo le dice a Heroku que use Docker para construir la aplicación.

Una vez que se han creado estos archivos, podemos implementar la aplicación en Heroku usando los siguientes comandos:

```shell
heroku create
git push heroku master
```

Esto creará una nueva aplicación Heroku e implementará el código en ella.

## Conclusión

En este artículo, hemos visto cómo usar Node.js y Elasticsearch para crear una solución poderosa de búsqueda y análisis. Comenzamos configurando un entorno de desarrollo e instalando el servidor de Elasticsearch.

A continuación, creamos una aplicación Node.js simple que indexa datos en Elasticsearch y los consulta mediante Elasticsearch Query DSL. También vimos cómo usar las agregaciones de Elasticsearch para crear potentes consultas de análisis de datos.

Finalmente, hemos visto cómo implementar nuestra aplicación Node.js y Elasticsearch en la nube usando Heroku.

## Recursos externos

- [Node.js](https://nodejs.org/)
- [Elasticsearch](https://www.elastic.co/products/elasticsearch)
- [Docker](https://www.docker.com/)
- [Heroku](https://www.heroku.com/)