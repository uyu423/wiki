---
title: ElasticBeanstalk에서 Load Balancer http to https 리다이렉션 설정하기
description: 놀랍게도 http(80) -> https(443) 리다이렉트는 EB 구성에서 설정할 수 없다...;
published: true
date: 2023-02-17T17:59:50.384Z
tags: aws, ec2, elasticbeanstalk
editor: markdown
dateCreated: 2022-11-26T20:31:42.413Z
---

- [Setting up Load Balancer http to https redirection in ElasticBeanstalk***English** version of this document is available*](/en/dev/AWS/Setting-up-Load-Balancer-http-to-https-redirection-in-ElasticBeanstalk)
{.links-list}

> Application Load Balancer 를 사용한다고 가정한다.

## ElasticBeanstalk 설정에서는 할 수 없다.

![스크린샷_2022-11-27_오전_5.23.05.png](/스크린샷_2022-11-27_오전_5.23.05.png =800x)

- ElasticBeanstalk 구성의 로드 밸런서 설정에서는 눈을 씻고 찾아봐도 http -> https 리다이렉션 설정이 없다.

> 그래도 여기서 80, 443 포트에 대한 설정은 해놓자
{.is-info}


## 해결책은 EC2 - Load Balancer 수동 설정이다.

- `EC2 - 로드밸런서`로 이동하고, 설정하려는 ElasticBeanstalk 환경에서 사용중인 로드밸런서를 찾는다.
- 찾은 로드밸런서의 `리스너` 항목으로 이동한다.
- 80 포트 리스너 설정을 변경한다.
- 기본 값으로 설정된 `Forward` 설정을 제거하고, `Redirect` 를 신규로 설정한다.
- 대충 아래와 같이 설정하면 된다.

![스크린샷_2022-11-27_오전_5.30.29.png](/스크린샷_2022-11-27_오전_5.30.29.png =600x)

---

- 무슨 ElasticBeanstalk 에 http -> https Redirect 설정 하나 없는지 모르겠다 :(
