---
title: "coredata"
date: 2016-06-30 08:00
---
[TOC]


### key principles

#### NSManagedObjectModel
An NSManagedObjectModel object describes a schema—a collection of entities (data models) that you use in your application.
```

let model = NSManagedObjectModel()
userEntity.properties = [nameAttribute,emailAttribute,userRelationship]
entryEntity.properties = [nameAttribute,timeAttribute,durationAttribute,entryRelationship]


model.entities = [userEntity, entryEntity]
```


#### NSEntityDescription

An NSEntityDescription object describes an entity in Core Data. Entities are to managed objects what Class is to id, or—to use a database analogy—what tables are to rows. An instance specifies an entity’s name, its properties (its attributes and relationships, expressed by instances of NSAttributeDescription and NSRelationshipDescription) and the class by which it is represented.

```
let userEntity = NSEntityDescription()
userEntity.name = Entity.user

```
#### NSAttributeDescription
The NSAttributeDescription class is used to describe attributes of an entity described by an instance of NSEntityDescription.


```
let nameAttribute = NSAttributeDescription()
nameAttribute.name = attribute.name
nameAttribute.attributeType = NSAttributeType.StringAttributeType
nameAttribute.optional = false
nameAttribute.indexed = false
```


#### NSRelationshipDescription
The NSRelationshipDescription class is used to describe relationships of an entity in an NSEntityDescription object.

```
entryRelationship.name = relationship.entry
entryRelationship.destinationEntity = entryEntity
entryRelationship.minCount = 0
entryRelationship.maxCount = 0
entryRelationship.deleteRule = NSDeleteRule.CascadeDeleteRule
entryRelationship.inverseRelationship = userRelationship
```

#### NSPersistentStoreCoordinator
NSPersistentStoreCoordinator
Instances of NSPersistentStoreCoordinator associate persistent stores (by type) with a model (or more accurately, a configuration of a model) and serve to mediate between the persistent store or stores and the managed object context or contexts. Instances of NSManagedObjectContext use a coordinator to save object graphs to persistent storage and to retrieve model information. A context without a coordinator is not fully functional as it cannot access a model except through a coordinator. The coordinator is designed to present a façade to the managed object contexts such that a group of persistent stores appears as an aggregate store. A managed object context can then create an object graph based on the union of all the data stores the coordinator covers.


```
userEntity.properties = [nameAttribute,emailAttribute,userRelationship]

entryEntity.properties = [nameAttribute,timeAttribute,durationAttribute,entryRelationship]
model.entities = [userEntity, entryEntity]

let persistentStoreCoordinator = NSPersistentStoreCoordinator(managedObjectModel:model)
```


#### NSManagedObjectContext
An instance of NSManagedObjectContext represents a single “object space” or scratch pad in an application. Its primary responsibility is to manage a collection of managed objects. These objects form a group of related model objects that represent an internally consistent view of one or more persistent stores. A single managed object instance exists in one and only one context, but multiple copies of an object can exist in different contexts. Thus object uniquing is scoped to a particular context.

```
let managedObjectContext = NSManagedObjectContext(concurrencyType: NSManagedObjectContextConcurrencyType.MainQueueConcurrencyType)

managedObjectContext.persistentStoreCoordinator = persistentStoreCoordinator
```


#### NSPredicate
The NSPredicate class is used to define logical conditions used to constrain a search either for a fetch or for in-memory filtering.

```
https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSPredicate_Class/
```
#### NSFetchRequest
```
https://developer.apple.com/library/mac/documentation/Cocoa/Reference/CoreDataFramework/Classes/NSFetchRequest_Class/
```



### xcdatamodeld

The Core Data model editor.

```

guard let modelURL = NSBundle.mainBundle().URLForResource("DataModel", withExtension:"momd") else {
    fatalError("Error loading model from bundle")
}
guard let mom = NSManagedObjectModel(contentsOfURL: modelURL) else {
    fatalError("Error initializing mom from: \(modelURL)")
}
```

### sqlite
sqlite will auto generate
```
let storeURL = docURL.URLByAppendingPathComponent("DataModel.sqlite")
do {
    try psc.addPersistentStoreWithType(NSSQLiteStoreType, configuration: nil, URL: storeURL, options: nil)
} catch {
    fatalError("Error migrating store: \(error)")
}
```
