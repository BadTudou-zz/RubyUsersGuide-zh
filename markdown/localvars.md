# 局部变量
**Local variables**

**局部变量**

A local variable has a name starting with a lower case letter or an underscore character (_). 

一个**局部变量**的名称以小写字母或下划线`_`开头。

Local variables do not, like globals and instance variables, have the value nil before initialization:

不同于**全局变量**和**实例变量**，**局部变量**初始化之前并没有默认的`nil`值。

```
ruby> $foo
   nil
ruby> @foo
   nil
ruby> foo
ERR: (eval):1: undefined local variable or method `foo' for main(Object)
```

The first assignment you make to a local variable acts something like a declaration.

你对**局部变量**做的第一个赋值就像是一个声明。

If you refer to an uninitialized local variable, the ruby interpreter cannot be sure whether you are referencing a bogus variable; you might, for example, have misspelled a method name. Hence the rather nonspecific error message you see above.

如果你引用一个未初始化的**局部变量**，**Ruby**解释器无法确定你是否引用了一个伪变量。例如，你可能会拼错一个方法名。因此，您可以看到上面所看到的非特定的错误消息。

Generally, the scope of a local variable is one of

一般来说，**局部变量**的范围是

1. proc{ ... }

2. loop{ ... }
3. def ... end
4. class ... end
5. module ... end
6. 整个脚本 (除了上述情况之外)

In the next example, defined? is an operator which checks whether an identifier is defined. 

接下来的示例中，`defined?`操作符用来检测标识符是否定义。

It returns a description of the identifier if it is defined, or nil otherwise. 

如果标识符定义了，它将返回标识符，否则返回`nil`。

As you see, bar's scope is local to the loop; when the loop exits, bar is undefined.

如你所见，`bar`的作用域是`loop`，但`loop`退出，`bar`便成了未定义的。

```
ruby> foo = 44; puts foo; defined?(foo)
44
   "local-variable"
ruby> loop{bar=45; puts bar; break}; defined?(bar)
45
   nil
```

Procedure objects that live in the same scope share whatever local variables also belong to that scope. Here, the local variable bar is shared by main and the procedure objects p1 and p2:

在相同范围内的过程对象共享也属于该范围的任何局部变量。此处，局部变量`bar`被`main`以及过程对象`p1`、`p2`所共享。

```
ruby> bar=nil
   nil
ruby> p1 = proc{|n| bar=n}
   #<Proc:0x8deb0>
ruby> p2 = proc{bar}
   #<Proc:0x8dce8>
ruby> p1.call(5)
   5
ruby> bar
   5
ruby> p2.call
   5
```

Note that the "bar=nil" at the beginning cannot be omitted; it ensures that the scope of bar will encompass p1 and p2. 

注意最开始的`bar=nil`不能省略，它确保了`bar`的范围将包括`p1`和`p2`。

Otherwise p1 and p2 would each end up with its own local variable bar, and calling p2 would have resulted in an "undefined local variable or method" error. 

否则，`p1`和`p2`将各自使用其局部变量`bar`，而调用p2将导致"**undefined local variable or method**"错误。

We could have said bar=0 instead, but using nil is a courtesy to others who will read your code later. 

我们也可以使用`bar=0`，但是使用`nil`显得对阅读你代码的人更友好。

It indicates fairly clearly that you are only establishing scope, because the value being assigned is not intended to be meaningful.

它很清楚地表明你只是在建立作用域，因为被分配的值并不是有意义的。

A powerful feature of procedure objects follows from their ability to be passed as arguments: shared local variables remain valid even when they are passed out of the original scope.

过程对象的一个强大功能来自它们可以作为参数被传递的能力：即使在最初的作用域之外，共享的局部变量仍然有效。

```
ruby> def box
        contents = nil
        get = proc{contents}
        set = proc{|n| contents = n}
        return get, set
     end
   nil
ruby> reader, writer = box
   [#<Proc:0x40170fc0>, #<Proc:0x40170fac>] 
ruby> reader.call
   nil
ruby> writer.call(2)
   2
ruby> reader.call
   2
```

Ruby is particularly smart about scope. It is evident in our example that the contents variable is being shared between the reader and writer. 

**Ruby**在作用域方面特别聪明。在我们的示例中很明显，变量`contents`是在**reader**和**writer**之间共享的。

But we can also manufacture multiple reader-writer pairs using box as defined above; each pair shares a contents variable, and the pairs do not interfere with each other.

但是，我们也可以使用如上所定义的**box**来制造多个**reader-writer**对。

```
ruby> reader_1, writer_1 = box
   [#<Proc:0x40172820>, #<Proc:0x4017280c>]
ruby> reader_2, writer_2 = box
   [#<Proc:0x40172668>, #<Proc:0x40172654>]
ruby> writer_1.call(99)
   99
ruby> reader_1.call
   99
ruby> reader_2.call  # nothing is in this box yet
   nil
```
This kind of programming could be considered a perverse little object-oriented framework. 

这种编程可以被认为是一个不合理的面向对象的框架。

The box method acts something like a class, with get and set serving as methods (except those aren't really the method names, which could vary with each box instance) and contents being the lone instance variable. 

**box**方法的作用类似于一个类，**get**和**set**作为方法(除了那些不是真正的方法名，它可能会随着每个box实例的不同而不同)，而`contents`是唯一的实例变量。

Of course, using ruby's legitimate class framework leads to much more readable code.

当然，使用**Ruby**的合法类框架会得到可读性更强的代码。

[上一章 实例变量](./instancevars.md "Instance variables")
[下一章 类常量](./constants.md "Class constants")
