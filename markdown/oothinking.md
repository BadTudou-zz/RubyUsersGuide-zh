# 面向对象的思考
**Object-oriented thinking**

**面向对象的思考**

Object oriented is a catchy phrase. To call anything object oriented can make you sound pretty smart. Ruby claims to be an object oriented scripting language; but what exactly does "object oriented" mean?

**面向对象**是一个引人注目的措辞。调用任何面向对象的东西都让你听起来感觉相当时髦。**Ruby**声称是面向对象的脚本语言，但是“**面向对象**”的确切含义又是什么呢？

There have been a variety of answers to that question, all of which probably boil down to about the same thing. Rather than sum it too quickly, let's think for a moment about the traditional programming paradigm.

关于这个问题有各种各样的答案，但所有这些都可能归结为同一件事。让我们来思考一下传统的编程范例，而不是简单地总结一下。

Traditionally, a programming problem is attacked by coming up with some kinds of data representations, and procedures that operate on that data. 

传统上，编程问题受到了一些数据表示形式，以及对这些数据进行操作的过程的攻击。

Under this model, data is inert, passive, and helpless; it sits at the complete mercy of a large procedural body, which is active, logical, and all-powerful.

在这个模型下，数据是惰性的，被动的，没有帮助的。它完全取决于一个庞大的程序主体，它是活跃的、合乎逻辑的，而且是全能的。

The problem with this approach is that programs are written by programmers, who are only human and can only keep so much detail clear in their heads at any one time. 

这种方法的问题在于程序是由程序员编写的，他们是人类，在任何时候，都只能在头脑中清楚地知道这些细节。

As a project gets larger, its procedural core grows to the point where it is difficult to remember how the whole thing works. 

随着项目规模的扩大，它的处理核心逐渐增长到难以记住整个过程是如何运作的地步。

Minor lapses of thinking and typographical errors become more likely to result in well-concealed bugs. 

思维和排版错误的小错误更容易导致隐藏的bug。

Complex and unintended interactions begin to emerge within the procedural core, and maintaining it becomes like trying to carry around an angry squid without letting any tentacles touch your face. 

复杂的和非预期的交互开始在过程核心中出现，维护它就像尝试让愤怒的鱿鱼不把任何触手碰到你脸上一样。

There are guidelines for programming that can help to minimize and localize bugs within this traditional paradigm, but there is a better solution that involves fundamentally changing the way we work.

有一些编程指南可以帮助最小化和局部化这个传统范例中的bug，但有一个能从根本上改变了我们的工作方式懂更好的解决方案。

What object-oriented programming does is to let us delegate most of the mundane and repetitive logical work to the data itself; it changes our concept of data from passive to active.

**面向对象编程**所做的是让我们将大多数普通的和重复的逻辑工作委托给数据本身，它改变了我们从被动到主动的数据概念。

Put another way,We stop treating each piece of data as a box with an open lid that lets us reach in and throw things around.

换句话说，我们不再把每个数据都当作一个盒子，盒子里有一个打开的盖子，可以让我们可以进去，并且把东西放在里面。

We start treating each piece of data as a working machine with a closed lid and a few well-marked switches and dials.

我们开始把每一个数据都当作一个工作的机器，它有一个封闭的盖子，还有一些很好的开关和刻度盘。

What is described above as a "machine" may be very simple or complex on the inside; we can't tell from the outside, and we don't allow ourselves to open the machine up (except when we are absolutely sure something is wrong with its design), so we are required to do things like flip the switches and read the dials to interact with the data. Once the machine is built, we don't want to have to think about how it operates.

上面所描述的“机器”可能非常简单，也可能非常复杂。我们不能从外部识别它，我们也不能允许我们自己把它打开(除非我们完全确定它的设计有问题)。所以我们需要做一些如翻转开关，读取刻度盘的事情来与数据进行交互。一旦构建好机器，我们便不需要考虑它是如何运作的。

You might think we are just making more work for ourselves, but this approach tends to do a nice job of preventing all kinds of things from going wrong.

你可能认为我们只是在为自己做更多的工作，但是这种方法能很好地防止所有的事情出错。

Let's start with a example that is too simple to be of practical value, but should illustrate at least part of the concept. 

让我们从一个由简单到拥有实用价值的例子开始，但是应该至少说明这个概念的一部分。

Your car has a tripmeter. Its job is to keep track of the distance the car has travelled since the last time its reset button was pushed. 

你的车有一个里程表。它的工作是追踪汽车行驶的距离，这是自上次按下了重置按钮情况。

How would we model this in a programming language?

我们如何在编程语言中对其进行建模呢?

 In C, the tripmeter would just be a numeric variable, possibly of type float. The program would manipulate that variable by increasing its value in small increments, with occasional resets to zero when appropriate. 

在**C**语言中，里程表可能只是一个数值变量，并且它的类型可能是`float`。程序将通过增加小增量的值来操作这个变量，在适当的时候会重新设置为0。

What's wrong with that? A bug in the program could assign a bogus value to the variable, for any number of unexpected reasons. 

