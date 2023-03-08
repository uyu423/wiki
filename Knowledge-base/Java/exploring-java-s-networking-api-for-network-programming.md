---
title: 네트워크 프로그래밍을 위한 Java의 네트워킹 API 탐색
description: 
published: true
date: 2023-01-31T04:23:51.485Z
tags: 
editor: markdown
dateCreated: 2023-01-31T04:23:49.858Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Exploring Java's Networking API for Network Programming***English** version of this document is available*](/en/Knowledge-base/Java/exploring-java-s-networking-api-for-network-programming)
{.links-list}

    
Java 프로그래밍에는 항상 강력한 네트워킹 구성 요소가 있습니다. 데스크톱에서 웹, 모바일에 이르기까지 광범위한 응용 프로그램을 개발하는 데 사용할 수 있는 다재다능한 언어입니다. Java 플랫폼에는 네트워크 프로그래밍에 필요한 모든 기능을 제공하는 네트워킹 클래스 및 인터페이스의 광범위한 라이브러리가 있습니다.

이 기사에서는 Java 네트워킹 API와 이를 사용하여 구현할 수 있는 몇 가지 일반적인 네트워킹 시나리오를 살펴봅니다. 또한 사용 가능한 몇 가지 고급 기능에 대해서도 살펴보겠습니다.

Java 플랫폼의 네트워킹 API는 요청/응답 모델을 기반으로 합니다. 클라이언트가 요청하고 서버가 응답합니다. 클라이언트와 서버는 동일한 시스템에 있을 수도 있고 다른 시스템에 있을 수도 있습니다. 요청 및 응답은 모든 형식일 수 있지만 가장 일반적인 형식은 HTTP입니다.

HTTP는 World Wide Web에서 사용하는 형식입니다. TCP/IP 프로토콜 위에 구축된 간단한 텍스트 기반 프로토콜입니다. HTTP는 상태 비저장입니다. 즉, 각 요청은 다른 요청과 독립적입니다. 이는 웹 애플리케이션을 위한 매우 효율적인 프로토콜이 됩니다.

Java 플랫폼의 네트워킹 API에는 네트워크 프로그래밍에 필요한 저수준 기능을 제공하는 일련의 클래스 및 인터페이스가 포함되어 있습니다. java.net 패키지에는 핵심 네트워킹 클래스와 인터페이스가 포함되어 있습니다. javax.net 패키지에는 핵심 네트워킹 클래스 및 인터페이스에 대한 확장이 포함되어 있습니다.

java.net.URL 클래스는 Java 플랫폼의 네트워킹 API에 대한 게이트웨이입니다. 인터넷에서 리소스를 식별하는 방법인 Uniform Resource Locator를 나타냅니다. 리소스는 웹 페이지, 이미지, 파일 또는 URL로 식별할 수 있는 모든 것이 될 수 있습니다.

java.net.URL 클래스에는 데이터를 읽고 URL에 쓰는 여러 메서드가 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getContent()
- openConnection()
- 오픈스트림()
- getInputStream()

getContent() 메서드는 URL의 내용을 나타내는 객체를 반환합니다. openConnection() 메서드는 URL에 대한 연결을 나타내는 URLConnection 객체를 반환합니다. openStream() 메서드는 URL에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다. getInputStream() 메서드는 URL에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다.

java.net.URLConnection 클래스는 URL에 대한 연결을 나타냅니다. 연결을 열고 URL에서 데이터를 읽는 데 사용할 수 있습니다. URLConnection 클래스에는 데이터를 읽고 URL에 쓰는 여러 메서드가 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getContent()
- getInputStream()
- getOutputStream()
- setDoInput()
- setDoOutput()
- 연결하다()

getContent() 메서드는 URL의 내용을 나타내는 객체를 반환합니다. getInputStream() 메서드는 URL에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다. getOutputStream() 메서드는 URL에 데이터를 쓰는 데 사용할 수 있는 OutputStream을 반환합니다. setDoInput() 메서드는 입력에 URLConnection을 사용해야 하는지 여부를 설정합니다. setDoOutput() 메서드는 출력에 URLConnection을 사용해야 하는지 여부를 설정합니다. connect() 메서드는 URL에 대한 연결을 엽니다.

java.net.Socket 클래스는 두 컴퓨터 간의 통신 끝점인 소켓을 나타냅니다. 소켓은 데이터를 읽고 쓰는 데 모두 사용할 수 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getInputStream()
- getOutputStream()
- 닫다()

getInputStream() 메서드는 Socket에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다. getOutputStream() 메서드는 Socket에 데이터를 쓰는 데 사용할 수 있는 OutputStream을 반환합니다. close() 메서드는 소켓을 닫습니다.

java.net.ServerSocket 클래스는 서버의 통신 끝점인 서버 소켓을 나타냅니다. ServerSocket을 사용하여 클라이언트에서 들어오는 연결을 수락할 수 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- 동의하기()
- 닫다()

accept() 메서드는 클라이언트에서 들어오는 연결을 수락합니다. close() 메서드는 ServerSocket을 닫습니다.

Java 플랫폼의 네트워킹 API를 사용하려면 TCP/IP 프로토콜에 대한 기본적인 이해가 있어야 합니다. TCP/IP는 인터넷에서 컴퓨터 간의 통신에 사용되는 프로토콜입니다. TCP(Transport Control Protocol)와 IP(Internet Protocol)로 구성된 두 부분으로 구성된 프로토콜입니다.

