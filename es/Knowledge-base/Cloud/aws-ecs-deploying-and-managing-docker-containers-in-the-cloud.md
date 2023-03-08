---
title: AWS ECS: implementación y administración de contenedores Docker en la nube
description: 
published: true
date: 2023-02-16T00:17:54.328Z
tags: 
editor: markdown
dateCreated: 2023-02-16T00:17:51.797Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS ECS: Deploying and Managing Docker Containers in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-ecs-deploying-and-managing-docker-containers-in-the-cloud)
{.links-list}


# AWS ECS: implementación y administración de contenedores Docker en la nube

Los contenedores Docker se han convertido en el estándar para empaquetar e implementar aplicaciones en los últimos años. Ofrecen una serie de beneficios sobre las máquinas virtuales tradicionales, incluida la portabilidad, la reducción de la sobrecarga de recursos y la fácil integración con las canalizaciones de integración continua/entrega continua (CI/CD).

AWS Elastic Container Service (ECS) es un servicio de orquestación de contenedores administrados que facilita la ejecución y administración de contenedores Docker en la nube. En este artículo, veremos cómo implementar y administrar contenedores Docker en AWS ECS.

## Creación de un clúster de ECS

El primer paso para usar AWS ECS es crear un clúster de ECS. Un clúster de ECS es una agrupación lógica de instancias de EC2 que se utilizan para alojar sus contenedores de Docker. Puede crear un clúster de ECS mediante la consola de administración de AWS, la interfaz de línea de comandos (CLI) de AWS o el SDK de AWS.

### Creación de un clúster de ECS con la Consola de administración de AWS

Para crear un clúster de ECS mediante la consola de administración de AWS, primero abra la consola de Amazon ECS y seleccione el enlace "Clusters" en la barra de navegación de la izquierda. Luego, haga clic en el botón "Crear clúster".

En la página "Crear clúster", seleccione la plantilla "Solo redes" y asigne un nombre a su clúster. Luego, haga clic en el botón "Crear".

Ahora se creará su clúster y podrá verlo en la lista "Clústeres".

### Creación de un clúster de ECS mediante la CLI de AWS

Para crear un clúster de ECS mediante la CLI de AWS, primero cree un archivo denominado "ecs-cli-cluster.json" con el siguiente contenido:

