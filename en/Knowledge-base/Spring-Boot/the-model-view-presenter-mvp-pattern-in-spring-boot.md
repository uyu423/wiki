---
title: The Model-View-Presenter (MVP) Pattern in Spring Boot
description: 
published: true
date: 2023-01-31T11:23:22.399Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:23:18.890Z
---

- [Spring Boot의 MVP(Model-View-Presenter) 패턴***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/the-model-view-presenter-mvp-pattern-in-spring-boot)
{.links-list}
- [Spring Boot の Model-View-Presenter (MVP) パターン***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/the-model-view-presenter-mvp-pattern-in-spring-boot)
{.links-list}
- [Spring Boot 中的模型-视图-呈现器 (MVP) 模式***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/the-model-view-presenter-mvp-pattern-in-spring-boot)
{.links-list}


  The MVP pattern is a derivative of the MVC pattern that is used to create user interfaces. It is a popular choice for web applications as it separates the concerns of the application into three distinct parts: the model, the view, and the presenter. This separation of concerns makes the code more maintainable and easier to test.

The MVP pattern is similar to the MVC pattern in that it also has a model, view, and controller. However, the MVP pattern has a few key differences. First, the MVP pattern does not have a direct connection between the view and the model. Instead, the presenter acts as a mediator between the two. This allows the view and the model to be completely independent of each other. Second, the MVP pattern places more emphasis on the presenter. The presenter is responsible for handling all the user input and updating the view accordingly.

There are many benefits to using the MVP pattern. First, it makes it easier to unit test the code. Second, it makes it easier to change the user interface without having to change the underlying code. Third, it makes it easier to reuse the code for other purposes.

If you're interested in using the MVP pattern in your next Spring Boot project, there are a few things you need to keep in mind. First, you need to create a separate presenter class for each view. Second, you need to inject the presenter into the view. Third, you need to bind the view to the presenter. Fourth, you need to wire the presenter to the model. And finally, you need to register the view with the presenter.

Once you've done all of that, you're ready to start using the MVP pattern in your Spring Boot project.