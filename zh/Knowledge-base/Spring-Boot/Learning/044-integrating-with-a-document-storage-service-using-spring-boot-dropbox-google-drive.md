---
title: 044：使用 Spring Boot（Dropbox、Google Drive）与文档存储服务集成
description: 
published: true
date: 2023-02-04T10:32:37.932Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:32:36.292Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [044: Integrating with a document storage service using Spring Boot (Dropbox, Google Drive)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/044-integrating-with-a-document-storage-service-using-spring-boot-dropbox-google-drive)
{.links-list}


# 044：使用 Spring Boot（Dropbox、Google Drive）与文档存储服务集成

与文档存储服务集成是为 Spring Boot 应用程序增加价值的好方法。在本文中，我们将了解如何与两种流行的文档存储服务集成：Dropbox 和 Google Drive。

## 投递箱

Dropbox 是一种基于云的文件存储服务，免费为用户提供 2 GB 的存储空间，1 TB 存储空间的付费计划起价为每月 9.99 美元。

要与 Dropbox 集成，您需要创建一个 Dropbox 应用程序。您可以前往 [Dropbox Developers](https://www.dropbox.com/developers) 站点并单击“创建应用程序”按钮来执行此操作。

创建应用程序后，您需要生成访问令牌。您可以前往 Dropbox 开发者网站上应用程序页面的“生成访问令牌”部分来执行此操作。

有了访问令牌，您现在可以开始使用 [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java) 与 Dropbox API 交互。

以下是如何使用 Dropbox Java SDK 将文件上传到 Dropbox 的简单示例：

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

有关与 Dropbox 集成的更多信息，请查看 [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java) 和 [Dropbox API](https://www.dropbox.com/开发人员/文档/http/文档）。

## 谷歌云端硬盘

Google Drive 是一种基于云的文件存储服务，可为用户免费提供 15 GB 的存储空间，100 GB 存储空间的付费计划起价为每月 1.99 美元。

要与 Google Drive 集成，您需要创建一个 Google API 项目并启用 Drive API。为此，您可以转到 [Google API 控制台](https://console.developers.google.com/) 并创建一个新项目。创建项目后，单击“启用 API 和服务”按钮并搜索 Drive API。

启用 Drive API 后，您现在可以创建服务帐户。服务帐户是属于您的应用程序的帐户，而不是属于单个用户的帐户。要创建服务帐户，请转到 Google API 控制台的“服务帐户”部分，然后单击“创建服务帐户”按钮。

创建服务帐户时，您需要为其指定名称和说明。您还需要为服务帐户选择一个角色。对于此示例，我们将选择“项目 > 所有者”角色。

最后，您需要生成一个服务帐户密钥。服务帐户密钥是一个文件，其中包含您的服务帐户的凭据。要生成服务帐户密钥，请单击“创建密钥”按钮并选择“JSON”密钥类型。

有了您的服务帐户密钥，您现在可以开始使用 [Google Drive API](https://developers.google.com/drive/api/v3/reference/) 与 Google Drive 交互。

以下是如何使用 Google Drive API 将文件上传到 Google Drive 的简单示例：

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

有关与 Google Drive 集成的更多信息，请查看 [Google Drive API](https://developers.google.com/drive/api/v3/reference/) 和 [Google Drive SDK](https://developers .google.com/drive/v3/web/about-sdk）。