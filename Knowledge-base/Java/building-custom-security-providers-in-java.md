---
title: Java에서 사용자 지정 보안 공급자 구축
description: 
published: true
date: 2023-02-25T03:32:57.630Z
tags: 
editor: markdown
dateCreated: 2023-02-25T03:32:50.265Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Custom Security Providers in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-security-providers-in-java)
{.links-list}


# Java로 맞춤형 보안 제공자 구축

Java 플랫폼은 보안 알고리즘을 구현하는 보안 제공자를 연결하는 방법을 제공합니다. 예를 들어 SunJCE 공급자는 디지털 서명 알고리즘(DSA), 키 계약 및 비밀 키 팩토리 알고리즘과 같은 다양한 알고리즘의 구현을 제공합니다.

이 기사에서는 Java로 자체 보안 공급자를 작성하는 방법과 이를 Java 보안 아키텍처에 통합하는 방법을 배웁니다.

## 보안 공급자란?

보안 공급자는 보안 알고리즘 구현을 제공하는 소프트웨어입니다. Java 플랫폼에는 "SUN" 제공자(또는 "SunJCE" 제공자)라는 기본 보안 제공자가 함께 제공되며, 이는 디지털 서명 알고리즘(DSA), 키 계약 및 비밀 키 팩토리 알고리즘과 같은 다양한 알고리즘의 구현을 제공합니다. .

그러나 SUN 제공자가 사용 가능한 유일한 보안 제공자는 아닙니다. Bouncy Castle 공급자와 같은 다른 공급자도 다양한 보안 알고리즘의 구현을 제공합니다.

## 공급자 아키텍처

Java 보안 아키텍처는 애플리케이션이 필요에 따라 다른 보안 제공자를 플러그인할 수 있도록 설계되었습니다. 이 아키텍처는 다음 개념을 기반으로 합니다.

- **서비스**는 공급자가 구현할 수 있는 잘 정의된 알고리즘(또는 기타 기능) 집합입니다.
- **제공자**는 하나 이상의 서비스 구현을 제공하는 패키지 또는 라이브러리입니다.
- **서비스 유형**은 특정 유형의 서비스를 지정하는 Java 인터페이스 또는 클래스입니다.

예를 들어, KeyFactory 서비스는 키(Key 유형)를 키 사양(KeySpec 유형)으로 또는 그 반대로 변환하는 일을 담당합니다. SUN 공급자는 이 서비스의 구현을 제공하고 Bouncy Castle 공급자도 이 서비스의 구현을 제공합니다.

Java 보안 아키텍처는 KeyFactory, KeyPairGenerator 및 MessageDigest와 같은 여러 표준 서비스 유형을 정의합니다. 이러한 표준 서비스 중 하나의 구현을 제공하는 공급자를 해당 서비스를 "구현"한다고 합니다.

## 공급자 등록

공급자를 사용하려면 먼저 Java 보안 아키텍처에 등록해야 합니다. 이는 Security.addProvider() 메서드를 호출하여 프로그래밍 방식으로 수행하거나 java.security 파일에 공급자를 추가하여 정적으로 수행할 수 있습니다.

공급자를 정적으로 추가하는 것은 응용 프로그램 코드를 수정할 필요가 없으므로 선호되는 접근 방식입니다.

다음은 공급자를 정적으로 추가하는 예입니다.

```
security.provider.1=com.example.MyProvider
```

이 예에서 MyProvider는 공급자 클래스의 이름입니다.

## 공급자 클래스

모든 공급자에는 공급자 클래스가 있어야 합니다. 공급자 클래스는 공급자 클래스의 구체적인 하위 클래스입니다. 공급자 클래스에는 공급자 이름인 단일 String 인수를 사용하는 공용 생성자가 있어야 합니다.

공급자 클래스는 공급자 클래스에서 상속된 getName() 및 getInfo() 메서드도 재정의해야 합니다.

다음은 공급자 클래스의 간단한 예입니다.

