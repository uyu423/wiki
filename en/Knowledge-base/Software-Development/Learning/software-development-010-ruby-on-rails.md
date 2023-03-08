---
title: Software Development 010: Ruby on Rails
description: 
published: true
date: 2023-02-07T20:56:13.078Z
tags: 
editor: markdown
dateCreated: 2023-02-07T20:56:06.914Z
---

- [Desarrollo de software 010: Ruby on Rails***Spanish** document is available*](/es/Knowledge-base/Software-Development/Learning/software-development-010-ruby-on-rails)
{.links-list}
- [软件开发 010：Ruby on Rails***Chinese Simplified** document is available*](/zh/Knowledge-base/Software-Development/Learning/software-development-010-ruby-on-rails)
{.links-list}
- [소프트웨어 개발 010: Ruby on Rails***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-010-ruby-on-rails)
{.links-list}


# Software Development 010: Ruby on Rails

In this post, we'll be taking a comprehensive and practical look at Ruby on Rails - a popular web development framework written in the Ruby programming language.

We'll cover the following topics:

* What is Ruby on Rails?
* Rails MVC
* Installing Ruby on Rails
* Rails Directory Structure
* Rails Routes
* Rails Controllers
* Rails Models
* Rails Views
* Rails Helpers
* Rails Layouts
* Rails Assets
* Rails Mailers
* Rails ActiveRecord
* Rails ActionPack
* Rails ActionView
* Rails ActionMailer
* Rails ActiveSupport
* Rails Asset Pipeline

## What is Ruby on Rails?

Ruby on Rails is a web development framework written in the Ruby programming language. It is designed to make developing web applications easier and faster by providing a standard way to build and deploy them.

Rails is often used with the Ruby on Rails framework, which provides a set of tools and libraries that make it easier to develop web applications.

## Rails MVC

Ruby on Rails is based on the Model View Controller (MVC) architectural pattern. This is a common design pattern for web applications that helps to keep the code organized and easy to maintain.

The MVC pattern is made up of three parts:

* The **Model** is responsible for storing and retrieving data.
* The **View** is responsible for displaying data to the user.
* The **Controller** is responsible for handling user input and interactions.

## Installing Ruby on Rails

Before you can start developing with Ruby on Rails, you will need to install it on your computer.

There are a few different ways to install Ruby on Rails, but we will be using the RubyInstaller package.

