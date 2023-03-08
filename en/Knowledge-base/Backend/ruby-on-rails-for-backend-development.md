---
title: Ruby on Rails for Backend Development
description: 
published: true
date: 2023-02-18T15:32:41.471Z
tags: 
editor: markdown
dateCreated: 2023-02-18T15:32:34.606Z
---

- [백엔드 개발을 위한 Ruby on Rails***Korean** document is available*](/ko/Knowledge-base/Backend/ruby-on-rails-for-backend-development)
{.links-list}


# Ruby on Rails for Backend Development

Ruby on Rails is a web application framework written in Ruby. It is designed to make programming web applications easier by making assumptions about what every developer needs to get started. It allows you to write less code while accomplishing more than many other frameworks and libraries.

## Why Ruby on Rails?

Ruby on Rails is a great choice for backend development for a number of reasons:

- It is a **full-stack** framework, meaning it provides all the tools you need to create a complete web application. This includes everything from the routing to the database to the front-end.

- It has a large and supportive **community**. Because Ruby on Rails is an open source project, there is a community of developers who are constantly improving the framework and creating helpful resources.

- It is a **convention-over-configuration** framework, meaning that it relies on conventions to minimize the amount of configuration required. This makes development faster and easier.

- It is a **DRY** framework, meaning that it emphasizes code reuse. This makes your code more maintainable and easier to scale.

## Getting Started

Before you can start developing with Ruby on Rails, you will need to install it. The easiest way to do this is with the [Ruby on Rails Installer](http://railsinstaller.org/). This will install Ruby, Rails, and all of the other dependencies you need to get started.

Once you have Ruby on Rails installed, you can create a new project with the `rails new` command:

```
$ rails new my_app
```

This will create a new directory called `my_app` with all of the files you need to get started.

## Hello, World!

Now that you have a new Ruby on Rails project, let's create a simple "Hello, World!" application.

First, you need to create a new controller. A controller is responsible for handling requests from the user and returning a response. In Ruby on Rails, controllers are stored in the `app/controllers` directory.

To create a new controller, you can use the `rails generate` command:

```
$ rails generate controller Welcome index
```

This will create a new file called `app/controllers/welcome_controller.rb` with the following contents:

```ruby
class WelcomeController < ApplicationController
  def index
  end
end
```

Next, you need to create a view. A view is responsible for displaying the response from the controller. In Ruby on Rails, views are stored in the `app/views` directory.

To create a new view, you can create a new file called `app/views/welcome/index.html.erb` with the following contents:

```
<h1>Hello, World!</h1>
```

Now that you have a controller and a view, you need to tell Ruby on Rails how to route requests to your controller. This is done in the `config/routes.rb` file:

```ruby
Rails.application.routes.draw do
  get 'welcome/index'
end
```

This tells Ruby on Rails that any requests to the `/welcome` path should be handled by the `WelcomeController` controller.

Finally, you need to start the Ruby on Rails server:

```
$ rails server
```

You can now visit http://localhost:3000/welcome/index in your web browser to see your "Hello, World!" application.

## Resources

- [Ruby on Rails Guides](http://guides.rubyonrails.org/)
- [Ruby on Rails API Documentation](http://api.rubyonrails.org/)
- [Ruby on Rails Tutorial](http://ruby.railstutorial.org/)