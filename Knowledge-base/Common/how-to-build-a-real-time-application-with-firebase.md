---
title: Firebase로 실시간 애플리케이션을 구축하는 방법
description: 
published: true
date: 2023-02-01T13:23:46.141Z
tags: 
editor: markdown
dateCreated: 2023-02-01T13:23:44.587Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [How to Build a Real-Time Application with Firebase***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-real-time-application-with-firebase)
{.links-list}



# Firebase로 실시간 애플리케이션을 구축하는 방법

Firebase는 실시간 애플리케이션을 구축하기 위한 강력한 플랫폼입니다. NoSQL 데이터베이스, 사용자 인증, 정적 호스팅 등 다양한 기능을 제공합니다.

이 기사에서는 Firebase로 실시간 애플리케이션을 구축하는 방법을 보여줍니다. NoSQL 데이터베이스를 사용하여 데이터를 저장하고 사용자 인증을 사용하여 앱을 보호하고 정적 호스팅을 사용하여 앱을 배포합니다.

## Firebase 설정

가장 먼저 해야 할 일은 Firebase 계정을 만들고 새 프로젝트를 만드는 것입니다.

![Firebase 콘솔](https://i.imgur.com/aVORi4k.png)

프로젝트를 생성하면 프로젝트 대시보드로 이동합니다. 여기에서 프로젝트 ID와 프로젝트 URL을 찾을 수 있습니다. 나중에 필요합니다.

![Firebase 프로젝트 대시보드](https://i.imgur.com/5bF9IyG.png)

## NoSQL 데이터베이스 생성

Firebase는 데이터 저장을 위한 강력한 NoSQL 데이터베이스를 제공합니다. 데이터베이스를 생성하려면 Firebase 콘솔의 데이터베이스 탭으로 이동하여 "데이터베이스 생성" 버튼을 클릭하십시오.

![Firebase 콘솔](https://i.imgur.com/pZhCkYE.png)

데이터베이스에 대한 보안 규칙을 선택하라는 메시지가 표시됩니다. 이 예에서는 인증되지 않은 사람이 데이터베이스에 액세스하지 못하도록 하는 "잠금 모드"를 선택합니다.

![Firebase 콘솔](https://i.imgur.com/W0zJgwc.png)

데이터베이스를 만든 후에는 데이터베이스에 데이터를 추가할 수 있습니다. 이렇게 하려면 "데이터 추가" 버튼을 클릭합니다.

![Firebase 콘솔](https://i.imgur.com/V0CgqEH.png)

이제 데이터베이스에 데이터를 추가할 수 있습니다. 이 예에서는 메시지를 추가합니다.

![Firebase 콘솔](https://i.imgur.com/TGiuk72.png)

## 사용자 인증

Firebase는 앱 보안을 위한 강력한 인증 시스템을 제공합니다. 인증을 설정하려면 Firebase 콘솔의 인증 탭으로 이동하여 '로그인 방법' 탭을 클릭하세요.

![Firebase 콘솔](https://i.imgur.com/3vHKTGi.png)

"이메일/비밀번호" 로그인 방법을 클릭하고 활성화합니다.

![Firebase 콘솔](https://i.imgur.com/ZU6kCbJ.png)

로그인 방법이 활성화되었으므로 이제 사용자를 생성할 수 있습니다. 이렇게 하려면 "사용자" 탭으로 이동하여 "사용자 추가" 버튼을 클릭합니다.

![Firebase 콘솔](https://i.imgur.com/XgbG0z7.png)

사용자의 이메일과 비밀번호를 입력하고 "사용자 추가" 버튼을 클릭합니다.

![Firebase 콘솔](https://i.imgur.com/V0CgqEH.png)

이제 사용자가 앱에 로그인할 수 있습니다.

## 앱 배포

Firebase는 앱 배포를 위한 정적 호스팅 서비스를 제공합니다. 호스팅을 설정하려면 Firebase 콘솔의 호스팅 탭으로 이동하여 '시작하기' 버튼을 클릭하세요.

![Firebase 콘솔](https://i.imgur.com/7DpjkZI.png)

이제 Firebase가 호스팅 설정 과정을 안내합니다. 먼저 Firebase CLI를 설치해야 합니다.

![Firebase 콘솔](https://i.imgur.com/l0G9UO4.png)

CLI가 설치되면 앱을 배포할 수 있습니다. 이렇게 하려면 프로젝트 디렉터리의 루트에서 다음 명령을 실행합니다.

```
firebase deploy
```

이렇게 하면 앱이 Firebase 서버에 배포됩니다.

## 결론

이 기사에서는 Firebase를 사용하여 실시간 애플리케이션을 빌드하는 방법을 설명했습니다. NoSQL 데이터베이스를 사용하여 데이터를 저장하고 사용자 인증을 사용하여 앱을 보호하고 정적 호스팅을 사용하여 앱을 배포했습니다.