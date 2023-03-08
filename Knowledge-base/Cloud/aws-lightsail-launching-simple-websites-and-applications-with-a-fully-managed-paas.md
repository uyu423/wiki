---
title: AWS Lightsail: 완전 관리형 PaaS로 간단한 웹사이트 및 애플리케이션 시작
description: 
published: true
date: 2023-02-06T11:56:00.514Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:55:58.658Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Lightsail: Launching Simple Websites and Applications with a Fully Managed PaaS***English** document is available*](/en/Knowledge-base/Cloud/aws-lightsail-launching-simple-websites-and-applications-with-a-fully-managed-paas)
{.links-list}


# AWS Lightsail: 완전 관리형 PaaS로 간단한 웹사이트 및 애플리케이션 시작

AWS Lightsail은 간단한 웹 사이트 및 애플리케이션을 쉽게 시작할 수 있게 해주는 완전관리형 PaaS(Platform as a Service)입니다. Lightsail에는 가상 사설 서버, 관리형 데이터베이스, DNS 관리 및 고정 IP 주소를 포함하여 프로젝트를 시작하는 데 필요한 모든 것이 포함되어 있습니다.

Lightsail은 사용하기 쉽고 사용한 리소스에 대해서만 요금을 지불하기 때문에 간단한 웹 사이트 및 애플리케이션을 시작하는 데 적합합니다. 선불 비용이나 장기 계약이 없습니다. 몇 분 만에 Lightsail 인스턴스를 생성하고 프로젝트 성장에 따라 리소스를 확장할 수 있습니다.

## Lightsail 시작하기

Lightsail을 시작하려면 먼저 계정을 만들고 리전을 선택해야 합니다. https://lightsail.aws.amazon.com/에서 계정을 생성할 수 있습니다.

계정을 생성하면 Lightsail 인스턴스를 생성할 수 있습니다. 이렇게 하려면 "인스턴스 생성" 버튼을 클릭하고 인스턴스 유형을 선택합니다. Lightsail은 Linux 및 Windows 가상 사설 서버, 컨테이너, 고정 IP 주소를 비롯한 다양한 인스턴스 유형을 제공합니다.

인스턴스 유형을 선택했으면 인스턴스 계획을 선택할 수 있습니다. Lightsail은 월별 및 시간별 플랜을 포함하여 다양한 플랜을 제공합니다.

인스턴스 계획을 선택한 후 인스턴스에 대한 운영 체제, 애플리케이션 및 추가 리소스를 선택할 수 있습니다. Lightsail은 Amazon Linux, Ubuntu 및 Windows Server를 포함하여 널리 사용되는 다양한 운영 체제를 제공합니다.

WordPress, Drupal, Joomla! 및 Magento와 같은 인스턴스에 대한 애플리케이션 및 추가 리소스를 선택할 수도 있습니다.

인스턴스에 대한 운영 체제, 애플리케이션 및 추가 리소스를 선택했으면 인스턴스 이름을 선택하고 "인스턴스 생성" 버튼을 클릭할 수 있습니다.

이제 Lightsail 인스턴스가 생성되고 Lightsail 콘솔을 통해 액세스할 수 있습니다.

## Lightsail 인스턴스에 연결

Lightsail 인스턴스에 연결하려면 먼저 Lightsail 클라이언트를 다운로드해야 합니다. Lightsail 클라이언트는 Lightsail 리소스를 관리하는 데 사용할 수 있는 명령줄 인터페이스(CLI)입니다.

Lightsail 콘솔에서 Lightsail 클라이언트를 다운로드할 수 있습니다. 이렇게 하려면 "계정" 메뉴를 클릭하고 "클라이언트 다운로드"를 선택합니다.

Lightsail 클라이언트를 다운로드했으면 다음 명령을 사용하여 Lightsail 인스턴스에 연결할 수 있습니다.

```
lightsail-client connect --instance-name my-instance
```

"my-instance"를 Lightsail 인스턴스의 이름으로 바꿉니다.

이제 Lightsail 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다. 자격 증명을 입력하면 Lightsail 인스턴스에 연결됩니다.

