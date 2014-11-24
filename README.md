Swift4ObjCProgrammers (Under construction)
=====================

This page intends to help people in transitioning from the Objective-C world to Swift by showing how certain pieces of Objective-C code are written in Apple's new language.

I've been programming in Objective-C since 2012, and as I'm starting to learn Swift this will be my note book to register what I've found so far as new or different in Swift, in comparison to the Obj-C's world.

Fell free to contribute to this page or correct me if you smell bad code from this page :)

# Dicionaries

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

