---
title: OWASP Top 10으로 보안 웹 애플리케이션을 구축하는 방법
description: 
published: true
date: 2023-02-27T06:32:38.981Z
tags: 
editor: markdown
dateCreated: 2023-02-27T06:32:37.588Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Secure Web Application with OWASP Top 10***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-secure-web-application-with-owasp-top-10)
{.links-list}


# OWASP Top 10으로 보안 웹 애플리케이션을 구축하는 방법

OWASP(Open Web Application Security Project) Top 10은 웹에서 가장 일반적인 공격을 분류한 것입니다. 2004년 처음 출시된 이후 몇 년마다 업데이트되었으며 가장 최신 버전은 2017년에 출시되었습니다.

이름에도 불구하고 OWASP Top 10은 가장 일반적인 10가지 공격 목록이 아닙니다. 오히려 웹 애플리케이션 개발자가 알아야 하는 보안 위험의 우선 순위 목록입니다. 이 목록은 개발자가 보다 안전한 애플리케이션을 구축하는 데 도움이 되는 가이드로 사용하기 위한 것입니다.

## 주사

인젝션 결함으로 인해 공격자는 백엔드 데이터베이스에서 악의적인 SQL 쿼리 또는 코드를 실행할 수 있습니다. 이를 사용하여 데이터를 삭제 또는 수정하거나 민감한 정보에 액세스할 수도 있습니다.

인젝션 결함을 방지하기 위해 개발자는 다음을 수행해야 합니다.

- 사용자 입력을 SQL 쿼리에 연결하는 대신 매개변수화된 쿼리 사용
- 저장 프로시저 사용
- 사용자 입력에서 특수 문자를 이스케이프 처리합니다.

## 손상된 인증 및 세션 관리

손상된 인증 및 세션 관리 결함으로 인해 공격자는 액세스해서는 안 되는 리소스나 데이터에 액세스할 수 있습니다. 이는 쿠키, 세션 ID를 훔치거나 기본 또는 쉽게 추측할 수 있는 암호를 사용하여 수행할 수 있습니다.

손상된 인증 및 세션 관리 결함을 방지하려면 개발자는 다음을 수행해야 합니다.

- 강력한 암호 및 암호 정책 사용
- 이중 인증 사용
- 세션 시간 초과 사용
- 로그아웃 후 세션 ID 무효화
- SSL/TLS 사용

## 교차 사이트 스크립팅(XSS)

XSS(교차 사이트 스크립팅) 결함을 통해 공격자는 악성 코드를 웹 페이지에 삽입할 수 있으며, 페이지를 방문하는 순진한 사용자에 의해 실행됩니다. 이는 암호 및 쿠키와 같은 정보를 도용하거나 사용자를 악성 사이트로 리디렉션하는 데 사용할 수 있습니다.

XSS 결함을 방지하려면 개발자는 다음을 수행해야 합니다.

- 사용자 입력에서 특수 문자를 이스케이프 처리합니다.
- 웹 애플리케이션 방화벽(WAF) 사용

## 손상된 액세스 제어

손상된 액세스 제어 결함으로 인해 권한이 없는 사용자가 액세스해서는 안 되는 데이터에 액세스하거나 수정할 수 있습니다. 이는 인증 또는 승인 확인을 우회하거나 URL을 변경하여 제한된 리소스에 액세스함으로써 수행할 수 있습니다.

손상된 액세스 제어 결함을 방지하려면 개발자는 다음을 수행해야 합니다.

- 적절한 인증 및 승인 제어 사용
- 최소 권한 원칙 사용
- 와일드카드 권한 사용 금지

## 보안 구성 오류

잘못된 보안 구성은 웹 응용 프로그램이 제대로 구성되지 않은 경우 발생하는 광범위한 범주의 결함입니다. 여기에는 기본 구성을 그대로 두거나 서버와 응용 프로그램을 공개하거나 파일 권한을 적절하게 설정하지 않는 것이 포함될 수 있습니다.

잘못된 보안 구성 결함을 방지하기 위해 개발자는 다음을 수행해야 합니다.

- 웹 애플리케이션 보안을 위한 모범 사례를 따릅니다.
- 웹 애플리케이션 방화벽(WAF) 사용
- 서버 구성 강화