1. Download the RubyInstaller package from the [RubyInstaller website](https://rubyinstaller.org/).

2. Run the installer and follow the prompts. Be sure to select the "Add Ruby executables to your PATH" option.

3. Once the installation is complete, open a new terminal window and type `ruby -v` to verify that Ruby is installed. You should see something like this:

```
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin18]
```

4. Now we need to install Rails. To do this, we will use the `gem` command, which is a package manager for Ruby. In the terminal, type `gem install rails`. This will install the latest version of Rails.

5. To verify that Rails is installed, type `rails -v`. You should see something like this:

```
Rails 5.2.3
```

## Rails Directory Structure

Now that we have Ruby on Rails installed, let's take a look at the directory structure of a Rails application.

A Rails application is made up of a number of different folders and files, each with a specific purpose.

Here is a list of the most important folders and files:

* The `app` folder contains the code for your application.
* The `bin` folder contains executable files for your application.
* The `config` folder contains configuration files for your application.
* The `db` folder contains the database files for your application.
* The `lib` folder contains library files for your application.
* The `log` folder contains the log files for your application.
* The `public` folder contains static files for your application.
* The `test` folder contains test files for your application.
* The `tmp` folder contains temporary files for your application.
* The `vendor` folder contains third-party code for your application.

## Rails Routes

Rails routes are used to map URLs to controller actions. They are defined in the `config/routes.rb` file.

For example, the following route would map the URL `/articles` to the `articles#index` action:

```ruby
get '/articles', to: 'articles#index'
```

Rails also supports wildcard routes, which can be used to map URLs to controller actions that take arguments.

For example, the following route would map the URL `/articles/:id` to the `articles#show` action:

```ruby
get '/articles/:id', to: 'articles#show'
```

## Rails Controllers

Rails controllers are responsible for handling user input and interactions. They are defined in the `app/controllers` folder.

Each controller is made up of a number of actions, which are methods that are responsible for handling a specific request.

For example, the `articles` controller might have an `index` action to handle requests for the `/articles` URL, and a `show` action to handle requests for the `/articles/:id` URL.

## Rails Models

Rails models are responsible for storing and retrieving data. They are defined in the `app/models` folder.

Each model represents a specific data type, such as an `Article` or a `User`. Models are typically used to store data in a database, but they can also be used to store data in other formats, such as XML or JSON.

Models can also be used to perform data validation, such as ensuring that an `Article` has a title and a body.

## Rails Views

Rails views are responsible for displaying data to the user. They are defined in the `app/views` folder.

Views are typically written in HTML, but they can also be written in other formats, such as XML or JSON.

Views can also use templates to DRY up their code. For example, a view that displays a list of articles might use a template that is responsible for displaying a single article.

## Rails Helpers

Rails helpers are modules that provide utility methods for use in views. They are defined in the `app/helpers` folder.

Helpers can be used to format data for display, such as converting a date to a human-readable format. They can also be used to generate HTML markup, such as links or form fields.

## Rails Layouts

Rails layouts are used to DRY up view code by defining a common layout for all views. They are defined in the `app/views/layouts` folder.

Layouts are typically written in HTML, but they can also be written in other formats, such as XML or JSON.

Layouts can also use templates to DRY up their code. For example, a layout that defines a common header and footer for all views might use a template that is responsible for displaying the content of a view.

## Rails Assets

Rails assets are static files that are used by your application, such as images, JavaScript files, or CSS files. They are stored in the `app/assets` folder.

Rails also provides a asset pipeline, which is a set of tools that can be used to process and compress assets.

## Rails Mailers

Rails mailers are used to send email from your application. They are defined in the `app/mailers` folder.

Mailers can be used to send notifications to users, such as password reset instructions or new article notifications.

## Rails ActiveRecord

Rails ActiveRecord is an object-relational mapping (ORM) library that is used to interact with databases. It is defined in the `activerecord` gem.

ActiveRecord provides a number of methods that make it easier to work with databases, such as `find` to retrieve data, and `save` to store data.

## Rails ActionPack

Rails ActionPack is a set of libraries that are used to build web applications. It is defined in the `actionpack` gem.

ActionPack provides a number of methods and classes that make it easier to develop web applications, such as `params` to access request parameters, and `render` to render views.

## Rails ActionView

Rails ActionView is a library that is used to render views. It is defined in the `actionview` gem.

ActionView provides a number of methods and classes that make it easier to render views, such as `render` to render views, and `partial` to render partial views.

## Rails ActionMailer

Rails ActionMailer is a library that is used to send email from your application. It is defined in the `actionmailer` gem.

ActionMailer provides a number of methods and classes that make it easier to send email, such as `mail` to send an email, and `attachments` to add attachments to an email.

## Rails ActiveSupport

Rails ActiveSupport is a set of utility classes and modules that are used by Rails. It is defined in the `activesupport` gem.

ActiveSupport provides a number of methods and classes that make it easier to work with Ruby objects, such as `Inflector` to pluralize and singularize words, and `Time` to format dates and times.

## Rails Asset Pipeline

Rails asset pipeline is a set of tools that can be used to process and compress assets. It is defined in the `sprockets` gem.

Asset pipeline provides a number of methods and classes that make it easier to work with assets, such as `uglifier` to compress JavaScript files, and `sass` to compile Sass files.

## Conclusion

In this post, we've taken a comprehensive and practical look at Ruby on Rails. We've covered a lot of ground, but there is still more to learn about this popular web development framework.

If you want to learn more about Ruby on Rails, check out the following resources:

* The [Ruby on Rails Guides](https://guides.rubyonrails.org/)
* The [Ruby on Rails API Documentation](https://api.rubyonrails.org/)
* The [Ruby on Rails Tutorial](https://www.railstutorial.org/)