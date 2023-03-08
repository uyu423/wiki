---
title: The Model-View-ViewModel (MVVM) Pattern in Spring Boot
description: 
published: true
date: 2023-02-08T12:32:42.006Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:32:36.161Z
---

- [El patrón Model-View-ViewModel (MVVM) en Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/the-model-view-viewmodel-mvvm-pattern-in-spring-boot)
{.links-list}
- [Spring Boot 中的模型-视图-视图模型 (MVVM) 模式***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/the-model-view-viewmodel-mvvm-pattern-in-spring-boot)
{.links-list}
- [Spring Boot의 MVVM(Model-View-ViewModel) 패턴***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/the-model-view-viewmodel-mvvm-pattern-in-spring-boot)
{.links-list}


# The Model-View-ViewModel (MVVM) Pattern in Spring Boot

The Model-View-ViewModel (MVVM) is an architectural design pattern that separates an application into three main logical components Model, View, and ViewModel. 

The main idea behind MVVM is to move the bulk of business logic and data manipulation away from the View layer into the ViewModel layer. This helps to clean up and decouple the code, making the application more maintainable and testable. 

The ViewModel then exposes data relevant to the View through observables. The ViewModel also exposes commands that the View can bind to. This gives the ViewModel full control over the View without the View having to know about the ViewModel. 

## Model

The Model represents the data and business logic of the application. In a MVVM application the Model does not know about the ViewModel and therefore it does not have any dependencies on the ViewModel. 

The Model is responsible for managing the data of the application. It responds to requests for data and notifies observers when the data changes. 

The Model also contains the business logic of the application. This is the logic that manipulates the data and enforces the business rules of the application. 

## View

The View is responsible for displaying the data and invoking operations on the ViewModel. 

The View should not contain any logic that manipulates the data or enforces the business rules of the application. This logic should be contained in the ViewModel. 

The View should also not be aware of the existence of the ViewModel. The ViewModel should be completely independent of the View. 

## ViewModel

The ViewModel is responsible for providing data to the View and for processing the user input. 

The ViewModel exposes data to the View through observables. The ViewModel also exposes commands that the View can bind to. 

The ViewModel contains the logic that manipulates the data and enforces the business rules of the application. The ViewModel also contains the code that is specific to the View. 

The ViewModel should not be aware of the View. The ViewModel should be completely independent of the View. 

## Data Binding

Data binding is a mechanism that allows the View and ViewModel to be automatically synchronized. 

Data binding allows the ViewModel to update the View automatically when the data in the ViewModel changes. Data binding also allows the View to update the ViewModel automatically when the user input changes. 

Data binding is a two-way process. Changes made to the data in the View are propagated to the ViewModel. Changes made to the data in the ViewModel are propagated to the View. 

Data binding is a powerful mechanism that helps to keep the View and ViewModel synchronized. 

## Conclusion

The Model-View-ViewModel (MVVM) is an architectural design pattern that separates an application into three main logical components Model, View, and ViewModel. 

The main idea behind MVVM is to move the bulk of business logic and data manipulation away from the View layer into the ViewModel layer. This helps to clean up and decouple the code, making the application more maintainable and testable. 

The ViewModel then exposes data relevant to the View through observables. The ViewModel also exposes commands that the View can bind to. This gives the ViewModel full control over the View without the View having to know about the ViewModel. 

Data binding is a mechanism that allows the View and ViewModel to be automatically synchronized. Data binding is a powerful mechanism that helps to keep the View and ViewModel synchronized. 

## References

1. [The Model-View-ViewModel (MVVM) Pattern](https://msdn.microsoft.com/en-us/library/hh848246.aspx)
2. [Model View ViewModel (MVVM) Explained](https://www.codeproject.com/Articles/100175/Model-View-ViewModel-MVVM-Explained)
3. [MVVM Light Toolkit](http://www.mvvmlight.net/)
4. [Data Binding in MVVM](https://www.tutorialspoint.com/mvvm/mvvm_data_binding.htm)