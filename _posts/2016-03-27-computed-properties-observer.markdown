---
title: Advance Properties in Swift
---

# Computed Properties

* Use only var

They provide a getter and an optional setter to retrieve and set other properties and values indirectly.

```swift
var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
```

or Shorthand Setter Declaration where if a computed property’s setter does not define a name for the new value to be set, a default name of 'newValue' is used.  

```swift

var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set {
            origin.x = newValue.x - (size.width / 2)
            origin.y = newValue.y - (size.height / 2)
        }

```

## Read-Only Computed Properties
A computed property with a getter but no setter is known as a read-only computed property.

```
var volume: Double {
        return width * height * depth
    }

```



# Property Observer
