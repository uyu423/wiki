---
title: Kotlin and Ruby on Rails: Building a Web Application with a Ruby Framework
description: 
published: true
date: 2023-01-31T08:15:37.930Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:15:33.378Z
---

- [Kotlin 및 Ruby on Rails: Ruby 프레임워크로 웹 애플리케이션 구축***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-ruby-on-rails-building-a-web-application-with-a-ruby-framework)
{.links-list}
- [Kotlin と Ruby on Rails: Ruby フレームワークを使用した Web アプリケーションの構築***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/kotlin-and-ruby-on-rails-building-a-web-application-with-a-ruby-framework)
{.links-list}
- [Kotlin 和 Ruby on Rails：使用 Ruby 框架构建 Web 应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-ruby-on-rails-building-a-web-application-with-a-ruby-framework)
{.links-list}
 of provided code.

Kotlin and Ruby on Rails: Building a Web Application with a Ruby Framework

When you want to build a web application, you have many options for frameworks. Ruby on Rails is a popular framework for building web applications, and Kotlin is a language that is gaining popularity for its interoperability with Java and its safety features. In this article, we will show you how to build a web application using the Ruby on Rails framework with Kotlin.

We will assume that you are familiar with the basics of Kotlin and Ruby on Rails. If you are not, there are many resources available to learn more about these technologies.

## Setting up a Kotlin/Ruby on Rails Project

The first thing we need to do is set up a Kotlin/Ruby on Rails project. We will use the following tools:

* Kotlin 1.3.72
* Ruby 2.6.5
* Rails 6.0.3.2

You can use any versions of these tools that are compatible with each other.

To set up a new Kotlin/Ruby on Rails project, we will use the rails new command with the -api option and the -d option to specify the database. We will use a PostgreSQL database.

    $ rails new my_app -api -d postgresql

This will create a new directory called my_app with a basic Rails application.

## Configuring Kotlin

Next, we need to add Kotlin to our project. We will do this by adding the kotlin-rails plugin to our project's Gemfile.

    group :development do
      gem 'kotlin-rails'
    end

Then, we need to install the plugin.

    $ bundle install

Now that we have installed the plugin, we need to configure Kotlin. We will do this by creating a file called kotlin.yml in the config directory. In this file, we will add the following configuration:

    kotlin:
      version: 1.3.72
      targets:
        - jvm-1.8

This will tell Kotlin to use version 1.3.72 and to compile to Java 8 bytecode.

## Creating Models

Now that we have our project set up, we can start building our web application. We will start by creating some models. In Ruby on Rails, models are classes that represent the data in our application. We will create a model for each type of data in our application.

Our first model will be a model for users. We will generate this model using the rails generate command.

    $ rails generate model user

This will create a new file called app/models/user.rb. We will open this file and add the following code:

    class User < ApplicationRecord
      has_secure_password
    end

This code defines a new model called User. The has_secure_password macro adds some methods to our model to help us store passwords securely.

Next, we need to generate a migration for our model. A migration is a file that contains the SQL code to create or modify a database table. To generate a migration, we will use the rails generate command again.

    $ rails generate migration create_users

This will create a new file in the db/migrate directory. We will open this file and add the following code:

    class CreateUsers < ActiveRecord::Migration[6.0]
      def change
        create_table :users do |t|
          t.string :name
          t.string :email
          t.string :password_digest
          t.timestamps
        end
      end
    end

This code creates a new database table called users. The table has columns for a name, an email, and a password_digest. The password_digest column is where the has_secure_password macro will store the password hash.

Now that we have created our model and migration, we need to run the migration to create the database table. We can do this by running the following command:

    $ rails db:migrate

## Creating Controllers

Now that we have our models set up, we can start creating our controllers. In Ruby on Rails, controllers are classes that handle incoming HTTP requests. We will create one controller for each type of request we want to handle.

Our first controller will be a controller for user registration. We will generate this controller using the rails generate command.

    $ rails generate controller users

This will create a new file called app/controllers/users_controller.rb. We will open this file and add the following code:

    class UsersController < ApplicationController
      def new
        @user = User.new
      end
    
      def create
        @user = User.new(user_params)
    
        if @user.save
          session[:user_id] = @user.id
          redirect_to root_path
        else
          render :new
        end
      end
    
      private
    
      def user_params
        params.require(:user).permit(:name, :email, :password, :password_confirmation)
      end
    end

This code defines a new controller called UsersController. The controller has two actions, new and create. The new action renders a form for creating a new user. The create action calls the User.create method to create a new user. If the user is successfully created, the user is logged in and redirected to the home page. If the user is not successfully created, the form is rendered again with the error messages.

## Creating Views

Now that we have our models and controllers set up, we can start creating our views. In Ruby on Rails, views are files that contain the HTML code for our web pages. We will create one view file for each page in our application.

Our first view file will be a file for the user registration form. We will create this file in the app/views/users directory. The file will be called new.html.erb and it will contain the following code:

    <%= form_for @user do |f| %>
      <%= f.label :name %>
      <%= f.text_field :name %>
    
      <%= f.label :email %>
      <%= f.text_field :email %>
    
      <%= f.label :password %>
      <%= f.password_field :password %>
    
      <%= f.label :password_confirmation %>
      <%= f.password_field :password_confirmation %>
    
      <%= f.submit %>
    <% end %>

This code creates a form for creating a new user. The form has fields for a name, email, password, and password confirmation. The form is submitted to the create action of the UsersController.

## Configuring Routes

Now that we have our views set up, we need to configure our routes. Routes are the URLs that our application responds to. We will configure our routes in the config/routes.rb file. We will open this file and add the following code:

    Rails.application.routes.draw do
      resources :users, only: [:new, :create]
    end

This code defines two routes, one for the new action and one for the create action of the UsersController.

## Testing the Application

Now that we have our application set up, we can test it. We will start by starting the Rails server.

    $ rails server

Then, we will go to http://localhost:3000 in our web browser. We should see the user registration form. We can fill out the form and submit it. If everything works correctly, we should see the home page.

## Conclusion

In this article, we have shown you how to build a web application using the Ruby on Rails framework with Kotlin. We have created models, controllers, and views. We have also configured our routes and tested our application.