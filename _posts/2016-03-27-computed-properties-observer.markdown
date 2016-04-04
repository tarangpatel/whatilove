---
title: Advance Properties in Swift
---

## Computed Properties
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

#### Read-Only Computed Properties
A computed property with a getter but no setter is known as a read-only computed property.

```swift
var volume: Double {
        return width * height * depth
    }

```



## Property Observer

Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.


You have the option to define either or both of these observers on a property:

* willSet is called just before the value is stored.
* didSet is called immediately after the new value is stored.

```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}

```

## Type Properties

```swift

static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 1
    }

```
