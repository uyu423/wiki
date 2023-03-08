---
title: Kotlin と Ruby on Rails: Ruby フレームワークを使用した Web アプリケーションの構築
description: 
published: true
date: 2023-01-31T08:15:36.086Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:15:33.380Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and Ruby on Rails: Building a Web Application with a Ruby Framework***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-ruby-on-rails-building-a-web-application-with-a-ruby-framework)
{.links-list}
 提供されたコードの。

KotlinとRuby on Rails：RubyフレームワークでWebアプリケーションを構築する

Webアプリケーションを構築する場合は、フレームワークの多くのオプションがあります。 Ruby on RailsはWebアプリケーションの構築に広く使用されているフレームワークであり、KotlinはJavaとの相互運用性とセキュリティ機能で人気を集めている言語です。この記事では、KotlinでRuby on Railsフレームワークを使用してWebアプリケーションを構築する方法について説明します。

KotlinとRuby on Railsの基本に慣れているとします。そうでない場合は、これらの技術の詳細を学ぶための多くのリソースがあります。

# # Kotlin/Ruby on Rails プロジェクト設定

最初にすべきことは、Kotlin / Ruby on Railsプロジェクトを設定することです。次のツールを使用してください。

*コトリン1.3.72
*ルビー2.6.5
* Rails 6.0.3.2

互換性のあるこれらのツールのすべてのバージョンを使用できます。

新しいKotlin / Ruby on Railsプロジェクトを設定するには、-apiオプションと-dオプションを指定してrails newコマンドを使用してデータベースを指定します。 PostgreSQLデータベースを使用します。

    $ rails new my_app -api -d postgresql

これにより、デフォルトのRailsアプリケーションを持つmy_appという名前の新しいディレクトリが作成されます。

# # Kotlinの設定

次に、プロジェクトにKotlinを追加する必要があります。プロジェクトのGemfileにkotlin-railsプラグインを追加してこれを行います。

    グループ：development do
      ジュエリー「kotlin-rails」
    終わり

その後、プラグインをインストールする必要があります。

    $バンドルのインストール

これでプラグインをインストールしたので、Kotlinを設定する必要があります。 configディレクトリにkotlin.ymlというファイルを作成してこれを行います。このファイルに次の構成を追加します。

    コトリン:
      バージョン: 1.3.72
      対象：
        - jvm-1.8

これにより、Kotlinはバージョン1.3.72を使用してJava 8バイトコードにコンパイルするように指示します。

## モデルの作成

これでプロジェクトが設定されたので、Webアプリケーションの構築を開始できます。いくつかのモデルを作ることから始めましょう。 Ruby on Railsでは、モデルはアプリケーションのデータを表すクラスです。アプリケーションの各データ型のモデルを生成します。

私たちの最初のモデルはあなたのためのモデルになります。 rails generateコマンドを使用してこのモデルを生成します。

    $レールはモデルユーザーを作成します。

これにより、app/models/user.rb という新しいファイルが作成されます。このファイルを開き、次のコードを追加します。

    クラスユーザー< ApplicationRecord
      has_secure_password
    終わり

このコードは、Userという新しいモデルを定義します。 has_secure_passwordマクロは、パスワードを安全に保存するのに役立ついくつかの方法をモデルに追加します。

次に、モデルの移行を作成する必要があります。マイグレーションは、データベース表を作成または変更するためのSQLコードを含むファイルです。移行を生成するには、rails generate コマンドを再利用します。

    $レール生成の移行 create_users

これにより、db / migrateディレクトリに新しいファイルが作成されます。このファイルを開き、次のコードを追加します。

    クラス CreateUsers < ActiveRecord::Migration[6.0]
      デフチェンジ
        create_table :ユーザーの実行 |t|
          t.文字列：名前
          t.string :Eメール
          t.string :password_digest
          t.タイムスタンプ
        終わり
      終わり
    終わり

