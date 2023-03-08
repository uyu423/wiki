---
title: HTTPS 및 SSL 인증서로 웹사이트를 보호하는 방법
description: 
published: true
date: 2023-02-25T16:32:33.984Z
tags: 
editor: markdown
dateCreated: 2023-02-25T16:32:32.610Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Secure Your Website with HTTPS and SSL Certificates***English** document is available*](/en/Knowledge-base/Common/how-to-secure-your-website-with-https-and-ssl-certificates)
{.links-list}


# HTTPS 및 SSL 인증서로 웹사이트를 보호하는 방법

HTTP(Hypertext Transfer Protocol)는 분산, 협업 및 하이퍼미디어 정보 시스템을 위한 애플리케이션 프로토콜입니다. HTTP는 World Wide Web을 위한 데이터 통신의 기반입니다. 하이퍼텍스트는 텍스트를 포함하는 노드 사이에 논리적 링크(하이퍼링크)를 사용하는 구조화된 텍스트입니다.

TLS(Transport Layer Security)로 보호되는 HTTP는 일반적으로 HTTPS로 알려져 있으며 사용자의 웹 브라우저와 웹사이트 간의 데이터 기밀성을 보호하는 데 사용됩니다. TLS는 인터넷을 통해 통신 보안을 제공하는 암호화 프로토콜입니다.

웹 브라우저가 HTTPS로 보호되는 웹 사이트에 액세스를 시도하면 브라우저와 웹 서버는 TLS를 사용하여 보안 연결을 설정합니다. TLS는 공개 키와 대칭 키 암호화의 조합을 사용하여 연결을 통해 전송되는 데이터를 암호화합니다.

HTTPS로 보호되는 웹사이트는 브라우저 주소 표시줄의 녹색 자물쇠로 식별됩니다.

## SSL이란?

SSL(Secure Sockets Layer)은 웹 서버와 웹 브라우저 간에 암호화된 링크를 설정하기 위한 표준 보안 기술입니다. SSL 연결을 생성하려면 SSL 인증서가 필요합니다.

SSL은 일반적으로 신용 카드 거래, 데이터 전송 및 로그인을 보호하는 데 사용됩니다. 또한 이메일, 인스턴트 메시징 및 VoIP(Voice over IP) 대화를 보호하는 데 사용됩니다.

 SSL 인증서는 웹사이트와 웹사이트 소유자의 신원을 확인하는 신뢰할 수 있는 제3자 인증 기관(CA)에서 발급합니다.

## SSL은 어떻게 작동합니까?

웹 브라우저가 SSL로 보호되는 웹 사이트에 액세스를 시도하면 브라우저와 웹 서버는 TLS 프로토콜을 사용하여 SSL 연결을 설정합니다.

TLS는 인터넷을 통해 통신 보안을 제공하는 암호화 프로토콜입니다. TLS는 공개 키와 대칭 키 암호화의 조합을 사용하여 연결을 통해 전송되는 데이터를 암호화합니다.

공개 키는 데이터를 암호화하는 데 사용되고 대칭 키는 데이터를 해독하는 데 사용됩니다.

## SSL 인증서란?

SSL 인증서는 SSL 연결을 만드는 데 사용되는 디지털 인증서입니다.

SSL 인증서는 웹사이트와 웹사이트 소유자의 신원을 확인하는 신뢰할 수 있는 제3자 인증 기관(CA)에서 발급합니다.

SSL로 보호되는 웹사이트는 브라우저 주소 표시줄의 녹색 자물쇠로 식별됩니다.

## HTTPS로 웹사이트를 보호하는 방법

HTTPS로 웹 사이트를 보호하려면 인증 기관에서 SSL 인증서를 받아야 합니다.

 SSL 인증서를 받으면 웹 서버에 SSL 인증서를 설치하고 HTTPS를 사용하도록 웹 사이트를 구성해야 합니다.

## SSL 인증서 받기

필요에 따라 선택할 수 있는 몇 가지 SSL 인증서 유형이 있습니다. SSL 인증서의 가장 일반적인 유형은 DV(Domain Validated) 인증서입니다.

DV SSL 인증서는 가장 단순하고 가장 일반적인 유형의 SSL 인증서입니다. DV SSL 인증서는 일반적으로 몇 분 안에 발급되며 어떠한 서류 작업도 필요하지 않습니다.

웹 사이트에 SSL 인증서가 필요한 경우 Let's Encrypt를 사용하여 무료로 DV SSL 인증서를 생성할 수 있습니다.

## 암호화하자

Let's Encrypt는 자동화된 무료 개방형 인증 기관입니다.

Let's Encrypt를 사용하면 무료 SSL/TLS 인증서를 쉽게 얻고 설치할 수 있으므로 웹 서버에서 암호화된 HTTPS를 사용할 수 있습니다.

## SSL 인증서 설치

SSL 인증서를 받으면 웹 서버에 설치해야 합니다.

SSL 인증서 설치 프로세스는 웹 서버 소프트웨어에 따라 다릅니다.

## HTTPS를 사용하도록 웹사이트 구성

SSL 인증서를 설치했으면 HTTPS를 사용하도록 웹 사이트를 구성해야 합니다.

HTTPS를 사용하도록 웹 사이트를 구성하는 프로세스는 웹 서버 소프트웨어에 따라 다릅니다.

## 웹사이트 테스트

HTTPS를 사용하도록 웹사이트를 구성한 후에는 웹사이트를 테스트하여 제대로 작동하는지 확인해야 합니다.

SSL Labs Server Test를 사용하여 웹사이트를 무료로 테스트할 수 있습니다.

## 외부 리소스

- [Let's Encrypt](https://letsencrypt.org/)
- [SSL Labs 서버 테스트](https://www.ssllabs.com/ssltest/)
- [SSL 인증서 취득 방법](https://www.namecheap.com/security/ssl-certificates/how-to-obtain-an-ssl-certificate.aspx)
- [SSL 인증서 설치 방법](https://www.namecheap.com/security/ssl-certificates/how-to-install-an-ssl-certificate.aspx)
- [HTTPS를 사용하도록 웹사이트를 구성하는 방법](https://www.namecheap.com/support/knowledgebase/article.aspx/9645/68/how-to-configure-your-website-to-use-https)