---
title: 서로 다른 Git 저장소를 하나의 저장소로 합치기
description: 
published: true
date: 2023-02-17T17:59:39.611Z
tags: git
editor: markdown
dateCreated: 2022-11-24T08:58:12.567Z
---


![image](https://cloud.githubusercontent.com/assets/8033320/20261447/1982ff3a-aaa1-11e6-844a-8965aa4e95e8.png)

한 8월달 부터 github PR의 오의를 깨닫고 재미가 들려 열심히 커밋을 하다가 회사를 다니기 시작한 뒤로 허전해진 그래프를 보며 많은 사람들이 시도했던 일일커밋을 해보기로 마음을 먹음. 기존에 스터디나 자료 존안용으로 흩어져 있던 여러 저장소를 새로운 하나의 저장소로 합쳐야할 필요성을 느꼈다. 그래도 지금까지 쌓아놓은 것들이 있으니 커밋 로그를 날리기는 실어서 최대한 유지하면서 합쳐보기로 했다. (그리고 이 생각이 모든 문제의 원흉이 되었다)

## git fetch
합치려고 하는 저장소들은 아래 4개다.
- [luckyyowu.tistory.com-posts](https://github.com/uyu423/luckyyowu.tistory.com-posts) : 블로그 포스트용 markdown 파일 모음 저장소
- [functional-js-study](https://github.com/uyu423/functional-js-study) : 함수형 자바스크립트 공부용으로 만들어놓고 1장 끝낸 저장소
- [Programming-Practice](https://github.com/uyu423/Programming-Practice) : 몇년간 틈틈히 생산한 코드 조각들의 모음집
- [Algorithm-Problem-Solving](https://github.com/uyu423/Algorithm-Problem-Solving) : 조금씩 풀었던 알고리즘 문제들의 모음집

각 저장소를 클론하고 미리 클론해둔 새로운 저장소에 fetch를 사용하여 새로운 브랜치로 만든다. 그리고 해당 브랜치에서 디렉토리를 간단하게 정리하고 새로운 커밋을 만들어 놓았다.
```bash
git fetch ../Programming-Practice master:merge/PP # Programming-Practice 저장소의 master 브랜치를 이 곳의 merge/PP로 fetch !
git checkout merge/PP
mkdir 프로그래밍\ 연습 && mv * 프로그래밍\ 연습
git add *
git commit -m "저장소 병합. PP"
```

![image](https://cloud.githubusercontent.com/assets/8033320/20261819/dde5a12e-aaa2-11e6-9d0c-3d6d973c3f7e.png)

다음과 같이 브랜치가 형성이 되었지만 병합이 안된다...;; 원인을 찾아보니 다른 히스토리를 가진 브랜치 끼리는 머지할 수가 없다고 한다. [생활코딩에 문의](https://www.facebook.com/groups/codingeverybody/permalink/1400317996675399/)한 결과..


## git cherry-pick
git cherry-pick으로 문제를 해결할 수 있다. 체리픽이란게 있는 줄은 알았지만 한번도 사용해본 적은 없다. 대충 찾아보니 커밋 해시 값을 가지고 해당 브런치에 해당 커밋을 그냥 쑤셔넣는 느낌..
```bash
git checkout merge/PP
git log #에서 가장 최근의 Commit SHA값을 복사해둔다.
git checkout master
git cherry-pick 9ede61845d75411e8cef35303b6eeaa5d7c26bdb
# 충돌 해결 후 commit. 나머지 브랜치도 동일하게 작업
git push origin master
```

다음과 같이 이쁘고도 괴상한 트리가 잘 만들어졌다..!

![image](https://cloud.githubusercontent.com/assets/8033320/20261829/e9a28540-aaa2-11e6-9ba9-928190e3a4e1.png)
