# 其他
**Nuts and bolts**

**其他**

This chapter addresses a few practical issues.

这一章解决了一些实际问题。

**Statement delimiters**

**语句分隔符**

Some languages require some kind of punctuation, often a semicolon (;), to end each statement in a program. 

有些语言需要某种标点符号，通常是分号(`;`)，以结束程序中的每个语句。

Ruby instead follows the convention used in shells like sh and csh. 

**Ruby**替换了了在像sh和csh这样的shell中使用的约定。

Multiple statements on one line must be separated by semicolons, but they are not required at the end of a line; 

同一行的多条语句必须用分号分隔，但在一行的末尾不需要;

a linefeed is treated like a semicolon. If a line ends with a backslash (\\), the linefeed following it is ignored; this allows you to have a single logical line that spans several lines.

一个换行符被当作分号对待。如果一行以fa反斜线(`\`)结尾，下面的换行符将被忽略。这允许你有一个跨越多行代码的逻辑行。

**Comments**

**注释**

Why write comments? 

为何要写注释？

Although well written code tends to be self-documenting, it is often helpful to scribble in the margins, and it can be a mistake to believe that others will be able to look at your code and immediately see it the way you do. 

尽管好的代码能够自我说明，但在空白处乱涂乱画通常也是有帮助的，如果相信其他人能够看到你的代码，并能一下就看到你的代码，那就大错特错了。

Besides, for practical purposes, you yourself are a different person within a few days anyway; which of us hasn't gone back to fix or enhance a program after the passage of time and said, I know I wrote this, but what in blazes does it mean?

此外，出于实际的目的，你自己在几天之内就会将之前写的代码遗忘。我们中的哪一个人在经过了一段时间后没有回过头去修复或加强一个项目，我知道我写了这个代码，但这到底是什么意思呢?

Some experienced programmers will point out, quite correctly, that contradictory or outdated comments can be worse than none at all.

一些有经验的程序员会指出，毫无疑问的是，矛盾或过时的注释可能比没有任何东西更糟糕。

Certainly, comments shouldn't be a substitute for readable code; 

没错，注释不应该是可读代码的替代品;

if your code is unclear, it's probably also buggy. 

如果你的代码不清晰，那它可能也会有问题

You may find that you need to comment more while you are learning ruby, and then less as you become better at expressing your ideas in simple, elegant, readable code.

你可能会发现，在学习**Ruby**时，你需要更多地注释，而当你在简单、优雅、可读的代码中表达自己的想法时，注释就会变得更少。

Ruby follows a common scripting convention, which is to use a pound symbol (#) to denote the start of a comment. 

**Ruby**遵循一种常见的脚本约定，即使用磅符号(`#`)来表示注释的开始。

Anything following an unquoted #, to the end of the line on which it appears, is ignored by the interpreter.

任何被`#`引用，到其出现的行尾的内容，都会被解释器忽略。

Also, to facilitate large comment blocks, the ruby interpreter also ignores anything between a line starting with "=begin" and another line starting with "=end".

此外，为了方便大型的注释块，**Ruby**解释器还忽略了从“`=begin`”开始的一行和从“`=end`”开始的另一行。

```
#!/usr/bin/env ruby

=begin
**********************************************************************
  This is a comment block, something you write for the benefit of
  human readers (including yourself).  The interpreter ignores it.
  There is no need for a '#' at the start of every line.
**********************************************************************
=end
```

**Organizing your code**

**组织你的代码**

Ruby's unusually high level of dynamism means that classes, modules, and methods exist only after their defining code runs. 

**Ruby**异常高的动态级别意味着类、模块和方法只在它们定义的代码运行之后才存在。

If you're used to programming in a more static language, this can sometimes lead to surprises.

如果你习惯于用一种更静态的语言编程，这有时会导致意外。

```
# The below results in an "undefined method" error:

puts successor(3)

def successor(x)
  x + 1
end
```

Although the interpreter checks over the entire script file for syntax before executing it, the def successor ... end code has to actually run in order to create the successor method. So the order in which you arrange a script can matter.

尽管解释器在执行脚本之前将检查整个脚本的语法，`def successor … end`为了创建后续的方法，终端代码必须实际运行。

This does not, as it might seem at first glance, force you to organize your code in a strictly bottom-up fashion. 

这并不像乍看上去那样，强迫你以一种严格的自下而上的方式组织您的代码。

When the interpreter encounters a method definition, it can safely include undefined references, as long as you can be sure they will be defined by the time the method is actually invoked:

当解释器遇到方法定义时，它可以安全地包含未定义的引用，只要你确信它们将在方法实际被调用的时间被定义:

```
# Conversion of fahrenheit to celsius, broken
# down into two steps.

def f_to_c(f)
  scale(f - 32.0)  # This is a forward reference, but it's okay.
end

def scale(x)
  x * 5.0 / 9.0
end

printf "%.1f is a comfortable temperature.\n", f_to_c(72.3)
```

So while this may seem less convenient than what you may be used to in Perl or Java, it is less restrictive than trying to write C without prototypes (which would require you to always maintain a partial ordering of what references what). 

因此，虽然这看起来不像你在**Perl**或**Java**中所使用的那样方便，但它没有尝试编写没有原型的C(这将要求你始终保持对引用的部分顺序的部分排序)。

Putting top-level code at the bottom of a source file always works. And even this is less of an annoyance than it might at first seem. 

在源文件的底部放置顶级代码总是有效的。即使这样，也不像乍看起来那样令人烦恼。

A sensible and painless way to enforce the behavior you want is to define a main function at the top of the file, and call it from the bottom.

执行你想要的行为的一种明智而无痛的方法是在文件的顶部定义一个主函数，并从底部调用它。

```
#!/usr/bin/env ruby

def main
  # Express the top level logic here...
end

# ... put support code here, organized as you see fit ...

main # ... and start execution here.
```

It also helps that ruby provides tools for breaking complicated programs into readable, reusable, logically related chunks. 

**Ruby**还提供了一些工具，可以将复杂的程序分解为可读的、可重用的、逻辑相关的块。

We have already seen the use of include for accessing modules. 

我们已经看到了用于访问模块的`include`。

You will also find the load and require facilities useful. 

您还会发现`load`和`require`的有用的工具。

load works as if the file it refers to were copied and pasted in (something like the #include preprocessor directive in C). require is somewhat more sophisticated, causing code to be loaded at most once and only when needed.

`load`工作的方式就像它所引用的文件被复制和粘贴到(类似于**C**中的预处理器指令)一样，需要更复杂一些，只需要在需要时才加载代码。

**That's it...**

**就是这样**

This tutorial should be enough to get you started writing programs in Ruby. 

本教程应该足以让你开始用**Ruby**编写程序。

As further questions arise, you can get more help from the user community, and from an always-growing body of printed and online resources.

其他的信息，你可以从用户社区获得更多的帮助，从不断增长的出版物和在线资源中获得更多的帮助。

Good luck, and happy coding!

祝你好运，编程快乐！

[上一章 对象初始化](./objinitialization.md "Object initialization")
[下一章 关于本指南](./about.md "About the guide")