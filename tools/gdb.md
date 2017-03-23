---  
title: "gdb"   
date: 2016-12-24 23:00  
---  
[TOC]  

# tui 
C+x + 1 start tui  
C+x + 2 show code and assmbly and register  
1. introduction to 'tui' mode in gdb (https://sourceware.org/gdb/onlinedocs/gdb/TUI.html)  
2. intro to python support in gdb (if it was compiled in)  
  2.1 python print('hello world')  

    2.1 set breakpoints with python gdb interface  
    3. Demo of reverse debugging in gdb, which helps isolate a stack-corrupting bug (https://www.gnu.org/software/gdb/news/reversible.html)  


# gdb python  api
python print (gdb.breakpoints())  
python print (gdb.breakpoints[0].location)  


