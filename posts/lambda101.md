<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [图灵机与 lambda calculus](#%E5%9B%BE%E7%81%B5%E6%9C%BA%E4%B8%8E-lambda-calculus)
- [图灵机](#%E5%9B%BE%E7%81%B5%E6%9C%BA)
  - [图灵机的停机问题](#%E5%9B%BE%E7%81%B5%E6%9C%BA%E7%9A%84%E5%81%9C%E6%9C%BA%E9%97%AE%E9%A2%98)
  - [lambda calculus](#lambda-calculus)
      - [Lambda Calculus Syntax](#lambda-calculus-syntax)
      - [currying](#currying)
    - [Free vs Bound Identifiers](#free-vs-bound-identifiers)
    - [Lambda Calculus Evaluation Rules](#lambda-calculus-evaluation-rules)
      - [Alpha 转换](#alpha-%E8%BD%AC%E6%8D%A2)
      - [Beta简化](#beta%E7%AE%80%E5%8C%96)
    - [Church Numerals](#church-numerals)
    - [Booleans and Choice in Lambda Calculus](#booleans-and-choice-in-lambda-calculus)
      - [Y combiner](#y-combiner)
    - [From Lambda calculus to Combinator Calculus](#from-lambda-calculus-to-combinator-calculus)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
title: "lambda calculus and turing machine"
date: 2014-02-14 08:00
---

[TOC]


### 图灵机与 lambda calculus
## 图灵机
理解图灵机，要从理解“机械计算”的定义开始说起。
图灵给这个词下的定义为机器可以完成的计算。为此他定义了一类机器，这类机器即为图灵机。
一台图灵机有如下几个部分组成。
1. 一条无限长的纸带TAPE。纸带上面有一个一个的小格子，每个格子中包含一个来自有限字母表的符号，字母表中有一个特殊的符号￼￼￼￼￼ ［］表示空白。纸带编号为\[0,1..2]
2. 读写头HEAD。该读写头可以在纸带上左右移动，可以读写所指格子上的符号。
3. 控制规则表。控制规则表是图灵机的核心，通过机器所处状态以及当前读写头所读的符号来确定读写头的下一个动作，并确定状态寄存器的值，令机器进入一个新的状态。
4. 一个状态寄存器。用来表示图灵机当前所处的状态。图灵机的所有可能状态的数目是有限的，并有一个特殊的状态称为停机状态。

整个图灵机的秘密在于状态转移表。状态转移表里是一种非常简单的规则，蕾丝，如果在状态a的读写头对着符号x，那么对当前各自写入y，并讲纸带移动，然后将机器的状态设为b。
实际上状态转移表相当于图灵机的源代码。
  
图灵机的秘密在于，如果我们给予图灵机更高的复杂度，让它有多条纸带多个读写头，对应于更复杂的机器模型，那么升级后的图灵机能完成的任务，原来的图灵机也能完成，也就是说，计算能力上和最原始的图灵机没有区别。人们造了一个转有名词，图灵等价。另外还有一个词，图灵完备，指的是一个语言具有和图灵机一样的计算能力。

图灵还证明了存在元图灵机（Universal Turing Machine），一个图灵机可以解决一个问题，但是为了一个问题就去创建一个特定的图灵机的话效率就太低了，就是一图灵机和输入数据为输入的图灵机，可以得到数据在特定图灵机上的结果。简单来说，我们只要输入特定图灵机编码（程序）以及数据，即刻得到结果。

### 图灵机的停机问题

停机问题（halting problem），简单来说就是给定一个图灵机，和输入图灵机的数据，来判断这个图灵机会不会终止运行，抑或无限循环。

我们通过反证法来证明这样的H不可能存在。假定存在这样的一个图灵机 P。我们用M来表示另外一个图灵机规则，I表示对另外一个图灵机的输入数据。那
么P（ M，I）返回的是M是否可以停机。
接下来我们来构造矛盾。

那么我们再构造一个图灵机，R。在R中，先调用P（M,I),如果P（M，I）返回M不停机，那么R停止，如果P（M,I)返回M停机，那么图灵机R进入死循环。接下来我们考虑R在自己的编码\<R\>上的运行情况。当然，要把M 和 I 分别绑定为 R ， \<R\>.那么矛盾就出来了，如果P（R，\<R\>) 不停机，那么R就停机，如果P（R，\<R\>)停机，那么R就停机。
如果上面太乱的话，这里有牛人的解释。[^1]
总之结论显而意见，停机问题不可计算。

图灵通过构建一台想像中的机器，完成了对希尔伯特的可判定性的回答。跟哥德尔不完备性定义一起埋葬了雄心勃勃的希尔伯特计划。

于此几乎同时间，邱奇通过另外一个有趣的系统也得到了类似的结论。这个有趣的系统就是lambda calculus。

### lambda calculus
##### Lambda Calculus Syntax
1. 函数定义：
在lambda calculus 里一个函数就是一个表达式，写作
lambda x . body
一个函数带有一个参数x，返回body的计算值。我们说这个lambda 表达式绑定了这个参数
2. 标识符引用（identifier reference)
一个标识符引用就是一个名字。这个名字对应着 包括这个引用的函数 定义的参数。
3. 函数应用(function application)
就是把要应用的值放到函数定义的后面就行了。
(lambda x . plus x x ) y

##### currying
搞Haskell 对currying 有一些了解，在有first class function 的语言里，curry的存在是方便把多参函数简化到单参函数的一种方法。

如果你仔细看上面的定义的话，lambda的参数只有一个，解决参数的限制的关键在于认识到函数也是数据（用更严格的说法，是值）。既然是数据，就可以传来穿去。如果有两个参数，我们可以写一个接受一个参数的函数，而这个函数返回的是接受第二个参数的函数。在有些编程语言中，currying是语言默认的。

接下来我们给个例子，比如我们想要写一个函数，把 x 和 y 加起来。我们可能会写出来像这样。
> lambda x y . plus x y.
实际上，我们写一个函数，接受一个参数，返回另外一个函数来接受另外一个参数。
就像这样：
> lambda x . (lambda y . plus  x y)
对于lambda 系统来说，多个参数并不是真正的多参，而是简单的语法简化，这是关键。

#### Free vs Bound Identifiers
上文提到的标识符和变量是一个意思。我们用currying解决了如果处理多参的问题，那么在讨论如何使用lambda 之前，我们还要解决一个重要的语法问题，closure。cloure这个词的翻译太多，闭包，封闭，等等。这里的closure 和 complete binding 一个意思。

对于一个 lambda calculus 表达式来说，当它被计算的时候，它无法查找到一个没有被绑定变量的值。也就是说，如果一个lambda calculus 被计算的时候，被计算的所有的变量，都被绑定。如果一个变量没有被任何的enclosing context bound, 那么我们叫这个变量叫 free variable.

下面是几个例子：
1. lambda x . plus x y : 在这个表达式里，“y” 和 “plus” 都是自由变量。而x（plus **x** y) 有界，因为它被包含在 plus x y里， 而plus x y 的参数有x。
2. lambda x y . y x : 在这个表达式里，x 和 y 都有界，因为它们是这个表达式的参数。
3.  lambda y . (lambda x . puls x y) ,在内嵌的表达式lambda x . plus x y 里 ， y 和 plus 是自由变量。而在整个表达式来看，x和y都有界，plus 依然自由。

我们用free(x) 来表示表达式x内所有自由变量的集合。
、
#### Lambda Calculus Evaluation Rules
lambda 算子的计算规则其实就俩，alpha和beta。 Alpha 规则又叫转换(conversion)规则，而beta规则又叫简化(reduction)规则

##### Alpha 转换
这个规则说的就是变量名可以更改：给定任意一个lambda表达式，我们可以任意改变参数的名字，只要我们相应地改变对应这些参数的变量名字。

下面是一个完整的alpha变换
> lambda x . if (= x 0) then 1 else x^2
> alpha\[x/y]
> lambda y . if (= y 0) then 1 else y^2
alpha 变换不会印象表达式的任何一点意思，但是这个规则很重要，它给了我们一种方法处理像递归这样的东西。

##### Beta简化
这个从本质上来说，可以算是替换模型，因为lambda calcus 中没有引入赋值，所以替换模型是成立的。详情请看SICP第三章。
对于lambda 算子来说，我们只需要这一个规则，就可以让lambda算子实现一台计算机能做的任何计算。就像元图灵机。

Beta规则是说，应用一个函数，等价于把函数体内有界的变量替换成对应参数的实际值，并把原来的函数做一个拷贝。

假设我们要应用一个函数
(lambda x . x + 1) x ，Beta规则是说，我们把整个表达式里有界的参数替换成有界参数的值。最后的结果是"3 + 1"

一个更复杂表达式的例子就像:
lambda y . (lambda x . x + y)) q
结果是 lambda x . x + q,简单来说，这就是一个生成表达式的表达式。

Beta的严格定义如下
> lambda x . B e = B\[x := e] if free(e) /subset free(B\[x := e]
这个定义末尾的条件，说明了我们需要Alpha转换的原因，仅当beta简化不会引起有界变量和自由变量冲突的时候，我们可以实施Beta化简。
如果自由变量和有界变量重名，我们必须先用alpha转换，使得重名变量不再重名。 

我们给个例子来说明:
(lambda z . (lambda x . x + z )) ( x + 2)
在实际的参数"(x+2)"里,x 是自由变量。但 x 不是表达式 lambda x . x + z 的自由变量。 也就是说, free(e) /subset free(B \[x:=e])不成立,如果我们直接开始简化，那么就可以得到
(lambda z . (lambda x . x + z)) ( x + 2)

lambda x . x + x + 2

应用上面的式子
(lambda x . x + x + 2 ) 3 
得到 3 + 3 + 2

如果我们先使用 alpha 变换。

by alpha\[x/y]: lambda z . ( lambda y . y + z )) (x + 2)
by beta: lambda y . y + x + 2) 3
by beta again : 3 + x +2

以上两种规则即可使 lambda calculus 为图灵完备的计算体系，我们还可以加上一个 Eta-化简 ，不过不是必须的。

#### Church Numerals

lambda 算子里根本没有数字。我们只有函数，所以我们需要一种用函数来表示数字的做法。
这种做法是由邱奇来搞出来的，这种用来表示数字的函数，叫做邱奇数（Church Numerals)

在邱奇数里，所有的数字都是两个参数的函数：
1. 零是 lambda s z . z 
2. 一是 lambda s z . s z
3. 二是 lambda s z . s ( s z)
4. 对于任意一个数"n" , 他的邱奇数都是一个函数 这个函数把他的第一个参数应到第二个参数上 n 次。
	用类似上面的写法就是 
![][image-1]
理解这个定义的好玩的办法是 把 s 看做后继函数（successor function）那么下个数就是把后继函数应用到前一个数上。

不过只有数还是不行，那么我们来看邱奇数对应的运算规则。
let add = lambda s z x y . x s (y s z)
那么这个这个数怎么去理解呢。
可以等价为
lambda x y  . (lambda s z . ( x s ( y s z )))
那么就是说，要把 x 和 y 相加，我们先用 s 和 z 创建邱奇数 y，然后再把 x 应用到 y 上。
我们把 add 应用到 2 和 3 上，来表示 2 + 3
add (lambda s2 z2 . s2 (s2 z2)) (lambda s3 z3 . s3 (s3 (s3 z3)))
把 add 替换为定义
(lambda x y .(lambda s z. (x s y (s z)))) (lambda s2 z2 . s2 (s2 z2)) (lambda s3 z3 . s3 (s3 (s3 z3)))

得到
lambda s z .( ( lambda s2 z2 . s2 (s2 z2)) s (lambda s3 z3 . s3 (s3 (s3 z3)) s z))
接下来对邱奇数三做 beta 置换
得到
lambda s z . (lambda s2 z2 . s2 (s2 z2)) s (s (s (s z)))

得到
lambda s z . s (s (s (s (s z))))

得到邱奇数5！

#### Booleans and Choice in Lambda Calculus
我们有了数的概念，接下来我们还差两件东西就可以建立起一个计算体系。选择的表达，以及循环的表达。我们先来看看如何表达选择。

类似邱奇数的定义，我们定义 TRUE 和 FALSE 的值作为一个函数，执行 if-then-else expression 在它的参数上。

let TRUE = lambda x y . x
let FALSE = lambda x y . y

那么我们现在可以去写一个 if 函数。
let IfThenElse = lambda cone true\_expr false\_expr . cond true\_expr false\_expr

我们接下来定义几个常规的逻辑操作

let BoolAnd = lambda x y .x y FALSE
let BoolOr = lambda x y. x TRUE y
let BoolNot = lambda x . x FALSE TRUE

看上去很奇妙，我们拿一个最简单的例子验证一下。

BoolAnd TRUE FALSE
展开得到
BoolAnd (lambda x y . x) (lambda x y . y)
Alpha:
BoolAnd (lambda xt yt . xt) (lambda xf yf . yf)  
expand BoolAnd:
(lambda x y . x y FALSE)(lambda xt yt . xt) (lambda xf yf . yf)
beta:
(lambda xf yf. yf) (lambda xt yt . xt) FALSE
beta:
FALSE

所以 BoolAnd FALSE TRUE = FALSE

接下来对 BoolAnd TRUE TRUE 做验证:
展开：
BoolAnd (lambda x y . x) (lambda x y . x)
Alpha: BoolAnd (lambda xa ya . xa) (lambda xb yb . xb)
展开：
(lambda x y . x y FALSE) (lambda xa ya . xa) (lambda xb yb . xb)
Beta:
(lambda xa ya . xa ) (lambda xb yb .xb ) FALSE
Beta:
(lambda xb y b . xb)

得到 BoolAnd TRUE TRUE = TRUE

##### Y combiner
lambda calculus 用递归来表示循环。但是因为所有的函数在 lambda calculus 里没有名字，我们实现递归就必须要一些有意思的技巧。我们管这个叫做 Y combinator,或者叫不动点算子。

我们从一个简餐的递归函数开始。
factorial(n) = 1 if n = 0
factorial(n) = n\* factorial(n-1) if n \> 0 

如果我们想要在 lambda calculus 里面表示这些，我们需要有几个工具。如何表示跟零相等，如何表示相成，如何去做减一操作。

对于相等我们用 IsZero,来表示。有三个参数：number number1 number2。如果 number 为零 返回number1,否则返回 number2。
对于相乘我们用 Mult x y 表示。
对于减一我们用 Pred x 来表示。返回 x - 1.

那么我们对factorial 可以翻译成.

lambda n . IsZero n 1 ( Mult n ( something (Pred n)))

现在我们可以对 something 来做一个定义。我们把 something 叫做结合子。组合子是特殊的高阶函数，在组合子的定义中不出现变量，只有函数调用。高阶函数是指，函数拿函数作为参数，返回一个参数。

Y combinator 是特殊甚至魔幻的一个函数，是 Y combinator 可以让递归成为可能。
下面是 Y combinator 的一种形式。
 let Y = lambda y . (lambda  x . y ( x x )) (lambda x . y ( x x))

Y 的特殊之处在于把 Y 应用到自身创造出另外一个 Y。
就是(Y Y) = Y( Y Y)

我们来验证一下上面的式子
Y Y
展开
(lambda y . (lambda x . y (x x)) (lambda x . y ( x x))) Y
Beta:
(lambda x . Y (x x)) (lambda x . Y (x x)))
Alpha\[x/z]到第二个式子
(lambda x . Y (x x)) (lambda z .Y (x x)))
Beta:
Y (( lambda z . Y (z z)) ( lambda z .Y (z z)))
展开 Y:
(lambda y . ( lambda x . y (x x)) (lambda x . y (x x)) ((lambda z . Y (z z)) (lambda z .Y (z z)))

Alpha\[y/a]\[x/b]:
(lambda a . ( lambda b . a (b b)) (lambda b . a (b b)))
((lambda z . Y (z z)) (lambda z . Y (z z)))

Beta:
(lambda b . ((lambda z . Y (z z)) (lambda  z. Y (z z))) ((b b )) (lambda b . ((lambda z . Y (z z)) (lambda z . Y (z z))) (b b))
Alpha\[b/x]\[z/y]:
(lambda x . (lambda y . Y (y y)) (lambda y . Y (y y))) (x  y)) (lambda x . ( lambda y . Y(y y))(lambda y . Y(y y))) (x x))
因为 
(Y Y)  = (lambda x . Y (x x)) (lambda x. Y (x x))
为
(lambda x . (Y Y) (x x )) (lambda x . (Y Y) (x x)

就是 Y Y = Y ( Y Y),Y可以不断重复自己。
(Y Y) = (Y ( Y Y ) = Y( Y (Y Y))

我们怎么去使用 Y 算子呢。
接上文的例子，定义阶乘函数为
let fact = lambda n . IsZero n 1 (Mult n (fact (Pred n)))

我们在这里定义的阶乘函数实际上是假设有一个全局变量 fact 的，我们下在要做的是怎么能在函数定义里去调用一个 fact。我们可以尝试定义一个函数。让他以 fact 为传入参数，然后我们再去写 fact 函数，让 fact 调用 fact 成为可能。

let metafact = lambda fact . (lambda n . IsZero n 1 (Mult n (fact Pred n))))

现在我们可以把 metafact 应用到他自身身上。

fact n =  (metafact metafact) n

当我们想要递归的时候 metafact ( Y metafact) 会给我们我们想要的。展开得到

(lambda fact . (lambda n . IsZero n 1 (Mult n (fact (Pred n))))) (Y (lambda fact . (lambda n . IsZero n 1 (Mult n (fact (Pred n))))))

这里上面的 lambda 里 fact 的参数是 (Y metafact)。那么我们可以得到，当 n 是 0 的时候 返回 1，当 n 不为零的时候，我们就调用 fact (pred n). fact 等价于 Y metafact.得到的是 metafact (Y metafact) (Pred n)

实际上用不严肃的写法可能更好的去理解这个事情。
metafact (Y metafact) n = mult n (Y metafact） （pred n)
= mult n (metafact (y metafact) pred n)
= mult n (metafact (y metafact) n -1)
这就是递归的过程，只是定义了一个 metafact 和 Y , 就实现了递归!!!


#### From Lambda calculus to Combinator Calculus

SKI组合子。
SKI的定义如下
1. S: S是函数应用的组合子：S = lambda x y z . (x z (y z)).
2. K: K 生成一个常数函数。当把生成的常数函数应用到任何一个参数上，都会得到K的第一个参数：K = lambda x . (lambda y . x).
3. I: I其实是一个恒等函数：I = lambda x . x
那么他的简单例子如下
S K K x =
(K x) (K x) =
(lambda y . x) (lambda y . x) = 
x
组合子的意义在于不用任何变量，仅用 sk 就能组合出任何一个 lambda 表达式的等价表达。再进一步，每一个lambda表达式都可以被表达为二叉树，数的叶子就是S或K。
 





[^1]:	[http://www.cgl.uwaterloo.ca/~csk/halt/][1]

[1]:	http://www.cgl.uwaterloo.ca/~csk/halt/

[image-1]:	No_name__6_.png
