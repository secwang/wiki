---
title: "cloure in go"
date: 2013-09-19 18:00
---
[TOC]

a typical function difination in go.

    func Add(a, b int)(ret int, err error) {
        // ...   
    } 

this anonymous function defination in golang means a function without function name.

    func (args) return_value{
         //function body
    }

anonymous function is the foundation of the cloure defination form my views. we have the func type in golang type system .  So we can assign the func to a variable.

    a := func(args ...) return_type {
          //func body
    }
    a()

we often see a intersting programming trick. people add "()" after a anonymous function body.

like:

    func(ch chan int) {
        ch <- ACK 
    } (reply_chan)

or

    func f() (result int) {
        defer func() {
            result++
        }() // why and how?
        return 0
    ｝

this "()" means a function call.And the language specs for the [defer statement](http://golang.org/ref/spec#Defer_statements) mandate that its 'Expression' always a function call.

finally we would unstand the below code well.

    package main  

    import (
        "fmt"
    )  

    func main() {
        var j int = 5

        a := func()(func()) {
            var i int = 10
            return func() {
                fmt.Printf("i, j: %d, %d\n", i, j)
            }
        }()

        a()
        j *= 2
        a()
    }