## 안전하지 않은 암호화 저장소

안전하지 않은 암호화 저장소 결함은 암호 및 신용 카드 번호와 같은 민감한 데이터가 제대로 암호화되지 않을 때 발생합니다. 이로 인해 데이터베이스가 침해될 경우 데이터가 손상될 수 있습니다.

안전하지 않은 암호화 저장소 결함을 방지하려면 개발자는 다음을 수행해야 합니다.

- 강력한 암호화 알고리즘 사용
- 적절한 키 관리 사용

## 불충분한 승인 및 인증

불충분한 권한 부여 및 인증 결함은 웹 애플리케이션이 사용자가 리소스에 액세스하거나 작업을 수행할 수 있는 권한이 있는지 제대로 확인하지 않을 때 발생합니다. 이는 권한을 제대로 확인하지 않거나 쉽게 추측할 수 있는 암호를 사용하여 수행할 수 있습니다.

불충분한 권한 부여 및 인증 결함을 방지하기 위해 개발자는 다음을 수행해야 합니다.

- 강력한 암호 및 암호 정책 사용
- 이중 인증 사용
- 적절한 권한 제어 사용

## 불충분한 암호화

불충분한 암호화 결함은 웹 애플리케이션이 취약한 암호화 알고리즘을 사용하거나 민감한 데이터를 적절하게 암호화하지 않을 때 발생합니다. 이로 인해 데이터베이스가 침해될 경우 데이터가 손상될 수 있습니다.

불충분한 암호화 스토리지 결함을 방지하기 위해 개발자는 다음을 수행해야 합니다.

- 강력한 암호화 알고리즘 사용
- 적절한 키 관리 사용

## 데이터 변조

데이터 변조 결함으로 인해 공격자는 데이터를 수정하거나 데이터를 삭제하거나 가격을 변경하거나 모조품을 장바구니에 추가하는 데 사용할 수 있습니다.

데이터 변조 결함을 방지하기 위해 개발자는 다음을 수행해야 합니다.

- 디지털 서명 사용
- 해시 민감한 데이터
- 적절한 암호화 사용

## 교차 사이트 요청 위조(CSRF)

CSRF(교차 사이트 요청 위조) 결함으로 인해 공격자는 사용자 모르게 또는 동의 없이 사용자를 대신하여 작업을 실행할 수 있습니다. 사용자를 속여 악성 링크를 클릭하거나 악성 웹페이지를 로드하도록 할 수 있습니다.

CSRF 결함을 방지하기 위해 개발자는 다음을 수행해야 합니다.

- 적절한 인증 및 승인 제어 사용
- CSRF 토큰 사용
- 동일 사이트 쿠키 사용

## 외부 리소스

- [https://www.owasp.org/index.php/Top\_10-2017\_Top\_10](https://www.owasp.org/index.php/Top_10-2017_Top_10)
- [https://www.owasp.org/index.php/SQL\_Injection](https://www.owasp.org/index.php/SQL_Injection)
- [https://www.owasp.org/index.php/Broken\_Authentication\_and\_Session\_Management](https://www.owasp.org/index.php/Broken_Authentication_and_Session_Management)
- [https://www.owasp.org/index.php/Cross-Site\_Scripting\_(XSS)](https://www.owasp.org/index.php/Cross-Site_Scripting_(XSS))
- [https://www.owasp.org/index.php/Broken\_Access\_Controls](https://www.owasp.org/index.php/Broken_Access_Controls)
- [https://www.owasp.org/index.php/Security\_Misconfiguration](https://www.owasp.org/index.php/Security_Misconfiguration)
- [https://www.owasp.org/index.php/부족\_Authorization\_and\_Authentication](https://www.owasp.org/index.php/Insufficient_Authorization_and_Authentication)
- [https://www.owasp.org/index.php/ Insufficient\_Cryptography](https://www.owasp.org/index.php/Insufficient_Cryptography)
- [https://www.owasp.org/index.php/Tampering\_with\_Data](https://www.owasp.org/index.php/Tampering_with_Data)
- [https://www.owasp.org/index.php/Cross-Site\_Request\_Forgery\_(CSRF)](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF) )