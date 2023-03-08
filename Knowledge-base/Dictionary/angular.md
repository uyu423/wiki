---
title: Angular
description: 
published: true
date: 2023-02-10T11:17:59.077Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:17:56.948Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Angular***English** document is available*](/en/Knowledge-base/Dictionary/angular)
{.links-list}


# 각도

## 개요
Angular는 Google에서 만들고 유지 관리하는 오픈 소스 웹 애플리케이션 프레임워크입니다. 단일 페이지 웹 애플리케이션 및 모바일 애플리케이션을 개발하는 데 사용됩니다. TypeScript로 작성되었으며 MVC(Model-View-Controller) 디자인 패턴을 기반으로 합니다.

## 설명
Angular는 웹 애플리케이션 개발을 위한 프레임워크이며 MVC(Model-View-Controller) 디자인 패턴을 기반으로 합니다. TypeScript로 작성되었으며 Google에서 관리합니다. 단일 페이지 애플리케이션 및 모바일 애플리케이션 개발에 사용하도록 설계되었습니다.

Angular는 Angular CLI(명령줄 인터페이스), Angular 컴파일러 및 Angular Core를 비롯한 여러 구성 요소로 구성됩니다. Angular CLI는 Angular 프로젝트를 만들고 관리하는 데 사용되는 반면 Angular Compiler는 TypeScript 코드를 컴파일하는 데 사용됩니다. Angular Core는 애플리케이션을 만드는 데 사용되는 핵심 구성 요소 및 서비스를 포함하는 기본 프레임워크입니다.

Angular에는 애플리케이션에서 라우팅을 관리하는 데 사용되는 Angular Router와 양식을 만들고 관리하는 데 사용되는 Angular Forms 라이브러리와 같은 여러 다른 라이브러리와 도구도 포함되어 있습니다.

## 특징
Angular에는 웹 및 모바일 애플리케이션 개발을 위한 매력적인 선택이 되는 몇 가지 기능이 포함되어 있습니다. 이러한 기능에는 다음이 포함됩니다.

- TypeScript 지원: Angular는 JavaScript의 상위 집합인 TypeScript로 작성되었습니다. 이를 통해 개발자는 JavaScript의 기능에 계속 액세스하면서 언어의 최신 기능을 사용할 수 있습니다.

- 구성 요소 기반 아키텍처: Angular는 구성 요소 기반 아키텍처를 사용하므로 개발자가 모듈식 및 재사용 가능한 구성 요소를 만들 수 있습니다. 이를 통해 애플리케이션을 더 쉽게 유지 관리하고 확장할 수 있습니다.

- 모듈화: Angular를 통해 개발자는 코드를 모듈화할 수 있으므로 애플리케이션을 보다 쉽게 관리하고 유지할 수 있습니다.

- 반응형 프로그래밍: Angular는 반응형 프로그래밍 모델을 사용하여 개발자가 사용자 입력에 더 반응하는 애플리케이션을 만들 수 있습니다.

- 도구: Angular에는 프로젝트를 만들고 관리하는 데 사용되는 Angular CLI와 TypeScript 코드를 컴파일하는 데 사용되는 Angular Compiler와 같이 응용 프로그램을 쉽게 개발할 수 있는 여러 도구가 포함되어 있습니다.

## 예
다음은 사용자 목록을 표시하는 Angular 애플리케이션의 예입니다. 애플리케이션은 Angular CLI를 사용하여 프로젝트를 만들고 Angular 라우터를 사용하여 라우팅을 관리하고 Angular Forms 라이브러리를 사용하여 양식을 만들고 관리합니다.

```
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  users: any[];
  userForm: FormGroup;

  constructor(private router: Router) { }

  ngOnInit() {
    this.userForm = new FormGroup({
      name: new FormControl('', Validators.required),
      email: new FormControl('', [Validators.required, Validators.email])
    });
  }

  onSubmit() {
    this.users.push(this.userForm.value);
    this.router.navigate(['/users']);
  }

}
```

## 장점과 단점
Angular에는 프레임워크를 선택할 때 고려해야 할 몇 가지 장점과 단점이 있습니다.

**장점:**

- 사용하기 쉬움: Angular는 상대적으로 사용하기 쉽고 지원 및 리소스를 제공할 수 있는 대규모 개발자 커뮤니티가 있습니다.

- 모듈화: Angular를 통해 개발자는 코드를 모듈화할 수 있으므로 애플리케이션을 더 쉽게 유지 관리하고 확장할 수 있습니다.

- 반응형 프로그래밍: Angular는 반응형 프로그래밍 모델을 사용하여 개발자가 사용자 입력에 더 반응하는 애플리케이션을 만들 수 있습니다.

**단점:**

- 가파른 학습 곡선: Angular는 가파른 학습 곡선을 가지고 있으며 프레임워크에 능숙해지는 데 시간이 걸릴 수 있습니다.

- 복잡성: Angular는 매우 복잡할 수 있으며 응용 프로그램을 디버깅하고 문제를 해결하기 어려울 수 있습니다.

- 성능: Angular 애플리케이션은 프레임워크의 복잡성으로 인해 다른 프레임워크로 구축된 애플리케이션보다 느릴 수 있습니다.

## 관련 기술
Angular는 TypeScript, React 및 Vue.js와 같은 여러 다른 기술과 관련이 있습니다. TypeScript는 Angular가 작성된 언어이며 JavaScript의 상위 집합입니다. React와 Vue.js는 둘 다 웹 애플리케이션 구축에 널리 사용되는 JavaScript 프레임워크입니다.

## 여담
Angular는 오픈 소스 프레임워크이며 많은 회사와 조직에서 웹 및 모바일 애플리케이션을 개발하는 데 사용됩니다. 사용 편의성과 TypeScript 및 기타 기술 지원으로 인해 개발자에게 매력적인 선택입니다.

## 기타
Angular는 2010년 처음 릴리스된 이후 인기가 높아졌으며 현재 가장 인기 있는 웹 애플리케이션 프레임워크 중 하나입니다. Google, Microsoft 및 Apple을 비롯한 많은 회사에서 사용합니다.