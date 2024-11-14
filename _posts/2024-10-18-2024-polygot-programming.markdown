---
title: Beyond Swift and Kotlin
subtitle: The Polyglot Path for Mobile Developers
categories: [software development, Polyglot programming, polygot, programming language, mobile app development, Expanding programming skills, Mobile development roadmap, Mobile developer skills]
tags:
  [Mobile development, Polyglot programming, Swift programming, Kotlin programming, Expanding programming skills]
image: /images/polygot.png
---

The world of mobile development is constantly evolving. In my previous article, [_Embarking on a software developer journey_](https://medium.com/@tarang0510/embarking-on-a-software-developer-journey-3872c9ab5b79), I talked about how to approach software development using Polygot Path.

The articles [_Future of Mobile Apps_](https://medium.com/@tarang0510/the-future-of-mobile-apps-embracing-ai-and-addressing-privacy-60205657afcd) _and_ [_2024 Landscape Of Mobile Development_](https://medium.com/@tarang0510/the-2024-landscape-of-mobile-apps-development-8323a7a383b0) talks about how mobile development is evolving and what’s the potential future like.

While mastering Swift for iOS or Kotlin for Android is crucial, today’s mobile developers need a broader skill set to thrive in the industry. This article explores why expanding your programming language repertoire is essential and provides a roadmap from beginner to expert in multi-language proficiency.

Core Languages for Mobile Development
=====================================

At the heart of mobile development lie the platform-specific languages:

*   **iOS**: Swift and Objective-C
*   **Android**: Kotlin and Java

Mastering these languages is non-negotiable for any serious mobile developer. They form the foundation upon which you’ll build your career. However, stopping here would be a mistake in today’s interconnected development ecosystem.

Expanding Your Language Toolkit
===============================

Beyond the core languages, several other programming languages play crucial roles in the mobile development lifecycle:

Scripting Languages
===================

1.  **Python**: Though it is not widely known but there is a project called [**Kivy**](https://kivy.org/) that aims to build mobile apps using Python. There are slim chance you will ever use it but where Python shine is in scripting. Versatile and powerful, Python is excellent for automation, **data analysis, and server-side scripting**. Ofcourse if are interested in AI/ML, Python will be your ally.
2.  **Ruby**: Known for its simplicity and productivity, Ruby is often used in build scripts and backend services. If you used **Cocoapods** then you know it is written in Ruby. You have been editing Podfile in Ruby the whole time.
3.  **Shell scripting**: Essential for automating tasks in Unix-like environments, crucial for DevOps and CI/CD pipelines. This is very common type of scripting that can help with automation like setting up development environment, checking and verifying localization file, asset file, check for duplicates, rename files in a template project, etc…
4.  **JavaScript:** Building mobile apps using JS has been dream since begining. Cordova tried very hard and React Native did succeed upto certain extent. But other than that learning JS is still important as you might have to intercept, modify or capture certain user actions from your in-app browser. Or you might want to spin a simple mock server for your native app.

Build and Configuration Languages
=================================

**YAML:** It is a human-readable data serialization format that plays several important roles in mobile app development.

*   It’s particularly crucial in Android for **project configuration**, and **dependency management**.
*   It is used in **GitHub Action** workflow.
*   It is used in **Fastlane** configuration.
*   While Podfile uses Ruby syntax, **Pod specs** often use YAML format.
*   **SwiftGen** uses YAML for configuration in `swiftgen.yml`

**Groovy**: Particularly important for Android developers, as it’s the language used in Gradle build scripts. But it is also used in writing CI/CD jobs on Jenkins.

The most common use of Groovy in Android development is in Gradle build scripts (`build.gradle`)

*   Creating custom tasks for build automation
*   Managing dependencies using Groovy DSL

While Groovy isn’t directly used in iOS development like it is in Android, it can be utilized in various build and automation scripts.

Query Languages
===============

1.  **SQL**: Fundamental for working with databases, whether local on the device or for backend services. Knowning SQL is fundamental to any software development.
2.  **JQL (JIRA Query Language)**: Important for issue tracking and project management in many development teams if your team is using Jira, which most software teams are.

**Markup and Styling Languages**
================================

**XML:**

*   Android layout files
*   Resource definitions
*   Configuration files
*   iOS Plist and Nib files.

The Benefits of Language Diversity
==================================

Expanding your language skills offers numerous advantages:

1.  **Improved problem-solving**: Each language approaches problems differently, broadening your thinking.
2.  **Better understanding of programming concepts**: Exposure to various paradigms deepens your comprehension.
3.  **Increased adaptability**: Learning new languages becomes easier, making you more versatile.
4.  **Enhanced collaboration**: Communicate more effectively with team members across different specialties.

Simple Strategy
===============

*   Focus intensively on Swift (iOS) or Kotlin/Java (Android).
*   Learn fundamental programming concepts that transcend specific languages.
*   Introduce yourself to Python or Ruby for scripting.
*   Begin exploring build tools and automation, including basic shell scripting.
*   Integrate scripting into your development workflow for increased productivity. Like depedency management, automated testing, etc…
*   Focus on specific areas like CI/CD or database management.
*   Learn SQL and start applying it in your projects.
*   Contribute to open-source projects to apply and expand your skills.
*   Mentor junior developers, solidifying your own knowledge.
*   Stay updated with emerging technologies and languages.

Practical Tips for Learning Multiple Languages
==============================================

1.  Start with languages similar to those you already know to leverage existing knowledge.
2.  Focus on understanding concepts rather than memorizing syntax.
3.  Build projects that integrate multiple languages to see how they work together.
4.  Understand what language can be used in what situation and it’s support in the community.
5.  Participate in coding challenges and hackathons to apply your skills in diverse scenarios.

Real-world Applications
=======================

Understanding multiple languages isn’t just academic — it has practical benefits:

1.  **Improved Development Workflows**: Use Python or Ruby to automate repetitive tasks.
2.  **Enhanced CI/CD Pipelines**: Leverage shell scripting and Groovy for robust build processes.
3.  **Efficient Data Management**: Use SQL to optimize local and server-side data operations.
4.  **Cross-Platform Opportunities**: Your diverse skill set opens doors to hybrid and cross-platform development.

Other Notable Languages
=======================

As the Flutter platform has gained traction in recent years, the **Dart** language has seen tremendous success in mobile application development. Though this is considered cross-platform development, knowing Dart might come in handy one day.

Conclusion
==========

In the dynamic field of mobile development, being a polyglot programmer is increasingly valuable. By expanding your language skills beyond Swift or Kotlin, you’ll not only become a more effective developer but also open up new career opportunities.

Embrace the challenge of continuous learning, and you’ll find yourself well-equipped to tackle the ever-evolving landscape of mobile development.

Remember, the journey from beginner to expert is a marathon, not a sprint. Take it step by step, and don’t be afraid to explore new languages and paradigms along the way. Your future self will thank you for the diverse skill set you’re building today.