## Lightsail 인스턴스 관리

Lightsail 인스턴스에 연결되면 Lightsail 클라이언트를 사용하여 인스턴스를 관리할 수 있습니다.

사용 가능한 모든 명령 목록을 보려면 "help" 명령을 사용할 수 있습니다.

```
lightsail-client help
```

특정 명령에 대한 정보를 보려면 "help" 명령 다음에 명령 이름을 사용할 수 있습니다. 예를 들어 "connect" 명령에 대한 정보를 보려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client help connect
```

계정의 모든 Lightsail 인스턴스 목록을 보려면 "list-instances" 명령을 사용할 수 있습니다.

```
lightsail-client list-instances
```

특정 Lightsail 인스턴스에 대한 정보를 보려면 "describe-instance" 명령 뒤에 인스턴스 이름을 사용할 수 있습니다. 예를 들어 "my-instance" Lightsail 인스턴스에 대한 정보를 보려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client describe-instance --instance-name my-instance
```

Lightsail 인스턴스를 중지하려면 인스턴스 이름 뒤에 "stop-instance" 명령을 사용할 수 있습니다. 예를 들어 "my-instance" Lightsail 인스턴스를 중지하려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client stop-instance --instance-name my-instance
```

Lightsail 인스턴스를 시작하려면 "start-instance" 명령 다음에 인스턴스 이름을 사용할 수 있습니다. 예를 들어 "my-instance" Lightsail 인스턴스를 시작하려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client start-instance --instance-name my-instance
```

Lightsail 인스턴스를 삭제하려면 "delete-instance" 명령 다음에 인스턴스 이름을 사용할 수 있습니다. 예를 들어 "my-instance" Lightsail 인스턴스를 삭제하려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client delete-instance --instance-name my-instance
```

## Lightsail 스냅샷 생성

Lightsail 스냅샷은 Lightsail 인스턴스의 특정 시점 백업입니다. 스냅샷을 사용하여 새 Lightsail 인스턴스를 생성하거나 기존 Lightsail 인스턴스를 복원할 수 있습니다.

Lightsail 인스턴스의 스냅샷을 생성하려면 "create-snapshot" 명령 뒤에 인스턴스 이름을 사용할 수 있습니다. 예를 들어 "my-instance" Lightsail 인스턴스의 스냅샷을 생성하려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client create-snapshot --instance-name my-instance
```

계정의 모든 스냅샷 목록을 보려면 "list-snapshots" 명령을 사용할 수 있습니다.

```
lightsail-client list-snapshots
```

특정 스냅샷에 대한 정보를 보려면 "describe-snapshot" 명령 다음에 스냅샷 이름을 사용할 수 있습니다. 예를 들어 "my-snapshot" 스냅샷에 대한 정보를 보려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client describe-snapshot --snapshot-name my-snapshot
```

스냅샷을 삭제하려면 "delete-snapshot" 명령 뒤에 스냅샷 이름을 입력하면 됩니다. 예를 들어 "my-snapshot" 스냅샷을 삭제하려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client delete-snapshot --snapshot-name my-snapshot
```

## 스냅샷에서 Lightsail 인스턴스 생성

스냅샷에서 Lightsail 인스턴스를 생성하려면 "create-instance-from-snapshot" 명령 다음에 스냅샷 이름을 사용할 수 있습니다. 예를 들어 "my-snapshot" 스냅샷에서 Lightsail 인스턴스를 생성하려면 다음 명령을 사용할 수 있습니다.

```
lightsail-client create-instance-from-snapshot --snapshot-name my-snapshot
```

## 결론

이 기사에서는 AWS Lightsail을 사용하여 간단한 웹 사이트 및 애플리케이션을 시작하는 방법을 살펴보았습니다. Lightsail은 사용하기 쉽고 사용한 리소스에 대해서만 요금을 지불하기 때문에 간단한 웹 사이트 및 애플리케이션을 시작하는 데 적합합니다.

다음 프로젝트를 시작하기 위해 완전관리형 PaaS를 찾고 있다면 Lightsail이 탁월한 선택입니다.