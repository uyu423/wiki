---
title: Kotlin 및 Ruby on Rails: Ruby 프레임워크로 웹 애플리케이션 구축
description: 
published: true
date: 2023-01-31T08:36:45.069Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:15:33.379Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and Ruby on Rails: Building a Web Application with a Ruby Framework***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-ruby-on-rails-building-a-web-application-with-a-ruby-framework)
{.links-list}


# Kotlin 및 Ruby on Rails: Ruby 프레임워크로 웹 애플리케이션 구축

웹 애플리케이션을 구축하려는 경우 프레임워크에 대한 많은 옵션이 있습니다. Ruby on Rails는 웹 애플리케이션 구축에 널리 사용되는 프레임워크이며 Kotlin은 Java와의 상호 운용성 및 보안 기능으로 인기를 얻고 있는 언어입니다. 이 기사에서는 Kotlin과 함께 Ruby on Rails 프레임워크를 사용하여 웹 애플리케이션을 빌드하는 방법을 보여줍니다.

Kotlin 및 Ruby on Rails의 기본 사항에 익숙하다고 가정합니다. 그렇지 않은 경우 이러한 기술에 대해 자세히 알아볼 수 있는 많은 리소스가 있습니다.

## Kotlin/Ruby on Rails 프로젝트 설정

가장 먼저 해야 할 일은 Kotlin/Ruby on Rails 프로젝트를 설정하는 것입니다. 다음 도구를 사용합니다.

* 코틀린 1.3.72
* 루비 2.6.5
* 레일즈 6.0.3.2

서로 호환되는 이러한 도구의 모든 버전을 사용할 수 있습니다.

새로운 Kotlin/Ruby on Rails 프로젝트를 설정하기 위해 -api 옵션 및 -d 옵션과 함께 rails new 명령을 사용하여 데이터베이스를 지정합니다. PostgreSQL 데이터베이스를 사용합니다.

    $ rails new my_app -api -d postgresql

이렇게 하면 기본 Rails 애플리케이션이 있는 my_app이라는 새 디렉토리가 생성됩니다.

## Kotlin 구성

다음으로 프로젝트에 Kotlin을 추가해야 합니다. 프로젝트의 Gemfile에 kotlin-rails 플러그인을 추가하여 이를 수행합니다.

    그룹 :development do
      보석 'kotlin-rails'
    끝

그런 다음 플러그인을 설치해야 합니다.

    $ 번들 설치

이제 플러그인을 설치했으므로 Kotlin을 구성해야 합니다. config 디렉토리에 kotlin.yml이라는 파일을 생성하여 이를 수행합니다. 이 파일에서 다음 구성을 추가합니다.

    코틀린:
      버전: 1.3.72
      대상:
        - jvm-1.8

이렇게 하면 Kotlin이 버전 1.3.72를 사용하고 Java 8 바이트코드로 컴파일하도록 지시합니다.

## 모델 만들기

이제 프로젝트가 설정되었으므로 웹 애플리케이션 구축을 시작할 수 있습니다. 몇 가지 모델을 만드는 것부터 시작하겠습니다. Ruby on Rails에서 모델은 애플리케이션의 데이터를 나타내는 클래스입니다. 애플리케이션의 각 데이터 유형에 대한 모델을 생성합니다.

우리의 첫 번째 모델은 사용자를 위한 모델이 될 것입니다. rails generate 명령을 사용하여 이 모델을 생성합니다.

    $ 레일은 모델 사용자를 생성합니다.

이렇게 하면 app/models/user.rb라는 새 파일이 생성됩니다. 이 파일을 열고 다음 코드를 추가합니다.

    클래스 사용자 < ApplicationRecord
      has_secure_password
    끝

이 코드는 User라는 새 모델을 정의합니다. has_secure_password 매크로는 암호를 안전하게 저장하는 데 도움이 되는 몇 가지 방법을 모델에 추가합니다.

다음으로 모델에 대한 마이그레이션을 생성해야 합니다. 마이그레이션은 데이터베이스 테이블을 생성하거나 수정하기 위한 SQL 코드가 포함된 파일입니다. 마이그레이션을 생성하려면 rails generate 명령을 다시 사용합니다.

    $ 레일 생성 마이그레이션 create_users

그러면 db/migrate 디렉토리에 새 파일이 생성됩니다. 이 파일을 열고 다음 코드를 추가합니다.

    클래스 CreateUsers < ActiveRecord::Migration[6.0]
      데프 변경
        create_table :사용자 수행 |t|
          t.문자열 :이름
          t.string :이메일
          t.string :password_digest
          t.타임스탬프
        끝
      끝
    끝