このコードは、usersという名前の新しいデータベーステーブルを作成します。テーブルには、名前、電子メール、およびpassword_digestの列があります。 password_digest 列は、has_secure_password マクロがパスワードハッシュを格納する場所です。

これでモデルと移行を作成したので、移行を実行してデータベーステーブルを作成する必要があります。次のコマンドを実行してこれを実行できます。

    $レールdb：移行

## コントローラの作成

これでモデルが設定されたので、コントローラの作成を開始できます。 Ruby on Railsでは、コントローラは着信HTTPリクエストを処理するクラスです。処理する要求タイプごとに1つのコントローラを作成します。

最初のコントローラはユーザー登録のためのコントローラになります。 rails generateコマンドを使用してこのコントローラを作成します。

    $レールはコントローラーユーザーを作成します。

これにより、app/controllers/users_controller.rbという新しいファイルが作成されます。このファイルを開き、次のコードを追加します。

    クラス UsersController < ApplicationController
      新しいデフ
        @ユーザー=ユーザー。新規
      終わり
    
      デフ生成
        @user = User.new(user_params)
    
        @user.saveの場合
          セッション[:user_id] = @user.id
          redirect_to root_path
        もう一つ
          レンダリング：新しい
        終わり
      終わり
    
      プライベート
    
      def user_params
        params.require(:user).permit(:name, :email, :password, :password_confirmation)
      終わり
    終わり

このコードはUsersControllerという新しいコントローラを定義します。コントローラにはnewとcreateの2つのタスクがあります。新しいアクションは、新しいユーザーを作成するためのフォームをレンダリングします。作成操作では、User.create メソッドを呼び出して新しいユーザーを作成します。ユーザーが正常に作成されると、ユーザーはログインしてホームページにリダイレクトされます。ユーザーが正常に作成されなかった場合は、エラーメッセージとともにフォームが再レンダリングされます。

# #ビューの作成

これでモデルとコントローラが設定されているので、ビューの作成を開始できます。 Ruby on Railsでは、ビューはWebページのHTMLコードを含むファイルです。アプリケーションの各ページに1つのビューファイルを作成します。

最初のビューファイルはユーザー登録フォーム用のファイルです。 app/views/users ディレクトリにこのファイルを生成します。ファイル名はnew.html.erbで、次のコードが含まれています。

    <%= form_for @user do |f| %>
      <％= f.ラベル：名前％>
      <%= f.text_field: 名前 %>
    
      <%= f.label :Eメール%>
      <%= f.text_field : メール %>
    
      <%= f.label :パスワード %>
      <%= f.password_field :パスワード %>
    
      <%= f.label :パスワード_確認 %>
      <%= f.password_field :password_confirmation %>
    
      <%= f.送信%>
    <%終了%>

このコードは新しいユーザーを作成するためのフォームを作成します。フォームには、名前、Eメール、パスワード、およびパスワードを確認するためのフィールドがあります。フォームはUsersControllerの作成操作に送信されます。

# # パスの設定

これでビューを設定したので、パスを設定する必要があります。パスはアプリケーションが応答するURLです。 config/routes.rb ファイルでパスを構成します。このファイルを開き、次のコードを追加します。

    Rails.application.routes.drawの実行
      リソース :ユーザー、専用: [:new, :create]
    終わり

このコードは2つのパスを定義します。 1つは新しいタスクのためのものであり、もう1つはUsersControllerの作成タスクのためのものです。

## アプリケーションテスト

これでアプリケーションが設定されているのでテストできます。 Railsサーバーを起動して起動します。

    $レールサーバー

その後、Webブラウザでhttp://localhost：3000に移動します。ユーザー登録フォームが表示されます。フォームに記入して送信できます。すべてが正しく機能すると、ホームページが表示されます。

## 結論

この記事では、KotlinでRuby on Railsフレームワークを使用してWebアプリケーションを構築する方法について説明しました。私たちはモデル、コントローラー、ビューを作成しました。また、パスを設定してアプリケーションをテストしました。