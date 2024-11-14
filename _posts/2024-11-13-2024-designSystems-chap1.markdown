---
title: The Missing Piece in Mobile Development - Design Tokens
subtitle: Chapter 1
categories: [Mobile development, Design systems, UI consistency, Mobile app design, iOS development, Android development, Design system tools, Storybook, Figma plugins, UIKit customizations, Material Design overrides, Design debt, Pixel-perfect consistency, Design handoff, Styled-components, Design guidelines, Design graveyard, Component libraries, Dark mode implementation, Banking app UI, Design review meetings]
tags:
  [Mobile development, Design systems, iOS development, Android development, Design system tools]
image: /images/DesignSystems/designSystems.png
---

The design step is a crucial phase within the overall design process, where designers shape the visual identity, interaction, and user experience of a product or application. This step involves a series of interconnected stages, each playing a vital role in the creation of a cohesive and consistent design system.

The Design Process Stages
=========================

1.  **Discovery and Research**
2.  **Ideation and Conceptualization**
3.  **Wireframing and Prototyping**
4.  **Visual Design**
5.  **Design System Creation**
6.  **Design Implementation and Handoff**

The first 4 stages are related to product development hence it is out of scope for this series. Last two stages are important which will layout the foundation of Design System and how well it works with software development lifecycle (SDLC). Let’s dive a bit deeper into it.

**Design System Creation**
==========================

As the product design matures, designers begin to codify the various design elements and patterns into a centralized design system. This system serves as a single source of truth, ensuring consistency and scalability across the entire product ecosystem.

At this stage _design tokens_ are introduced into the design system.

> **Design tokens** are design decisions, translated into data. They act as a “source of truth” to help ensure that product experiences feel unified and cohesive[1].

![Typography, Spacing, Corner Radius, Color](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*yiOQEkz2-k-v3v0kemBL3Q.png)

**Tokens** are the fundamental building blocks that power a design system. These tokens encapsulate the various design definitions needed to construct a cohesive and scalable user experience. They can represent a wide range of design elements, including:

*   Color values (e.g., RGB, hex, HSL)
*   Typographic attributes (e.g., font family, size, weight, line height)
*   Spacing and layout metrics (e.g., padding, margin, grid)
*   Animation properties (e.g., duration, easing, delay)
*   Elevation and shadow properties
*   Border styles

By abstracting these design decisions into reusable tokens, organizations can ensure consistent application of the design system across multiple products and platforms. This token-based approach allows the design system to scale and adapt to the evolving needs of the ecosystem, without relying on hard-coded values that can quickly become outdated or difficult to maintain. The centralized management of design tokens empowers designers and developers to work in harmony, delivering a seamless and cohesive user experience.

Types of Tokens
---------------

Tokens can be categorized in two types: _Global Tokens and Component Tokens_

*   **Global Tokens or Primitive Tokens**: As name suggests it is used globally in the design systems. For example it is used in Themeing the overall look and feel of the app. It can provides consistent spacing, color and typography to all the pages of the app.
*   **Component Tokens or Semantic Tokens:** These tokens are component specific. In an app you might some views that require specific size, spacing or corner radius than other components. For example an Avatar can be of multiple sizes, and it has a specific corner radius which will not be same for iteam image view.

