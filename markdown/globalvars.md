# 全局变量
Global variables

A global variable has a name beginning with $. It can be referred to from anywhere in a program. Before initialization, a global variable has the special value nil.

ruby> $foo
   nil
ruby> $foo = 5
   5
ruby> $foo
   5
Global variables should be used sparingly. They are dangerous because they can be written to from anywhere. Overuse of globals can make isolating bugs difficult; it also tends to indicate that the design of a program has not been carefully thought out. Whenever you do find it necessary to use a global variable, be sure to give it a descriptive name that is unlikely to be inadvertently used for something else later (calling it something like $foo as above is probably a bad idea).

One nice feature of a global variable is that it can be traced; you can specify a procedure which is invoked whenever the value of the variable is changed.

ruby> trace_var :$x, proc{puts "$x is now #{$x}"}
   nil
ruby> $x = 5
$x is now 5
   5
When a global variable has been rigged to work as a trigger to invoke a procedure whenever changed, we sometimes call it an active variable. For instance, it might be useful for keeping a GUI display up to date.

There is a collection of special variables whose names consist of a dollar sign ($) followed by a single character. For example, $$ contains the process id of the ruby interpreter, and is read-only. Here are the major system variables:
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

它们的名称表明它们应该是全局的，但是它们在这种方式中更有用，使用这些名字的历史原因也有很多。