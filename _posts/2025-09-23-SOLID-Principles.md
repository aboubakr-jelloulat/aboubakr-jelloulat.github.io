---
title: "SOLID Principles: Building Better Software Architecture"
date: 2025-09-23
categories: [Architecture, SOLID Principles]
tags: [clean code, SOLID, SRP, OCP, LSP, ISP, DIP, software design, object-oriented programming]
toc: true
---

# **SOLID Principles: Building Better Software Architecture**



## **Table of Contents**

1. [**Introduction**](#introduction)
2. [**What are SOLID Principles?**](#what-are-solid-principles)
3. [**Single Responsibility Principle (SRP)**](#single-responsibility-principle-srp)
4. [**Open/Closed Principle (OCP)**](#openclosed-principle-ocp)


---

## **Introduction**

Have you ever looked at a piece of code and thought, "This is a mess"? We've all been there. Code that's hard to read, difficult to modify, and breaks whenever you touch it. The good news is that there's a way to avoid this nightmare  and it starts with understanding the SOLID principles.

In this comprehensive guide, we'll explore one of the most fundamental concepts in software engineering. Keep in mind that no single tutorial can make you an expert you need consistent practice. This tutorial is meant to introduce you to the basic concepts. Also, be aware that there might be mistakes, so use it as a starting point rather than a definitive guide.


---
## **What are SOLID Principles?**

>The SOLID principles are a set of five design principles that help developers create more maintainable, flexible, and scalable software. Introduced by Robert C. Martin , these principles serve as guidelines for writing clean, object-oriented code that stands the test of time.

**SOLID** is an acronym that stands for:

- **S** - Single Responsibility Principle (SRP)
- **O** - Open/Closed Principle (OCP)
- **L** - Liskov Substitution Principle (LSP)
- **I** - Interface Segregation Principle (ISP)
- **D** - Dependency Inversion Principle (DIP)

These principles aren't just theoretical concepts  they're practical tools that solve real problems developers face every day. When applied correctly, they help create code that is:

- **Easy to understand**: Each component has a clear, single purpose
- **Simple to modify**: Changes can be made without breaking existing functionality
- **Highly testable**: Components can be tested in isolation
- **Reusable**: Well-designed components can be used across different parts of your application
- **Maintainable**: The codebase remains clean and organized as it grows

---


## Single Responsibility Principle (SRP)

### Core Concept

**A module should have one and only one reason to change.**


>The Single Responsibility Principle is the cornerstone of clean architecture, as emphasized by Robert C. Martin in his book "Clean Architecture." At its core, SRP states that every software module, class, or function should have responsibility over a single part of the functionality and should encapsulate that part completely.

>But what does "single responsibility" really mean? It's not about doing only one thing—it's about having only one reason to change. As Uncle Bob explains, this principle is fundamentally about people. When you write a class, you should identify the actors (users, stakeholders, or systems) who might request changes to that class. If multiple actors could request changes for different reasons, then the class violates SRP.


### Example: Violating SRP

Let's look at a common violation of SRP  a class that handles both user data and email notifications:

!["Violating SRP Example"](/assets/img/carbon.png)


#### Problems with this approach 

- **_Changes to email logic require modifying UserManager_**
- **_Changes to database logic also require modifying UserManager_**
- **_The class becomes harder to test and maintain_**


### Example: Following SRP


Here's how we can refactor this to follow SRP:



!["Following SRP Example"](/assets/img/solutionsSRP.png) 


#### SRP Benefits and Architecture

This refactored design aligns perfectly with clean architecture principles:

- **_UserRepository: Represents the data layer, handling persistence concerns_**

- **_EmailService: Represents external service integration, handling notification concerns_**

- **_UserService: Represents the use case layer, orchestrating business logic_**

- **_User: Represents the entity layer, containing core business data_**

Each class now has a single, well defined responsibility and can evolve independently. Changes to email logic only affect EmailService, database changes only affect UserRepository, and business logic changes only affect UserService.


---


## Open/Closed Principle (OCP)


### Core Concept

**Software entities should be open for extension but closed for modification.**

>The Open/Closed Principle, as articulated by Robert C. Martin in "Clean Architecture," represents one of the most powerful concepts in software design. This principle states that you should be able to extend a class's behavior without modifying its source code. In essence, your code should be open for extension but closed for modification.

>The genius of OCP lies in its ability to protect existing, working code from changes while still allowing new functionality to be added. As Uncle Bob emphasizes, this principle is the heart of object-oriented design it's what makes code flexible, reusable, and maintainable. When properly applied, OCP allows systems to be easily extended with new functionality without risking the stability of existing features.

### Example: Violating OCP

Let's examine a common violation of OCP a class that handles different notification types using conditional statements:

!["Violating OCP"](/assets/img/OCPViolatingOCP.png) 


#### Problems with this approach

- **_Adding new notification types requires modifying the NotificationService classs_**

- **_Risk of breaking existing functionality when adding new featuress_**

- **_Violates the principle that classes should be closed for modifications_**

- **_Testing becomes more complex as the class growss_**

### Example: Following OCP

Here's how we can refactor this design to follow OCP using interfaces:


!["Following OCP"](/assets/img/FollowingOCP.png) 


#### OCP Benefits and Architecture

This refactored design embodies the essence of clean architecture and OCP:

- **_Shape (Abstract Interface): Defines the contract that all shapes must follows_**

- **_Concrete Shape Classes: Each encapsulates its own area calculation logics_**

- **_AreaCalculator: Depends on the abstraction, not concrete implementationss_**

- **_Extensibility: New shapes can be added without touching existing codes_**




---


## Liskov Substitution Principle (LSP)

### Core Concept
**you should be able to use any derived class instead of a parent class and have it behave in the same manner without modification.**


>The Liskov Substitution Principle, named after Barbara Liskov, is perhaps the most misunderstood of the SOLID principles. At its essence, LSP states that you should be able to use any derived class instead of a parent class and have it behave in the same manner without modification. It ensures that a derived class does not affect the behavior of the parent class in other words, a derived class must be substitutable for its base class.


>Think of it this way: if you have a function that works with a base class, it should work equally well with any of its subclasses without knowing which specific subclass it's dealing with. As Robert C. Martin explains in "Clean Architecture," this principle is what makes inheritance truly powerful and safe. When LSP is violated, you end up with fragile code that requires constant type checking and conditional logic.


### Example: Violating LSP

Let's look at a game engine where different character types have different capabilities:

!["Violating LSPP Example"](/assets/img/ViolatingLSP.png)


#### Problems with this approach

- **_Ghost throws exception for Jump(), breaking substitutability_**
- **_Client code must know specific types to avoid calling Jump() on ghosts_**
- **_Violates LSP because you can't safely replace PlayerCharacter with Ghost_**
- **_Forces meaningless or error-prone implementations in subclasses_**



### Example: Following LSP

Here's how we can refactor this design to follow LSP using proper interfaces:

!["Following LSP Example"](/assets/img/FollowingLSP.png)


#### LSP Benefits and Architecture

This refactored design perfectly demonstrates clean architecture and LSP compliance:

- **_PlayerCharacter (Base Class): Contains only behavior that ALL characters share_**

- **_ICanJump Interface: Segregates jumping capability to only characters that can jump_**

- **_Warrior: Implements both character movement and jumping capability_**

- **_Ghost: Implements only character movement, staying true to its ethereal nature_**

- **_Substitutability: Any PlayerCharacter can be used interchangeably without breaking client code_**