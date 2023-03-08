---
title: Linux 커널 디버깅 기술
description: 
published: true
date: 2023-02-11T21:32:59.164Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:32:52.288Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Kernel Debugging Techniques***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-debugging-techniques)
{.links-list}


# 리눅스 커널 디버깅 기법

Linux 커널은 움직이는 부분이 많은 복잡한 소프트웨어입니다. 따라서 일이 잘못되면 디버깅하기 어려울 수 있습니다. 이 기사에서는 Linux 커널을 디버깅하는 가장 유용한 기술 중 일부를 탐색합니다.

## 커널 메시지 인쇄

커널 디버깅을 위한 가장 기본적이고 유용한 기술 중 하나는 커널 로그에 메시지를 출력하는 것입니다. 커널 로그는 `/var/log/kern.log` 파일에 저장되는 모든 커널 활동의 기록입니다. 메시지는 `printk` 기능을 사용하여 커널 로그에 인쇄할 수 있습니다.

`printk` 함수는 형식 문자열과 가변 개수의 인수를 사용합니다. 형식 문자열은 사용자 공간의 `printf` 함수와 유사하지만 몇 가지 중요한 차이점이 있습니다. 첫째, `printk` 형식 문자열은 각각 현재 작업의 주소, 현재 시간(jiffies) 및 현재 CPU ID인 `%p`, `%t` 및 `%i`에 대한 형식 지정자를 포함할 수 있습니다. . 둘째, `printk` 형식 문자열은 다음 인수의 크기를 바이트 단위로 나타내는 `%ln` 지정자를 포함할 수 있습니다. 마지막으로 `printk` 형식 문자열은 다음 인수의 문자열 표현을 인쇄하는 `%s` 지정자를 포함할 수 있습니다.

다음은 `printk` 사용법의 간단한 예입니다.

```c
#include <linux/kernel.h>

void print_message(void)
{
    printk("This is a test message.\n");
}
```

## 커널 디버거 사용

커널 디버거 또는 `kdb`는 커널 디버깅을 위한 강력한 도구입니다. `kdb`는 커널 데이터 구조를 검사 및 변경하고, 중단점을 설정하고, 단일 단계 커널 코드를 사용하는 데 사용할 수 있습니다. `kdb` 명령줄 옵션을 커널 부팅 매개변수에 추가하여 `kdb`를 호출합니다. 이 옵션으로 커널을 부팅하면 커널 패닉이 발생할 때 `kdb`가 자동으로 입력됩니다.

`Ctrl-Alt-SysRq-K` 키 조합을 눌러 `kdb`를 수동으로 입력할 수도 있습니다. `kdb`를 입력하면 `kdb>` 프롬프트가 표시됩니다. 이 프롬프트에서 `kdb` 명령을 입력할 수 있습니다. 사용 가능한 명령 목록을 보려면 `kdb>` 프롬프트에 `help`를 입력하십시오.

가장 유용한 `kdb` 명령 중 하나는 `bt`입니다. 이 명령은 현재 호출 스택의 역추적을 인쇄합니다. 이는 커널 패닉이 발생한 위치와 이유를 이해하는 데 도움이 될 수 있습니다.

또 다른 유용한 `kdb` 명령은 `md`입니다. 이 명령은 메모리의 내용을 검사하는 데 사용할 수 있습니다. 예를 들어, `md 0xffffffff80000000 0x200` 명령은 커널 메모리의 처음 512바이트 내용을 인쇄합니다.

## 커널 프로브 사용

커널 프로브 또는 `kprobe`는 특정 커널 함수가 호출될 때 사용자 공간 코드의 실행을 허용하는 Linux 커널 기능입니다. `kprobe`는 디버깅 목적으로 커널을 계측하는 데 사용할 수 있습니다.

`kprobe`는 `kprobe` 명령줄 옵션을 사용하여 호출됩니다. `kprobe` 옵션은 커널 함수 이름과 사용자 공간 핸들러 함수를 사용합니다. 핸들러 함수는 커널 함수가 호출될 때마다 실행됩니다. 핸들러 함수는 커널 함수의 인수 및 반환 값에 액세스할 수 있습니다.

다음은 `kprobe` 사용법의 간단한 예입니다.

```c
#include <linux/kprobes.h>

static int handler_kprobe(struct kprobe *p, void *data)
{
    printk("kprobe hit!\n");
    return 0;
}

static struct kprobe kp = {
    .symbol_name    = "do_fork",
    .handler        = handler_kprobe,
};

static int __init kprobe_init(void)
{
    register_kprobe(&kp);
    return 0;
}

static void __exit kprobe_exit(void)
{
    unregister_kprobe(&kp);
}

module_init(kprobe_init)
module_exit(kprobe_exit)
```

이 예에서는 `do_fork` 커널 함수에 대해 `kprobe`가 등록됩니다. `do_fork`가 호출될 때마다 `handler_kprobe` 함수가 실행됩니다. `handler_kprobe` 함수는 단순히 커널 로그에 메시지를 출력합니다.

## 커널 추적 사용

커널 추적 또는 `ktrace`는 커널 활동을 추적할 수 있는 Linux 커널 기능입니다. `ktrace`는 디버깅 목적으로 커널을 계측하는 데 사용할 수 있습니다.

`ktrace`는 `ktrace` 명령줄 옵션을 사용하여 호출됩니다. `ktrace` 옵션은 추적 버퍼 크기와 추적 파일 이름을 사용합니다. 추적 버퍼는 추적 이벤트를 저장하는 데 사용됩니다. 추적 파일은 사람이 읽을 수 있는 추적 이벤트 표현을 저장하는 데 사용됩니다.

다음은 `ktrace` 사용의 간단한 예입니다.

```c
#include <linux/ktrace.h>

static int __init ktrace_init(void)
{
    ktrace("/tmp/ktrace.out", 1024);
    return 0;
}

static void __exit ktrace_exit(void)
{
    ktrace_stop();
}

module_init(ktrace_init)
module_exit(ktrace_exit)
```

이 예에서 `ktrace`는 `/tmp/ktrace.out` 파일에 대한 커널 활동을 추적하도록 구성됩니다. 추적 버퍼는 1024KB로 설정됩니다.

## 커널 프로파일러 사용

커널 프로파일러 또는 `kprof`는 커널 코드의 프로파일링을 허용하는 Linux 커널 기능입니다. `kprof`는 커널에 대한 성능 정보를 수집하는 데 사용할 수 있습니다.

`kprof`는 `kprof` 명령줄 옵션을 사용하여 호출됩니다. `kprof` 옵션은 프로파일링 간격과 추적 파일 이름을 사용합니다. 프로파일링 간격은 샘플 사이의 시간(나노초)입니다. 추적 파일은 프로파일링 정보를 저장하는 데 사용됩니다.

다음은 `kprof` 사용법의 간단한 예입니다.

```c
#include <linux/kprof.h>

static int __init kprof_init(void)
{
    kprof("/tmp/kprof.out", 10000000);
    return 0;
}

static void __exit kprof_exit(void)
{
    kprof_stop();
}

module_init(kprof_init)
module_exit(kprof_exit)
```

이 예에서 `kprof`는 10밀리초마다 커널 코드를 프로파일링하도록 구성됩니다. 프로파일링 정보는 `/tmp/kprof.out` 파일에 저장됩니다.

## 결론

이 기사에서는 Linux 커널을 디버깅하는 가장 유용한 기술 중 일부를 살펴보았습니다. 이러한 기술을 사용하여 커널 패닉, 성능 문제 및 기타 문제를 디버깅할 수 있습니다.