Swift4ObjCProgrammers (under construction)
=====================

This page intends to help people in transitioning from the Objective-C world to Swift by showing how certain pieces of Objective-C code are written in Apple's new language.

I've been programming in Objective-C since 2012, and as I'm starting to learn Swift this will be my note book to register what I've found so far as new or different in Swift, in comparison to the Obj-C's world.

Fell free to contribute to this page or correct me if you smell bad code from this page :)

## Optionals

In Swift variables (not constants) can be of type `T` or `T?`. The first one implies that the variable always have a value whereas in the second one the variable can have no value set. *No value* is exactly what `nil` means in Swift, as we can see in Apple's reference: *in Objective-C, `nil` is a pointer to a non-existant object. In Swift `nil` is not a pointer – it is the absence of a value of a certain type.*.

What does all this mean? We know exactly when we'll receive (or potencially not receive) a value in the arguments of a method or from the return of a method. [This article](https://medium.com/swift-programming/facets-of-swift-part-1-optionals-b8ba5b0051a2) gives a good example of how good this is, let's fastly analyze it. Consider the following method signature in Objective-C:

    - (NSInteger)indexOfItem:(Item *)item;

Looking to this code we notice that nothing prevents us to send a nil pointer as argument, although there can be an assert to check if the parameter is nil, what would crash the app in this case. We also don't know exactly what will be returned if `item` is not found (`NSNotFound` which is defined as `NSIntegerMax`? Or `NSIntegerMin`? Or `-1`?). Now look to this method signature in Swift:

    func indexOfItem(item: Item) -> Int?
    
We know exactly what's happening here. `item` must always have a value and if we try to pass as argument a value of type `Item?` we get an error at compile time. We also notice that this method can return "no value", i.e., `nil`, meaning that `item` is not present.

#### Optional unwrapping and `if let`

## `;`

You don't need to put a semicolon in the end of one-line statements, but you can use a semicolon to separate multiple statements in the same line.

## `Int` as `Bool`

You can NOT use an integer value as a boolean, like this: `let array = []; if array.count { /* some logic */ }`. Write the whole (and more readable) expression instead: `if array.count > 0 { /* some logic */ }`

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

## Try-Catch

At the time I'm writing this (11/25/2014) there's no try-catch in Swift. If you deeply want it you can use wrap Obj-C's try-catch like [this](https://medium.com/swift-programming/adding-try-catch-to-swift-71ab27bcb5b8)

## Class methods and class properties

## Enums
