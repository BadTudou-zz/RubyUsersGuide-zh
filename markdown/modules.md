# 模块
**Modules**

**模块**

Modules in ruby are similar to classes, except:

**Ruby**中的**模块**同**类**非常相似，但有些许不同：

- A module can have no instances.
- 一个模块可以没有实例。
- A module can have no subclasses.
- 一个模块可以没有子类。
- A module is defined by module ... end.
- 一个模块是由`module … end`定义的。

Actually... the Module class of module is the superclass of the Class class of class. Got that? No? Let's move on.

实际上，module的`Module`类是class的`Class`类的父类。明白了吗?没有?让我们继续。

There are two typical uses of modules. One is to collect related methods and constants in a central location. The Math module in ruby's standard library plays such a role:

模块有两种典型的用法。其一是在中心位置收集相关的方法和常量。**Ruby**标准库中的数学模块发挥了这样的作用:

```
ruby> Math.sqrt(2)
   1.41421
ruby> Math::PI
   3.14159
```

The :: operator tells the ruby interpreter which module it should consult for the value of a constant (conceivably, some module besides Math might mean something else by PI). 

这个`::`操作符告诉**Ruby**解释器，它应该为一个常量的值进行协商(可以想象，除了数学之外，某些模块还可能有**PI**)。

If we want to refer to the methods or constants of a module directly without using ::, we can include that module:

如果我们想直接引用**模块**的**方法**或**常量**，而不需要使用`::`，我们可以`include`那个模块：

```
ruby> include Math
   Object
ruby> sqrt(2)
   1.41421
ruby> PI
   3.14159
```

Another use of modules is called mixin. Some OO programming languages, including C++, allow multiple inheritance, that is, inheritance from more than one superclass. 

另外一种使用模块的方法被称为**mixin**。许多**OO**编程语言，包括**C++**，允许**多重继承**，也就是说，从多个**父类**继承。

A real-world example of multiple inheritance is an alarm clock; you can think of alarm clocks as belonging to the class of clocks and also the class of things with buzzers.

现实世界中**多重继承**的例子是闹钟。你可以把闹钟看作属于**钟**类，也可以看作属于**蜂鸣器**类。

Ruby purposely does not implement true multiple inheritance, but the mixin technique is a good alternative. 

**Ruby**故意不实现真正的多重继承，但是**mixin**技术是一个不错的选择。

Remember that modules cannot be instantiated or subclassed; but if we include a module in a class definition, its methods are effectively appended, or "mixed in", to the class.

记住，**模块**不能被**实例化**或**子类化**，但是如果我们在一个类定义中包含了模块，它的方法便被有效地附加或“**混合**”到了类中。

Mixin can be thought of as a way of asking for whatever particular properties we want to have. 

**Mixin**可以被认为是一种询问我们想要的特定属性的方法。

For example, if a class has a working each method, mixing in the standard library's Enumerable module gives us sort and find methods for free.

比如，如果一个类有一个工作的`each`方法，混合了在标准库的可枚举模块中提供的排序和查找方法。

This use of modules gives us the basic functionality of multiple inheritance but allows us to represent class relationships with a simple tree structure, and so simplifies the language implementation considerably (a similar choice was made by the designers of Java).

模块的使用提供了多重继承的基本功能，但允许我们用简单的树结构来表示类关系，这样就大大简化了语言的实现(**Java**设计者也做出了类似的选择)。

[上一章 单例方法](./singletonmethods.md "Singleton methods")
[下一章 过程对象](./procobjects.md "Procedure objects")