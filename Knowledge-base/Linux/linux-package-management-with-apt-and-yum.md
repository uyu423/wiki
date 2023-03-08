---
title: apt 및 yum을 사용한 Linux 패키지 관리
description: 
published: true
date: 2023-02-12T09:32:25.387Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:32:18.628Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Package Management with apt and yum***English** document is available*](/en/Knowledge-base/Linux/linux-package-management-with-apt-and-yum)
{.links-list}



# apt와 yum으로 리눅스 패키지 관리

패키지 관리는 모든 Linux 배포에서 중요한 부분입니다. 시스템에서 소프트웨어 패키지를 설치, 업데이트 및 제거할 수 있습니다. 이 기사에서는 가장 널리 사용되는 두 가지 패키지 관리 도구인 apt와 yum을 살펴보겠습니다.

## 적절한

apt(고급 패키지 도구)는 Debian 및 Ubuntu 시스템의 기본 패키지 관리자입니다. 시스템에서 소프트웨어 패키지를 설치, 업데이트 및 제거하는 데 사용할 수 있는 강력한 도구입니다. apt는 또한 종속성을 해결할 수 있으므로 특정 소프트웨어 패키지에 필요한 모든 종속성을 수동으로 설치하는 것에 대해 걱정할 필요가 없습니다.

apt를 사용하여 소프트웨어 패키지를 설치하려면 다음 명령을 사용할 수 있습니다.

```
sudo apt install {package-name}
```

예를 들어 "vim" 텍스트 편집기를 설치하려면 다음 명령을 사용합니다.

```
sudo apt install vim
```

시스템의 모든 소프트웨어 패키지를 업데이트하려면 다음 명령을 사용할 수 있습니다.

```
sudo apt update
```

시스템의 모든 소프트웨어 패키지를 최신 버전으로 업그레이드하려면 다음 명령을 사용할 수 있습니다.

```
sudo apt upgrade
```

시스템에서 소프트웨어 패키지를 제거하려면 다음 명령을 사용할 수 있습니다.

```
sudo apt remove {package-name}
```

예를 들어 "vim" 텍스트 편집기를 제거하려면 다음 명령을 사용합니다.

```
sudo apt remove vim
```

## 냠

yum(Yellowdog Updater Modified)은 Red Hat 및 CentOS 시스템의 기본 패키지 관리자입니다. 시스템에서 소프트웨어 패키지를 설치, 업데이트 및 제거하는 데 사용할 수 있는 강력한 도구입니다. yum은 종속성을 해결할 수도 있으므로 특정 소프트웨어 패키지에 필요한 모든 종속성을 수동으로 설치하는 것에 대해 걱정할 필요가 없습니다.

yum을 사용하여 소프트웨어 패키지를 설치하려면 다음 명령을 사용할 수 있습니다.

```
sudo yum install {package-name}
```

예를 들어 "vim" 텍스트 편집기를 설치하려면 다음 명령을 사용합니다.

```
sudo yum install vim
```

시스템의 모든 소프트웨어 패키지를 업데이트하려면 다음 명령을 사용할 수 있습니다.

```
sudo yum update
```

시스템의 모든 소프트웨어 패키지를 최신 버전으로 업그레이드하려면 다음 명령을 사용할 수 있습니다.

```
sudo yum upgrade
```

시스템에서 소프트웨어 패키지를 제거하려면 다음 명령을 사용할 수 있습니다.

```
sudo yum remove {package-name}
```

예를 들어 "vim" 텍스트 편집기를 제거하려면 다음 명령을 사용합니다.

```
sudo yum remove vim
```

## 결론

이 기사에서는 가장 널리 사용되는 두 가지 패키지 관리 도구인 apt와 yum을 살펴보았습니다. 이 도구는 모두 강력하며 시스템에서 소프트웨어 패키지를 관리하는 데 사용할 수 있습니다.