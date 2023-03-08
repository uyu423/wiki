---
title: 044: Integración con un servicio de almacenamiento de documentos mediante Spring Boot (Dropbox, Google Drive)
description: 
published: true
date: 2023-02-04T10:32:37.947Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:32:36.295Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [044: Integrating with a document storage service using Spring Boot (Dropbox, Google Drive)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/044-integrating-with-a-document-storage-service-using-spring-boot-dropbox-google-drive)
{.links-list}


# 044: Integración con un servicio de almacenamiento de documentos mediante Spring Boot (Dropbox, Google Drive)

La integración con un servicio de almacenamiento de documentos puede ser una excelente manera de agregar valor a su aplicación Spring Boot. En esta publicación, veremos cómo integrarse con dos servicios populares de almacenamiento de documentos: Dropbox y Google Drive.

## Dropbox

Dropbox es un servicio de almacenamiento de archivos basado en la nube que ofrece a los usuarios 2 GB de almacenamiento gratis, con planes pagos a partir de $9.99/mes por 1 TB de almacenamiento.

Para integrarse con Dropbox, deberá crear una aplicación de Dropbox. Para hacerlo, vaya al sitio de [Dropbox Developers](https://www.dropbox.com/developers) y haga clic en el botón "Crear aplicación".

Una vez que haya creado su aplicación, deberá generar un token de acceso. Para hacerlo, vaya a la sección "Generar token de acceso" de la página de su aplicación en el sitio de Dropbox Developers.

Con su token de acceso en la mano, ahora puede comenzar a usar el [SDK de Dropbox Java] (https://github.com/dropbox/dropbox-sdk-java) para interactuar con la API de Dropbox.

Este es un ejemplo simple de cómo usar el SDK de Java de Dropbox para cargar un archivo en Dropbox:

```java
import com.dropbox.core.DbxRequestConfig;
import com.dropbox.core.v2.DbxClientV2;
import com.dropbox.core.v2.files.FileMetadata;

import java.io.FileInputStream;
import java.io.InputStream;

public class DropboxExample {
    public static void main(String[] args) throws Exception {
        // Create a Dropbox client
        DbxRequestConfig config = DbxRequestConfig.newBuilder("dropbox-sdk-java-example").build();
        DbxClientV2 client = new DbxClientV2(config, args[0]);

        // Upload a file
        InputStream in = new FileInputStream("test.txt");
        try {
            FileMetadata metadata = client.files().uploadBuilder("/test.txt").uploadAndFinish(in);
        } finally {
            in.close();
        }
    }
}
```

Para obtener más información sobre la integración con Dropbox, consulte [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java) y [Dropbox API](https://www.dropbox.com/ desarrolladores/documentación/http/documentación).

## Google Drive

Google Drive es un servicio de almacenamiento de archivos basado en la nube que ofrece a los usuarios 15 GB de almacenamiento de forma gratuita, con planes de pago a partir de $1,99 al mes por 100 GB de almacenamiento.

Para integrarse con Google Drive, deberá crear un proyecto de API de Google y habilitar la API de Drive. Puede hacerlo yendo a la [Consola API de Google](https://console.developers.google.com/) y creando un nuevo proyecto. Una vez que haya creado su proyecto, haga clic en el botón "Habilitar API y servicios" y busque la API de Drive.

Con la API de Drive habilitada, ahora puede crear una cuenta de servicio. Una cuenta de servicio es una cuenta que pertenece a su aplicación, en lugar de a un usuario individual. Para crear una cuenta de servicio, vaya a la sección "Cuentas de servicio" de la Consola API de Google y haga clic en el botón "Crear cuenta de servicio".

Cuando cree su cuenta de servicio, deberá especificar un nombre y una descripción para ella. También deberá seleccionar una función para la cuenta de servicio. Para este ejemplo, seleccionaremos el rol "Proyecto > Propietario".

Finalmente, deberá generar una clave de cuenta de servicio. Una clave de cuenta de servicio es un archivo que contiene las credenciales de su cuenta de servicio. Para generar una clave de cuenta de servicio, haga clic en el botón "Crear clave" y seleccione el tipo de clave "JSON".

Con la clave de su cuenta de servicio en la mano, ahora puede comenzar a usar la [API de Google Drive] (https://developers.google.com/drive/api/v3/reference/) para interactuar con Google Drive.

Aquí hay un ejemplo simple de cómo usar la API de Google Drive para cargar un archivo en Google Drive:

```java
import com.google.api.client.auth.oauth2.Credential;
import com.google.api.client.extensions.java6.auth.oauth2.AuthorizationCodeInstalledApp;
import com.google.api.client.extensions.jetty.auth.oauth2.LocalServerReceiver;
import com.google.api.client.googleapis.auth.oauth2.GoogleAuthorizationCodeFlow;
import com.google.api.client.googleapis.auth.oauth2.GoogleClientSecrets;
import com.google.api.client.googleapis.javanet.GoogleNetHttpTransport;
import com.google.api.client.http.FileContent;
import com.google.api.client.http.javanet.NetHttpTransport;
import com.google.api.client.json.JsonFactory;
import com.google.api.client.json.jackson2.JacksonFactory;
import com.google.api.client.util.store.FileDataStoreFactory;
import com.google.api.services.drive.Drive;
import com.google.api.services.drive.DriveScopes;
import com.google.api.services.drive.model.File;

import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.security.GeneralSecurityException;
import java.util.Collections;
import java.util.List;

public class GoogleDriveExample {
    private static final String APPLICATION_NAME = "Google Drive API Java Quickstart";
    private static final JsonFactory JSON_FACTORY = JacksonFactory.getDefaultInstance();
    private static final String TOKENS_DIRECTORY_PATH = "tokens";

    /**
     * Global instance of the scopes required by this quickstart.
     * If modifying these scopes, delete your previously saved tokens/ folder.
     */
    private static final List<String> SCOPES = Collections.singletonList(DriveScopes.DRIVE_FILE);
    private static final String CREDENTIALS_FILE_PATH = "/credentials.json";

    /**
     * Creates an authorized Credential object.
     * @param HTTP_TRANSPORT The network HTTP Transport.
     * @return An authorized Credential object.
     * @throws IOException If the credentials.json file cannot be found.
     */
    private static Credential getCredentials(final NetHttpTransport HTTP_TRANSPORT) throws IOException {
        // Load client secrets.
        InputStream in = GoogleDriveExample.class.getResourceAsStream(CREDENTIALS_FILE_PATH);
        GoogleClientSecrets clientSecrets = GoogleClientSecrets.load(JSON_FACTORY, new InputStreamReader(in));

        // Build flow and trigger user authorization request.
        GoogleAuthorizationCodeFlow flow = new GoogleAuthorizationCodeFlow.Builder(
                HTTP_TRANSPORT, JSON_FACTORY, clientSecrets, SCOPES)
                .setDataStoreFactory(new FileDataStoreFactory(new java.io.File(TOKENS_DIRECTORY_PATH)))
                .setAccessType("offline")
                .build();
        LocalServerReceiver receiver = new LocalServerReceiver.Builder().setPort(8888).build();
        return new AuthorizationCodeInstalledApp(flow, receiver).authorize("user");
    }

    public static void main(String[] args) throws IOException, GeneralSecurityException {
        // Build a new authorized API client service.
        final NetHttpTransport HTTP_TRANSPORT = GoogleNetHttpTransport.newTrustedTransport();
        Drive service = new Drive.Builder(HTTP_TRANSPORT, JSON_FACTORY, getCredentials(HTTP_TRANSPORT))
                .setApplicationName(APPLICATION_NAME)
                .build();

        // Upload a file
        File fileMetadata = new File();
        fileMetadata.setName("test.txt");
        java.io.File filePath = new java.io.File("test.txt");
        FileContent mediaContent = new FileContent("text/plain", filePath);
        File file = service.files().create(fileMetadata, mediaContent)
                .setFields("id")
                .execute();
        System.out.println("File ID: " + file.getId());
    }
}
```

Para obtener más información sobre la integración con Google Drive, consulte la [API de Google Drive](https://developers.google.com/drive/api/v3/reference/) y el [SDK de Google Drive](https://developers .google.com/drive/v3/web/about-sdk).