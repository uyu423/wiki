---
title: 백엔드 개발을 위한 Ruby on Rails
description: 
published: true
date: 2023-02-18T15:32:35.967Z
tags: 
editor: markdown
dateCreated: 2023-02-18T15:32:34.603Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Ruby on Rails for Backend Development***English** document is available*](/en/Knowledge-base/Backend/ruby-on-rails-for-backend-development)
{.links-list}


# 백엔드 개발을 위한 Ruby on Rails

Ruby on Rails는 Ruby로 작성된 웹 애플리케이션 프레임워크입니다. 모든 개발자가 시작하는 데 필요한 사항을 가정하여 웹 애플리케이션 프로그래밍을 더 쉽게 만들도록 설계되었습니다. 다른 많은 프레임워크 및 라이브러리보다 더 많은 것을 수행하면서 더 적은 코드를 작성할 수 있습니다.

## 왜 Ruby on Rails인가?

Ruby on Rails는 여러 가지 이유로 백엔드 개발에 탁월한 선택입니다.

- 완전한 웹 애플리케이션을 만드는 데 필요한 모든 도구를 제공하는 **풀 스택** 프레임워크입니다. 여기에는 라우팅에서 데이터베이스, 프런트 엔드에 이르는 모든 것이 포함됩니다.

- 지원을 아끼지 않는 대규모 **커뮤니티**가 있습니다. Ruby on Rails는 오픈 소스 프로젝트이기 때문에 지속적으로 프레임워크를 개선하고 유용한 리소스를 만드는 개발자 커뮤니티가 있습니다.

- 이는 **구성보다 관례** 프레임워크로, 필요한 구성의 양을 최소화하기 위해 관례에 의존한다는 의미입니다. 이렇게 하면 개발이 더 빠르고 쉬워집니다.

- 코드 재사용을 강조하는 **DRY** 프레임워크입니다. 이렇게 하면 코드를 유지 관리하기 쉽고 쉽게 확장할 수 있습니다.

## 시작하기

Ruby on Rails로 개발을 시작하기 전에 Ruby on Rails를 설치해야 합니다. 가장 쉬운 방법은 [Ruby on Rails 설치 프로그램](http://railsinstaller.org/)을 사용하는 것입니다. 이렇게 하면 Ruby, Rails 및 시작하는 데 필요한 다른 모든 종속 항목이 설치됩니다.

Ruby on Rails가 설치되면 `rails new` 명령을 사용하여 새 프로젝트를 만들 수 있습니다.

```
$ rails new my_app
```

이렇게 하면 시작하는 데 필요한 모든 파일이 있는 `my_app`이라는 새 디렉토리가 생성됩니다.

## 헬로월드!

이제 새 Ruby on Rails 프로젝트가 있으므로 간단한 "Hello, World!" 애플리케이션.

먼저 새 컨트롤러를 만들어야 합니다. 컨트롤러는 사용자의 요청을 처리하고 응답을 반환하는 역할을 합니다. Ruby on Rails에서 컨트롤러는 `app/controllers` 디렉토리에 저장됩니다.

새 컨트롤러를 생성하려면 `rails generate` 명령을 사용할 수 있습니다.

```
$ rails generate controller Welcome index
```

그러면 다음 내용이 포함된 `app/controllers/welcome_controller.rb`라는 새 파일이 생성됩니다.

```ruby
class WelcomeController < ApplicationController
  def index
  end
end
```

다음으로 보기를 만들어야 합니다. 보기는 컨트롤러의 응답을 표시하는 역할을 합니다. Ruby on Rails에서 뷰는 `app/views` 디렉토리에 저장됩니다.

새 보기를 만들려면 다음 내용으로 `app/views/welcome/index.html.erb`라는 새 파일을 만들 수 있습니다.

```
<h1>Hello, World!</h1>
```

이제 컨트롤러와 뷰가 있으므로 Ruby on Rails에 요청을 컨트롤러로 라우팅하는 방법을 알려야 합니다. 이는 `config/routes.rb` 파일에서 수행됩니다:

```ruby
Rails.application.routes.draw do
  get 'welcome/index'
end
```

이것은 `/welcome` 경로에 대한 모든 요청이 `WelcomeController` 컨트롤러에 의해 처리되어야 한다고 Ruby on Rails에 알려줍니다.

마지막으로 Ruby on Rails 서버를 시작해야 합니다.

```
$ rails server
```

이제 웹 브라우저에서 http://localhost:3000/welcome/index를 방문하여 "Hello, World!"를 볼 수 있습니다. 애플리케이션.

## 자원

- [Ruby on Rails 가이드](http://guides.rubyonrails.org/)
- [Ruby on Rails API 문서](http://api.rubyonrails.org/)
- [Ruby on Rails 튜토리얼](http://ruby.railstutorial.org/)