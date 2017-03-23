<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Method receiver](#method-receiver)
- [Little metaprogramming](#little-metaprogramming)
- [Pointer ](#pointer)
- [Interface design](#interface-design)
- [Assignments with interface types](#assignments-with-interface-types)
- [reference:](#reference)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
title: "interface type in golang"
date: 2013-09-20 7:00
---
[TOC]


### Method receiver

first , we need spend some time in unstanding "receiver".

Normal function 

`func name( arguments) return type.`

Method 

`func ( receiver) name( arguments) return type. `

What is a Method Receiver?

specs [says](http://golang.org/ref/spec#Method_sets):

> The method set of the corresponding pointer type \*T is the set of all methods with receiver \*T or T (that is, it also contains the method set of T).

[method calls](http://golang.org/ref/spec#Calls) says:

> A method call `x.m()` is valid if the method set of (the type of) x contains m and the argument list can be assigned to the parameter list of m. If x is addressable and &x's method set contains m,`x.m()` is shorthand for `(&x).m()`.

so the Method Receiver syntax defined  also for function calling. So, we can use this feature to implements lightweight OO in golang.

### Little metaprogramming

    type Integer int
    func (a Integer) Less(b Integer) bool {
        return a < b
    }
    func main() {
       var a Integer = 1
       if a.Less(2) {
           fmt.Println(a, "Less 2")
       }
    }

### Pointer 

Only when we want to change the instance , we pass the pointer as method receiver paras. 

    func (a *Integer) Add1(b Integer) {
        *a += b
    }

    func (a Integer) Add2(b Integer) {
        a += b
    }
    func main() {
        var a Integer = 1
        a.Add1(2)
            fmt.Println("a =", a)
        a.Add2(2)
           fmt.Println9("a =", a)
    }
    Embedding types type Job struct {
        Command string
        *log.Logger 
    }
    func NewJob(command string, logger *log.Logger) *Job {
        return &Job{command, logger}
    }

    //or
    //job := &Job{command, log.New(os.Stderr, "Job: ", log.Ldate)}

Through this way, all the method in the jod type can use log method by nature.

    func (job *Job)Start() {
        job.Log("starting now...")
        ... // function body
        job.Log("started.")
    }

### Interface design

Go Object Oriented Design means "GOOD":)

The golang use implicitly interface ,unlike Java or C\#, so interfaces can be defined for code we don't own.

This means that to implement an interface you simply have to implement the method signatures that the interface defines.

So,we can understand this
```
type File struct {  
   // ... 
   }
 func (f *File) Read(buf []byte) (n int, err error) 
 func (f *File) Write(buf []byte) (n int, err error)
  func (f *File) Seek(off int64, whence int) (pos int64, err error) 
  func (f *File) Close() error
  type IFile interface {     
    Read(buf []byte) (n int, err error)     
    Write(buf []byte) (n int, err error)     
    Seek(off int64, whence int) (pos int64, err error)     
    Close() error 
    }  
    type IReader interface {     
    Read(buf []byte) (n int, err error) 
    }  
    type IWriter interface {    
     Write(buf []byte) (n int, err error) 
    }  
    type ICloser interface {     Close() error } 

    var file1 IFile = new(File)
    var file2 IReader = new(File)
    var file3 IWriter = new(File)
    var file4 ICloser = new(File)
```
Another trick about interface

    type ReadWrite interface{
        Reader
        Writer
    }

the above code is equal with:

    type ReadWriter interface {

        Read(p []byte) (n int, err error)

        Write(p []byte) (n int, err error)

    }

### Assignments with interface types

assignments in golang have two means.

​1. assgin a instance to a interface.

​2. assgin a interface to another interface variable.

    type Integer int
    func (a Integer) Less(b Integer) bool {
        return a < b
    }
    func (a *Integer) Add(b Integer) { 
       *a += b
    }

    type LessAdder interface {
        Less(b Integer) bool
        Add(b Integer)
    }

    var a Integer = 1
    var b LessAdder = &a

    //the reason is that golang can make such little change,generate some inter//esting code behide.
    func (a *Integer) Add(b Integer) ->

    func (a Integer) Add(b Integer)
    EOF

### reference:

[Go Data Structures: Interfaces](http://research.swtch.com/interfaces)


