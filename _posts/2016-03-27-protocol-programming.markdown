---
title: Protocol Oriented Programing (Swift) 
---

POP: Protocol Oriented Programing

* [Apple - WWDC 2015](https://developer.apple.com/videos/play/wwdc2015/408/)
* [Into to POP in Swift 2 - Ray Wenderlich](https://www.raywenderlich.com/109156/introducing-protocol-oriented-programming-in-swift-2)
* [POP - UIKit](https://www.captechconsulting.com/blogs/ios-9-tutorial-series-protocol-oriented-programming-with-uikit)
* [Problem with Subclassing - KrakenDev](http://krakendev.io/blog/subclassing-can-suck-and-heres-why)
* [Real world example - Matthew Palmer](http://matthewpalmer.net/blog/2015/08/30/protocol-oriented-programming-in-the-real-world/)
* [POP MVVM - NatashaTheRobot](https://www.natashatherobot.com/swift-2-0-protocol-oriented-mvvm/)



#### Protocol Extension Limitations [1]

* Cannot call protocol extension members from Objective-C.
* Cannot use the where clause with a struct type.
* Cannot define multiple comma-separated where clauses, similar to an if let statement.
* Cannot store dynamic variables inside a protocol extension.
* This is also true for non-generic extensions.
* Static variables are supposed to be allowed, but as of Xcode 7.0 they print the error "static stored properties not yet supported in generic types."
* For this reason there's no real concept of protocol extension inheritance.
* Cannot adopt multiple protocol extensions with duplicate members.
* The Swift runtime chooses the last protocol adopted and ignores the others.
* For example, if we have 2 protocol extensions which implement the same methods, only the last one we've adopted will be used when the method is invoked. There's no way to invoke the methods from the other extensions.
* Cannot extend optional protocol methods.
* Optional protocol methods require the @objc tag, which cannot be used together with a protocol extension.
* Cannot declare a protocol & its extension at the same time.
* It would be nice to be able to declare extension protocol SomeProtocol {} to simultaneously declare the protocol and implement the extension, since protocols don't always have any members when the extension contains all of the important logic.


Resources:
[1] * [POP - UIKit](https://www.captechconsulting.com/blogs/ios-9-tutorial-series-protocol-oriented-programming-with-uikit)
