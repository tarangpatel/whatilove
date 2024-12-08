---
title: The Missing Piece in Mobile Development - Style Dictionary
subtitle: Chapter 2
categories: [Mobile development, Design systems, UI consistency, Mobile app design, iOS development, Android development, Design system tools, Storybook, Figma plugins, UIKit customizations, Material Design overrides, Design debt, Pixel-perfect consistency, Design handoff, Styled-components, Design guidelines, Design graveyard, Component libraries, Dark mode implementation, Banking app UI, Design review meetings]
tags:
  [Mobile development, Design systems, iOS development, Android development, Design system tools]
image: /images/DesignSystems/designSystem-styleDict.png
---

In the  [previous article](https://medium.com/@tarang0510/the-missing-piece-in-mobile-development-design-tokens-chapter-1-499cf4d38a2c), we have focused on the design aspects of Design Systems. We saw how a design team approachs designing and setting up design tokens by taking Figma as an example.

# Intro

Design tokens are great way to share design elements with development team and make sure app stays consistent with the design changes. It reduces the amount of work manualy required to make changes to the UI in an app.

You can directly consume the design token JSON file in your app. This will require some JSON parsing to convert the raw data to app specific design model. You should not use the raw data directly.

But this defeats one of the purpose of Design System, which is to prevent the duplication of work. Each platform will require a parser to parse the token file.

To make sure each platform receives exactly what it is needed with minimal development effort we require the transformer that will act as mediator between design and development.

In this article, we will see how those tokens are converted to code. We saw this briefly in the previous article, but we will use a specific tool called  **Style Dictionary**  from Amazon to elaborate on how tokens are transformed to any front-end code.

_As this series is on mobile development we will only focus on Swift and Kotlin code as output._

# What is Style Dictionary?

Style Dictionary is an open-source platform that transforms design tokens into multiple platform-specific code formats. It acts as a central source of truth for design system properties, enabling designers and developers to maintain consistency across different platforms and technologies.

> **Style Dictionary**  is a build system that allows you to define styles once, in a way for any platform or language to consume. A single place to create and edit your styles, and a single command exports these rules to all the places you need them — iOS, Android, CSS, JS, HTML, sketch files, style documentation, or anything you can think of. It is available as a CLI through npm, but can also be used like any normal node module if you want to extend its functionality. —  [Tagline](https://amzn.github.io/style-dictionary/#/)

# Why Use Style Dictionary?

-   **Single Source of Truth**: Define design tokens once and generate code for multiple platforms
-   **Consistency**: Eliminate manual translation of design properties
-   **Scalability**: Easily manage and update design system properties
-   **Platform Flexibility**: Support for Swift, Kotlin, CSS, React Native, and more
-   **Documentation:**  Creates human readable artifacts (e.g. documentation, design libraries, etc)

More features can be found  [here](https://amzn.github.io/style-dictionary/#/)

# Integration with CI/CD

Written in node.js, Style Dictionary seamlessly integrates into continuous integration and deployment pipelines:

-   **Automated Token Generation**: Automatically convert design tokens during build processes
-   **Version Control**: Sync design tokens across development environments
-   **Consistent Builds**: Ensure design consistency in every release

# Implementation Example: Design Tokens to Swift and Kotlin

1. Basic Token JSON Configuration

   ``` {  
      "color": {  
        "primary": {  
          "value": "#3498db",  
          "name": "primary"  
        },  
        "secondary": {  
          "value": "#2ecc71",  
          "name": "secondary"  
        }  
      },  
      "sizing": {  
        "small": {  
          "value": "8",  
          "name": "small"  
        },  
        "medium": {  
          "value": "16",  
          "name": "medium"  
        }  
      }  
    }
    ```

2. Style Dictionary Configuration (config.js)

```
const StyleDictionary = require('style-dictionary');  
  
StyleDictionary.registerFormat({  
  name: 'swift/nested',  
  formatter: function(dictionary) {  
    return `public enum StyleTokens {  
      ${dictionary.allProperties.map(prop =>   
        `  static let ${prop.name} = ${prop.value}`  
      ).join('\n')}  
    }`;  
  }  
});  
  
StyleDictionary.registerFormat({  
  name: 'kotlin/nested',  
  formatter: function(dictionary) {  
    return `object StyleTokens {  
      ${dictionary.allProperties.map(prop =>   
        `  val ${prop.name} = "${prop.value}"`  
      ).join('\n')}  
    }`;  
  }  
});  
  
const StyleDictionaryConfig = {  
  source: ['tokens.json'],  
  platforms: {  
    swift: {  
      transformGroup: 'swift',  
      buildPath: 'generated/',  
      files: [{  
        destination: 'StyleTokens.swift',  
        format: 'swift/nested'  
      }]  
    },  
    kotlin: {  
      transformGroup: 'kotlin',  
      buildPath: 'generated/',  
      files: [{  
        destination: 'StyleTokens.kt',  
        format: 'kotlin/nested'  
      }]  
    }  
  }  
};  
  
module.exports = StyleDictionaryConfig;
```

3. Generated Swift Output (StyleTokens.swift)
```
public enum StyleTokens {  
  static let primaryColor = "#3498db"  
  static let secondaryColor = "#2ecc71"  
  static let smallSize = "8"  
  static let mediumSize = "16"  
}
```
4. Generated Kotlin Output (StyleTokens.kt)
```
object StyleTokens {  
  val primaryColor = "#3498db"  
  val secondaryColor = "#2ecc71"  
  val smallSize = "8"  
  val mediumSize = "16"  
}
```
# Customization Capabilities

Style Dictionary offers extensive customization options:

-   **Custom Transformations**: Create unique token transformations
-   **Platform-Specific Configurations**: Define custom output formats
-   **Preprocessors and Postprocessors**: Modify token generation workflow
-   **Color Manipulations**: Advanced color transformations and formats

## Custom Transformations

Style Dictionary allows creating custom transformations for:

-   Color conversions
-   Size and spacing normalization
-   Platform-specific formatting
```
StyleDictionary.registerTransform({  
  name: 'custom/size/px',  
  type: 'value',  
  matcher: (token) => token.type === 'dimension',  
  transformer: (token) => `${token.value}px`  
})
```
## Transform Groups

Create comprehensive transformation pipelines:
```
StyleDictionary.registerTransformGroup({  
  name: 'custom-web',  
  transforms: [  
    'name/cti/kebab',  
    'color/css',  
    'custom/size/px'  
  ]  
});
```
## Custom Output Formats

Define platform-specific output formats:
```
StyleDictionary.registerFormat({  
  name: 'custom/swift/enum',  
  formatter: function(dictionary) {  
    return `public enum StyleTokens {  
      ${dictionary.allProperties.map(prop =>   
        `  static let ${prop.name} = ${prop.value}`  
      ).join('\n')}  
    }`;  
  }  
});
```
## Advanced Customization Techniques

Preprocessors and Filters
```
StyleDictionary.registerFilter({  
  name: 'isColor',  
  matcher: function(token) {  
    return token.type === 'color';  
  }  
});  

const StyleDictionaryExtended = StyleDictionary.extend({  
  source: ['tokens.json'],  
  platforms: {  
    web: {  
      // Only process color tokens  
      filter: 'isColor',  
      // ... other configurations  
    }  
  }  
});
```
## Dynamic Token Manipulation
```
StyleDictionary.registerTransform({  
  name: 'color/adjust-opacity',  
  type: 'value',  
  matcher: (token) => token.type === 'color',  
  transformer: (token) => {  
    // Custom color manipulation logic  
    return adjustOpacity(token.value, 0.5);  
  }  
});
```
## Composition and Inheritance
```
Token Composition

{  
  "color": {  
    "brand": {  
      "primary": { "value": "#3498db" },  
      "secondary": {   
        "value": "{color.brand.primary}",  
        "modifier": "darken(10%)"  
      }  
    }  
  }  
}
```
# Performance Optimizations

## Caching and Performance

-   Built-in caching mechanisms
-   Incremental builds
-   Parallel processing support

# Alternatives to Style Dictionary

## [**Theo**](https://github.com/salesforce-ux/theo)

Developed by Salesforce, focuses on design token transformations. Theo serves the same purpose, transforming design token into multiple format that is compatible with multiple platforms.

For mobile Theo do not convert design tokens to code. But rather it takes different approach. It converts design tokens to JSON for iOS and XML for Android. Hence it requires another step to consume the JSON and XML for respective platforms.

_Theo is an abstraction for transforming and formatting Design Tokens._

As I mentioned before we will still need some parser logic in app that can parse these ternsformed JSON and XML files. Hence Theo might not be efficient if you are not adopting SalesForce design system. Theo is meant to be used with SalesForce design system. You can check it out  [here](https://github.com/salesforce-ux).

## **Custom Transformer**

What the above tools (Style Dictionary and Theo) does is achievable by developing transformers of your own. The main task is to convert design tokens to platfrom compatible format. It can be either data model or other other formats like json or xml.

![](https://miro.medium.com/v2/resize:fit:875/1*z8scOSaOh7Gy3GVKDKvEwg.png)

Here is very basic code generator in javascript.

_Note: Below code was generated by AI as it is to show what is possbile bare minimum._
```
const fs = require('fs');  
const path = require('path');  
  
class DesignTokenGenerator {  
    constructor(tokensPath) {  
        this.tokens = this.loadTokens(tokensPath);  
    }  
      
    loadTokens(filePath) {  
        try {  
            const rawData = fs.readFileSync(filePath, 'utf8');  
            return JSON.parse(rawData);  
        } catch (error) {  
            console.error('Error loading tokens:', error);  
            return {};  
        }  
    }  
      
    generateSwiftCode() {  
        const swiftCode = `  
import UIKit  
  
public enum DesignTokens {  
  ${this.generateSwiftCategories()}  
}  
  
extension UIColor {  
  convenience init(hex: String) {  
    let hexString = hex.trimmingCharacters(in: .whitespacesAndNewlines)  
    let scanner = Scanner(string: hexString)  
      
    if hexString.hasPrefix("#") {  
      scanner.scanLocation = 1  
    }  
      
    var color: UInt32 = 0  
    scanner.scanHexInt32(&color)  
      
    let red = CGFloat((color >> 16) & 0xFF) / 255.0  
    let green = CGFloat((color >> 8) & 0xFF) / 255.0  
    let blue = CGFloat(color & 0xFF) / 255.0  
      
    self.init(red: red, green: green, blue: blue, alpha: 1.0)  
  }  
}`;  
        return swiftCode;  
    }  
      
    generateKotlinCode() {  
        const kotlinCode = `  
import android.graphics.Color  
  
object DesignTokens {  
  ${this.generateKotlinCategories()}  
}`;  
        return kotlinCode;  
    }  
      
    generateSwiftCategories() {  
        return Object.entries(this.tokens)  
            .map(([category, values]) => {  
                const categoryEntries = Object.entries(values)  
                    .map(([name, value]) => this.formatSwiftEntry(category, name, value))  
                    .join('\n    ');  
                  
                return `  
  public enum ${this.capitalizeFirst(category)} {  
    ${categoryEntries}  
  }`;  
            })  
            .join('\n');  
    }  
      
    generateKotlinCategories() {  
        return Object.entries(this.tokens)  
            .map(([category, values]) => {  
                const categoryEntries = Object.entries(values)  
                    .map(([name, value]) => this.formatKotlinEntry(category, name, value))  
                    .join('\n    ');  
                  
                return `  
  object ${this.capitalizeFirst(category)} {  
    ${categoryEntries}  
  }`;  
            })  
            .join('\n');  
    }  
      
    formatSwiftEntry(category, name, value) {  
        if (category === 'color') {  
            return `public static let ${name} = UIColor(hex: "${value}")`;  
        }  
        return `public static let ${name}: CGFloat = ${value}`;  
    }  
      
    formatKotlinEntry(category, name, value) {  
        if (category === 'color') {  
            return `val ${name} = Color.parseColor("${value}")`;  
        }  
        return `const val ${name} = ${value}`;  
    }  
      
    capitalizeFirst(string) {  
        return string.charAt(0)  
            .toUpperCase() + string.slice(1);  
    }  
      
    writeFiles(outputDir) {  
        const swiftOutput = path.join(outputDir, 'DesignTokens.swift');  
        const kotlinOutput = path.join(outputDir, 'DesignTokens.kt');  
          
        fs.mkdirSync(outputDir, {  
            recursive: true  
        });  
        fs.writeFileSync(swiftOutput, this.generateSwiftCode());  
        fs.writeFileSync(kotlinOutput, this.generateKotlinCode());  
          
        console.log('Design token files generated successfully.');  
    }  
}  
  
// Example usage  
const generator = new DesignTokenGenerator('tokens.json');  
generator.writeFiles('./output');
```
There is more to these build system than just parsing design token file. You can parse the design token files to formats you want but there is still additional step that Style Dictionary and Theo provides that is  _transformer._

Transfomer will make sure the design language is properly converted to specific platform language. For eg: Colors can be turned into hex values, rgb, hsl, hsv, etc… that is suitable for the platform you need.

> When using Style Dictionary you can write your own custom transformer that can help tranform name, values or attributes of a token into the format that you want.

# Best Practices

-   Keep token definitions semantic and platform-agnostic
-   Version control your design token configurations
-   Use consistent naming conventions
-   Implement automated testing for token generations
-   Keep transformations modular

# Who is responsible?

In a well-organized team, this task will be taken by a UI Engineering team. The  **UI Engineering**  team focuses on all aspects of UI. They develop reusable UI components following proper Design System guidelines, document, and maintain UI artifacts that are brand-agnostic and can be used by any internal or external client applications.

UI Engineers can work with the Design team to set up token synchronization processes and trigger code generators based on changes made to the design by the Design team.

In other team structures,  **architects**  should be able to own the tool and related processes to ensure code generation is automated and versioned with proper rollback strategies.

This is ultimately a  **team’s decision**  to determine the ownership of the tool and related processes.

# Conclusion

We have seen how design tokens can be converted to formats that can be easily adopted by different platforms. You can either use existing versatile and well documented tool like  **Style Dictionary**  or  **build your own internal tool**.

These tools bridge the gap between design and development, providing a robust, scalable solution for managing design system tokens across multiple platforms.

As design and development continue to converge, embracing design tokens represents more than just a technical strategy — it’s a transformative approach to creating more consistent, efficient, and collaborative digital experiences. By implementing a systematic approach to design token management, teams can unlock unprecedented levels of design-development alignment, reduce redundancy, and accelerate product innovation.

The journey of design tokens is not just about code conversion; it’s about creating a shared language that empowers designers and developers to work seamlessly together, turning design vision into pixel-perfect reality across every platform and device.
