# 全局变量
**Global variables**

**全局变量**

A global variable has a name beginning with $. 

**全局变量**的名字以`$`开头。

It can be referred to from anywhere in a program. Before initialization, a global variable has the special value nil.

你可以在程序的任何地方引用**全局变量**。在对其进行初始化之前，一个全局变量的值是特殊的`nil`值。

```
ruby> $foo
   nil
ruby> $foo = 5
   5
ruby> $foo
   5
```

Global variables should be used sparingly. 

应当谨慎使用**全局变量**。

They are dangerous because they can be written to from anywhere. 

全局变量非常危险，因为它们可以在任何地方被改写。

Overuse of globals can make isolating bugs difficult; it also tends to indicate that the design of a program has not been carefully thought out. 

过度使用**全局变量**会使隔离Bug变得很困难;它也倾向于表明一个程序的设计并没有经过仔细的考虑。

Whenever you do find it necessary to use a global variable, be sure to give it a descriptive name that is unlikely to be inadvertently used for something else later (calling it something like $foo as above is probably a bad idea).

无论何时，当你发现确实有必要使用**全局变量**时，一定要给它一个描述性的名称，这个名称不太可能在以后因为其他事情而无意中使用它(将其命名为`$foo`很可能是一个坏主意)。

One nice feature of a global variable is that it can be traced; you can specify a procedure which is invoked whenever the value of the variable is changed.

**全局变量**的一个很好的特性是它可以被跟踪;你可以指定一个**过程**，该**过程**在变量的值被更改时被调用。

```
ruby> trace_var :$x, proc{puts "$x is now #{$x}"}
   nil
ruby> $x = 5
$x is now 5
   5
```

When a global variable has been rigged to work as a trigger to invoke a procedure whenever changed, we sometimes call it an active variable. 

当一个**全局变量**被操纵，作为触发器来调用一个过程时，我们有时会把它称为一个**活动变量**。

For instance, it might be useful for keeping a GUI display up to date.

例如，对于保持GUI展示最新内容，全局变量可能有用。

There is a collection of special variables whose names consist of a dollar sign ($) followed by a single character. 

有一组特殊的变量，它们的名字由一个美元符号(`$`)组成，后面跟着一个字符。

For example, $$ contains the process id of the ruby interpreter, and is read-only. Here are the major system variables:

例如，`$$`包含**Ruby**解释器的进程id，并且是只读的。以下是主要的系统变量:

|  标识符 |                    类型 |
| ---: | --------------------: |
|   $! |               最新的错误消息 |
|   $@ |                 错误的位置 |
|   $_ |              最后读取的字符串 |
|   $. |           解释器读取的最后的行号 |
|   $& |         最后匹配的正则表达式字符串 |
|   $~ |     最后的正则表达式匹配，子表达式数组 |
|   $n | 最后匹配的第N个子表达式 (同$~[n]) |
|   $= |             不区分大小写的标记 |
|   $/ |               输入记录分隔符 |
|   $\ |               输出记录分隔符 |
|   $0 |           Ruby脚本文件的名字 |
|   $* |                 命令行参数 |
|   $$ |               解释器进程ID |
|   $? |          执行子进程的最后退出状态 |

In the above, $_ and $~ have local scope. 

上面的`$_`和`$~`都有局部作用域。

Their names suggest they should be global, but they are much more useful this way, and there are historical reasons for using these names.

它们的名称表明它们应该是全局的，但是它们在这种方式中更有用，使用这些名字有一些历史原因。

[上一章 变量](./variables.md "Variables")
[下一章 实例变量](./instancevars.md "Instance variables")
