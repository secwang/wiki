---
title: "spacemacs"
date: 2016-06-30 23:00
---
[TOC]
# spacemacs usage
flyspell insert to personal dictionary

SPC S c  show helm correct list
M+$ will show how to change this word with flyspell mode.
# redo last command
Is the ack search you were doing using Helm? If so, you can press SPC h l to resume last Helm session. If you Ack search is not the last active Helm session, you can add prefix argumente C-u to select one.

You can also press f3 to store the search result into a buffer (or press TAB to open action buffer and select the 3rd one; TAB is replaced by C-z for opening action menu in next Spacemacs release), and use M-n or M-p to navigate next and previous match, M-N or M-P to go to next and previous file in the search buffer.

```
@x-ji
x-ji commented on Apr 27
I see. That applies to scenarios involving helm well. Thanks.

Also, for others like me who are unfamiliar with Emacs, from this Stackoverflow question
http://stackoverflow.com/questions/275842/is-there-a-repeat-last-command-in-emacs, to
repeat the last general command one can use C-x z, and to repeat the last "complex"
command one can use C-x Esc Esc. To bring up complex command his
tory one can use M-x M-p. Seems that commands like those of Ido can be repeated in this fashion.

```
