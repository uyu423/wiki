---
title: Wiki.js 2.x에 sitemap.xml 을 추가하는 임시단편적인 방법
description: 
published: true
date: 2023-02-17T17:59:51.755Z
tags: wikijs, cron, sitemap
editor: markdown
dateCreated: 2022-12-01T13:20:12.695Z
---

- [Ad-hoc way to add sitemap.xml to Wiki.js 2.x***English** version of this document is available*](/en/dev/Wiki-js/How-to-add-temporary-sitemap-xml-to-Wiki-js)
{.links-list}

> Wiki.js 3.0 에서 sitemap 기능을 공식적으로 지원할 예정이라 임시로 사용하는 방법이다.
> 아래의 방법은 Wiki.js가 설치된 서버 환경의 프로젝트 디렉토리 내부 `assets` 접근과 `crontab` 명령어 사용이 가능함을 전제로 한다.

---

- wiki.js 구동 환경이 아래와 같이 구성되어있다.
  - wiki.js 설치 디렉토리: `/home/wiki/app`
  - sitemap.xml 생성 스크립트 위치: `/home/wiki/.scripts/wikijs-sitemap` (empty directory)
  
## Wiki.js 사전 준비

- 본인의 wiki.js 첫 페이지에서 모든 페이지를 탐색할 수 있도록 링크를 달아둔다.
- wiki.yowu.dev의 [Home](/home) 하단을 참고하면 된다.

## sitemap.xml 생성 스크립트

### 초기화

```bash
cd /home/wiki/.scripts/wikijs-sitemap
npm init -y
npm install --save https://github.com/uyu423/sitemap-generator
```

> `sitemap-generator` 프로젝트가 wiki.js 페이지를 제대로 파싱하지 못하는 이슈가 있다.
> 프로젝트에서 사용하는 `cheerio` 버전 이슈로 현재 Pull Request로 수정 요청이 진행 중. [sitemap-generator#119](https://github.com/lgraubner/sitemap-generator/pull/119)
> 해당 프로젝트의 `cheerio`이 올라갔다면 원본 프로젝트를 사용할 수 있다.
> ```bash
> npm install sitemap-generator
> ```
> 😎
{.is-warning}

### 스크립트 생성

```javascript
const SitemapGenerator = require("sitemap-generator");

const service = SitemapGenerator("https://your.wiki.address", {
  filepath: "/home/wiki/app/assets/sitemap.xml",
  stripQuerystring: true,
  priorityMap: [0.5, 0.5, 1.0]
});

service.start();
```

- `filepath` 와 `priorityMap` 은 본인 wiki.js 구성에 맞게 변경한다.
  - Wiki.js 가 존재하는 파일 시스템 하위 디렉토리 `app/assets/*` 는 `your.wiki.address/_assets/*` URL 로 맵핑된다.
- `node index.js` 를 실행하면 `sitemap-generator` 크롤러가 페이지 본문의 `<a href>` 태그를 재귀적으로 찾아서 sitemap.xml 로 생성한다.
- wiki.js assets 디렉토리에 sitemap.xml 이 정상적으로 생기는지 확인한다.

## crontab

- 나는 Linux 기본 유틸인 `crontab` 을 사용하여 하루에 한번씩 sitemap.xml 을 갱신해주도록 했다.

```bash
crontab -e
```
```cron
23 4 * * * node /home/wiki/.scripts/wikijs-sitemap/index.js
```
- 매일 오전 04:23 에 `sitemap.xml` 갱신

## 마무리

- 이제 본인이 필요한 검색 엔진에 `https://your.wiki.address/_assets/sitemap.xml` 주소로 사이트맵을 등록하면 된다.

> 여기서는 굉장히 번거로운 방법으로 서버 로컬 환경에 `sitemap.xml` 을 추가한 예제를 공유했다. 
> 가능하다면 본인 Wiki.js 가 구동되는 서버 환경에 맞게 커스터마이징하는 것이 좋을 것이다.