---
title: 버전 관리를 위해 Git 및 GitHub를 사용하는 방법
description: 
published: true
date: 2023-02-02T06:29:20.343Z
tags: 
editor: markdown
dateCreated: 2023-02-02T06:23:35.062Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Use Git and GitHub for Version Control***English** document is available*](/en/Knowledge-base/Common/how-to-use-git-and-github-for-version-control)
{.links-list}


# 버전 관리를 위해 Git 및 GitHub를 사용하는 방법

Git은 개발자가 코드 변경 사항을 추적하고, 공동 프로젝트에서 다른 사람과 함께 작업하고, 세상과 코드를 공유할 수 있는 강력한 도구입니다. GitHub는 Git 리포지토리를 호스팅하고 관리하기 위한 인기 있는 온라인 서비스입니다. 이 기사에서는 버전 제어를 위해 Git 및 GitHub를 사용하는 방법을 보여줍니다.

## 버전 관리란 무엇입니까?

버전 제어는 시간 경과에 따라 파일의 변경 사항을 추적하는 시스템입니다. 이는 개발자가 변경 사항을 실행 취소하고, 새로운 기능을 실험하고, 코드 프로젝트에서 다른 사람과 공동 작업할 수 있기 때문에 개발자에게 유용합니다.

## 힘내란?

Git은 Linux 운영 체제를 만든 Linus Torvalds가 만든 버전 관리 시스템입니다. Git은 개발자들이 널리 사용하는 무료 오픈 소스 도구입니다.

## GitHub가 무엇인가요?

GitHub는 Git 리포지토리를 호스팅하고 관리하기 위한 인기 있는 온라인 서비스입니다. GitHub를 사용하면 코드 프로젝트에서 쉽게 협업하고 코드 변경 사항을 추적할 수 있습니다.

## 버전 관리를 위해 Git 및 GitHub를 사용하는 방법

이 섹션에서는 버전 제어를 위해 Git 및 GitHub를 사용하는 방법을 보여줍니다.

### Git 설치 방법

Git은 [Git 웹사이트](https://git-scm.com/)에서 다운로드할 수 있는 무료 오픈 소스 도구입니다. Git을 설치하려면 운영 체제에 대한 지침을 따르십시오.

- [윈도우](https://git-scm.com/downloads/windows)
- [macOS](https://git-scm.com/downloads/mac)
- [리눅스](https://git-scm.com/downloads/linux)

### Git 리포지토리를 만드는 방법

Git 리포지토리는 Git에서 추적하는 파일 모음입니다. 새 Git 리포지토리를 만들려면 `git init` 명령을 사용합니다.

```
$ git init
```

### Git 리포지토리에 파일을 추가하는 방법

Git 리포지토리를 만든 후에는 `git add` 명령을 사용하여 파일을 추가할 수 있습니다. Git 리포지토리에 파일을 추가하려면 `git add` 명령 다음에 파일 경로를 사용합니다.

```
$ git add filename
```

`-A` 옵션과 함께 `git add` 명령을 사용하여 디렉토리에 있는 모든 수정 및 추적되지 않은 파일을 Git 리포지토리에 추가할 수도 있습니다.

```
$ git add -A
```

### Git 리포지토리에 대한 변경 사항을 커밋하는 방법

Git 리포지토리에 파일을 추가한 후에는 `git commit` 명령을 사용하여 해당 변경 사항을 리포지토리에 커밋할 수 있습니다. Git 리포지토리에 대한 변경 사항을 커밋하려면 `git commit` 명령 다음에 변경 사항을 설명하는 메시지를 사용합니다.

```
$ git commit -m "message"
```

### 변경 사항을 원격 Git 리포지토리로 푸시하는 방법

Git 리포지토리에 변경 사항을 커밋하면 `git push` 명령을 사용하여 해당 변경 사항을 원격 리포지토리로 푸시할 수 있습니다. 변경 사항을 원격 Git 리포지토리로 푸시하려면 `git push` 명령 다음에 원격 리포지토리 이름을 사용하십시오.

```
$ git push origin
```

### GitHub 리포지토리를 만드는 방법

GitHub는 Git 리포지토리를 호스팅하고 관리하기 위한 인기 있는 온라인 서비스입니다. 새 GitHub 리포지토리를 만들려면 GitHub 계정에 가입한 다음 GitHub 웹 사이트에서 새 리포지토리를 만듭니다.

### 기존 Git 리포지토리를 GitHub에 푸시하는 방법

기존 Git 리포지토리가 있는 경우 `git push` 명령을 사용하여 GitHub에 푸시할 수 있습니다. 기존 Git 리포지토리를 GitHub에 푸시하려면 `git push` 명령 다음에 `-u` 옵션 및 원격 리포지토리 이름을 사용하십시오.

```
$ git push -u origin
```

### 원격 Git 리포지토리에서 변경 사항을 가져오는 방법

원격 Git 리포지토리가 있는 경우 `git pull` 명령을 사용하여 해당 리포지토리에서 변경 사항을 가져올 수 있습니다. 원격 Git 리포지토리에서 변경 사항을 가져오려면 `git pull` 명령 뒤에 원격 리포지토리 이름을 사용합니다.

```
$ git pull origin
```

## 결론

이 기사에서는 버전 제어를 위해 Git 및 GitHub를 사용하는 방법을 보여주었습니다. Git은 개발자가 코드 변경 사항을 추적하고, 공동 프로젝트에서 다른 사람과 함께 작업하고, 세상과 코드를 공유할 수 있는 강력한 도구입니다. GitHub는 Git 리포지토리를 호스팅하고 관리하기 위한 인기 있는 온라인 서비스입니다.