# 迭代器
**Iterators**

**迭代器**

Iterators are not an original concept with ruby. 

**迭代器**并不是**Ruby**的原创概念。

They are in common use in object-oriented languages. 

它们在面向对象的语言中是通用的。

They are also used in Lisp, though there they are not called iterators. However the concept of iterator is an unfamiliar one for many so it should be explained in more detail.

它们也被用于**Lisp**中，尽管不被叫做迭代器。然而，**迭代器**的概念对于很多人来说都是陌生的，所以应该更详细地解释它。

The verb iterate means to do the same thing many times, you know, so an iterator is something that does the same thing many times.

谓词**迭代**意味着多次执行相同的操作，所以**迭代器**就是多次执行相同操作的东西。

When we write code, we need loops in various situations. In C, we code them using for or while. For example,

当我们编写代码时，我们需要在不同的情况下循环。在**C**语言中，我们用`for`或者`while`来编写它们，举个例子：

```
char *str;
for (str = "abcdefg"; *str != '\0'; str++) {
  /* process a character here */
}
```

C's for(...) syntax provides an abstraction to help with the creation of a loop, but the test of *str against a null character requires the programmer to know details about the internal structure of a string. 

**C**的`for(…)`语法提供了一个抽象来帮助创建循环，但是，要测试`*str`是否为一个空的字符串，则要求程序员了解一个字符串内部结构的细节究竟是怎样的。

This makes C feel like a low-level language. Higher level languages are marked by their more flexible support for iteration. Consider the following sh shell script:

这让**C**感觉像是一种低级语言，更高级别的语言z则通过对**迭代**的显式支持使其更加灵活。考虑下面的`shell`脚本：

```
 #!/bin/sh
for i in *.[ch]; do
  # ... 这里是对每个文件要执行的操作
done
```

All the C source and header files in the current directory are processed, and the command shell handles the details of picking up and substituting file names one by one. I think this is working at a higher level than C, don't you?

当前目录中的所有**C**源文件和头文件都被处理了，并且命令shell将处理获取和替换文件名的详细信息。相比**C**，我认为我们更关注于处理比较高层次的工作，你觉得呢？

But there is more to consider: while it is fine for a language to provide iterators for built-in data types, it is a disappointment if we must go back to writing low level loops to iterate over our own data types. In OOP, users often define one data type after another, so this could be a serious problem.

但是这里仍有一些问题要考虑：对于一种语言来说，为内置数据类型提供迭代器是很好的，如果我们必须回到编写低级别循环来迭代我们自己的数据类型，这将是一个令人失望的事情。在**OOP**中，用户经常定义一个数据类型，因此这可能是一个严重的问题。

So every OOP language includes some facilities for iteration. Some languages provide a special class for this purpose; ruby allows us to define iterators directly.

所以每个**OOP**语言都包含了一些用于迭代的工具，有一些语言提供了用于迭代的类，**Ruby**则允许我们直接定义**迭代器**。

Ruby's String type has some useful iterators:

**Ruby**的**字符串**类型就有一些有用的迭代器：

```
ruby> "abc".each_byte{|c| printf "<%c>", c}; print "\n"
<a><b><c>
   nil
```

each_byte is an iterator for each character in the string. Each character is substituted into the local variable c. This can be translated into something that looks a lot like C code ...

`each_byte`是字符串中的每个字符的**迭代器**。每个字符都被局部变量`c`替换，这可以被翻译成看起来很像**C**代码的东西。

```
ruby> s="abc";i=0
   0
ruby> while i<s.length
    |    printf "<%c>", s[i]; i+=1
    | end; print "\n"
<a><b><c>
   nil
```

... however, the each_byte iterator is both conceptually simpler and more likely to continue to work even if the String class happens to be radically modified in the future. 

然而，迭代器`each_byte`在概念上都更简单，即使字符串类在将来会被彻底修改，它仍可能会继续工作。

One benefit of iterators is that they tend to be robust in the face of such changes; indeed that is a characteristic of good code in general. (Yes, have patience, we're about to talk about what classes are, too.)

**迭代器**的一个优点是，面对这样的变化时，它们往往是健壮的，这确实是好代码所拥有的特点。(是的，要有耐心，我们也要谈谈课程的内容。)

Another iterator of String is each_line.

字符串的另一个**迭代器**是`each_line`。

```
ruby> "a\nb\nc\n".each_line{|l| print l}
a
b
c
   nil
```

The tasks that would take most of the programming effort in C (finding line delimiters, generating substrings, etc.) are easily tackled using iterators.

使用**迭代器**可以很容易地完成**C**语言(查找行分隔符、生成子字符串等)的大多数编程工作。

The for statement appearing in the previous chapter does iteration by way of an each iterator. String's each works the same as each_line, so let's rewrite the above example with for:

在前一章节中出现的`for`语句通过**迭代器**的方法对每一个进行迭代，

```
ruby> for l in "a\nb\nc\n"
    |   print l 
    | end
a
b
c
   nil
```

We can use a control structure retry in conjunction with an iterated loop, and it will retry the loop from the beginning.

我们可以将迭代器循环和控制结构`retry`结合使用，它会从头开始重新尝试循环。

```
ruby> c=0
   0
ruby> for i in 0..4
    |   print i
    |   if i == 2 and c == 0
    |     c = 1
    |     print "\n"
    |     retry
    |   end
    | end; print "\n"
012
01234
   nil
```

Replacing retry in the above example with redo causes just the current iteration of the loop to be redone, with this output:

在上面的例子中，用`redo`来替换`retry`，只会导致循环的当前迭代被重新执行，会有如下输出：

**012**
**234**
yield occurs sometimes in a definition of an iterator. 

`yield`有时出现于迭代器的定义中。

yield moves control to the block of code that is passed to the iterator (this will be explored in more detail in the chapter about procedure objects). 

`yield`将控制权移交到传递给**迭代器**的代码块(这将在关于过程对象的章节中更详细地探讨)。

The following example defines an iterator repeat, which repeats a block of code the number of times specified in an argument.

下面的示例定义了一个重复执行的`迭代器`，它重复一个代码块，重复的次数由传递给它的参数指定。

```
ruby> def repeat(num)
    |   while num > 0
    |     yield
    |     num -= 1
    |   end
    | end
   nil
ruby> repeat(3) { puts "foo" }
foo
foo
foo
   nil
```

With retry, one can define an iterator which works something like ruby's standard while.

通过`retry`，可以定义一个**迭代器**，它的工作方式类似于**Ruby**标准的`while`。

```
ruby> def WHILE(cond)
    |   return if not cond
    |   yield
    |   retry
    | end
   nil
ruby> i=0; WHILE(i<3) { print i; i+=1 }
012   nil
```

Do you understand what an iterator is? There are a few restrictions, but you can write your original iterators; and in fact, whenever you define a new data type, it is often convenient to define suitable iterators to go with it. 

你明白**迭代器**是什么了么？这里有几个条件，但是你可以编写你自己的**迭代器**原型。事实上，无论在什么时候定义一个新的数据类型，定义合适的迭代器通常都是很方便的。

In this sense, the above examples are not terribly useful. We can talk about practical iterators after we have a better understanding of what classes are.

从这个意义上来说，上面的例子并不是很有用。在我们对课程有了更好的理解之后，我们可以讨论一些实际的迭代器。