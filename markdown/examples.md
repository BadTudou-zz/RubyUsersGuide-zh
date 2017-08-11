# 简单示例

**Simple examples**

**简单示例**

Let's write a function to compute factorials. The mathematical definition of `n` factorial is:

让我们来写一个计算阶乘的函数。`n`的阶乘在数学上的定义是：

```
n! = 1                (when n==0)
   = n * (n-1)!       (otherwise)
```

In ruby, this can be written as:

在**Ruby**中，我们可以这样写：

```
def fact(n)
  if n == 0
​    1
  else
​    n * fact(n-1)
  end
end
```

You may notice the repeated occurrence of `end`. Ruby has been called "Algol-like" because of this. (Actually, the syntax of ruby more closely mimics that of a langage named Eiffel.)

你可能注意到了上面反复出现的`end`，正是由于这个原因，**Ruby**也被称为“**类Algol**”语言(事实上，**Ruby**的语法更接近模仿一门叫做**Eiffel**的语言)。

You may also notice the lack of a `return` statement. It is unneeded because a ruby function returns the last thing that was evaluated in it. Use of a `return` statement here is permissible but unnecessary.

你可能还注意到了没有`return`语句，因为它并不是必须要有的，**Ruby**中函数将自动返回最后一个求得的值。因此这里可以选择要不要使用`return`，并没有强制规定要求必须要使用它。

Let's try out our factorial function. Adding one line of code gives us a working program:

让我们试用一下我们的阶乘函数。给我们的程序添加一行：

```
 # Program to find the factorial of a number
 # Save this as fact.rb
def fact(n)
  if n == 0
    1
  else
    n * fact(n-1)
  end
end
puts fact(ARGV[0].to_i)
```
Here, `ARGV` is an array which contains the command line arguments, and `to_i` converts a character string to an integer.

这里，`ARGV`是一个包含了**命令行参数**的**数组**，`to_i`则将一个字符转换成了整数。

`% ruby fact.rb 1`
**1**
`% ruby fact.rb 5`
**120**

Does it work with an argument of 40? It would make your calculator overflow...

如果参数是40它仍会正常工作么？嗯，它可能会让你的计算器**溢出**......

`% ruby fact.rb 40`
**815915283247897734345611269596115894272000000000**

It does work. Indeed, ruby can deal with any integer which is allowed by your machine's memory. So 400! can be calculated:

没问题，**Ruby**甚至还可以处理你机器内存所允许的任何整数，所以400的阶乘也可以被计算出来：

`% ruby fact.rb 400`
**64034522846623895262347970319503005850702583026002959458684**
**44594280239716918683143627847864746326467629435057503585681**
**08482981628835174352289619886468029979373416541508381624264**
**61942352307046244325015114448670890662773914918117331955996**
**44070954967134529047702032243491121079759328079510154537266**
**72516278778900093497637657103263503315339653498683868313393**
**52024373788157786791506311858702618270169819740062983025308**
**59129834616227230455833952075961150530223608681043329725519**
**48526744322324386699484224042325998055516106359423769613992**
**31917134063858996537970147827206606320217379472010321356624** 
**61380907794230459736069956759583609615871512991382228657857** 
**95493616176544804532220078258184008484364155912294542753848** 
**03558374518022675900061399560145595206127211192918105032491** 
**00800000000000000000000000000000000000000000000000000000000**
**0000000000000000000000000000000000000000000**

We cannot check the correctness at a glance, but it must be right. :-)

我们显然不能通过匆匆一瞥就能判断其是否正确，但它应该是没有问题的。:-)

## The input/evaluation loop

## 输入/执行 交互环境

When you invoke ruby with no arguments, it reads commands from standard input and executes them after the end of input:

当你调用**Ruby**时没有传递参数，它将从**标准输入设备**读取命令，并在输入结束后执行输入的命令。

```% ruby
puts "hello world"
puts "good-bye world"
^D
```
**hello world**
**good-bye world**

The *^D* above means control-D, a conventional way to signal end-of-input in a Unix context. In DOS/Windows, try pressing *F6* or *^Z* instead.

上面的**^D**代表**Ctrl+D**，它是一种用于在**Unix**上下文中表示结束输入的传统方法，在**DOS/Windows**上，对应的则应该输入**F6**或**Ctrl+Z**。

Ruby also comes with a program called `eval.rb` that allows you to enter ruby code from the keyboard in an interactive loop, showing you the results as you go. It will be used extensively through the rest of this guide.

**Ruby**还附带了一个名为`eval.rb`的程序，它允许你在一个交互环境中从键盘输入**Ruby**代码，并且在退出后将结果返回给你。在本指南的其他章节，我们将广泛使用它。

If you have an ANSI-compliant terminal (this is almost certainly true if you are running some flavor of UNIX; under old versions of DOS you need to have installed `ANSI.SYS` or `ANSI.COM`; Windows XP, unfortunately, has now made this nearly impossible), you should use this [enhanced `eval.rb`](http://www.rubyist.net/~slagell/ruby/eval.txt)that adds visual indenting assistance, warning reports, and color highlighting. 

如果您有一个兼容**ANSI**的终端，那么你就应该使用这个[增强版的`eval.rb`](http://www.rubyist.net/~slagell/ruby/eval.txt)。(如果你运行的是**UNIX**系列的系统，这几乎是肯定的;在旧版本的**DOS**下，那么你需要安装`ANSI.SYS`或`ANSI.COM`；不幸的是，**Windows XP**现在几乎还不可能实现这一点了)。增强版的`eval.rb`增加了视觉缩进帮助，警告提醒以及颜色高亮。

Otherwise, look in the `sample` subdirectory of the ruby distribution for the non-ANSI version that works on any terminal. Here is a short `eval.rb` session:

如果不是的话，请查看在任何终端上工作的**非ANSI**版本的**Ruby**的`sample`子目录。以下是一个简短的`eval.rb`会话:

```% ruby eval.rb
ruby>  puts "Hello, world."
Hello, world.
​	nil
ruby>  exit
```

`hello world` is produced by `puts`. The next line, in this case `nil`, reports on whatever was last evaluated; ruby does not distinguish between *statements* and *expressions*, so evaluating a piece of code basically means the same thing as executing it. 

`hello world`是由`puts`产生的。在这个例子中下一行是`nil`，它代表最后一次计算的结果；**Ruby**没有区分语句和表达式，因此对一段代码进行计算基本上等同于执行它。

Here, `nil` indicates that `puts` does not return a meaningful value. Note that we can leave this interpreter loop by saying `exit`, although `^D` still works too.

这里的`nil`表示`puts`没有返回一个有意义的值。注意，我们可以通过`exit`命令来离开这个解释器交互环境，或者也使用之前的`Ctrl+D`。

Throughout this guide, "`ruby>`" denotes the input prompt for our useful little `eval.rb` program.

在本指南中，当我们正在运行`eval.rb`这个有用的程序时，就会有`Ruby`这个输入提示。