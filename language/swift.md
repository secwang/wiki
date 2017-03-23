<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [list and dictionary](#list-and-dictionary)
- [closure](#closure)
- [what is the quention mark.](#what-is-the-quention-mark)
- [GCD](#gcd)
- [Bind action to Left mouse down](#bind-action-to-left-mouse-down)
- [as! and as?](#as-and-as)
- [singletion](#singletion)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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