전송 제어 프로토콜(TCP)은 데이터가 올바르고 올바른 순서로 전달되도록 하는 역할을 합니다. 두 대의 컴퓨터 사이에 연결을 설정한 다음 데이터를 작은 패킷으로 전송하여 이를 수행합니다. 그런 다음 패킷은 목적지에서 올바른 순서로 재조립됩니다.

인터넷 프로토콜(IP)은 소스에서 대상으로 데이터 패킷을 라우팅하는 역할을 합니다. 이는 라우팅 테이블로 알려진 일련의 규칙을 사용하여 수행합니다.

Java 플랫폼의 네트워킹 API에는 네트워크 프로그래밍에 필요한 저수준 기능을 제공하는 일련의 클래스 및 인터페이스가 포함되어 있습니다. java.net 패키지에는 핵심 네트워킹 클래스와 인터페이스가 포함되어 있습니다. javax.net 패키지에는 핵심 네트워킹 클래스 및 인터페이스에 대한 확장이 포함되어 있습니다.

java.net.URL 클래스는 Java 플랫폼의 네트워킹 API에 대한 게이트웨이입니다. 인터넷에서 리소스를 식별하는 방법인 Uniform Resource Locator를 나타냅니다. 리소스는 웹 페이지, 이미지, 파일 또는 URL로 식별할 수 있는 모든 것이 될 수 있습니다.

java.net.URL 클래스에는 데이터를 읽고 URL에 쓰는 여러 메서드가 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getContent()
- openConnection()
- 오픈스트림()
- getInputStream()

getContent() 메서드는 URL의 내용을 나타내는 객체를 반환합니다. openConnection() 메서드는 URL에 대한 연결을 나타내는 URLConnection 객체를 반환합니다. openStream() 메서드는 URL에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다. getInputStream() 메서드는 URL에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다.

java.net.URLConnection 클래스는 URL에 대한 연결을 나타냅니다. 연결을 열고 URL에서 데이터를 읽는 데 사용할 수 있습니다. URLConnection 클래스에는 데이터를 읽고 URL에 쓰는 여러 메서드가 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getContent()
- getInputStream()
- getOutputStream()
- setDoInput()
- setDoOutput()
- 연결하다()

getContent() 메서드는 URL의 내용을 나타내는 객체를 반환합니다. getInputStream() 메서드는 URL에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다. getOutputStream() 메서드는 URL에 데이터를 쓰는 데 사용할 수 있는 OutputStream을 반환합니다. setDoInput() 메서드는 입력에 URLConnection을 사용해야 하는지 여부를 설정합니다. setDoOutput() 메서드는 출력에 URLConnection을 사용해야 하는지 여부를 설정합니다. connect() 메서드는 URL에 대한 연결을 엽니다.

java.net.Socket 클래스는 두 컴퓨터 간의 통신 끝점인 소켓을 나타냅니다. 소켓은 데이터를 읽고 쓰는 데 모두 사용할 수 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getInputStream()
- getOutputStream()
- 닫다()

getInputStream() 메서드는 Socket에서 데이터를 읽는 데 사용할 수 있는 InputStream을 반환합니다. getOutputStream() 메서드는 Socket에 데이터를 쓰는 데 사용할 수 있는 OutputStream을 반환합니다. close() 메서드는 소켓을 닫습니다.

java.net.ServerSocket 클래스는 서버의 통신 끝점인 서버 소켓을 나타냅니다. ServerSocket을 사용하여 클라이언트에서 들어오는 연결을 수락할 수 있습니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- 동의하기()
- 닫다()

accept() 메서드는 클라이언트에서 들어오는 연결을 수락합니다. close() 메서드는 ServerSocket을 닫습니다.

java.net.DatagramSocket 클래스는 데이터그램을 송수신하기 위한 통신 끝점인 데이터그램 소켓을 나타냅니다. 데이터그램은 오래 지속되는 연결 없이 보낼 수 있는 작고 독립적인 메시지입니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- 보내다()
- 받다()
- 닫다()

send() 메서드는 데이터그램을 보냅니다. receive() 메소드는 데이터그램을 수신합니다. close() 메서드는 DatagramSocket을 닫습니다.

java.net.DatagramPacket 클래스는 오래 지속되는 연결을 요구하지 않고 보낼 수 있는 작고 독립적인 메시지인 데이터그램 패킷을 나타냅니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

- getData()
- getLength()
- getAddress()
- getPort()

getData() 메서드는 패킷에 포함된 데이터를 반환합니다. getLength() 메서드는 패킷에 포함된 데이터의 길이를 반환합니다. getAddress() 메서드는 보낸 사람의 주소를 반환합니다. getPort() 메서드는 보낸 사람의 포트를 반환합니다.

Java 프로그래밍에는 항상 강력한 네트워킹 구성 요소가 있습니다. 데스크톱에서 웹, 모바일에 이르기까지 광범위한 응용 프로그램을 개발하는 데 사용할 수 있는 다재다능한 언어입니다. Java 플랫폼에는 네트워크 프로그래밍에 필요한 모든 기능을 제공하는 네트워킹 클래스 및 인터페이스의 광범위한 라이브러리가 있습니다.

이 기사에서는 Java 네트워킹 API와 이를 사용하여 구현할 수 있는 몇 가지 일반적인 네트워킹 시나리오를 살펴보았습니다. 또한 사용 가능한 몇 가지 고급 기능도 살펴보았습니다.