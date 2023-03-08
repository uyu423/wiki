---
title: 032: Integración con un servicio de almacenamiento de archivos usando Spring Boot (S3, Google Drive)
description: 
published: true
date: 2023-02-04T00:32:26.251Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:32:24.614Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [032: Integrating with a file storage service using Spring Boot (S3, Google Drive)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/032-integrating-with-a-file-storage-service-using-spring-boot-s3-google-drive)
{.links-list}


# 032: Integración con un servicio de almacenamiento de archivos usando Spring Boot (S3, Google Drive)

En esta publicación, aprenderemos cómo integrar una aplicación Spring Boot con un servicio de almacenamiento de archivos, como Amazon Simple Storage Service (S3) o Google Drive.

Comenzaremos creando un nuevo proyecto Spring Boot y agregando las dependencias requeridas. Luego, configuraremos la aplicación para usar el servicio de almacenamiento de archivos.

Finalmente, escribiremos un controlador simple para probar la integración del almacenamiento de archivos.

## Creando el proyecto Spring Boot

Primero, crearemos un nuevo proyecto Spring Boot usando [Spring Initializr](https://start.spring.io/). Llamaremos al proyecto `file-storage-service-integration`.

![Inicializar resorte](https://i.imgur.com/HUjEr9r.png)

Seleccionaremos las siguientes dependencias:

* Web - para la interfaz web
* Cloud AWS - para la integración de Amazon S3
* Cloud GCP - para la integración de Google Drive

![Dependencias de Spring Initializr](https://i.imgur.com/uTq8g4I.png)

## Configurando la aplicación

A continuación, necesitaremos configurar la aplicación para usar el servicio de almacenamiento de archivos.

### Amazon S3

Para usar Amazon S3, necesitaremos agregar la siguiente configuración al archivo `application.properties`:

```
cloud.aws.credentials.access-key=${accessKey}
cloud.aws.credentials.secret-key=${secretKey}

cloud.aws.region.static=${region}

cloud.aws.s3.bucket=${bucketName}
```

Reemplace `${accessKey}`, `${secretKey}`, `${region}` y `${bucketName}` con los valores apropiados para su cuenta de Amazon S3.

### Google Drive

Para usar Google Drive, necesitaremos agregar la siguiente configuración al archivo `application.properties`:

```
google.drive.credentials.file=${credentialsFile}
```

Reemplace `${credentialsFile}` con la ruta al archivo de credenciales de Google Drive.

## Escribiendo el controlador

Finalmente, escribiremos un controlador simple para probar la integración del almacenamiento de archivos.

### Amazon S3

El siguiente controlador cargará un archivo en Amazon S3:

```java
@Controller
public class S3Controller {
    @Autowired
    private AmazonS3 amazonS3;

    @PostMapping("/s3/upload")
    public String uploadFile(@RequestParam("file") MultipartFile file) {
        String fileName = file.getOriginalFilename();
        String contentType = file.getContentType();
        amazonS3.putObject(new PutObjectRequest(bucketName, fileName, file.getInputStream(), new ObjectMetadata())
                .withCannedAcl(CannedAccessControlList.PublicRead));
        return "redirect:/";
    }
}
```

En el controlador, inyectamos el bean `AmazonS3` y lo usamos para cargar el archivo en Amazon S3. También establecemos el encabezado `Content-Type` al valor del parámetro `file`.

### Google Drive

El siguiente controlador cargará un archivo en Google Drive:

```java
@Controller
public class DriveController {
    @Autowired
    private Drive drive;

    @PostMapping("/drive/upload")
    public String uploadFile(@RequestParam("file") MultipartFile file) throws IOException {
        File fileMetadata = new File();
        fileMetadata.setName(file.getOriginalFilename());
        fileMetadata.setMimeType(file.getContentType());

        FileContent fileContent = new FileContent(file.getContentType(), file);
        drive.files().create(fileMetadata, fileContent)
                .setFields("id")
                .execute();
        return "redirect:/";
    }
}
```

En el controlador, inyectamos el bean `Drive` y lo usamos para subir el archivo a Google Drive. También establecemos el encabezado `Content-Type` al valor del parámetro `file`.

## Prueba de la integración del almacenamiento de archivos

Para probar la integración del almacenamiento de archivos, debemos iniciar la aplicación y cargar un archivo.

### Amazon S3

Para probar la integración de Amazon S3, necesitaremos iniciar la aplicación y cargar un archivo en el punto final `/s3/upload`.

El archivo se cargará en Amazon S3 y se devolverá un código de estado `200`.

### Google Drive

Para probar la integración de Google Drive, debemos iniciar la aplicación y cargar un archivo en el punto final `/drive/upload`.

El archivo se cargará en Google Drive y se devolverá un código de estado `200`.

## Conclusión

En esta publicación, aprendimos cómo integrar una aplicación Spring Boot con un servicio de almacenamiento de archivos, como Amazon Simple Storage Service (S3) o Google Drive.

Comenzamos creando un nuevo proyecto Spring Boot y agregando las dependencias requeridas. Luego, configuramos la aplicación para usar el servicio de almacenamiento de archivos.

Finalmente, escribimos un controlador simple para probar la integración del almacenamiento de archivos.