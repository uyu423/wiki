---
title: Wiki.js Group Permission (Page Rules) Sample
description: Wiki.js 그룹 사용자 권한 (Page Rules) 샘플
published: true
date: 2023-02-17T17:59:58.396Z
tags: wikijs
editor: markdown
dateCreated: 2022-12-07T09:36:53.363Z
---

> Wiki.js 의 Admin - Groups - Page Rules 를 이것저것 테스트 해보고 샘플을 남김

![스크린샷_2022-12-07_오후_6.21.00.png](/스크린샷_2022-12-07_오후_6.21.00.png)

- 위와 같이 설정 시, 해당 그룹은
  - `/` 페이지 접근 가능 (Page, Assets Readonly)
  - `/secret-dir`, `/banned-dir` 접근 불가능 (리스트에 보이지 않음)
  - `/multi-dir/inner-dir-A` CRUD 가능
  - `/multi-dir/` 하위의 다른 디렉토리는 접근 불가능 (리스트에서 보이지 않음)
    - 예를 들어, `/multi-dir/inner-dir-B` 가 있을 경우 보이지 않음.
    - `/multi-dir/` 끝에 슬래쉬(`/`) 가 없으면, `/multi-dir` 자체가 보이지 않고 접근이 불가능함
      - 개발자가 의도한 스펙인지는 모르겠음(...)

  
> Page Rules 에 적절한 권한을 추가했는데도 해당 페이지에 권한이 생기지 않았다면, Permissions 탭에서 전역 권한을 체크해본다. 
> Page Rules 권한이 있어도, 전역 권한이 없다면 Page Rules 에 따른 권한이 생성되지 않는다.
{.is-warning}

### References

- [Users, Groups & Permissions*english*](https://docs.requarks.io/groups)
{.links-list}

