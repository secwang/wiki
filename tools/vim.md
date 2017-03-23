<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [what I'm short for practical vim user.](#what-im-short-for-practical-vim-user)
- [appearance](#appearance)
- [replace](#replace)
- [ctags](#ctags)
- [call shell](#call-shell)
- [Explore](#explore)
- [vim tabs](#vim-tabs)
- [global marks](#global-marks)
- [filelist](#filelist)
- [my open nav file work flow](#my-open-nav-file-work-flow)
- [add markdown space](#add-markdown-space)
- [Vim bytes](#vim-bytes)
- [execute shell command](#execute-shell-command)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---  
title: "vim"   
date: 2016-11-18 23:00  
---  
[TOC]  
  
# what I'm short for practical vim user.  
- tags   
- brower dir  
- quick open file   
- like ag ?  
- tabs,tables  
- select between line to line  
  
# appearance  
:set nu :set nonu  close and open line number.  
  
:set hl :set nohl syntax highlight  
  
# replace   
:%s/goo/foo/g g means global.    
:%s/goo/foo/gc c means confirm.    
if want replace in all the files you have open.    
:bufdo %s/foo/bar/g    
  
  
# ctags  
  
:! ctags -R .    
:se tags=../../../tags    
:ta /function    
Ctrl-] go to function difination.    
Ctrl-T go back.    
  
# call shell  
:pwd    
:cd     
:Ex go to explore mode    
:! node %    
  
# Explore  
:Ex     
:find txt Tap    
  
vim deault file Explore named Netrw.    
  
i change info     
% create a new file    
d create a new directory    
R rename the file/directory under the cursor    
D Delete the file/directory under the cursor  
  
  
:r ! fzf     
:! ag xxx    
  
  
./mysql.md    
  
gf / localmd  
<ctrl-w> + f open in another windows;  
<ctrl-w> + gf open in another windows;  
C-Wv+gf - Edit existing file under cursor in vertically split window  
  
  
  
# vim tabs  
<ctrl-w>  + T move in tab.  
:tabe file new tab.  
:tabc tableclose.  
:tabonly close all tabs aparts from the current one.  
  
gt   
gT  
#gt move to tab number #  
  
:tabmove   #move tab to where   
  
  
# global marks  
  
mC  
mT  
'C  
'T  
  
  
  
# filelist  
Ctrl-o jump back to last jump location  
ctrl-i oppose as jump back.  
  
# my open nav file work flow  

- Macvim
:set hidden http://stackoverflow.com/questions/2414626/unsaved-buffer-warning-when-switching-files-buffers  
  
tabe new tab  
:r ! find . -name xxxx (read file to vim buffer.)  
gF (open file under cursor)  
so perfect.  

- vim 
set rtp+=/usr/local/opt/fzf   
FZF .  in vim 

# add markdown space  
:%s/$/  /  
  
# Vim bytes 
vim -b bytefile
:%!xxd
:%!xxd -r


# execute shell command 
```
:! luajit %
q:k<CR>
```
