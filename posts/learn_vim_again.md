---
title: learn vim again 
date: 2013-10-14 09:00
---

[TOC]

# learning vim again.
I've been using vi and vim for 2 years. Just liking DSL working well than some common-range language, the IDE or special edting tools ,such as Ulysses , work better than vim in special area. However, vim as a serious text editor worth every programmer to learn.

The below are some note about relearning the vim editor, so I decide conclude each by topics.  The topic I wil talk will not suit for beginner of vim. 

### Basic command
`s`  

Usage: The **s** command compounds two steps into one: it deletes the character under the cursor and then enters Insert mode.

`f`  

Usage: The **f** command tells vim to look ahead for the next occurence of the specfied character and then move the cursor directly to it if a match is found. The **F** command do the simliar action in opposite direction.  

`*`  

press \* command , vim will search for the word which your cusor placed . A liitle tips to make it more useful is  just add ::set hlsearch:: in your .vimrc.  

`ma a`  

the m means mark it. you can return to the place you marked by press a later.  

`<C-o>zz (in insert mode)`  

\<C-o\>zz redraw the screen and position cursor in middle screen.  

`zz zt zb(in normal mode)`  

position cursor at middle, top, or bottom of screen  

`<C-a> and <C-x>`  

calc the number by vim , not by your brain.  

`<C-r>=6*35<CR>`  

another trick to use calc.  

`gu gU g`  

change the word lowercase , or make the word uppercase. It works  in normal mode, don't forget add a movement.   

`gg=G`  

autoident the entire file.  

`gv`    

 Reselect the last visual selection  

`dw db daw dab`  

### Movement tricks

`j k gj gk`  

vim provides motions for interacting with real lines and display lines. Tht j and k commanfds move down and up by real lines, where gj and gk commands move down and up by display line.

`w b, e ge`  
w and b commands target the start of word, w means forward b means backwords. e target the next end of a word and ge target the backward end of previous word.

`ea , gea`  

The ea commands can be read as "Append char after the current word." The gea commands means that "Append char at the end of the previous word."

`W B E gE`  

A word consists of a sequence of letters, digits, and underscores, or as a sequence of other nonblank characters separated with whitespace (see :h word ). The definition of a WORD is simpler: it consists of a sequence of nonblank characters separated with whitespace (see :h WORD ).

`f{char} F{char} t{char} T{char} ; , `  

The f{char} commands searches for the specified character, starting with the cursor position and continuing to the end of the current line. If a match is found, then the cursor advances to the specified character. The F command search for the previous occurrences  of the char.However , ; and , just like . symble in other operations means do the same search again. However the different commands determine the different search direction.  

`/{char} `    

search more than one character.  

`a i + )}]> '"(in vitual mode)`  

va} move the cursor to the pair of another }, vi} move the cursor inder of }    

`iw aw iW aW is as ip ap`  

a means plus one space than i.    

`%`  

The % command lets us jump between opening and closing sets of parentheses    
`vbb o e(in vitual mode)`    

the o key  toggles the free end.     

`U u (in vitual mode)`  

Up case or loweer case.    

`<C-w>s <C-w>v`    

split and vsplit  

`<C-w>c <C-w>o`  

close thie active window. Only active this window.
#### tricks in insert mode

`<C-h>`  

 Delete back one character  

`<C-w> `  

Delete back to start of line  

`<C-u> `  

Delete back one word  

`<C-r>{register} `  

 paste form the register. and 0 is default register y commands use.  

`<C-r><C-p>{register} `  

command smart register


#### What the range means
a range takes this form:{start},{end}.
We can use the . symbol as an address to represent the current line.And the % symbol stands for all line in current file.  

`:'<,'>p`  

'\< means first line of the vistual selection. The '\> means the last line of the visual seletion.  

`:[range]copy{address} example: :6t.`   

copy line from ex mode.   

`:[range]move{address} exameple:  :'<,'>m$`  


#### tricks for ex mode

`'<,'>normal .`    

this commands can be read as "For each line in the vistual selection, execute the normal mode . commands.  

`@: (in normal)`    

The vim will ex the last comamand in ex mode.  

`:col<C-d> `    

\<C-d\> will show suggestion for the ex mode,and tab will complete it.    

`write | !ruby %`    

ruby % means ruby the entire file.  

`:w !sudo tee % > /dev/null`    

and press L(load) after this command.
very useful trick to edits some high permissions file like hosts.
### tricks for marcos
### understand register
### tricks for search

### tricks for subtitute 
### vbundle system
#### useful bundle and usage

further read:
[Best of Vim Tips][1]
[Simple VIM commands you wish you'd known earlier][2]



[1]:	http://rayninfo.co.uk/vimtips.html "Best of vim tips"
[2]:	http://stackoverflow.com/questions/1276403/simple-vim-commands-you-wish-youd-known-earlier
