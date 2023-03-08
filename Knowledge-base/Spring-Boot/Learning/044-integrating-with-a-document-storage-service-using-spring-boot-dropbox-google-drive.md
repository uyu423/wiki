---
title: 044: Spring Boot를 이용한 문서 저장 서비스 연동(Dropbox, Google Drive)
description: 
published: true
date: 2023-02-04T10:32:37.979Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:32:36.292Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [044: Integrating with a document storage service using Spring Boot (Dropbox, Google Drive)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/044-integrating-with-a-document-storage-service-using-spring-boot-dropbox-google-drive)
{.links-list}


# 044: Spring Boot(Dropbox, Google Drive)를 이용한 문서 저장 서비스 연동

문서 스토리지 서비스와 통합하는 것은 Spring Boot 애플리케이션에 가치를 추가하는 좋은 방법이 될 수 있습니다. 이 게시물에서는 널리 사용되는 두 가지 문서 저장 서비스인 Dropbox 및 Google Drive와 통합하는 방법을 살펴보겠습니다.

## 드롭 박스

Dropbox는 사용자에게 2GB의 스토리지를 무료로 제공하는 클라우드 기반 파일 스토리지 서비스로, 1TB 스토리지에 대해 월 $9.99부터 시작하는 유료 요금제를 제공합니다.

Dropbox와 통합하려면 Dropbox 앱을 만들어야 합니다. [Dropbox 개발자](https://www.dropbox.com/developers) 사이트로 이동하여 "앱 만들기" 버튼을 클릭하면 됩니다.

앱을 만든 후에는 액세스 토큰을 생성해야 합니다. Dropbox Developers 사이트에서 앱 페이지의 "액세스 토큰 생성" 섹션으로 이동하면 됩니다.

액세스 토큰이 있으면 이제 [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java)를 사용하여 Dropbox API와 상호 작용할 수 있습니다.

다음은 Dropbox Java SDK를 사용하여 Dropbox에 파일을 업로드하는 방법에 대한 간단한 예입니다.

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

Dropbox와의 통합에 대한 자세한 내용은 [Dropbox Java SDK](https://github.com/dropbox/dropbox-sdk-java) 및 [Dropbox API](https://www.dropbox.com/ 개발자/문서/http/문서).

## 구글 드라이브

Google 드라이브는 클라우드 기반 파일 저장 서비스로 사용자에게 15GB의 저장 공간을 무료로 제공하며 유료 요금제는 100GB의 저장 공간에 대해 월 $1.99부터 시작합니다.

Google Drive와 통합하려면 Google API 프로젝트를 생성하고 Drive API를 활성화해야 합니다. [Google API 콘솔](https://console.developers.google.com/)로 이동하여 새 프로젝트를 생성하면 됩니다. 프로젝트를 생성했으면 "API 및 서비스 활성화" 버튼을 클릭하고 Drive API를 검색합니다.

Drive API를 사용하도록 설정하면 이제 서비스 계정을 만들 수 있습니다. 서비스 계정은 개별 사용자가 아닌 애플리케이션에 속하는 계정입니다. 서비스 계정을 만들려면 Google API 콘솔의 "서비스 계정" 섹션으로 이동하고 "서비스 계정 만들기" 버튼을 클릭합니다.

서비스 계정을 만들 때 이름과 설명을 지정해야 합니다. 서비스 계정의 역할도 선택해야 합니다. 이 예에서는 "프로젝트 > 소유자" 역할을 선택합니다.

마지막으로 서비스 계정 키를 생성해야 합니다. 서비스 계정 키는 서비스 계정의 사용자 인증 정보가 포함된 파일입니다. 서비스 계정 키를 생성하려면 '키 만들기' 버튼을 클릭하고 'JSON' 키 유형을 선택합니다.

서비스 계정 키가 있으면 이제 [Google Drive API](https://developers.google.com/drive/api/v3/reference/)를 사용하여 Google Drive와 상호 작용할 수 있습니다.

다음은 Google 드라이브 API를 사용하여 Google 드라이브에 파일을 업로드하는 방법에 대한 간단한 예입니다.

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

Google 드라이브 통합에 대한 자세한 내용은 [Google 드라이브 API](https://developers.google.com/drive/api/v3/reference/) 및 [Google 드라이브 SDK](https://developers .google.com/drive/v3/web/about-sdk).