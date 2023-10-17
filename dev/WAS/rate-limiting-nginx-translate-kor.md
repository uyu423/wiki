---
title: NGINX Rate Limiting (번역)
description: 
published: true
date: 2023-10-17T09:22:15.681Z
tags: nginx
editor: markdown
dateCreated: 2023-10-17T08:56:03.676Z
---

> - 원문 포스트는 [Rate Limiting with NGINX and NGINX Plus](https://www.nginx.com/blog/rate-limiting-nginx/) 입니다.
> - 해당 포스트는 원문을 번역했으며, 개인 적인 추가 주석이 첨부되어 있습니다.

가장 유용하지만 종종 오해되거나 잘못 설정되는 NGINX의 기능 중 하나는 요청 제한(Rate Limiting)입니다. 이 기능을 사용하면 사용자가 주어진 기간 동안 수행할 수 있는 HTTP 요청의 양을 제한할 수 있습니다. 요청은 웹사이트 홈페이지에 대한 GET 요청이나 로그인 양식에 대한 POST 요청과 같이 간단할 수 있습니다.

Rate Limiting은 무차별 암호 대입 공격 속도를 늦추는 등 보안 목적으로 사용할 수 있습니다. 들어오는 요청 속도를 실제 사용자에게 일반적인 값으로 제한하여 [DDoS 공격으로부터 보호](https://www.nginx.com/blog/mitigating-ddos-attacks-with-nginx-and-nginx-plus/)하고 (로깅을 통해) 표적 URL을 식별하는 데 도움이 될 수 있습니다. 보다 일반적으로는 동시에 너무 많은 사용자 요청으로 인해 업스트림 애플리케이션 서버가 과부하되지 않도록 보호하는 데 사용됩니다.

이 블로그에서는 NGINX를 사용한 전송률 제한의 기본 사항과 고급 구성에 대해 다룹니다. Rate Limiting는 NGINX Plus에서도 동일한 방식으로 작동합니다.

NGINX Plus R16 이상은 "글로벌 요청 제한(global rate limiting)"을 지원합니다. 즉, 클러스터의 NGINX Plus 인스턴스는 요청이 클러스터의 어느 인스턴스에 도착하는지에 관계없이 들어오는 요청에 일관된 Rate Limiting을 적용합니다. (클러스터의 상태 공유는 다른 NGINX Plus 기능에도 사용할 수 있습니다.) 자세한 내용은 [블로그](https://www.nginx.com/blog/nginx-plus-r16-released/#r16-cluster-rate-limiting)와 [NGINX Plus 관리자 가이드](https://docs.nginx.com/nginx/admin-guide/high-availability/zone_sync/)를 참조하세요.

# NGINX의 Rate Limiting 방식

NGINX의 rate limiting은 전기통신과 패킷 스위치 컴퓨터 네트워크에서 대역폭이 제한될 때 발생하는 버스트성을 처리하기 위해 널리 사용되는 Leaky Bucket 알고리즘을 사용합니다. 이것은 물이 위에서 부어지고 아래쪽에서 누출되는 양동이에 비유됩니다; 물이 부어지는 속도가 누출되는 속도를 초과하면 양동이는 넘쳐 흐릅니다. 요청 처리 측면에서 봤을 때, 물은 클라이언트로부터의 요청을 나타내고, 양동이는 요청이 선입선출 (FIFO) 스케줄링 알고리즘에 따라 처리를 기다리는 대기열을 나타냅니다. 누출되는 물은 서버에 의해 처리를 위해 버퍼에서 나가는 요청을 나타내며, 넘치는 것은 버려지고 서비스되지 않는 요청을 나타냅니다.

![leaky-bucket-featured-image-300x180.jpg](/leaky-bucket-featured-image-300x180.jpg){.align-center}

> **Leaky Bucket 알고리즘**
> 
> Leaky Bucket 알고리즘은 네트워크 트래픽 제어 및 rate limiting과 같은 서비스에서 초당 특정 요청 수를 제한하는데 널리 사용되는 메커니즘입니다. 이 알고리즘의 작동 방식을 실제 물이 흐르는 양동이로 생각해보면 쉽게 이해할 수 있습니다.
> 
> - **기본 원칙**:
>   - 양동이는 특정 용량으로 제한됩니다.
>   - 물(또는 데이터 패킷)이 일정한 속도로 양동이에 들어옵니다.
>   - 양동이의 하단에는 일정한 크기의 구멍이 있어 물이 지속적으로 흘러나갑니다. 이 구멍을 통해 나오는 물의 속도는 일정합니다.
>   - 양동이가 꽉 차게 되면 더 이상 물을 받아들일 수 없으며, 초과되는 물은 넘쳐 흐르게 됩니다.
> - **Rate Limiting과의 관계**:
>   - 양동이의 용량은 'burst' 또는 '최대 버퍼 크기'로 해석될 수 있습니다.
>   - 구멍을 통해 흘러나가는 물의 속도는 허용된 요청 속도나 데이터 전송률로 해석될 수 있습니다.
>   - 양동이가 넘치면 (즉, 요청이 허용된 속도를 초과하면) 해당 요청은 거부됩니다.
> - **장점 및 한계**:
>   - 장점: Leaky Bucket 알고리즘은 매우 간단하며, 리소스 소비가 크지 않기 때문에 실제 시스템에서 효과적으로 구현할 수 있습니다. 서비스의 오버로드를 방지하고 안정적인 서비스를 제공하는데 도움을 줍니다.
>   - 한계: 일정한 속도로 요청이 들어올 때만 잘 작동하며, 급격한 트래픽 변동에서는 일부 유효한 요청이 거부될 수 있습니다.

# 기본 Rate Limiting 설정하기

Rate Limiting은 주로 `limit_req_zone`과 `limit_req` 두 가지 지시어를 사용하여 설정됩니다. 아래는 그 예시입니다:

```nginx
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

server {
    location /login/ {
        limit_req zone=mylimit;

        proxy_pass http://my_upstream;
    }
}
```

`limit_req_zone` 지시어는 Rate Limiting을 위한 매개변수를 정의하며, `limit_req`는 해당 지시어가 위치한 컨텍스트(예시에서는 /login/로의 모든 요청) 내에서 Rate Limiting을 활성화합니다.

`limit_req_zone` 지시어는 일반적으로 http 블록에서 정의되어 여러 컨텍스트에서 사용할 수 있습니다. 이 지시어는 다음 세 가지 매개변수를 사용합니다:

## Key

제한이 적용되는 요청 특성을 정의합니다. 예시에서는 클라이언트 IP 주소의 이진 표현을 갖는 NGINX 변수 `$binary_remote_addr`을 사용하였습니다. 이는 우리가 각 고유 IP 주소에 대해 세 번째 매개변수에 의해 정의된 요청 속도로 제한한다는 것을 의미합니다. (이 변수는 클라이언트 IP 주소의 문자열 표현인 `$remote_addr`보다 공간을 적게 차지하기 때문에 사용됩니다).

> **limit_req_zone 에서 사용 가능한 Key 변수**
> 
> - `$binary_remote_addr`: 클라이언트의 IP 주소를 바이너리 형태로 표현한 값입니다.
> - `$remote_addr`: 클라이언트의 IP 주소를 텍스트 형태로 표현한 값입니다.
> - `$http_user_agent`: 클라이언트의 User-Agent 헤더를 나타냅니다.
> - `$http_referer`: 클라이언트의 Referer 헤더를 나타냅니다.
> - `$server_addr`: 현재 서버의 IP 주소를 나타냅니다.
> - `$uri`: 요청된 URI를 나타냅니다.
> - `$request_uri`: 클라이언트가 실제로 보낸 요청 URI를 나타냅니다.
> - `$args`: 요청의 쿼리 스트링을 나타냅니다.
> - `$query_string`: $args와 같은 역할을 합니다.
> - `$request_method`: 클라이언트의 요청 메서드를 나타냅니다.
> - `$server_name`: 현재 서버의 이름을 나타냅니다.
> - `$host`: 클라이언트의 요청 헤더의 Host 값을 나타냅니다.

## Zone
각 IP 주소의 상태와 Rate Limiting URL에 얼마나 자주 액세스 되었는지를 저장하는 공유 메모리 영역을 정의합니다. 공유 메모리에서 정보를 유지하면 NGINX 작업 프로세스 간에 정보를 공유할 수 있습니다. 정의는 두 부분으로 이루어집니다. `zone=` 키워드로 식별되는 영역 이름과 콜론(:) 뒤의 `m` 단위의 크기로 구성됩니다. (대략 16,000개의 IP 주소에 대한 상태 정보는 1메가바이트를 차지하므로, 우리의 영역은 대략 160,000개의 주소를 저장할 수 있습니다.)

새 항목을 추가해야 할 때 저장 공간이 모두 소진되면 NGINX는 가장 오래된 항목을 제거합니다. 확보된 공간이 여전히 새 레코드를 수용하기에 충분하지 않으면 NGINX는 상태 코드 503(서비스를 일시적으로 사용할 수 없음)을 반환합니다. 또한 메모리가 고갈되는 것을 방지하기 위해 NGINX는 새 항목을 만들 때마다 이전 60초 동안 사용되지 않은 항목을 최대 2개까지 제거합니다.

## Rate 

최대 요청 속도를 설정합니다. 위 예제에서는 초당 10회의 요청을 초과할 수 없습니다. 실제로 NGINX는 밀리초 단위로 요청을 추적하므로, 이 제한은 100 밀리초마다 1회의 요청에 해당합니다. 우리가 버스트(bursts)을 허용하지 않기 때문에, 이전에 허용된 요청 이후 100ms 이내에 요청이 도착하면 요청이 거부됩니다.

---

`limit_req_zone` 지시어는 Rate Limiting 및 공유 메모리 영역의 매개변수를 설정하지만 실제로 요청 속도를 제한하지는 않습니다. 이를 위해서는 특정 위치나 서버 블록에 limit_req 지시어를 포함하여 제한을 적용해야 합니다. 예시에서는 `/login/`로의 요청을 제한하고 있습니다.

따라서 이제 각 고유 IP 주소는 `/login/`에 대해 초당 10회의 요청으로 제한되며 – 더 정확하게는 이전 요청 후 100ms 이내에 해당 URL에 대한 요청을 만들 수 없습니다

- [limit_req_zone*nginx.org*](http://nginx.org/en/docs/http/ngx_http_limit_req_module.html#limit_req_zone)
{.links-list}
- [limit_req*nginx.org*](http://nginx.org/en/docs/http/ngx_http_limit_req_module.html#limit_req)

# 대량의 요청 처리하기

100ms 내에 2개의 요청이 도착하면 어떻게 될까요? 두 번째 요청에 대해서 NGINX는 클라이언트에게 503 상태 코드를 반환합니다. 이것은 우리가 원하는 결과가 아닐 것입니다. 왜냐하면 애플리케이션은 자연스럽게 요청이 대량으로 집중될 수 있기 때문입니다. 대신 우리는 초과된 요청을 버퍼에 저장하고 적절한 시간 안에 처리하길 원합니다. 이런 상황에서 `burst` 매개변수를 `limit_req`에 사용합니다. 아래의 업데이트된 설정에서 확인할 수 있습니다:

```nginx
location /login/ {
    limit_req zone=mylimit burst=20;
 
    proxy_pass http://my_upstream;
}
```

`burst` 매개변수는 지정된 Rate(예시에서는 `mylimit` 영역으로 초당 10회 요청, 또는 100ms마다 1회)을 초과하여 클라이언트가 얼마나 많은 요청을 할 수 있는지를 정의합니다. 이전 요청 후 100ms 이내에 도착하는 요청은 큐에 들어가며, 여기서 우리는 큐의 크기를 20으로 설정합니다.

즉, 주어진 IP 주소에서 동시에 21개의 요청이 도착하면 NGINX는 첫 번째 요청을 즉시 상위 서버 그룹으로 전달하고 나머지 20개는 큐에 넣습니다. 그런 다음 100ms마다 큐에 있는 요청을 전달하며, 들어오는 요청으로 큐에 있는 요청 수가 20을 초과하면 클라이언트에게 503을 반환합니다.

# 지연 없이 큐잉하기

burst와 함께 설정을 하면 트래픽의 흐름이 부드러워지지만, 실제로는 사이트가 느리게 보일 수 있어 실용적이지 않습니다. 예를 들어, 큐에 20번째 패킷이 2초 동안 대기한 후 전달되면, 그 시점에 클라이언트에게 응답이 더 이상 유용하지 않을 수 있습니다. 이 상황을 해결하기 위해 `nodelay` 매개변수를 `burst` 매개변수와 함께 추가합니다:

```nginx
location /login/ {
    limit_req zone=mylimit burst=20 nodelay;
 
    proxy_pass http://my_upstream;
}
```

`nodelay` 매개변수를 사용하면, NGINX는 여전히 burst 매개변수에 따라 큐에서 슬롯을 할당하고 설정된 Rate Limit을 적용하지만, 큐에 있는 요청의 전달을 간격을 두고 할당하는 것이 아닙니다. 대신 요청이 "너무 빨리" 도착하면, 큐에 슬롯이 사용 가능한 한 NGINX는 즉시 요청을 전달합니다. 그 슬롯을 "사용 중"으로 표시하고 적절한 시간이 지난 후에 다른 요청에 의해 사용되도록 해제합니다(예제에서는 100ms 후).

이제 첫 번째 요청 세트가 전달된 후 101ms가 지나고 동일한 IP 주소에서 20개의 요청이 동시에 도착한다고 가정해봅시다. 큐의 슬롯 중 1개만 해제되었으므로 NGINX는 1개의 요청을 전달하고 나머지 19개는 503 상태로 거절합니다. 대신 501ms가 지나기 전에 20개의 새 요청이 도착하면, 5개의 슬롯이 해제되므로 NGINX는 즉시 5개의 요청을 전달하고 15개를 거절합니다.

이 효과는 초당 10회의 Rate Limiting과 동일합니다. nodelay 옵션은 요청 간 허용된 간격에 제약을 받지 않고 Rate Limit을 적용하려는 경우 유용합니다.

> **참고**: 대부분의 배포에서는 `limit_req` 지시어에 `burst`와 `nodelay` 매개변수를 포함하는 것을 권장합니다.

## 2단계 Rate Limiting

NGINX Plus R17 또는 NGINX Open Source 1.15.7에서는 일반적인 웹 브라우저의 요청 패턴에 맞게 일정량의 요청을 허용한 후, 추가로 과도한 요청을 일정 수준까지 제한하고, 그 이후의 과도한 요청은 거절할 수 있도록 NGINX를 설정할 수 있습니다. 2단계 Rate Limit은 `limit_req` 지시어의 `delay` 매개변수를 사용하여 활성화됩니다.

2단계 Rate Limit을 설명하기 위해, 초당 5회의 요청(r/s) 제한을 가진 웹사이트를 보호하도록 NGINX를 설정해보겠습니다. 웹사이트는 일반적으로 페이지당 4~6개의 리소스를 갖고, 최대 12개의 리소스를 초과하지 않습니다. 이 설정에서는 최대 12회의 요청을 허용하며, 처음 8회의 요청은 지연 없이 처리됩니다. 8회의 과도한 요청 후에는 5r/s 제한을 강제하기 위해 지연이 추가됩니다. 12회의 과도한 요청 후에는 추가 요청은 모두 거절됩니다.

```nginx
limit_req_zone $binary_remote_addr zone=ip:10m rate=5r/s;

server {
    listen 80;
    location / {
        limit_req zone=ip burst=12 delay=8;
        proxy_pass http://website;
    }
}
```

`delay` 매개변수는 지정된 Rate Limit을 준수하기 위해, 허용된 burst 크기 내에서 언제 과도한 요청이 제한(지연)되는지를 정의합니다. 이 설정을 사용하면, 초당 8회의 요청을 지속적으로 수행하는 클라이언트는 다음과 같은 동작을 경험하게 됩니다.

- [delay*nginx.org*](https://nginx.org/en/docs/http/ngx_http_limit_req_module.html#limit_req_delay)
{.links-list}


## rate=5r/s, burst=12, delay=8 설정으로 인한 Rate Limit 동작 예시

![two-stage-rate-limiting-example.png](/two-stage-rate-limiting-example.png){.align-center}

첫 8개의 요청(delay의 값)은 NGINX Plus에서 지연 없이 프록시됩니다. 다음 4개의 요청(`burst` - `delay`)은 정의된 5r/s 을 초과하지 않도록 지연됩니다. 다음 3개의 요청은 총 burst 크기가 초과되었기 때문에 거절됩니다. 이후의 요청들은 지연됩니다.

# 고급 설정 예제

기본 Rate Limit과 다른 NGINX 기능들을 결합하면, 더욱 미세하게 트래픽 제한을 구현할 수 있습니다.

## 허용 목록
아래 예제는 "허용 목록"에 없는 사용자의 요청에 대해 Rate Limit을 부과하는 방법을 보여줍니다.

```nginx
geo $limit {
    default 1;
    10.0.0.0/8 0;
    192.168.0.0/24 0;
}
 
map $limit $limit_key {
    0 "";
    1 $binary_remote_addr;
}
 
limit_req_zone $limit_key zone=req_zone:10m rate=5r/s;
 
server {
    location / {
        limit_req zone=req_zone burst=10 nodelay;
 
        # ...
    }
}
```

이 예제는 geo와 map 지시어를 모두 사용합니다. geo 블록은 허용 목록에 있는 IP 주소에 대해 $limit 값을 0으로 설정하고, 나머지는 1로 설정합니다. 그 다음 map을 사용하여 이러한 값을 키로 변환하여:

- `$limit`이 0인 경우, `$limit_key`는 빈 문자열로 설정됩니다
- `$limit`이 1인 경우, `$limit_key`는 이진 형식의 클라이언트 IP 주소로 설정됩니다

따라서, 허용된 IP 주소는 빈 문자열로, 그 외의 IP 주소는 클라이언트의 IP 주소로 `$limit_key`가 설정됩니다. `limit_req_zone` 디렉토리의 첫 번째 매개변수(키)가 빈 문자열인 경우, 제한이 적용되지 않으므로 허용 목록에 있는 IP 주소(10.0.0.0/8 및 192.168.0.0/24 서브넷)는 제한되지 않습니다. 다른 모든 IP 주소는 초당 5회의 요청으로 제한됩니다.

`limit_req` 지시어는 / 위치에 제한을 적용하고, 설정된 제한을 초과하여 최대 10개의 패킷을 허용하며 전달 시 지연이 발생하지 않습니다.

- [geo*nginx.org*](http://nginx.org/en/docs/http/ngx_http_geo_module.html#geo)
- [map*nginx.org*](http://nginx.org/en/docs/http/ngx_http_map_module.html#map)
{.links-list}

## 위치(Location)에서 여러 limit_req 지시어 포함하기

하나의 위치(location)에 여러개의 `limit_req` 지시어를 포함할 수 있습니다. 주어진 요청과 일치하는 모든 제한이 적용되며, 가장 제한적인 것이 사용됩니다. 예를 들어, 한 개 이상의 지시어가 지연을 부과하면 가장 긴 지연이 사용됩니다. 마찬가지로, 어떤 지시어의 효과로 요청이 거절되면 다른 지시어들이 허용하더라도 요청은 거절됩니다.

이전 예제를 확장하여 허용 목록에 있는 IP 주소에 Rate Limit을 적용할 수 있습니다:

```nginx
http {
    # ...
 
    limit_req_zone $limit_key zone=req_zone:10m rate=5r/s;
    limit_req_zone $binary_remote_addr zone=req_zone_wl:10m rate=15r/s;
 
    server {
        # ...
        location / {
            limit_req zone=req_zone burst=10 nodelay;
            limit_req zone=req_zone_wl burst=20 nodelay;
            # ...
        }
    }
}
```

허용 목록에 있는 IP 주소는 첫 번째 Rate Limit(`req_zone`)과 일치하지 않지만 두 번째(`req_zone_wl`)와 일치하므로 초당 15회로 제한됩니다. 허용 목록에 없는 IP 주소는 두 Rate Limit과 모두 일치하므로 더 제한적인 것이 적용됩니다 (초당 5회의 요청)

# 관련 기능 구성하기

## 로깅 (Logging)

기본적으로 NGINX는 다음 예제와 같이 Rate Limit으로 인해 지연되거나 드롭된 요청을 기록합니다:

```
2015/06/13 04:20:00 [error] 120315#0: *32086 limiting requests, excess: 1.000 by zone "mylimit", client: 192.168.1.2, server: nginx.com, request: "GET / HTTP/1.0", host: "nginx.com"
```

로그 항목에 포함된 필드는 다음과 같습니다:

- `2015/06/13 04:20:00` – 로그 항목이 기록된 날짜 및 시간
- `[error]` – 중요도 수준
- `120315#0` – NGINX 작업자의 프로세스 ID와 스레드 ID, # 기호로 구분됩니다.
- `*32086` – Rate Limiting 된 프록시 연결의 ID
- `limiting requests` – 로그 항목이 Rate Limit을 기록하고 있음을 나타내는 지시자
- `excess` – 이 요청이 나타내는 설정된 Rate보다 초과된 밀리초당 요청 수
- `zone` – 부과된 Rate Limiting을 정의하는 구역
- `client` – 요청을 수행하는 클라이언트의 IP 주소
- `server` – 서버의 IP 주소 또는 호스트 이름
- `request` – 클라이언트에 의해 수행된 실제 HTTP 요청
- `host` – Host HTTP 헤더의 값

기본적으로 NGINX는 위의 예제에서 `[error]`로 표시된 것처럼 거부된 요청을 오류 수준에서 기록합니다. (지연된 요청은 기본적으로 하나의 수준 낮은 경고로 기록됩니다.) 로깅 수준을 변경하려면 `limit_req_log_level` 지시어를 사용합니다. 여기에서는 거부된 요청을 경고 수준에서 로그로 기록하도록 설정합니다:

```nginx
location /login/ {
    limit_req zone=mylimit burst=20 nodelay;
    limit_req_log_level warn;
 
    proxy_pass http://my_upstream;
}
```

- [limit_req_log_level*nginx.org*](http://nginx.org/en/docs/http/ngx_http_limit_req_module.html#limit_req_log_level)
{.links-list}

## 클라이언트에게 전송되는 오류 코드

기본적으로 클라이언트가 Rate Limit을 초과할 때 NGINX는 상태 코드 503(Service Temporarily Unavailable)으로 응답합니다. 다른 상태 코드를 설정하려면 `limit_req_status` 지시어를 사용하십시오(이 예제에서는 444):

```nginx
location /login/ {
    limit_req zone=mylimit burst=20 nodelay;
    limit_req_status 444;
}
```

- [limit_req_status*nginx.org*](http://nginx.org/en/docs/http/ngx_http_limit_req_module.html#limit_req_status)
{.links-list}

## 특정 위치에 대한 모든 요청 거부

특정 URL에 대한 모든 요청을 거절하려면(제한하는 대신) `location` 블록을 구성하고 거부 모두(`deny all`) 지시어를 포함하십시오:

```nginx
location /foo.php {
    deny all;
}
```

- [location*nginx.org*](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)
- [deny*nginx.org*](http://nginx.org/en/docs/http/ngx_http_access_module.html#deny)
{.links-list}

# 결론

NGINX 및 NGINX Plus가 제공하는 Rate Limiting의 많은 기능들을 다루었습니다. HTTP 요청에 대한 다른 위치에 대한 요청 속도를 설정하고, `burst` 및 `nodelay` 매개변수와 같은 Rate Limit에 대한 추가 기능을 구성하는 것을 포함합니다. 허용 목록(allowlist)과 거부 목록(denylist)에 있는 클라이언트 IP 주소에 대한 다른 제한을 적용하기 위한 고급 구성도 다루었으며, 거절되고 지연된 요청을 어떻게 기록하는지에 대해서도 설명했습니다.