这样有什么问题呢？程序中的一个错误可以是为该变量分配了一个虚假的值，因为很多意想不到的原因。

Anyone who has programmed in C knows what it is like to spend hours or days tracking down such a bug whose cause seems absurdly simple once it has been found. (The moment of finding the bug is commonly indicated by the sound of a loud slap to the forehead.)

任何用**C**编程的人都知道，花上几个小时或几天时间来追踪这样的bug是什么感觉，因为一旦找到了它，它的起因似乎是荒谬的。(发现bug的那一刻，通常就像在你的脑门上拍上一记响亮的耳光)

The same problem would be attacked from a much different angle in an object-oriented context. 

同样的问题在面向对象的环境中会受到不同的角度的攻击。

The first thing a programmer asks when designing the tripmeter is not "which of the familiar data types comes closest to resembling this thing?" but "how exactly is this thing supposed to act?" 

程序员在设计里程表时要问的第一件事不是“哪个熟悉的数据类型最接近于这个东西”，而是“这件事该怎么做？”。

The difference winds up being a profound one. It is necessary to spend a little bit of time deciding exactly what an odometer is for, and how the outside world expects to interact with it. We decide to build a little machine with controls that allow us to increment it, reset it, read its value, and nothing else.

两者的区别是深刻的。有必要花时间来确定一个里程表是什么，以及它会外部世界是如何互动的。我们决定构建一个带有控制的小机器，我们可以对它进行增加，重置，读取，以及其他任何东西。

We don't provide a way for a tripmeter to be assigned arbitrary values; why? because we all know tripmeters don't work that way. 

为什么我们不提供一种可以让里程表被赋予任意的值的方法呢？为什么呢？因为我们都知道里程表不工作。

There are only a few things you should be able to do with a tripmeter, and those are all we allow.

有几件事可以让里程表去做，并且这些是我们所允许的。

Thus, if something else in the program mistakenly tries to place some other value (say, the target temperature of the vehicle's climate control) into the tripmeter, there is an immediate indication of what went wrong. 

因此，如果程序中的其他东西错误地尝试将其他值(比如车辆的气候控制的目标温度)放入里程表中，就会立即显示出哪里出了问题。

We are told when running the program (or possibly while compiling, depending on the nature of the language) that we are not allowed to assign arbitrary values to Tripmeter objects. 

当运行程序时(或者可能在编译时，取决于语言的性质)，我们被告知，我们不被允许将任意值赋给Tripmeter对象。

The message might not be exactly that clear, but it will be reasonably close to that. 

这个信息可能不是很清楚，但是它会和那个很接近。

It doesn't prevent the error, does it? But it quickly points us in the direction of the cause. This is only one of several ways in which OO programming can save a lot of wasted time.

它并不能阻止错误，不是么？但是它很快就为我们指向了方向。

We commonly take one step of abstraction above this, because it turns out to be as easy to build a factory that makes machines as it is to make an individual machine. 

我们通常在这上面做一个抽象的步骤，因为它很容易建造一个制造机器的工厂，就像制造一台机器一样。

We aren't likely to build a single tripmeter directly; rather, we arrange for any number of tripmeters to be built from a single pattern. 

我们不太可能直接就创建一个里程表，相反，我们可以从一个单个模式来构建里程表的任何部分。

The pattern (or if you like, the tripmeter factory) corresponds to what we call a class, and an individual tripmeter generated from the pattern (or made by the factory) corresponds to an object. Most OO languages require a class to be defined before we can have a new kind of object, but ruby does not.

这个模式(如果你喜欢的话也可以叫它里程表工厂)对应的是我们所称的类，从模式中产生的一个单独的里程表(或由工厂制造)对应于一个对象。大多数**OO**语言都需要在我们能够拥有一种新的对象之前先定义一个类，但是**Ruby**不这样做。

It's worth noting here that the use of an OO language will not enforce proper OO design. 

这里值得注意的是，使用**OO**语言并不会强制执行**OO**设计。

Indeed it is possible in any language to write code that is unclear, sloppy, ill-conceived, buggy, and wobbly all over. 

实际上，任何语言都有可能编写不清楚、草率、构思错误、漏洞百出、到处都是不稳定的代码。

What ruby does for you (as opposed, especially, to C++) is to make the practice of OO programming feel natural enough that even when you are working on a small scale you don't feel a necessity to resort to ugly code to save effort. 

**Ruby**为你所做的事情(而不是，特别的，对C++)，是使面向对象编程的实践变得足够自然，即使你正在进行小规模的工作，你也没有必要求助于丑陋的代码来节省精力。

We will be discussing the ways in which ruby accomplishes that admirable goal as this guide progresses; the next topic will be the "switches and dials" (object methods) and from there we'll move on to the "factories" (classes). Are you still with us?

我们将在这个指南中讨论**Ruby**实现这个令人钦佩的目标的方式，下一个主题将是“开关和刻度盘”(对象方法)，然后我们将进入“工厂”(类)。你要和我们一起探究下去么?