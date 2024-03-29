---
title: Git Branch 전략에 대한 질문
description: 2018-02-27
published: true
date: 2023-02-17T17:59:32.762Z
tags: qna, git
editor: markdown
dateCreated: 2022-11-24T07:57:13.614Z
---

|댓글 작성 일시|작성 방법|커뮤니티|질문자|원문 링크|
|---|---|---|---|---|
|2018-02-27 01:37|PC Web + Notepad|생활코딩 페이스북|강*|[link](https://www.facebook.com/groups/codingeverybody/permalink/2045772165463309/)|

## 질문 요약
Git을 사용할 때 브랜치를 나누는 기준은 무엇인가요?

## 나의 댓글
git branch를 언제 나누고 사용하는지에 대해 잘 모르시겠다면 일반적으로 많이 쓰는 방법을 무작정 따라해보는 것도 나쁘지 않은 선택입니다. 쓰다보면 감이 옵니다. 질문자님이 말씀하신게 git branch 전략 이라는 내용인데, 일반적으로 git-flow를 많이 따릅니다. 추천드리는 글은 우아한 형제들의 [기술 블로그 포스트](http://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html)를 보시는 것도 좋습니다. 내용자체는 처음부터 이해하기는 어려우니 감만 익힌다는 느낌으로 슬쩍보세요.

git branch 전략은 회사마다, 개발자마다 다를 경우가 많은데 일반적으로는 다음과 같은 전략을 많이 취합니다.

하나의 서비스가 있으면 그 서비스는 '실제 사용 단계 (master)', '개발 단계 (develop)', '기능별 개발 단계 (feature/*)' 와 같은 단계를 가질 수 있습니다.

> 1. 특정 소프트웨어 개발 요구 사항-1이 발생한다.
> 2. A 개발자가 요구 사항-1 을 해결하기 위해 develop 브랜치에서 새로운 feature/function-1 을 만들고 개발을 진행한다.
> 3. 새로운 요구사항-2 가 발생했다.
> 4. B 개발자가 요구 사항-2 를 해결하기 위해 develop 브랜치에서 새로운 feature/function-2 를 만들고 개발을 진행한다.
> 5. B 개발자가 A 개발자 보다 먼저 일을 마쳤다. B 개발자는 자신이 개발한 부분을 검토 받고 feature/function-2 브랜치를 develop 브랜치로 merge 했다.
> 6. A 개발자도 개발이 끝났다. A 역시 feature/function-1을 develop 브랜치로 merge 시켰다.
> 7. develop 브랜치를 개발 서버에 배포하고 테스트를 거친다.
> 8. 테스트가 성공적으로 되었다면 develop 브랜치를 master 브랜치와 merge 하고 master 브랜치를 production 서버에 배포한다.

간단하게 생각해본 git branch 시나리오입니다. 사실 모든 상황이 저렇게 깔끔하게 떨어지지는 않고, git commit들이 꼬이거나 꼬이거나 꼬이는 별의 별 상황이 다 있을 수 있습니다. 그냥 몇 번 꼬이고 그걸 풀고 하다보면 git은 늡니다. 어느정도 익숙해지시고 우아한형제들 기술 블로그 포스트를 다시보시면 느낌이 다르실 겁니다.

저도 git 사용한지 몇 년이나 되어가지만 여전히 git은 어렵고 심오한 시스템입니다. 우리존재화이팅입니다.