> A good design system breaks down large views into small components/views. Each components are specific views like button, image, label or textField. A screen/page/viewController is created by composing multiple components. Think about atoms and molecules. An object is made by combining multiple molecules and molecules are made or combining multiple atoms. This is a good read to understand [Atomic Design](https://atomicdesign.bradfrost.com/).

![Composing components to form a view](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*HPZGQyYsKGOBv2UooXMufQ.png)

**Alias Token**

There is one more token type called **Alias.** This token references another token, instead of referencing a hard-coded value.

**Alias tokens**, also known as **semantic tokens**, play a crucial role in design systems by creating relationships between global tokens and specific contexts.

*   They create clear connections between visual attributes and their intended purpose in the UI.
*   They allow for easy theme switching by simply updating the values referenced by alias tokens.
*   They provide consistent design language.
*   They provide a centralized way to manage color schemes, typography, and other visual attributes across an entire product [2].
*   They allow for the creation of a hierarchical structure of design decisions. This structure makes it easier to scale the design system while maintaining consistency and flexibility [2].

Token Structure
---------------

Tokens can be organized into different levels of abstraction. These levels help organize tokens based on their purpose, scope, or usage.

Brad Frost suggests a [three-tiered model](https://bradfrost.com/blog/post/the-many-faces-of-themeable-design-systems/) that uses a vertical hierarchy.

> **Tier-1:** The lowest tier, contains tokens that encapsulate raw visual design materials. These are raw values like color hex or size in px.
> 
> **Tier-2:** Tokens are semantic theme layer, and link Tier-1 tokens to high-level usage withing a UI.
> 
> **Tier-3:** Tokens are specific to components and link to Tier-2 tokens.

Example:
- Tier 1: _green.50 = #27ae60_
- Tier 2: _theme.brand.color.background = {green.50}_
- Tier 3: _button.primary.background.color = {theme.brand.color.background}_

Token’s naming structure should describe their purpose and context. It should be easy to understand. The naming convention should be documented and communicate with development team.

Checkout this [**article**](https://smart-interface-design-patterns.com/articles/naming-design-tokens/) for guide on effective naming of the design tokens. Your Design System can define it’s own naming convention. Hence effective communication is very important.

Exporting Tokens
----------------

Design tools like Sketch, Figma, InVision and others provides ways to convert these tokens into a commonly used JSON structure that is readable and easily integrates with software development. There are also some automation tools discussed in next section that also helps setup end-to-end process.

![Examples of JSON sctructure](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*d5XzpL-v83Ir5vZxQgNG7g.png)

**Design Implementation and Handoff**
=====================================

The final stage of the design step involves collaborating closely with the development team to ensure a smooth transition from design to implementation. This includes providing clear specifications, design assets, and guidelines to enable efficient front-end integration.

The traditional way to do that is sharing the design in Figma and letting the developers manually read the tokens and its raw value from the design. There are lot of issues with this approach:

*   Inconsistency in design interpretation.
*   Platform discrepancies: iOS and Android interpret values differently.
*   It’s a Repetative task that costs time.
*   Communication overhead with endless back-and-forth with design team and multiple review meetings.
*   Outdated information in design documents. Changes in Figma not reflected in documnent shared with developers.
*   Updating desing takes long time and is error prone.
*   Code maintenance and eventual business impact.

For this reason there are tools like [Tokens Studio](https://tokens.studio/) that manages the whole lifecycle of tokens especially for Figma. Sketch, InVision and others provide similar tools which works almost in same way.

[**Tokens Studio for Figma**](https://www.figma.com/community/plugin/843461159747178978/tokens-studio-for-figma) is one of the most popular plugin that helps setup the design tokens and export the tokens into JSON format as seen above that can be handed over to development team through any versioning system like GitHub or GitLab.

Automation
----------

Now that you have design tokens all setup we need an automated way to connect designers and developers in the most intuiative way. This is where automation tools comes in.

Well known tools are: [_Supernova_](https://www.supernova.io/), [_Storybook_](https://storybook.js.org/) and [_ZeroHeight_](https://zeroheight.com/).

*   **End-to-End:** These tools helps build a design system that _actually_ connects design and development by sharing information between tools and delivering tokens to each stage of the development pipeline.
*   **Design System Management:** These tools provide way to manage all tokens in one place and also automate the work of exporting token to JSON and pushing to Git repository as needed by providing consistent versioning system.
*   **Documentation:** These tools also makes documenting designs easier. Documentation are categorized based on components, patterns, themes and other necessary information. These tools makes sure designs are versioned and in sync with the documentation.

These tools also provides extra features such as **Code Generation** and **Asset creation** which makes life easier for developers to develop the UI in a way that is maintainable.

Manual
------

You dont have to use these tools to be able to handoff design tokens to development team. You can just use Tokens Studio (or similar) to directly push token in JSON format to Git repository and consume the JSON on the other side in code.

This will give you more flexibility on what you can do with the tokens. It is budget friendly way to adopt proper design systems with design tokens during prototyping stage or even for production. You might need to build some tooling around it.

![Design System High level View](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*y0ni7hVd3yun2_ZyPIzDQw.png)

Conclusion
==========

In this article we went through what are Design Tokens, how they are structured and what are ways to hand-off designs to the development team.

In next article we will explore on automated Code Generation using **Style Dictionary**, where the JSON file we get from the design team will be used to generate structs and classes that represents the themeing of our application.

_Stay tuned…_

References:
===========

[1][https://spectrum.adobe.com/page/design-tokens/](https://spectrum.adobe.com/page/design-tokens/)

[2][https://uxdesign.cc/supercharge-your-design-system-with-design-tokens-55044fa29142](https://uxdesign.cc/supercharge-your-design-system-with-design-tokens-55044fa29142)

[3][https://uxplanet.org/design-tokens-a-design-system-superpower-dab07a5f0035](https://uxplanet.org/design-tokens-a-design-system-superpower-dab07a5f0035)

[4][https://bradfrost.com/blog/post/the-many-faces-of-themeable-design-systems/](https://bradfrost.com/blog/post/the-many-faces-of-themeable-design-systems/)