```java
package com.example;

import java.security.Provider;

public class MyProvider extends Provider {

    public MyProvider() {
        super("MyProvider", 1.0, "MyProvider");
    }

    @Override
    public String getName() {
        return "MyProvider";
    }

    @Override
    public String getInfo() {
        return "MyProvider 1.0";
    }
}
```

이 예에서 공급자 이름은 "MyProvider"이고 공급자 버전은 "1.0"입니다.

## 서비스 구현

공급자 클래스가 작성되면 다음 단계는 하나 이상의 서비스를 구현하는 것입니다. 앞서 언급했듯이 서비스는 공급자가 구현할 수 있는 잘 정의된 알고리즘(또는 기타 기능) 집합입니다.

예를 들어 SUN 공급자는 KeyFactory 서비스, KeyPairGenerator 서비스 및 MessageDigest 서비스와 같은 다양한 서비스의 구현을 제공합니다.

서비스를 구현하려면 공급자는 Service 클래스의 구체적인 하위 클래스를 제공해야 합니다. 이 하위 클래스에는 다음 인수를 사용하는 공용 생성자가 있어야 합니다.

- 제공자 객체.
- 서비스 유형인 String 개체입니다.
- 알고리즘 이름인 String 객체.
- 구현의 클래스 이름인 String 개체입니다.

다음은 Service 하위 클래스의 간단한 예입니다.

```java
package com.example;

import java.security.Provider;
import java.security.Service;

public class MyService extends Service {

    public MyService(Provider provider, String type, String algorithm, String className) {
        super(provider, type, algorithm, className, null, null);
    }
}
```

이 예에서 서비스 유형은 "KeyFactory"이고 알고리즘 이름은 "DSA"이며 구현의 클래스 이름은 "com.example.MyKeyFactory"입니다.

## 키팩토리 서비스

KeyFactory 서비스는 키(Key 유형)를 키 사양(KeySpec 유형)으로 또는 그 반대로 변환하는 일을 담당합니다.

KeyFactory 서비스는 다음 메소드를 구현해야 합니다.

- generatePublic(KeySpec keySpec)
- generatePrivate(KeySpec keySpec)
- getKeySpec(키 키, 클래스 keySpec)
- translateKey(키 키)

또한 KeyFactory 서비스는 선택적으로 다음 메서드를 구현할 수 있습니다.

- generateSecretKey(KeySpec 키 사양)
- getKeySpec(키 키, 클래스 keySpec)

KeyFactory 서비스는 일반적으로 응용 프로그램에서 서로 다른 키 형식 간에 변환하는 데 사용됩니다. 예를 들어 애플리케이션에 X.509 인증서 형식의 키가 있을 수 있으며 서명 서비스에서 사용할 수 있는 형식으로 변환해야 합니다.

다음은 KeyFactory 서비스의 간단한 예입니다.

```java
package com.example;

import java.security.Key;
import java.security.KeyFactory;
import java.security.KeySpec;
import java.security.spec.X509EncodedKeySpec;

public class MyKeyFactory extends KeyFactory {

    public MyKeyFactory() {
        super("MyKeyFactory");
    }

    @Override
    public Key generatePublic(KeySpec keySpec) {
        // TODO: Implement this method
        return null;
    }

    @Override
    public Key generatePrivate(KeySpec keySpec) {
        // TODO: Implement this method
        return null;
    }

    @Override
    public KeySpec getKeySpec(Key key, Class keySpec) {
        // TODO: Implement this method
        return null;
    }

    @Override
    public Key translateKey(Key key) {
        // TODO: Implement this method
        return null;
    }
}
```

이 예에서 KeyFactory 서비스의 이름은 "MyKeyFactory"이며 generatePublic(), generatePrivate(), getKeySpec() 및 translateKey() 메서드를 구현합니다.

## 시그니처 서비스

서명 서비스는 디지털 서명 생성 및 확인을 담당합니다.

서명 서비스는 다음 메서드를 구현해야 합니다.