```json
{
    "clusterName": "my-ecs-cluster",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

Reemplace los valores en los campos "clusterName", "subnets" y "securityGroups" con los valores apropiados para su entorno. Luego, ejecute el siguiente comando para crear el clúster:

```
aws ecs create-cluster --cli-input-json file://ecs-cli-cluster.json
```

## Creación de una definición de tarea de ECS

Ahora que tiene un clúster de ECS, puede implementar aplicaciones en él. Una aplicación en ECS se define mediante una definición de tarea, que especifica las imágenes de Docker y otros recursos que se necesitan para ejecutar la aplicación.

Puede crear una definición de tarea mediante la Consola de administración de AWS, la CLI de AWS o el SDK de AWS.

### Creación de una definición de tarea mediante la Consola de administración de AWS

Para crear una definición de tareas mediante la consola de administración de AWS, primero abra la consola de Amazon ECS y seleccione el enlace "Definiciones de tareas" en la barra de navegación de la izquierda. Luego, haga clic en el botón "Crear nueva definición de tarea".

En la página "Seleccionar tipo de lanzamiento", seleccione el tipo de lanzamiento "EC2" y haga clic en el botón "Siguiente paso".

En la página "Configurar tareas y definiciones de contenedores", asigne un nombre y una descripción a su tarea. Luego, desplácese hacia abajo hasta la sección "Definiciones de contenedores" y haga clic en el botón "Agregar contenedor".

En el modal "Agregar contenedor", ingrese los siguientes valores:

- **Nombre del contenedor:** mi-contenedor
- **Imagen:** nginx:último
- **Límite de memoria (MiB):** 512
- **Asignaciones de puertos:** 80:80

Luego, haga clic en el botón "Agregar".

Su contenedor ahora se agregará a la definición de la tarea. Desplácese hacia abajo hasta la sección "Rol de tarea" y seleccione la opción "Ninguno". Luego, desplácese hacia abajo hasta la sección "Modo de red" y seleccione la opción "puente". Finalmente, haga clic en el botón "Siguiente paso".

En la página "Revisar", revise la definición de su tarea y haga clic en el botón "Crear".

Ahora se creará la definición de su tarea y podrá verla en la lista "Definiciones de tareas".

### Creación de una definición de tarea mediante la AWS CLI

Para crear una definición de tarea mediante la AWS CLI, primero cree un archivo denominado "ecs-cli-task-definition.json" con el siguiente contenido:

```json
{
    "family": "my-task-definition",
    "networkMode": "bridge",
    "containerDefinitions": [
        {
            "name": "my-container",
            "image": "nginx:latest",
            "memory": 512,
            "portMappings": [
                {
                    "containerPort": 80,
                    "hostPort": 80
                }
            ]
        }
    ]
}
```

Reemplace los valores en los campos "familia" y "definiciones de contenedor" con los valores apropiados para su entorno. Luego, ejecute el siguiente comando para crear la definición de la tarea:

```
aws ecs register-task-definition --cli-input-json file://ecs-cli-task-definition.json
```

## Implementación de una aplicación en un clúster de ECS

Ahora que tiene un clúster de ECS y una definición de tarea, puede implementar su aplicación en el clúster. Puede implementar una aplicación en un clúster de ECS mediante la Consola de administración de AWS, la CLI de AWS o el SDK de AWS.

### Implementación de una aplicación mediante la Consola de administración de AWS

Para implementar una aplicación mediante la consola de administración de AWS, primero abra la consola de Amazon ECS y seleccione el enlace "Clusters" en la barra de navegación de la izquierda. Luego, seleccione el clúster en el que desea implementar y haga clic en la pestaña "Tareas".

En la pestaña "Tareas", haga clic en el botón "Ejecutar nueva tarea".

En la página "Configurar ajustes de tarea y contenedor", seleccione la definición de tarea "my-task-definition" y haga clic en el botón "Siguiente paso".

En la página "Configurar red", seleccione el modo de red "puente" y haga clic en el botón "Siguiente paso".

En la página "Revisar", revise la configuración de su tarea y haga clic en el botón "Ejecutar tarea".

Su tarea ahora se implementará en el clúster y podrá ver su estado en la pestaña "Tareas".

### Implementación de una aplicación mediante la AWS CLI

Para implementar una aplicación mediante la AWS CLI, primero cree un archivo denominado "ecs-cli-run-task.json" con el siguiente contenido:

```json
{
    "taskDefinition": "my-task-definition",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

Reemplace los valores en los campos "taskDefinition", "subnets" y "securityGroups" con los valores apropiados para su entorno. Luego, ejecute el siguiente comando para implementar la tarea:

```
aws ecs run-task --cli-input-json file://ecs-cli-run-task.json
```

## Monitoreo de un clúster de ECS

AWS ECS ofrece una serie de herramientas para monitorear su clúster y las tareas que se ejecutan en él.

La primera herramienta es CloudWatch. CloudWatch es un servicio de AWS que recopila y procesa datos de monitoreo para los recursos de AWS, incluidos los clústeres de ECS. Puede usar CloudWatch para ver las métricas de su clúster de ECS, configurar alarmas y ver registros.

La segunda herramienta es Amazon CloudWatch Logs. CloudWatch Logs es un servicio que puede usar para monitorear, almacenar y acceder a los archivos de registro de los recursos de AWS, incluidos los clústeres de ECS. Puede usar CloudWatch Logs para ver los registros de su clúster de ECS y las tareas que se ejecutan en él.

La tercera herramienta es Amazon CloudWatch Events. CloudWatch Events es un servicio que puede usar para monitorear eventos de los recursos de AWS, incluidos los clústeres de ECS. Puede usar Eventos de CloudWatch para ver eventos de su clúster de ECS y las tareas que se ejecutan en él.

## Eliminación de un clúster de ECS

Si ya no necesita un clúster de ECS, puede eliminarlo mediante la Consola de administración de AWS, la CLI de AWS o el SDK de AWS.

### Eliminación de un clúster de ECS mediante la consola de administración de AWS

Para eliminar un clúster de ECS mediante la consola de administración de AWS, primero abra la consola de Amazon ECS y seleccione el enlace "Clusters" en la barra de navegación de la izquierda. Luego, seleccione el clúster que desea eliminar y haga clic en el botón "Eliminar".

En la página "Eliminar clúster", revise la información sobre el clúster y haga clic en el botón "Eliminar".

Su clúster ahora será eliminado.

### Eliminación de un clúster de ECS mediante la CLI de AWS

Para eliminar un clúster de ECS mediante la AWS CLI, ejecute el siguiente comando:

```
aws ecs delete-cluster --cluster my-ecs-cluster
```

## Conclusión

En este artículo, analizamos cómo implementar y administrar contenedores Docker en AWS ECS. Hemos visto cómo crear un clúster de ECS, crear una definición de tareas e implementar una aplicación en el clúster. También vimos cómo monitorear un clúster de ECS usando CloudWatch. Finalmente, hemos visto cómo eliminar un clúster de ECS.