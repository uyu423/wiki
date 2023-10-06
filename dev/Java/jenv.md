---
title: jenv (Java 버전 관리 도구)
description: 여러 버전의 Java를 관리하고 프로젝트별로 Java 환경을 설정할 수 있는 Java 버전 관리 도구
published: true
date: 2023-10-06T07:02:41.996Z
tags: java, jenv
editor: markdown
dateCreated: 2023-10-06T07:02:41.996Z
---


![jenv_logo.png](/jenv_logo.png){.align-center}

# 개요

`jenv` 다양한 버전의 Java를 간편하게 관리하고 Java 프로젝트별로 환경을 구성할 수 있는 플러그인 기반의 Java 버전 관리 도구다. 개발자는 시스템 전체 또는 프로젝트별로 Java 버전을 선택하고 스위치하는 일이 간편해지며, 다양한 Java 애플리케이션 개발 환경을 관리하는 데 도움을 받을 수 있다.

# 설치

## MacOS

```bash
brew install jenv
```

## Ubuntu Linux

- TBU

## 

- TBU

# 환경 구성

- 내가 사용하는 쉘이 zsh 이라 `.zshrc` 파일에 프롬프트를 추가했지만, 각 사용자별로 적당한 rc 파일에 추가하면 된다.

```bash
echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(jenv init -)"' >> ~/.zshrc
```

# 사용

## 현재 설치된 전체 Java 버전 확인

```bash
jenv versions

  system
* 11.0 (set by /Users/user/.jenv/version)
  11.0.15
  17.0
  17.0.3
  18.0
  18.0.1
```

## Java 버전 추가

- `jenv versions` 에서 인식되지 않은 자바 버전이 있을 경우 수동으로 추가

```bash
jenv add /Users/user/Library/Java/JavaVirtualMachines/temurin-17.0.3/Contents/Home/
```

## 글로벌 Java 버전 설정

```bash
jenv global 11.0 # 쉘 기본 자바 버전을 11 로 변경
```

## 로컬 Java 버전 설정

```bash
jenv local 17.0 # 현재 세션의 자바 버전을 17 로 변경
```

```bash
jenv local --unset # 현재 세션에 설정된 로컬 자바 버전을 해제 (글로벌 자바 버전으로 변경)
```

# 기타 팁

- zsh 사용시 일부 테마에서는 현재 적용된 jenv 자바 버전을 보여준다.
  - global 로 설정된 자바 버전은 따로 보이지 않으며, local 로 별도 버전을 지정한 경우만 보여짐 
  - 아래에 설정된 zsh 테마는 [powerlevel10](https://github.com/romkatv/powerlevel10k)
  
![스크린샷_2023-10-06_오후_4.01.13.png](/스크린샷_2023-10-06_오후_4.01.13.png)
  
- maven wrapper 와 같은 도구를 사용할 경우 `JAVA_HOME` 환경 변수의 자바 런타임을 사용한다. jenv 로 자바 버전 스위칭을 했지만 maven 에서 사용하는 자바 변경 버전이 바뀌지 않는 경우 아래 트러블 슈팅을 참고

# 트러블슈팅

**이미 Java가 설치되어 있고, java 명령어 사용시 `/usr/bin/java` 와 같이 설정되어 있어 jenv 로 Java 버전 스위칭이 되지 않는 경우**
- `jenv rehash`

**jenv 사용하고 있지만 `JAVA_HOME` 환경 변수 변경이 제대로 되지 않는 경우**
- `jenv enable-plugin export`

---

- [jEnv - Manage your Java environment*https://www.jenv.be*](https://www.jenv.be/)
{.links-list}