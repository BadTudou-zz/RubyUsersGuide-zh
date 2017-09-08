# 方法
**Methods**

**方法**

What is a method? In OO programming, we don't think of operating on data directly from outside an object; rather, objects have some understanding of how to operate on themselves (when asked nicely to do so). 

方法是什么呢？在**OO编程**中，我们不考虑直接从对象外部操作数据。相反，对象知道该如何操作它自己(当被要求做得很好时)。

You might say we pass messages to an object, and those messages will generally elicit some kind of an action or meaningful reply. 

你可能会说我们将消息传递给了一个对象，这些消息通常会引发某种行为或有意义的回应。

This ought to happen without our necessarily knowing or caring how the object really works inside. The tasks we are allowed to ask an object to perform (or equivalently, the messages it understands) are that object's methods.

这应该发生在我们不需要知道或关心对象如何在内部运作的情况下。我们允许请求对象执行的任务(或者是它所理解的消息)是对象的方法。

In ruby, we invoke a method of an object with dot notation (just as in C++ or Java). The object being talked to is named to the left of the dot.

在`Ruby`中，我们通过点号`.`来调用一个对象的方法(就像C++或Java)。讨论的对象在点号`.`左边有一个名字。

```
ruby> "abcdef".length
   6
```

Intuitively, this string object is being asked how long it is. Technically, we are invoking the length method of the object "abcdef".

直观上看，我们正在询问这个字符串对象它的长度是多少。在技术上来说，我们正在调用对象"abcdef"的`length`方法。

Other objects may have a slightly different interpretation of length, or none at all. 

其他对象对长度的解释，可能有稍微的不同，或者完全不相同。

Decisions about how to respond to a message are made on the fly, during program execution, and the action taken may change depending on what a variable refers to.

关于如何对消息作出响应的决定是在程序执行期间进行的，而在程序执行期间，程序所采取的操作可能会随着变量的引用而发生变化。

```
ruby> foo = "abc"
   "abc"
ruby> foo.length
   3
ruby> foo = ["abcde", "fghij"]
   ["abcde", "fghij"]
ruby> foo.length
   2
```

What we mean by length can vary depending on what object we are talking about. 

对我们所说的长度有何种不同的理解，取决于我们正在谈论的对象。

The first time we ask foo for its length in the above example, it refers to a simple string, and there can only be one sensible answer. 

在上面的例子中，我们第1次询问foo的长度，它指向的是一个简单的字符串，而且只能有一个合理的答案。

The second time, foo refers to an array, and we might reasonably think of its length as either 2, 5, or 10; but the most generally applicable answer is of course 2 (the other kinds of length can be figured out if wished).

第2次foo指向来一个数组，我们可以合理地把它的长度看成是**2,5**或**10**。

```
ruby> foo[0].length
   5
ruby> foo[0].length + foo[1].length
   10
```

The thing to notice here is that an array knows something about what it means to be an array.

这里要值得注意的是，数组对象知道，对于一个数组而言，`length`的含义是什么。

Pieces of data in ruby carry such knowledge with them, so that the demands made on them can automatically be satisfied in the various appropriate ways. 

**Ruby**中的数据块携带了这样的知识，因此，可以通过各种适当的方式自动满足他们的要求。

This relieves the programmer from the burden of memorizing a great many specific function names, because a relatively small number of method names, corresponding to concepts that we know how to express in natural language, can be applied to different kinds of data and the results will be what we expect. 

这使程序员免除了记忆许多特定函数名的负担，因为相对较少的方法名，对应于我们知道如何用自然语言表达的概念，可以应用于不同类型的数据，而其结果也将是我们所期望的。

This feature of OO programming languages (which, IMHO, Java has done a poor job of exploiting) is called polymorphism.

**OO编程**语言的这一特性(即IMHO，Java在开发方面做得很差)被称为**多态**。

When an object receives a message that it does not understand, an error is "raised":

当一个对象接收到了一个它不能理解的消息，一个错误便出现了。

```
ruby> foo = 5
   5
ruby> foo.length
ERR: (eval):1: undefined method `length' for 5(Fixnum)
```

So it is necessary to know what methods are acceptable to an object, though we need not know how the methods are processed.

所以尽管我们不需要知道一个对象是如何处理方法的，但知道它可以接收何种方法仍是很有必要的，

If arguments are given to a method, they are generally surrounded by parentheses,

如果参数被赋予一个方法，它们通常都被圆括号括起来`()`，

```
object.method(arg1, arg2)
```

but they can be omitted if doing so does not cause ambiguity.

但如果省略圆括号而不会造成歧义，就可以省略它们。

```
object.method arg1, arg2
```
There is a special variable self in ruby; it refers to whatever object calls a method. This happens so often that for convenience the "self." may be omitted from method calls from an object to itself:

**Ruby**中有一个特殊变量`self`，它指向的是调用方法的任何对象。这种情况经常发生，为了方便，对象的方法调用中可以忽略“**self**”。

```
self.method_name(args...)
```

is the same as

它等同于

```
method_name(args...)
```

What we would think of traditionally as a function call is just this abbreviated way of writing method invocations by self. 

我们通常认为，函数调用是由self来编写方法调用的一种缩写形式。

This makes ruby what is called a pure object oriented language. Still, functional methods behave quite similarly to the functions in other programming languages for the benefit of those who do not grok how function calls are really object methods in ruby. We can speak of functions as if they were not really object methods if we want to.

这使得**Ruby**成为一种纯粹的面向对象语言。尽管如此，函数方法与其他编程语言中的函数非常相似，这对那些不知道**Ruby**中是对象方法是如何同函数方法一样被调用的人来说是有好处的。我们可以谈论函数，就好像它们不是真正的对象方法，如果我们想的话。

[上一章 面向对象的思考](./oothinking.md "Object-oriented thinking")
[下一章 类](./classes.md "Classes")