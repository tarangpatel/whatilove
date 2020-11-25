---
title: Architecting Mobile Apps
categories: [architecture, design patterns, mobile]
tags: [architecture, design patterns, mobile apps, software design, software architecture, MVVM, MVC, SOLID]
---
 
When developing mobile application we generally start by asking shall we use MVVM or VIPER? MVP gets to shine sometime but MVC gets completely side tracked by calling it massive view controller.

The truth is a software architecture is a combination of **various design patterns** applied using **key design principles** following **key design philosophies**.

This can sound confusing so let me break it down each individually. 

> Everything in software architecture is a trade-off.

## Design Patterns

There are three main categories of design patterns:


| Behavioral                              | Creational                | Structural                |
| ------------------------------------------------------ | ---------------------------------------- | ---------------------------------------- |
| 🐝 Chain Of Responsibility | 🌰 Abstract Factory | 🔌 Adapter                   |
| 👫 Command                                 | 👷 Builder                   | 🌉 Bridge                     |
| 🎶 Interpreter                         | 🏭 Factory Method     | 🌿 Composite               |
| 🍫 Iterator                               | 🔂 Monostate              | 🍧 Decorator               |
| 💐 Mediator                               | 🃏 Prototype              | 🎁 Façade                     |
| 💾 Memento                                 | 💍 Singleton               | 🍃 Flyweight               |
| 👓 Observer                               |                                           | ☔ Protection Proxy |
| 🐉 State                                     |                                           | 🍬 Virtual Proxy       |
| 💡 Strategy                               |                                          |                                          |
| 🏃 Visitor                                 |                                          |                                          |


These patterns were introduced in book [Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns#Patterns_by_type) by *Gang of Four*. There are lot of artciles and videos that explains each of these in details. I will suggest to please check them out.

All these patterns combines to make architectural patterns like MVC, MVVM, VIPER, REDUX. The decision to select an architectural pattern depends on the nature of the project. You can start with MVC pattern for your prototype but may progress towards MVVM for your final product. Even sticking with MVC will not be a bad idea given following design principles are applied properly.

## Design Principles

Design patterns alone will not give us best architecture. These patterns need to follow certain principles that will make them work better together and in turn soldifies the architcture of an application. 
These are some of the well known princiles:

* SOLID
* KISS
* YAGNI
* DRY

The main idea is to keep your code simple, maintain seperate of concern, expose whatever is necessary and remove redudant code. 

## Design Philosophies

Where design principles are *how* of the software design, design philosophies are the *why* and *what*.
Why do we use design patterns and what problems does it solve? 

 1. It hides complexity and provide simpler interface
 2. Provides stability and robustness to the code base
 3. To write reusable code
 4. To make application modular
 5. Makes code communicate better
 6. Makes easier to modify and maintain
 7. Easy to test
 8. Reduce development and maintenance cost
 9. Keeps developers happy and motivated
 10. Improve overall SDLC

When architecting mobile application first we need to find out the nature of the application. Application can be divided into following categories:

- Static app that displays static contents. Data can be either in a databse locally or static file.
- Dynamic app that loads the data from outside the device. It can further broken down into 2 main categories: 
    * Real time: Updated app based on events occuring for eg: chat, live sport, uber location
    * Non-real time: Basically covers most of the apps where app will ask for data from the backend
    