- initSign(프라이빗키 프라이빗키)
- initVerify(공개키 공개키)
- 징후()
- 검증(바이트[] 서명)

또한 서명 서비스는 선택적으로 다음 메서드를 구현할 수 있습니다.

- setParameter(문자열 매개변수 이름, 개체 매개변수 값)
- getParameter(문자열 매개변수 이름)

서명 서비스는 일반적으로 응용 프로그램에서 디지털 서명을 만들고 확인하는 데 사용됩니다. 예를 들어 애플리케이션은 네트워크를 통해 문서를 보내기 전에 서명 서비스를 사용하여 문서에 서명할 수 있습니다.

다음은 서명 서비스의 간단한 예입니다.

```java
package com.example;

import java.security.Key;
import java.security.PrivateKey;
import java.security.PublicKey;
import java.security.Signature;

public class MySignature extends Signature {

    public MySignature() {
        super("MySignature");
    }

    @Override
    public void initSign(PrivateKey privateKey) {
        // TODO: Implement this method
    }

    @Override
    public void initVerify(PublicKey publicKey) {
        // TODO: Implement this method
    }

    @Override
    public void sign() {
        // TODO: Implement this method
    }

    @Override
    public boolean verify(byte[] signature) {
        // TODO: Implement this method
        return false;
    }
}
```

이 예에서 서명 서비스의 이름은 "MySignature"이며 initSign(), initVerify(), sign() 및 verify() 메서드를 구현합니다.

## 메시지 다이제스트 서비스

MessageDigest 서비스는 메시지 다이제스트 생성을 담당합니다. 메시지 다이제스트는 데이터 조각의 디지털 지문을 생성하는 데 사용되는 암호화 해시 함수입니다.

MessageDigest 서비스는 다음 메서드를 구현해야 합니다.

- 업데이트(바이트[] 데이터)
- 업데이트(byte[] 데이터, int 꺼짐, int len)
- 다이제스트()
- 다이제스트(바이트[] 데이터)
- isEqual(바이트[] 다이제스트A, 바이트[] 다이제스트B)

또한 MessageDigest 서비스는 선택적으로 다음 메서드를 구현할 수 있습니다.

- 초기화()
- 클론()

MessageDigest 서비스는 일반적으로 애플리케이션에서 메시지 다이제스트를 생성하는 데 사용됩니다. 예를 들어 애플리케이션은 MessageDigest 서비스를 사용하여 네트워크를 통해 문서를 보내기 전에 문서의 메시지 다이제스트를 생성할 수 있습니다.

다음은 MessageDigest 서비스의 간단한 예입니다.

```java
package com.example;

import java.security.MessageDigest;

public class MyMessageDigest extends MessageDigest {

    public MyMessageDigest() {
        super("MyMessageDigest");
    }

    @Override
    public void update(byte[] data) {
        // TODO: Implement this method
    }

    @Override
    public void update(byte[] data, int off, int len) {
        // TODO: Implement this method
    }

    @Override
    public byte[] digest() {
        // TODO: Implement this method
        return null;
    }

    @Override
    public int digest(byte[] data, int off, int len) {
        // TODO: Implement this method
        return 0;
    }

    @Override
    public boolean isEqual(byte[] digestA, byte[] digestB) {
        // TODO: Implement this method
        return false;
    }

    @Override
    public void reset() {
        // TODO: Implement this method
    }

    @Override
    public Object clone() {
        // TODO: Implement this method
        return null;
    }
}
```

이 예에서 MessageDigest 서비스의 이름은 "MyMessageDigest"이며 update(), update(), digest(), digest(), isEqual(), reset() 및 clone() 메서드를 구현합니다.

## 결론

이 기사에서는 Java로 자체 보안 공급자를 작성하는 방법과 이를 Java 보안 아키텍처에 통합하는 방법을 배웠습니다. 또한 KeyFactory 서비스, 서명 서비스 및 MessageDigest 서비스와 같이 공급자가 구현할 수 있는 서비스의 몇 가지 예를 살펴보았습니다.