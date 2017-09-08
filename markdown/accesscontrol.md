# 访问控制
**Access control**

**访问控制**

Earlier, we said that ruby has no functions, only methods. 

之前我们曾说，**Ruby**没有**函数**，只有**方法**。

However there is more than one kind of method. In this chapter we introduce access controls.

然而，有不止一种方法。在本章节中，我们将介绍访问控制。

Consider what happens when we define a method in the "top level", not inside a class definition. 

考虑一下，当我们在“顶层”中定义一个**方法**，而不是在类定义中时，发生了什么。

We can think of such a method as analogous to a function in a more traditional language like C.

我们可以把这种**方法**想象成像**C**这样的更传统的语言的**函数**。

```
ruby> def square(n)
    |   n * n
    | end
   nil
ruby> square(5)
   25
```

Our new method would appear not to belong to any class, but in fact ruby gives it to the Object class, which is a superclass of every other class. 

我们的新方法似乎不属于任何类，但是事实上**Ruby**将给它**Object**类，这是其他类的父类。

As a result, any object should now be able to use that method. That turns out to be true, but there's a small catch: it is a private method of every class. 

作为结果，任何对象现在都能使用这个方法。这是事实，但是有一个小问题：它是每个类的私有方法。

We'll discuss some of what this means below, but one consequence is that it may be invoked only in function style, as here:

我们将在下面讨论这是什么意思，但一个结果是，它可能只在函数样式中被调用，如下:

```
ruby> class Foo
    |   def fourth_power_of(x)
    |     square(x) * square(x)
    |   end
    | end
  nil
ruby> Foo.new.fourth_power_of 10
  10000
```
We are not allowed to explicitly apply the method to an object:

我们不允许显式地将该方法应用于对象:

```
ruby> "fish".square(5)
ERR: (eval):1: private method `square' called for "fish":String
```

This rather cleverly preserves ruby's pure-OO nature (functions are still object methods, but the receiver is self implicitly) while providing functions that can be written just as in a more traditional language.

这很巧妙地保留了**Ruby**的纯**OO**特性(函数仍然是对象方法，但是接收方是隐式的)，同时提供了可以用更传统的语言编写的函数。

A common mental discipline in OO programming, which we have hinted at in an earlier chapter, concerns the separation of specification and implementation, or what tasks an object is supposed to accomplish and how it actually accomplishes them. 

在**OO**编程中，一个常见的心智规则，我们在前面的章节中已经提到过，它关注的是规范和实现的分离，或者对象应该完成什么任务，以及它是如何实现的。

The internal workings of an object should be kept generally hidden from its users; they should only care about what goes in and what comes out, and trust the object to know what it is doing internally. 

对象内部的工作状态对使用者而言，应该保持在隐藏状态。使用者只关心传进去的是什么，得到的又是什么，并且信任这个对象，知道它在内部做什么。

As such it is often helpful for classes to have methods that the outside world does not see, but which are used internally (and can be improved by the programmer whenever desired, without changing the way users see objects of that class). In the trivial example below, think of engine as the invisible inner workings of the class.

因此，对于类来说，拥有外部世界没有看到的方法是很有帮助的，这些方法是在内部使用的(并且可以在需要的时候由程序员改进，而不会改变用户查看该类的方法)。

在下面的简单例子中，将**engine**看作是类中不可见的内部工作。

```
ruby> class Test
    |   def times_two(a)
    |     puts "#{a} times two is #{engine(a)}"
    |   end
    |   def engine(b)
    |     b*2
    |   end
    |   private:engine  # this hides engine from users
    | end
   Test
ruby> test = Test.new
   #<Test:0x4017181c>
ruby> test.engine(6)
ERR: (eval):1: private method `engine' called for #<Test:0x4017181c>
ruby> test.times_two(6)
6 times two is 12.
   nil
```

We might have expected test.engine(6) to return 12, but instead we learn that engine is inaccessible when we are acting as a user of a Test object. 

我们可能期望`Test.engine(6)`返回`12`，但是我们知道当我们作为一个`Test`对象的用户时，`engine`是不可访问的。

Only other Test methods, such as times_two, are allowed to use engine. 

只有其他的`Test`的方法，比如`times_two`，被允许使用`engine`。

We are required to go through the public interface, which consists of the times_two method. 

我们需要通过公共接口，它由`times_tow`方法组成。

The programmer who is in charge of this class can change engine freely (here, perhaps by changing b*2 to b+b, assuming for the sake of argument that it improved performance) without affecting how the user interacts with Test objects. 

负责这个类的程序员可以自由地改变engie(在这里，可能是通过将`b*2`修改为`b+b`，假设是为了提高性能)，而不影响用户与测试对象的交互。

This example is of course much too simple to be useful; the benefits of access controls become more clear only when we begin to create more complicated and interesting classes.

这个例子当然太简单了，不可能有用;只有当我们开始创建更复杂、更有趣的类时，访问控制的好处才会变得更加明显。

[上一章 重新定义方法](./redefinemethods.md "Redefinition of methods")
[下一章 单例方法](./singletonmethods.md "Singleton methods")