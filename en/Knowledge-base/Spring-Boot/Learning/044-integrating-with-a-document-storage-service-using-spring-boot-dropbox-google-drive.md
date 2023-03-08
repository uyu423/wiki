---
title: 044: Integrating with a document storage service using Spring Boot (Dropbox, Google Drive)
description: 
published: true
date: 2023-02-04T10:32:41.651Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:32:36.298Z
---

- [044: Integración con un servicio de almacenamiento de documentos mediante Spring Boot (Dropbox, Google Drive)***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/044-integrating-with-a-document-storage-service-using-spring-boot-dropbox-google-drive)
{.links-list}
- [044：使用 Spring Boot（Dropbox、Google Drive）与文档存储服务集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/044-integrating-with-a-document-storage-service-using-spring-boot-dropbox-google-drive)
{.links-list}
- [044: Spring Boot를 이용한 문서 저장 서비스 연동(Dropbox, Google Drive)***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/044-integrating-with-a-document-storage-service-using-spring-boot-dropbox-google-drive)
{.links-list}


# 044: Integrating with a document storage service using Spring Boot (Dropbox, Google Drive)

Integrating with a document storage service can be a great way to add value to your Spring Boot application. In this post, we'll take a look at how to integrate with two popular document storage services: Dropbox and Google Drive.

## Dropbox

Dropbox is a cloud-based file storage service that offers users 2 GB of storage for free, with paid plans starting at $9.99/month for 1 TB of storage.

To integrate with Dropbox, you'll need to create a Dropbox app. You can do this by going to the [Dropbox Developers](https://www.dropbox.com/developers) site and clicking on the "Create App" button.

Once you've created your app, you'll need to generate an access token. You can do this by going to the "Generate access token" section of your app's page on the Dropbox Developers site.

With your access token in hand, you can now start using the [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java) to interact with the Dropbox API.

Here's a simple example of how to use the Dropbox Java SDK to upload a file to Dropbox:

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

For more information on integrating with Dropbox, check out the [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java) and the [Dropbox API](https://www.dropbox.com/developers/documentation/http/documentation).

## Google Drive

Google Drive is a cloud-based file storage service that offers users 15 GB of storage for free, with paid plans starting at $1.99/month for 100 GB of storage.

To integrate with Google Drive, you'll need to create a Google API project and enable the Drive API. You can do this by going to the [Google API Console](https://console.developers.google.com/) and creating a new project. Once you've created your project, click on the "Enable APIs and Services" button and search for the Drive API.

With the Drive API enabled, you can now create a service account. A service account is an account that belongs to your application, rather than to an individual user. To create a service account, go to the "Service accounts" section of the Google API Console and click on the "Create service account" button.

When you create your service account, you'll need to specify a name and description for it. You'll also need to select a role for the service account. For this example, we'll select the "Project > Owner" role.

Finally, you'll need to generate a service account key. A service account key is a file that contains the credentials for your service account. To generate a service account key, click on the "Create key" button and select the "JSON" key type.

With your service account key in hand, you can now start using the [Google Drive API](https://developers.google.com/drive/api/v3/reference/) to interact with Google Drive.

Here's a simple example of how to use the Google Drive API to upload a file to Google Drive:

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

For more information on integrating with Google Drive, check out the [Google Drive API](https://developers.google.com/drive/api/v3/reference/) and the [Google Drive SDK](https://developers.google.com/drive/v3/web/about-sdk).