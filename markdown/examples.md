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

你可能还注意到了没有`return`语句，因为它并不是必须要有的，**Ruby**中函数将自动返回最后一个求得的值。在这里使用`return`指令是可以的，但是却是多余的。

Let's try out our factorial function. Adding one line of code gives us a working program:

让我们试用一下我们的阶乘函数。给我们的程序添加一行：

```
 # 这个程序用来计算一个数字的阶乘
 # 将其保存到fact.rb
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

```
ruby fact.rb 1
1

ruby fact.rb 5
120
```

Does it work with an argument of 40? It would make your calculator overflow...

如果参数是40它仍会正常工作么？嗯，它可能会让你的计算器**溢出**......

```
ruby fact.rb 40
815915283247897734345611269596115894272000000000

```

It does work. Indeed, ruby can deal with any integer which is allowed by your machine's memory. So 400! can be calculated:

没问题，**Ruby**甚至还可以处理你机器内存所允许的任何整数，所以400的阶乘也可以被计算出来：

```
ruby fact.rb 400
64034522846623895262347970319503005850702583026002959458684445942802397169186831436278478647463264676294350575035856810848298162883517435228961988646802997937341654150838162426461942352307046244325015114448670890662773914918117331955996440709549671345290477020322434911210797593280795101545372667251627877890009349763765710326350331533965349868386831339352024373788157786791506311858702618270169819740062983025308591298346162272304558339520759611505302236086810433297255194852674432232438669948422404232599805551610635942376961399231917134063858996537970147827206606320217379472010321356624613809077942304597360699567595836096158715129913822286578579549361617654480453222007825818400848436415591229454275384803558374518022675900061399560145595206127211192918105032491008000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
```

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

上面的 **^D** 代表 **Ctrl+D**，它是一种用于在**Unix**上下文中表示结束输入的传统方法，在**DOS/Windows**上，对应的则应该输入**F6**或**Ctrl+Z**。

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

在本指南中，当我们正在运行`eval.rb`这个有用的程序时，就会有`ruby>`这个输入提示。

[上一章 起步](./getstarted.md "起步")
[下一章 字符串](./strings.md "字符串") 
