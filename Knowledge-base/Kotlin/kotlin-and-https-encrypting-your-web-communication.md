---
title: Kotlin 및 HTTPS: 웹 통신 암호화
description: 
published: true
date: 2023-02-15T14:17:53.580Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:17:51.111Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and HTTPS: Encrypting Your Web Communication***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-https-encrypting-your-web-communication)
{.links-list}


     

Kotlin 및 HTTPS: 웹 통신 암호화
====================================================

데이터 보안의 중요성이 점점 커지면서 웹 통신을 암호화하는 것이 그 어느 때보다 중요해졌습니다. Kotlin을 사용하면 코드 몇 줄만으로 웹 통신에 HTTPS 암호화를 쉽게 추가할 수 있습니다.

HTTPS란 무엇입니까?
---------------

HTTPS는 인터넷을 통한 보안 통신을 위한 프로토콜입니다. 웹 사이트와 사용자의 웹 브라우저 간에 교환되는 데이터의 개인 정보를 보호하기 위해 암호화를 사용합니다. HTTPS는 웹에서 보안 통신을 위한 표준이며 온라인 뱅킹 및 쇼핑과 같은 많은 민감한 작업에 필요합니다.

HTTPS를 사용하는 이유
---------------

HTTPS 암호화는 제3자가 웹 통신을 도청하거나 변조하는 것을 방지합니다. 이는 사용자 데이터의 개인정보 보호와 웹사이트 보안을 위해 중요합니다. HTTPS는 또한 사용자가 자신이 생각하는 웹사이트에 실제로 연결하고 있는지 확인하는 데 도움이 되며, 이는 피싱 공격을 방지하는 데 중요합니다.

Kotlin에서 HTTPS를 사용하는 방법
-------------------------

Kotlin을 사용하면 웹 통신에 HTTPS 암호화를 쉽게 추가할 수 있습니다. 가장 먼저 해야 할 일은 SSLContext를 만드는 것입니다. 보안 구성의 세부 정보가 포함된 개체입니다.

    val sslContext = SSLContext.getInstance("TLS")

다음으로 키 저장소를 만들어야 합니다. 이것은 웹사이트의 ID를 확인하는 데 사용되는 보안 인증서 데이터베이스입니다. Java Keytool을 사용하여 키 저장소를 생성할 수 있습니다.

    keytool -genkey -keyalg RSA -alias mysite -keystore mysite.jks -storepass 암호 -validity 365 -keysize 2048

"mysite"를 웹사이트 이름으로 바꾸고 "password"를 보안 암호로 바꿉니다. 그러면 현재 디렉토리에 "mysite.jks"라는 키 저장소 파일이 생성됩니다.

이제 키 저장소가 있으므로 이를 사용하도록 SSLContext를 구성해야 합니다.

    val keyStore = FileInputStream("mysite.jks")
    발 암호 = "비밀번호"
    val keyStoreType = "jks"
    val keyManagerFactory = KeyManagerFactory.getInstance(KeyManagerFactory.getDefaultAlgorithm())
    keyManagerFactory.init(keyStore, password.toCharArray())
    val trustManagerFactory = TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm())
    trustManagerFactory.init(키스토어)
    val trustManagers = trustManagerFactory.trustManagers
    sslContext.init(keyManagerFactory.keyManagers, trustManagers, null)

마지막으로 HTTPS를 사용하도록 웹 서버에 지시해야 합니다. 예를 들어 Jetty 웹 서버를 사용하는 경우 "jetty.xml" 구성 파일에 다음을 추가하여 이를 수행할 수 있습니다.

    <통화 이름="addConnector">
      <인수>
        <New class="org.eclipse.jetty.server.ssl.SslSelectChannelConnector">
          <세트 이름="포트">8443</세트>
          <Set name="maxIdleTime">30000</Set>
          <Set name="keystore">mysite.jks</Set>
          <Set name="password">비밀번호</Set>
          <Set name="keyPassword">비밀번호</Set>
          <Set name="truststore">mysite.jks</Set>
          <Set name="trustPassword">비밀번호</Set>
          <세트 이름="프로토콜">TLS</세트>
          <Set name="sslProtocols">TLSv1</Set>
          <Set name="ciphers">TLS_RSA_WITH_AES_128_CBC_SHA,TLS_DHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</세트>
        </New>
      </인수>
    </콜>

"mysite.jks"를 키 저장소 파일의 경로로 바꾸고 "password"를 키 저장소를 만드는 데 사용한 암호로 바꿉니다.

Apache 및 Nginx와 같은 다른 웹 서버에서 HTTPS를 구성할 수도 있습니다. 자세한 내용은 웹 서버 설명서를 참조하십시오.

HTTPS 연결 테스트
--------------------------------------------

HTTPS를 사용하도록 웹 서버를 구성한 후에는 다음 명령을 사용하여 연결을 테스트할 수 있습니다.

    컬 --안전하지 않은 -v https://mysite.com

"mysite.com"을 귀하의 웹사이트 이름으로 바꾸십시오. 이 명령은 프로토콜(HTTPS), 암호화 제품군 및 인증서 체인을 포함하여 연결에 대한 많은 정보를 출력합니다.

웹 브라우저를 사용하여 HTTPS 연결을 테스트할 수도 있습니다. 웹 브라우저에서 웹사이트를 열고 주소 표시줄을 확인하여 연결이 암호화되었는지 확인하십시오. 주소 옆에 자물쇠 아이콘도 표시되어야 합니다.

오류가 표시되면 웹 서버가 올바르게 구성되어 있고 웹 사이트의 DNS 레코드가 올바른 IP 주소를 가리키고 있는지 확인하십시오.

자원
---------

- [HTTPS 튜토리얼](https://www.sslshopper.com/article-how-to-set-up-ssl-on-nginx.html)
- [코틀린 SSL/TLS 가이드](https://kotlinlang.org/docs/reference/ssl-tls.html)
- [Java Keytool 설명서](https://docs.oracle.com/cd/E19906-01/820-4916/ablqw/index.html)