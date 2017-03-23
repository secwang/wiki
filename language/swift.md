---
title: "swift note"
date: 2016-06-30 08:00
---
[TOC]

# list and dictionary

```swift
shoppingList = ["catfish", "water", "tulips", "blue paint"]
var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
```

# closure
closure can be use with in syntax
```
{ (params) -> returnType in
  statements
}
```


# what is the quention mark.

question marks after a type refer to Optionals
var optionalString: String? = "Hello"


# GCD

GCD is market name for libdispatch.

This is a apple style abstraction for Concurrency;
```
dispatch_async(queue: dispatch_queue_t, _ block: dispatch_block_t)


```
dispatch_get_main_queue() will back result in main threads;
```
dispatch_async(dispatch_get_main_queue()) {
    ///
}
```


# Bind action to Left mouse down
```
let action = Int(NSEventMask.LeftMouseDownMask.rawValue)
shareButton.sendActionOn(action)
```


# as! and as?

as? means cast with optional , the result can be null.
as! means cast must be type after mark, if not will get runtime error.
```
var optionalString = dict.objectForKey("SomeKey") as? String

var optionalString = dict.objectForKey("SomeKey") as! String

```

# singletion

```
class EventAPI{
    class var sharedInstance: EventAPI {
        struct Singleton {
            static let instance = EventAPI()
        }
        
        return Singleton.instance
    }
}

  func sharedInstance() -> AppDelegate {
        return UIApplication.sharedApplication().delegate as! AppDelegate
    }


    self.eventAPI = EventAPI.sharedInstance
```
