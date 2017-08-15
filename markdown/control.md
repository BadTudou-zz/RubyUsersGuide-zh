# 流程控制
**Control structures**

**流程控制**

This chapter explores more of ruby's control structures.

本章节探究了更多的**Ruby**流程控制。

**case**

We use the case statement to test a sequence of conditions. This is superficially similar to switch in C and Java but is considerably more powerful, as we shall see.

我们使用`case`语句来测试一个条件序列。表面上看它与**C**和**JAVA**中的`switch`类似，但正如我们所看到的，实际上它要比`switch`强大得多。

```
ruby> i=8
ruby> case i
    | when 1, 2..5
    |   puts "1..5"
    | when 6..10
    |   puts "6..10"
    | end
**6..10**
 **nil**
```

2..5 is an expression which means the range between 2 and 5, inclusive. The following expression tests whether the value of i falls within that range:

`2..5`是一个表达式，它表示2到5的范围(包括2和5)。下面的表达式测试了我的值是否在这个范围内:

```
(2..5) === i
```

case internally uses the relationship operator === to check for several conditions at a time.

`case`来内部使用关系运算符`===`来一次检查多个条件。

In keeping with ruby's object oriented nature, === is interpreted suitably for the object that appeared in the when condition. 

为了与**Ruby**面向对象的特性保持一致，`===`会对出现在`when`条件下的对象进行适当解释。

For example, the following code tests string equality in the first when, and regular expression matching in the second when.

举个例子，下面的代码在第1个`when`中会检测字符串是否相等，在第2个`when`中会检测字符串是否与正则表达式匹配。

```
ruby> case 'abcdef'
    | when 'aaa', 'bbb'
    |   puts "aaa or bbb"
    | when /def/
    |   puts "includes /def/"
    | end
includes /def/
   nil
while
```

Ruby provides convenient ways to construct loops, although you will find in the next chapter that learning how to use iterators will make it unnecessary to write explicit loops very often.

**Ruby**提供了非常便捷的方法来构建循环，尽管你将在下一章中发现，学习如何使用**迭代器**将使编写显式的循环变得不再必要。

A while is a repeated if. We used it in our word-guessing puzzle and in the regular expression programs (see the previous chapter); there, it took the form while condition ... end surrounding a block of code to be repeated while condition was true. But while and if can as easily be applied to individual statements:

一个`while`就是一个重复的`if`。我们在“猜谜语”和正则表达式中使用了`while`(参见上一章节)。这里，它以`while 条件 … end`的形式出现。在条件为真的情况下，重复执行代码块中的代码。但是`while`和`if`都可以很容易地应用于单个语句。

```
ruby> i = 0
   0
ruby> puts "It's zero." if i==0
It's zero.
   nil
ruby> puts "It's negative." if i<0
   nil
ruby> puts i+=1 while i<3
1
2
3
   nil
```

Sometimes you want to negate a test condition. An unless is a negated if, and an until is a negated while. We'll leave it up to you to experiment with these.

有时你想要否定一个测试条件，`unless`就是`否定的if`，并且`until`就是`否定的while`。我们把它留给你来做实验。

There are four ways to interrupt the progress of a loop from inside. 

有四种方法可以从内部中断循环的进程。

First, break means, as in C, to escape from the loop entirely. 

**1**，`break`意味着，就像在C中一样，会完全终止循环。

Second, next skips to the beginning of the next iteration of the loop (corresponding to C's continue).

**2**，`next`跳到循环的下一次迭代的开始(相当于**C**的`continue`)。

 Third, ruby has redo, which restarts the current iteration. 

**3**.Ruby有`redo`，这将重新启动当前的迭代。

The following is C code illustrating the meanings of break, next, and redo:

下面用**C语言**代码说明了`break`，`next`以及`redo`的含义。

```
while (condition) {
label_redo:
   goto label_next;        /* ruby's "next" */
   goto label_break;       /* ruby's "break" */
   goto label_redo;        /* ruby's "redo" */
   ...
   ...
label_next:
}
label_break:
...
```

The fourth way to get out of a loop from the inside is return. An evaluation of return causes escape not only from a loop but from the method that contains the loop. If an argument is given, it will be returned from the method call, otherwise nil is returned.

**4**.从内部退出循环的第4种方法是`return`。对`return`的运算不仅会导致终止循环，还会从包含循环的方法中退出，否则将返回`nil`。

**for**

C programmers will be wondering by now how to make a "for" loop.

**C**程序员现在可能想知道该如何如何创建一个`for`循环。

Ruby's for can serve the same purpose, but adds some flexibility.

**Ruby**的`for`可以达到同样的目的，而且还增加了一些灵活性。

The loop below runs once for each element in a collection (array, hash, numeric sequence, etc.), but doesn't make the programmer think about indices:

下面的循环为**集合**(**数组**，**哈希**，**数字序列**等等)中的每个元素运行一次，但是并不需要程序员考虑**索引**。

```
for elt in collection
  # ... 此处，elt引用了集合中的每一个元素
end
```

The collection can be a range of values (this is what most people mean when they talk about a for loop):

这个**集合**也可以是某个范围内的值(这也是大多数人在谈论`for`循环时的意思)：

```
ruby> for num in (4..6)
    |    puts num
    | end
4
5
6
   4..6
```

In this example we step through some array elements:

在这个例子中，我们逐步介绍了一些**数组元素**：

```
ruby> for elt in [100,-9.6,"pickle"]
    |    puts "#{elt}\t(#{elt.class})"
    | end
100    (Fixnum)
-9.6   (Float)
pickle (String)
   [100, -9.6, "pickle"]
```

But we're getting ahead of ourselves. for is really another way of writing each, which, it so happens, is our first example of an iterator. The following two forms are equivalent:

但是我们已经超越了自己。`for`确实是另一种写`each`的方法，它是我们第一个**迭代器**的例子。以下两种形式是等价的：

```
 #如果你曾使用C或JAVA，你可能倾向于这种.
for element in collection
  ...
end
```

```
#一个Smalltalk程序员可能更钟爱这种
collection.each {|element|
  ...
}
```
Iterators can often be substituted for conventional loops, and once you get used to them, they are generally easier to deal with. So let's move on and learn more about them.

**迭代器**通过被用来代替传统的**循环**，并且一旦你使用它们，它们通常更容易处理。因此，让我们继续学习，更多地了解它们。