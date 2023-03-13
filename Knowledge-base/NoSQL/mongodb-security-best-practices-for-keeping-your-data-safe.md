---
title: MongoDB 보안: 데이터를 안전하게 유지하기 위한 모범 사례
description: 
published: true
date: 2023-03-13T02:32:40.919Z
tags: 
editor: markdown
dateCreated: 2023-03-13T02:32:40.919Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Security: Best Practices for Keeping Your Data Safe***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-security-best-practices-for-keeping-your-data-safe)
{.links-list}

MongoDB 보안: 데이터를 안전하게 유지하기 위한 모범 사례

MongoDB는 확장성과 유연성으로 인해 많은 조직에서 널리 사용되는 NoSQL 데이터베이스입니다. 그러나 다른 데이터베이스와 마찬가지로 보안 위협에 취약합니다. 이 문서에서는 MongoDB 데이터베이스를 안전하게 유지하기 위한 모범 사례를 살펴봅니다.

### 강력한 인증 사용

인증은 사용자 또는 시스템의 ID를 확인하는 프로세스입니다. MongoDB는 다음을 포함한 여러 인증 메커니즘을 지원합니다.

- SCRAM: 보안 챌린지-응답 인증 메커니즘
- X.509: 디지털 인증서 생성을 위한 프로토콜
- LDAP: 경량 디렉터리 액세스 프로토콜

인증을 구성할 때 강력한 사용자 이름과 암호를 사용하고 기본 자격 증명을 사용하지 않는 것이 중요합니다.

```{javascript}
db.createUser({
  user: "admin",
  pwd: "strongpassword",
  roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
})
```

위의 예에서는 강력한 암호를 사용하여 "admin"이라는 사용자를 생성하고 사용자가 모든 데이터베이스의 사용자를 관리할 수 있는 "userAdminAnyDatabase" 역할을 할당합니다.

### 네트워크 노출 제한

최소 권한 원칙은 필요한 시스템에만 네트워크 노출을 제한할 것을 권장합니다. 기본적으로 MongoDB는 보안 위험이 될 수 있는 모든 네트워크 인터페이스에서 수신 대기합니다. 대신 특정 IP 주소 또는 네트워크 인터페이스에서 수신 대기하도록 MongoDB를 구성하십시오.

```{javascript}
# mongod.conf
net:
  port: 27017
  bindIp: 127.0.0.1
```

위의 예에서는 포트 27017의 루프백 네트워크 인터페이스(127.0.0.1)에서만 수신 대기하도록 MongoDB를 구성합니다.

### 통신 암호화

MongoDB 클라이언트와 서버 간의 통신을 암호화하면 도청 및 변조를 방지할 수 있습니다. MongoDB는 클라이언트와 서버 간의 연결을 위해 TLS(전송 계층 보안) 암호화를 지원합니다.

```{javascript}
# mongod.conf
net:
  port: 27017
  bindIp: 127.0.0.1
  tls:
    mode: requireTLS
    certificateKeyFile: /path/to/server.pem
    CAFile: /path/to/ca.pem
```

위의 예에서는 서버 인증서 및 인증 기관(CA) 파일을 사용하여 TLS 암호화를 요구하도록 MongoDB를 구성합니다.

### 역할 기반 액세스 제어 시행

RBAC(역할 기반 액세스 제어)는 ID가 아닌 역할을 기반으로 사용자에게 권한을 부여하는 프로세스입니다. MongoDB는 역할 및 권한을 통해 RBAC를 지원합니다.

```{javascript}
# Create a role with read-only access to a specific database
db.createRole({
  role: "readOnly",
  privileges: [
    { resource: { db: "mydatabase", collection: "" }, actions: [ "find" ] }
  ],
  roles: []
})

# Create a user and assign the read-only role
db.createUser({
  user: "reader",
  pwd: "strongpassword",
  roles: [ { role: "readOnly", db: "mydatabase" } ]
})
```

위의 예에서는 사용자가 "mydatabase" 데이터베이스에서 문서를 찾을 수 있도록 허용하는 "readOnly" 역할과 "readOnly" 역할을 가진 "reader"라는 사용자를 만듭니다.

### 감사 구현

감사는 데이터베이스 활동을 기록하고 검토하는 프로세스입니다. MongoDB는 감사 로그를 통한 감사를 지원합니다.

```{javascript}
# mongod.conf
security:
  authorization: enabled
  auditLog:
    destination: file
    path: /var/log/mongodb/audit.log
    format: JSON
```

위의 예에서는 JSON 형식의 파일에 대한 권한 부여 및 감사 로깅을 활성화하도록 MongoDB를 구성합니다.

### MongoDB를 최신 상태로 유지

마지막으로 최신 보안 패치 및 업데이트로 MongoDB를 최신 상태로 유지하는 것이 중요합니다. MongoDB는 정기적으로 보안 패치 및 업데이트를 릴리스합니다. MongoDB를 최신 상태로 유지하면 알려진 취약점으로부터 보호할 수 있습니다.

### 외부 리소스

- [MongoDB 보안 체크리스트](https://docs.mongodb.com/manual/administration/security-checklist/)
- [MongoDB 보안 아키텍처](https://www.mongodb.com/security/architecture)
- [MongoDB 보안 강화](https://www.virtuesecurity.com/hardening-mongodb-security/)

이러한 모범 사례를 따르면 MongoDB 데이터베이스를 안전하게 유지하고 잠재적인 보안 위협으로부터 보호할 수 있습니다.