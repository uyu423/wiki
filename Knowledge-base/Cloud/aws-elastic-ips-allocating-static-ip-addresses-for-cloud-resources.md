---
title: AWS 탄력적 IP: 클라우드 리소스에 고정 IP 주소 할당
description: 
published: true
date: 2023-02-06T19:17:38.128Z
tags: 
editor: markdown
dateCreated: 2023-02-06T19:17:36.383Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Elastic IPs: Allocating Static IP Addresses for Cloud Resources***English** document is available*](/en/Knowledge-base/Cloud/aws-elastic-ips-allocating-static-ip-addresses-for-cloud-resources)
{.links-list}


# AWS 탄력적 IP: 클라우드 리소스에 대한 고정 IP 주소 할당

탄력적 IP 주소는 동적 클라우드 컴퓨팅을 위해 설계된 고정 IP 주소입니다. 탄력적 IP 주소는 AWS 계정과 연결됩니다. 탄력적 IP 주소를 사용하면 주소를 계정의 다른 인스턴스에 빠르게 다시 매핑하여 인스턴스 또는 소프트웨어의 장애를 숨길 수 있습니다.

탄력적 IP 주소는 인스턴스 또는 네트워크 인터페이스에 할당할 수 있는 퍼블릭 IP 주소입니다. 탄력적 IP 주소를 이미 퍼블릭 IP 주소가 있는 인스턴스와 연결하면 인스턴스의 원래 퍼블릭 IP 주소가 탄력적 IP 주소로 대체됩니다. 탄력적 IP 주소를 네트워크 인터페이스와 연결하면 IP 주소가 네트워크 인터페이스의 기본 프라이빗 IP 주소와 연결됩니다.

Amazon EC2 콘솔을 사용하여 인스턴스를 생성하는 동안 새로운 탄력적 IP 주소를 할당할 수 있습니다. 기존 탄력적 IP 주소 풀에서 새 탄력적 IP 주소를 할당할 수도 있습니다. 언제든지 탄력적 IP 주소를 인스턴스 또는 네트워크 인터페이스와 연결할 수 있습니다.

인스턴스에서 탄력적 IP 주소의 연결을 해제하면 퍼블릭 IP 주소의 Amazon EC2 풀에서 인스턴스에 새 퍼블릭 IP 주소가 할당됩니다. 네트워크 인터페이스에서 탄력적 IP 주소의 연결을 해제하면 네트워크 인터페이스의 기본 프라이빗 IP 주소가 탄력적 IP 주소에서 서브넷의 IP 주소 풀에 있는 다른 프라이빗 IP 주소로 다시 할당됩니다.

## 탄력적 IP 주소 할당

Amazon EC2 콘솔을 사용하여 탄력적 IP 주소를 할당하려면

1. https://console.aws.amazon.com/ec2/에서 Amazon EC2 콘솔을 엽니다.

2. 탐색 창에서 **Elastic IPs**를 선택합니다.

3. **새 주소 할당**을 선택합니다.

4. **할당**을 선택합니다.

5. **닫기**를 선택합니다.

이제 탄력적 IP 주소가 할당되었으며 인스턴스 또는 네트워크 인터페이스와 연결할 준비가 되었습니다.

## 탄력적 IP 주소를 인스턴스와 연결

Amazon EC2 콘솔을 사용하여 탄력적 IP 주소를 인스턴스와 연결하려면

1. https://console.aws.amazon.com/ec2/에서 Amazon EC2 콘솔을 엽니다.

2. 인스턴스 목록에서 인스턴스를 선택합니다.

3. **작업**, **네트워킹**, **탄력적 IP 주소 변경**, **탄력적 IP 주소 연결**을 선택합니다.

4. 목록에서 탄력적 IP 주소를 선택한 다음 **연결**을 선택합니다.

이제 인스턴스가 탄력적 IP 주소와 연결됩니다.

## 탄력적 IP 주소를 네트워크 인터페이스와 연결

Amazon EC2 콘솔을 사용하여 탄력적 IP 주소를 네트워크 인터페이스와 연결하려면

1. https://console.aws.amazon.com/ec2/에서 Amazon EC2 콘솔을 엽니다.

2. 탐색 창에서 **네트워크 인터페이스**를 선택합니다.

3. 네트워크 인터페이스를 선택한 다음 **Action**, **Networking**, **Change Elastic IP Address**, **Associate Elastic IP Address**를 선택합니다.

4. 목록에서 탄력적 IP 주소를 선택한 다음 **연결**을 선택합니다.

이제 네트워크 인터페이스가 탄력적 IP 주소와 연결됩니다.

## 탄력적 IP 주소 연결 해제

Amazon EC2 콘솔을 사용하여 인스턴스 또는 네트워크 인터페이스에서 탄력적 IP 주소의 연결을 해제하려면

1. https://console.aws.amazon.com/ec2/에서 Amazon EC2 콘솔을 엽니다.

2. 탐색 창에서 **Elastic IPs**를 선택합니다.

3. 연결 해제하려는 탄력적 IP 주소 옆의 확인란을 선택합니다.

4. **작업**, **네트워킹**, **탄력적 IP 주소 변경**, **탄력적 IP 주소 연결 해제**를 선택합니다.

5. 확인 메시지가 표시되면 **예, 연결 해제**를 선택합니다.

탄력적 IP 주소는 이제 인스턴스 또는 네트워크 인터페이스에서 분리됩니다.

## 탄력적 IP 주소 해제

더 이상 필요하지 않으면 탄력적 IP 주소를 해제할 수 있습니다. Amazon EC2 콘솔을 사용하여 탄력적 IP 주소를 해제하려면

1. https://console.aws.amazon.com/ec2/에서 Amazon EC2 콘솔을 엽니다.

2. 탐색 창에서 **Elastic IPs**를 선택합니다.

3. 해제하려는 탄력적 IP 주소 옆의 확인란을 선택합니다.

4. **작업**, **네트워킹**, **탄력적 IP 주소 변경**, **탄력적 IP 주소 해제**를 선택합니다.

5. 확인 메시지가 나타나면 **Yes, Release**를 선택합니다.

이제 탄력적 IP 주소가 해제되고 더 이상 AWS 계정과 연결되지 않습니다.

## 추가 정보

탄력적 IP 주소에 대한 자세한 내용은 다음을 참조하십시오.

- Linux 인스턴스용 Amazon EC2 사용 설명서의 탄력적 IP 주소
- Windows 인스턴스용 Amazon EC2 사용 설명서의 탄력적 IP 주소

## 외부 리소스

- Amazon EC2: 탄력적 IP 주소(EIP)
- AWS IP 주소 계획
- AWS 탄력적 IP 사용 방법