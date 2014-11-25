Swift4ObjCProgrammers (under construction)
=====================

This page intends to help people in transitioning from the Objective-C world to Swift by showing how certain pieces of Objective-C code are written in Apple's new language.

I've been programming in Objective-C since 2012, and as I'm starting to learn Swift this will be my note book to register what I've found so far as new or different in Swift, in comparison to the Obj-C's world.

Fell free to contribute to this page or correct me if you smell bad code from this page :)

## Optionals

From Apple's reference: *in Objective-C, `nil` is a pointer to a non-existant object. In Swift `nil` is not a pointer – it is the absence of a value of a certain type.*

Here is a [good article](https://medium.com/swift-programming/facets-of-swift-part-1-optionals-b8ba5b0051a2) about optionals.

## `Int` as `Bool`

You can NOT use an integer value as a boolean, like this: `let array = []; if array.count { /* some logic */ }`. Write the whole (and more readable) expression instead: `if array.count > 0 { /* some logic */ }`

## `;`

You don't need to put a semicolon in the end of one-line statements, but you can use a semicolon to separate multiple statements in the same line.

## `id`

Now `id` is not a type anymore. We can use it as a property name \o/. The equivalent in Swift is `AnyObject`, or `AnyObject?` if your variable can be nil.

## Dicionaries

The major difference among collection types in Swift like Dictionaries is that they are typed. The Syntax is the following:

    var dictionary = Dictionary<TypeForKey, TypeForValue>()
  
This will create an empty **mutable** dictionary, something equivalent to:

    NSMutableDictionary *dictionary = [NSMutableDictionary new];

Some thoughts:
* `TypeForValue` can be of type `AnyObject` but `TypeForKey` needs to be a **hashable** type.
* There's no method `objectForKey` in Swift dictionaries, we use the `[]` operator instead, like this: `let value = dictionary["stringKey"]?` (notice the `?`, because the `[]` operator can return nil) 
* Because the collections are typed in Swift, you know in advance the type of the value you're getting from a dictionary, so you don't need to cast values to use them
* Immutability is attained by using `let` instead of `var`
* Dictionary literals look like this: `[key1: value1, key2: value2, key3: value3]`

## Arrays

* The equivalent to `addObject:` is `append`;

## `long` and `long long`

I've used `long long` in rare situations, like in some calls to a `NSFileManager`. This `long` type, and others like `char` and `double`, come from the C language, and apple provides a [guide](https://developer.apple.com/library/ios/documentation/swift/conceptual/buildingcocoaapps/InteractingWithCAPIs.html) to interact with C APIs. However, in this guide Apple says to "use `Int` wherever possible", and that's exactly what has been done in `NSFileManager`, where the `NSDictionary` extension that used to return the file size in `unsigned long long` now returns `UInt64`

## Class methods and class properties

## Enums
