---
title: Robert C. Martin
description: 
published: true
date: 2023-02-02T17:24:44.094Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:24:38.987Z
---

- [Robert C. Martin***Japanese** document is available*](/ja/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}
- [Robert C. Martin***Spanish** document is available*](/es/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}
- [Robert C. Martin***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}
- [Robert C. Martin***Korean** document is available*](/ko/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}


# Overview 
Robert C. Martin (also known as Uncle Bob) is a renowned software engineer, author, and speaker. He is well-known for his work on software design principles, such as the SOLID principles, and his writing on software engineering and software craftsmanship. He is a strong advocate of agile software development practices and has written several books on the subject.

# Description
Robert C. Martin is a software engineer, author, and speaker who is well-known for his work on software design principles, such as the SOLID principles, and his writing on software engineering and software craftsmanship. He is a strong advocate of agile software development practices and has written several books on the subject.

Martin is the founder of the successful consulting firm, Object Mentor Inc., and is the author of several books, including "Clean Code: A Handbook of Agile Software Craftsmanship" and "The Clean Coder: A Code of Conduct for Professional Programmers". He is also the creator of the popular software architecture and design framework, Uncle Bob's Architecture.

Martin is a strong advocate of software craftsmanship and the importance of writing clean, maintainable code. He is a frequent speaker at conferences, and has given many talks on topics such as software design, software testing, and software engineering best practices.

# History
Robert C. Martin was born in 1952 in Pennsylvania, and graduated from the University of Massachusetts in 1976 with a degree in Computer Science. After graduation, he began working as a software engineer and has since held various positions in the software industry.

In the late 1980s, Martin began working on the SOLID principles, which are a set of five software design principles that provide a framework for creating maintainable and extensible software. In the mid-1990s, he began writing on software engineering and software craftsmanship, and in 2000, he founded Object Mentor Inc., a successful consulting firm. 

Since then, Martin has written several books, including "Clean Code: A Handbook of Agile Software Craftsmanship" and "The Clean Coder: A Code of Conduct for Professional Programmers". He is also the creator of the popular software architecture and design framework, Uncle Bob's Architecture.

# Features
The SOLID principles are the cornerstone of Robert C. Martin's work, and are a set of five software design principles that provide a framework for creating maintainable and extensible software. These principles are: 

- Single Responsibility Principle: A class should have one and only one reason to change.
- Open-Closed Principle: Software entities should be open for extension, but closed for modification.
- Liskov Substitution Principle: Derived classes must be substitutable for their base classes.
- Interface Segregation Principle: Clients should not be forced to depend on methods they do not use.
- Dependency Inversion Principle: Depend on abstractions, not on concretions.

Martin is also a strong advocate of software craftsmanship and the importance of writing clean, maintainable code. He has written several books and given many talks on topics such as software design, software testing, and software engineering best practices.

# Example
As an example of how the SOLID principles can be applied, consider the following code:

```
class Database {
  public void save(String data) {
    // code to save data to the database
  }
 
  public void delete(String data) {
    // code to delete data from the database
  }
}
```

This code violates the Single Responsibility Principle, as both saving and deleting data are handled in the same class. To adhere to the principle, the code should be refactored to create two separate classes - one for saving data, and one for deleting data.

# Pros and Cons
The SOLID principles are a set of five software design principles that provide a framework for creating maintainable and extensible software. The main benefit of these principles is that they make it easier to maintain and extend code, as each class has a single responsibility and is open for extension but closed for modification.

However, there are some drawbacks to these principles. For example, it can be difficult to adhere to the Single Responsibility Principle when designing complex systems, and it can take more time and effort to refactor code to adhere to the principles.

# Controversy
Martin's work on software design principles and software craftsmanship has been met with some controversy. Some have argued that the SOLID principles are too rigid and can lead to overly complicated code. Others have argued that Martin's focus on software craftsmanship can lead to a focus on "perfect" code, which can be time consuming and not always necessary.

# Related Technology
The SOLID principles are closely related to the DRY (Don't Repeat Yourself) principle, which states that code should not be repeated unnecessarily. The DRY principle is often used in conjunction with the SOLID principles to create maintainable and extensible code.

# Digression
Martin is also a strong advocate of agile software development practices. He has written several books on the subject, including "Agile Software Development: Principles, Patterns, and Practices" and "The Agile Manifesto".

# Others
In addition to his work on software design and agile software development, Martin is also a strong advocate of software testing. He has written several books on the subject, including "The Art of Software Testing" and "Test-Driven Development: By Example".