이 코드는 users라는 새 데이터베이스 테이블을 만듭니다. 테이블에는 이름, 이메일 및 password_digest에 대한 열이 있습니다. password_digest 열은 has_secure_password 매크로가 암호 해시를 저장하는 위치입니다.

이제 모델과 마이그레이션을 생성했으므로 마이그레이션을 실행하여 데이터베이스 테이블을 생성해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

    $ 레일 db:마이그레이션

## 컨트롤러 만들기

이제 모델이 설정되었으므로 컨트롤러 생성을 시작할 수 있습니다. Ruby on Rails에서 컨트롤러는 들어오는 HTTP 요청을 처리하는 클래스입니다. 처리하려는 각 요청 유형에 대해 하나의 컨트롤러를 생성합니다.

첫 번째 컨트롤러는 사용자 등록을 위한 컨트롤러가 될 것입니다. rails generate 명령을 사용하여 이 컨트롤러를 생성합니다.

    $ 레일은 컨트롤러 사용자를 생성합니다.

이렇게 하면 app/controllers/users_controller.rb라는 새 파일이 생성됩니다. 이 파일을 열고 다음 코드를 추가합니다.

    클래스 UsersController < ApplicationController
      새로운 데프
        @사용자 = 사용자.신규
      끝
    
      데프 생성
        @user = User.new(user_params)
    
        @user.save인 경우
          세션[:user_id] = @user.id
          redirect_to root_path
        또 다른
          렌더링 :새
        끝
      끝
    
      사적인
    
      def user_params
        params.require(:user).permit(:name, :email, :password, :password_confirmation)
      끝
    끝

이 코드는 UsersController라는 새 컨트롤러를 정의합니다. 컨트롤러에는 new와 create의 두 가지 작업이 있습니다. 새 작업은 새 사용자를 만들기 위한 양식을 렌더링합니다. 만들기 작업은 User.create 메서드를 호출하여 새 사용자를 만듭니다. 사용자가 성공적으로 생성되면 사용자가 로그인되고 홈 페이지로 리디렉션됩니다. 사용자가 성공적으로 생성되지 않으면 오류 메시지와 함께 양식이 다시 렌더링됩니다.

## 보기 만들기

이제 모델과 컨트롤러가 설정되었으므로 뷰 생성을 시작할 수 있습니다. Ruby on Rails에서 뷰는 웹 페이지의 HTML 코드를 포함하는 파일입니다. 애플리케이션의 각 페이지에 대해 하나의 보기 파일을 생성합니다.

첫 번째 보기 파일은 사용자 등록 양식용 파일입니다. app/views/users 디렉토리에 이 파일을 생성합니다. 파일 이름은 new.html.erb이며 다음 코드를 포함합니다.

    <%= form_for @user do |f| %>
      <%= f.레이블 :이름 %>
      <%= f.text_field :이름 %>
    
      <%= f.label :이메일 %>
      <%= f.text_field :이메일 %>
    
      <%= f.label :비밀번호 %>
      <%= f.password_field :암호 %>
    
      <%= f.label :암호_확인 %>
      <%= f.password_field :password_confirmation %>
    
      <%= f.제출 %>
    <% 종료 %>

이 코드는 새 사용자를 만들기 위한 양식을 만듭니다. 양식에는 이름, 이메일, 비밀번호 및 비밀번호 확인을 위한 필드가 있습니다. 양식은 UsersController의 만들기 작업에 제출됩니다.

## 경로 구성

이제 보기를 설정했으므로 경로를 구성해야 합니다. 경로는 애플리케이션이 응답하는 URL입니다. config/routes.rb 파일에서 경로를 구성합니다. 이 파일을 열고 다음 코드를 추가합니다.

    Rails.application.routes.draw 수행
      리소스 :사용자, 전용: [:new, :create]
    끝

이 코드는 두 개의 경로를 정의합니다. 하나는 새 작업에 대한 것이고 다른 하나는 UsersController의 만들기 작업에 대한 것입니다.

## 애플리케이션 테스트

이제 애플리케이션이 설정되었으므로 테스트할 수 있습니다. Rails 서버를 시작하여 시작하겠습니다.

    $ 레일 서버

그런 다음 웹 브라우저에서 http://localhost:3000으로 이동합니다. 사용자 등록 양식이 표시되어야 합니다. 양식을 작성하여 제출할 수 있습니다. 모든 것이 올바르게 작동하면 홈페이지가 표시됩니다.

## 결론

이 기사에서는 Kotlin과 함께 Ruby on Rails 프레임워크를 사용하여 웹 애플리케이션을 빌드하는 방법을 설명했습니다. 우리는 모델, 컨트롤러 및 보기를 만들었습니다. 또한 경로를 구성하고 애플리케이션을 테스트했습니다.