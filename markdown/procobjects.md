# 过程对象
**Procedure objects**

**过程对象**

It is often desirable to be able to specify responses to unexpected events. 

我们通常希望能够指定对意外事件的响应。

As it turns out, this is most easily done if we can pass blocks of code as arguments to other methods, which means we want to be able to treat code as if it were data.

事实证明，如果我们可以将代码块作为参数传递给其他方法，这是最容易做到的，这意味着我们希望能够将代码看作是数据。

A new procedure object is formed using proc:

一个新的过程对象是通过`proc`来形成的：

```
ruby> quux = proc {
    |   puts "QUUXQUUXQUUX!!!"
    | }
   #<Proc:0x4017357c>
```

Now what quux refers to is an object, and like most objects, it has behavior that can be invoked. Specifically, we can ask it to execute, via its call method:

现在quux指向了一个对象，并且如同大多数对象，它有行为可供调用。特别的，我们可以通过它的`call`方法来要求它执行。

```
ruby> quux.call
QUUXQUUXQUUX!!!
   nil
```
So, after all that, can quux be used as a method argument? Sure.

那么，在这之后，可以使用quux作为一个方法参数吗?当然。

```
ruby> def run( p )
    |   puts "About to call a procedure..."
    |   p.call
    |   puts "There: finished."
    | end
   nil
ruby> run quux
About to call a procedure...
QUUXQUUXQUUX!!!
There: finished.
   nil
```

The trap method lets us assign the response of our choice to any system signal.

`trap`方法允许我们将选择的响应分配给任何系统信号。

```
ruby> inthandler = proc{ puts "^C was pressed." }
   #<Proc:0x401730a4>
ruby> trap "SIGINT", inthandler
   #<Proc:0x401735e0>
```

Normally pressing ^C makes the interpreter quit. 

通常情况下，`^C`会让解释器退出。

Now a message is printed and the interpreter continues running, so you don't lose the work you were doing. (You're not trapped in the interpreter forever; you can still exit by typing exit.)

现在已经打印了一条消息，解释器继续运行，所以你不会丢失你正在做的工作。(你不会被永远困在解释器中;你仍然可以通过输入`exit`来退出。)

A final note before we move on to other topics: it's not strictly necessary to give a procedure object a name before binding it to a signal. An equivalent anonymous procedure object would look like

在我们继续讨论其他话题之前最后要注意的是：在将其绑定到一个信号之前，不需要给一个过程对象一个名称。一个等价的匿名过程对象是

```
ruby> trap "SIGINT", proc{ puts "^C was pressed." }
   nil
```

or more compactly still,

或者更加简洁,

```
ruby> trap "SIGINT", 'puts "^C was pressed."'
   nil
```

This abbreviated form provides some convenience and readability when you write small anonymous procedures.

当您编写小型的匿名程序时，这个简短的表单提供了一些便利和可读性。

[上一章 模块](./modules.md "Modules")
[下一章 变量](./variables.md "Variables")
