---
title: VPN(가상 사설망)을 만드는 방법
description: 
published: true
date: 2023-01-31T07:23:47.490Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:57:45.096Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [How to Create a Virtual Private Network (VPN)***English** version of this document is available*](/en/Knowledge-base/Common/how-to-create-a-virtual-private-network-vpn)
{.links-list}

# VPN(가상 사설망)을 만드는 방법

VPN(가상 사설망)은 기기와 인터넷 사이에 암호화된 비공개 터널을 생성합니다. 이를 통해 개인적이고 안전하게 웹을 탐색하고 IP 주소를 숨기고 스니퍼와 해커로부터 데이터를 보호할 수 있습니다.

## 왜 VPN을 사용해야 할까요?

다음을 포함하여 VPN을 사용하는 데는 여러 가지 이유가 있습니다.

- **프라이버시:** VPN은 데이터를 암호화하고 IP 주소를 숨김으로써 정부 기관, ISP 및 기타 제3자가 인터넷 활동을 모니터링하는 것을 방지합니다.

- **보안:** VPN은 트래픽을 암호화하여 해커가 데이터를 가로채기 어렵습니다. 이는 공용 Wi-Fi 네트워크를 사용할 때 특히 중요합니다.

- **접근성:** VPN은 검열 및 제한을 우회하여 해당 국가에서 사용할 수 없는 웹사이트 및 콘텐츠에 액세스할 수 있습니다.

## VPN 설정 방법

VPN을 설정하는 방법에는 여러 가지가 있지만 가장 널리 사용되는 두 가지 방법인 VPN 서비스 사용 또는 VPN 서버 설정에 중점을 둘 것입니다.

### VPN 서비스

VPN 서비스는 다른 국가의 서버를 통해 트래픽을 암호화하고 라우팅하는 구독 기반 서비스입니다. 계정에 가입하고 VPN 소프트웨어를 설치하기만 하면 되므로 VPN을 설정하는 가장 간단한 방법입니다.

선택할 수 있는 VPN 서비스가 많으며 강력한 보안 기능을 갖춘 평판이 좋은 서비스를 선택하는 것이 중요합니다. 최고의 VPN 서비스는 다음과 같습니다.

- [ExpressVPN](https://www.expressvpn.com)
- [NordVPN](https://nordvpn.com)
- [사이버고스트](https://www.cyberghostvpn.com)
- [서프샤크](https://surfshark.com)

서비스를 사용하여 VPN을 설정하려면 계정에 가입하고 VPN 소프트웨어를 설치하기만 하면 됩니다. 소프트웨어가 설치되면 소프트웨어를 열고 계정 정보로 로그인하십시오. 서버 위치를 선택하고 '연결'을 클릭합니다. 이제 트래픽이 암호화되어 선택한 서버를 통해 라우팅됩니다.

### VPN 서버

VPN을 더 잘 제어하려면 자체 VPN 서버를 설정할 수 있습니다. 이것은 VPN 서비스를 사용하는 것보다 더 많은 노력이 필요하지만 서버를 사용자 지정하고 자체 보안 기능을 선택할 수 있는 기능을 제공합니다.

VPN 서버 설정을 위한 많은 소프트웨어 옵션이 있지만 [OpenVPN](https://openvpn.net)에 중점을 둘 것입니다. OpenVPN은 대부분의 운영 체제와 호환되는 무료 오픈 소스 소프트웨어입니다.

OpenVPN 서버를 설정하려면 먼저 서버에 [OpenVPN 소프트웨어를 설치](https://openvpn.net/community-downloads/)해야 합니다. 소프트웨어가 설치되면 [보안 키](https://openvpn.net/how-to/tutorials/what-is-an-ssl-vpn/)를 생성해야 합니다. 이 키는 트래픽을 암호화하는 데 사용됩니다.

다음으로 [서버를 구성](https://openvpn.net/community-downloads/)하고 [방화벽을 설정](https://openvpn.net/vpn-server-resources/setting-up해야 합니다. -a-firewall-for-a-vpn-server/) VPN 연결을 허용합니다. 마지막으로 서버에 연결할 각 클라이언트에 대해 [구성 파일을 생성](https://openvpn.net/community-downloads/)해야 합니다.

서버가 설정되면 클라이언트는 [OpenVPN 소프트웨어 설치](https://openvpn.net/community-downloads/) 및 [구성 파일 가져오기](https://openvpn.net/vpn- server-resources/importing-a-package-file-into-the-client/).

##VPN 프로토콜

다양한 VPN 프로토콜은 다양한 수준의 보안 및 개인 정보 보호를 제공합니다. 가장 일반적인 프로토콜은 다음과 같습니다.

- **OpenVPN:** OpenVPN은 가장 강력한 암호화 알고리즘을 사용하는 무료 오픈 소스 프로토콜입니다. 가장 안전한 VPN 프로토콜로 간주됩니다.

- **IKEv2:** IKEv2는 모바일 장치에서 자주 사용되는 빠르고 안전한 프로토콜입니다. 가장 강력한 암호화 알고리즘을 사용하며 매우 안전한 것으로 간주됩니다.

- ** PPTP:** PPTP는 OpenVPN 또는 IKEv2만큼 안전하지 않은 오래된 프로토콜입니다. 그러나 빠르고 쉽게 설정할 수 있어 경험이 없는 사용자에게 적합한 옵션입니다.

## 결론

VPN은 온라인에서 개인 정보와 보안을 보호하는 강력한 도구입니다. VPN은 트래픽을 암호화하고 IP 주소를 숨김으로써 정부 기관, ISP 및 기타 제3자가 인터넷 활동을 모니터링하는 것을 방지합니다. VPN은 또한 검열 및 제한을 우회하여 해당 국가에서 사용할 수 없는 웹 사이트 및 콘텐츠에 액세스할 수 있습니다.

VPN을 설정하는 방법에는 여러 가지가 있지만 가장 일반적인 방법은 VPN 서비스를 사용하거나 VPN 서버를 설정하는 것입니다. VPN 서비스는 VPN을 설정하는 가장 간단한 방법입니다. 계정에 가입하고 VPN 소프트웨어를 설치하기만 하면 됩니다. 그러나 VPN을 더 잘 제어하려면 자체 VPN 서버를 설정할 수 있습니다. 이것은 VPN 서비스를 사용하는 것보다 더 많은 노력이 필요하지만 서버를 사용자 지정하고 자체 보안 기능을 선택할 수 있는 기능을 제공합니다.

다양한 VPN 프로토콜은 다양한 수준의 보안 및 개인 정보 보호를 제공합니다. 가장 일반적인 프로토콜은 OpenVPN, IKEv2 및 PPTP입니다. OpenVPN은 가장 안전한 프로토콜이지만 설정하기가 가장 어렵습니다. IKEv2는 모바일 장치에서 자주 사용되는 빠르고 안전한 프로토콜입니다. PPTP는 OpenVPN 또는 IKEv2만큼 안전하지는 않지만 빠르고 쉽게 설정할 수 있는 오래된 프로토콜입니다.

자원:

- https://www.expressvpn.com
- https://nordvpn.com
- https://www.cyberghostvpn.com
- https://surfshark.com
- https://openvpn.net
- https://openvpn.net/community-downloads/
- https://openvpn.net/how-to/tutorials/what-is-an-ssl-vpn/
- https://openvpn.net/vpn-server-resources/setting-up-a-firewall-for-a-vpn-server/
- https://openvpn.net/community-downloads/
- https://openvpn.net/vpn-server-resources/importing-a-package-file-into-the-client/