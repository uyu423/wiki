---
title: 고급 Bash 스크립팅
description: 
published: true
date: 2023-02-11T10:32:39.471Z
tags: 
editor: markdown
dateCreated: 2023-02-11T10:32:37.747Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Advanced Bash Scripting***English** document is available*](/en/Knowledge-base/Linux/advanced-bash-scripting)
{.links-list}


# 고급 Bash 스크립팅

Bourne Again SHell(Bash)은 UNIX 시스템용 무료 셸입니다. 대부분의 Linux 배포판의 기본 셸이며 Mac OS X 및 기타 UNIX 시스템에서 찾을 수 있습니다.

Bash는 간단한 스크립트에서 복잡한 애플리케이션에 이르기까지 모든 것에 사용할 수 있는 강력한 스크립팅 언어를 제공합니다. 이 기사에서는 스크립트를 더욱 강력하고 견고하게 만드는 데 사용할 수 있는 Bash의 고급 기능 중 일부를 살펴보겠습니다.

## 조건부

Bash는 조건을 테스트하고 스크립트에서 결정을 내리는 다양한 방법을 제공합니다. 조건을 테스트하는 가장 일반적인 방법은 'if' 문을 사용하는 것입니다.

`if` 문 구문은 다음과 같습니다.

```
if CONDITION
then
    STATEMENTS
fi
```

'CONDITION'은 부울 값(true 또는 false)을 반환하는 모든 테스트가 될 수 있습니다. `then`과 `fi` 키워드 사이의 `STATEMENTS`는 `CONDITION`이 true로 평가되는 경우 실행됩니다.

다음은 간단한 예입니다.

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
fi
```

이 예에서 `$USER` 변수는 `"root"` 문자열과 같은지 확인하기 위해 검사됩니다. 그렇다면 `echo` 명령이 실행되어 메시지를 화면에 출력합니다.

`CONDITION`이 false인 경우 `else` 키워드를 사용하여 다른 `STATEMENTS` 세트를 실행할 수도 있습니다.

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
else
    echo "You are logged in as a normal user."
fi
```

여러 조건을 확인해야 하는 경우 `elif` 키워드("else if"의 줄임말)를 사용할 수 있습니다.

```bash
if [ $USER = "root" ]
then
    echo "You are logged in as the root user."
elif [ $USER = "bob" ]
then
    echo "You are logged in as Bob."
else
    echo "You are logged in as a normal user."
fi
```

`&&` 및 `||` 연산자를 사용하여 여러 조건을 결합할 수도 있습니다.

```bash
if [ $USER = "root" ] && [ $SHELL = "/bin/bash" ]
then
    echo "You are logged in as the root user and using the Bash shell."
fi

if [ $USER = "root" ] || [ $USER = "bob" ]
then
    echo "You are logged in as the root user or Bob."
fi
```

## 루프

루프는 일련의 명령문을 여러 번 실행하는 데 사용됩니다. Bash는 `for` 루프와 `while` 루프라는 두 가지 유형의 루프를 제공합니다.

### For 루프

For 루프는 값 목록을 반복하는 데 사용됩니다. for 루프의 구문은 다음과 같습니다.

```
for VARIABLE in LIST
do
    STATEMENTS
done
```

'LIST'는 파일 목록, 인수 목록 또는 숫자 목록과 같은 값 목록이 될 수 있습니다. `do` 및 `done` 키워드 사이의 `STATEMENTS`는 `LIST`의 각 값에 대해 한 번씩 실행됩니다.

다음은 간단한 예입니다.

```bash
for FILE in *.txt
do
    echo $FILE
done
```

이 예제는 `.txt` 확장자로 끝나는 현재 디렉토리의 모든 파일 이름을 인쇄합니다.

`seq` 명령을 사용하여 숫자 목록을 생성할 수도 있습니다.

```bash
for NUM in $(seq 1 10)
do
    echo $NUM
done
```

이 예제는 1에서 10까지의 숫자를 인쇄합니다.

### While 루프

While 루프는 조건이 충족될 때까지 일련의 명령문을 실행하는 데 사용됩니다. while 루프의 구문은 다음과 같습니다.

```
while CONDITION
do
    STATEMENTS
done
```

`do`와 `done` 키워드 사이의 `STATEMENTS`는 `CONDITION`이 false로 평가될 때까지 실행됩니다.

다음은 간단한 예입니다.

```bash
while [ $USER != "root" ]
do
    echo "You are not logged in as the root user."
done
```

이 예는 "루트 사용자로 로그인하지 않았습니다."라는 메시지를 계속 인쇄합니다. `$USER` 변수에 문자열 `"root"`가 포함될 때까지.

## 기능

함수는 일련의 명령문을 함께 그룹화하는 데 사용됩니다. 함수는 명령처럼 사용할 수 있으며 인수를 사용할 수 있습니다. 함수 구문은 다음과 같습니다.

```
function NAME {
    STATEMENTS
}
```

`NAME`은 함수에 부여하려는 이름이 될 수 있습니다. `{` 및 `}` 키워드 사이의 `STATEMENTS`는 함수가 호출될 때 실행됩니다.

다음은 간단한 예입니다.

```bash
function print_message {
    echo "This is a message."
}

print_message
```

이 예제는 화면에 메시지를 인쇄하는 `print_message`라는 함수를 정의합니다. 이 함수는 스크립트 끝에서 호출됩니다.

함수에 인수를 전달할 수도 있습니다.

```bash
function print_message {
    echo $1
}

print_message "This is a message."
```

이 예에서 `$1` 변수는 함수에 전달된 첫 번째 인수를 포함합니다. `$2`, `$3` 등의 변수를 사용하여 추가 인수에 액세스할 수 있습니다.

## 배열

배열은 여러 값을 포함할 수 있는 변수입니다. 배열을 만드는 구문은 다음과 같습니다.

```bash
NAME=(VALUE1 VALUE2 VALUE3...)
```

`NAME`은 배열에 부여하려는 이름이 될 수 있습니다. `VALUE`는 배열에 저장될 값입니다.

다음은 간단한 예입니다.

```bash
FILES=(*.txt *.sh)

for FILE in ${FILES[@]}
do
    echo $FILE
done
```

이 예제는 `.txt` 또는 `.sh` 확장자로 끝나는 현재 디렉토리의 모든 파일을 포함하는 `FILES`라는 배열을 만듭니다. `@` 기호는 배열을 개별 값 목록으로 확장하는 데 사용됩니다.

인덱스를 사용하여 배열의 개별 값에 액세스할 수도 있습니다.

```bash
FILES=(*.txt *.sh)

echo ${FILES[0]}
echo ${FILES[1]}
```

이 예는 `FILES` 배열의 첫 번째 값과 두 번째 값을 인쇄합니다(각각 `*.txt` 및 `*.sh`).

## 참조

  - [Bash 스크립팅 튜토리얼](https://www.shellscript.sh/)
  - [고급 Bash 스크립팅 가이드](https://tldp.org/LDP/abs/html/)
  - [초보자를 위한 배쉬 가이드](https://www.softpanorama.org/Scripting/Shellorama/bash_guide_for_beginners.shtml)