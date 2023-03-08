---
title: 비차단 I/O 작업을 위한 Java의 java.nio 패키지
description: 
published: true
date: 2023-02-15T11:17:44.977Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:17:43.327Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's java.nio Package for Non-Blocking I/O Operations***English** document is available*](/en/Knowledge-base/Java/java-s-java-nio-package-for-non-blocking-io-operations)
{.links-list}



# Non-Blocking I/O 작업을 위한 Java의 java.nio 패키지

Java의 `java.nio` 패키지는 Java에서 *비차단* 입출력(I/O) 작업을 수행하기 위한 API를 제공합니다. Non-blocking I/O는 작업이 완료될 때까지 기다리지 않고 스레드가 I/O 작업을 시작할 수 있음을 의미합니다. 이는 I/O 작업이 수행되는 동안 스레드가 다른 작업을 수행할 수 있으므로 보다 효율적인 I/O 작업으로 이어질 수 있습니다.

## java.nio 개요

`java.nio` 패키지는 Java 1.4에서 도입되었으며 다음을 제공합니다.

- 다양한 기본 유형으로 데이터를 저장하기 위한 `Buffer` 클래스 집합
- I/O 작업을 수행하기 위한 `Channel` 클래스 집합
- 다중 I/O 작업을 위한 `Selector` 클래스 집합
- 파일 기반 I/O 작업을 수행하기 위한 `FileLock` 및 `FileChannel` 클래스 세트

또한 `java.nio.file` 패키지는 Java 7에서 도입되었으며 파일 기반 I/O 작업을 지원합니다.

## 버퍼

'버퍼'는 특정 기본 유형의 데이터에 대한 컨테이너입니다. 기본 데이터 유형인 `ByteBuffer`, `CharBuffer`, `DoubleBuffer`, `FloatBuffer`, `IntBuffer`, `LongBuffer` 및 `ShortBuffer` 각각에 대한 `Buffer` 클래스가 있습니다.

`버퍼`에는 다음과 같은 속성이 있습니다.

- **용량:** 버퍼에 저장할 수 있는 최대 요소 수입니다.
- **제한:** 읽거나 쓰지 않아야 하는 첫 번째 요소의 인덱스입니다.
- **위치:** 읽거나 쓸 다음 요소의 인덱스입니다.

`Buffer`에는 다음과 같은 메서드도 있습니다.

- `clear()`: 위치를 0으로, 제한을 용량으로 설정합니다.
- `flip()`: 리미트를 현재 위치로 설정하고 위치를 0으로 설정합니다.
- `rewind()`: 위치를 0으로 설정합니다.
- `remaining()`: 위치와 한계 사이의 요소 수를 반환합니다.
- `hasRemaining()`: 요소가 남아 있으면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.

## 채널

'채널'은 I/O 장치에 대한 열린 연결을 나타내는 '버퍼'와 같은 구조입니다. '채널'은 읽기, 쓰기 또는 둘 다를 위해 열릴 수 있습니다.

`FileChannel`, `DatagramChannel`, `SocketChannel` 및 `Pipe.SinkChannel`을 포함하여 여러 유형의 `Channel`이 있습니다.

`Channel`에는 다음과 같은 메서드가 있습니다.

- `isOpen()`: 채널이 열려 있으면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.
- `close()`: 채널을 닫습니다.
- `read(Buffer)`: 채널에서 주어진 버퍼로 데이터를 읽습니다.
- `write(Buffer)`: 주어진 버퍼에서 채널로 데이터를 씁니다.

## 선택자

'Selector'는 I/O 작업을 다중화하는 데 사용됩니다. 하나 이상의 `Channel`에서 I/O 작업이 완료되기를 기다리는 데 `Selector`를 사용할 수 있습니다.

`Selector`에는 다음과 같은 메서드가 있습니다.

- `open()`: `선택기`를 엽니다.
- `close()`: `선택기`를 닫습니다.
- `select()`: I/O 작업을 수행할 준비가 된 `Channel`에 대한 `SelectionKey`를 반환합니다.
- `select(long)`: I/O 작업을 수행할 준비가 된 `Channel`에 대한 `SelectionKey`를 반환하거나 시간 제한이 만료되면 `null`을 반환합니다.
- `selectedKeys()`: I/O 작업을 수행할 준비가 된 `Channel`에 대한 `SelectionKey`의 `Set`을 반환합니다.
- `keys()`: 이 `Selector`에 등록된 모든 `Channel`에 대한 `SelectionKey`의 `Set`을 반환합니다.

## 파일 잠금

`FileLock`은 `FileChannel`의 영역을 잠그는 데 사용됩니다. `FileLock`에는 다음과 같은 방법이 있습니다.

- `isShared()`: 잠금이 공유되면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.
- `release()`: 잠금을 해제합니다.
- `isValid()`: 잠금이 여전히 유효하면 `true`를 반환하고 그렇지 않으면 `false`를 반환합니다.

## 파일채널

'FileChannel'은 파일 기반 I/O 작업을 수행하는 데 사용되는 'Channel'입니다. `FileChannel`에는 다음과 같은 메서드가 있습니다.

- `lock(long, long, boolean)`: 파일의 영역을 잠급니다.
- `tryLock()`: 파일의 영역을 잠그려고 시도합니다.
- `read(ByteBuffer, long)`: 파일에서 주어진 버퍼로 데이터를 읽습니다.
- `write(ByteBuffer, long)`: 주어진 버퍼의 데이터를 파일에 씁니다.

## java.nio.file

`java.nio.file` 패키지는 Java 7에서 도입되었으며 파일 기반 I/O 작업을 지원합니다. 이 패키지에는 다음 클래스가 포함되어 있습니다.

- `경로`: 파일 시스템 경로를 나타냅니다.
- `Paths`: `Path` 개체를 생성하기 위한 팩터리입니다.
- `파일`: 파일 관련 작업을 수행하기 위한 유틸리티 클래스입니다.

## 결론

Java의 `java.nio` 패키지는 Java에서 비차단 I/O 작업을 수행하기 위한 API를 제공합니다. `java.nio.file` 패키지는 Java 7에서 도입되었으며 파일 기반 I/O 작업을 지원합니다.