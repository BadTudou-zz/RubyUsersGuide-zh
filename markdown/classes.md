# 类
**Classes**

**类**

The real world is filled by objects, and we can classify them. 

现实世界中充满了对象，并且我们还可以给它们分类。

For example, a very small child is likely to say "bow-wow" when seeing a dog, regardless of the breed; we naturally see the world in terms of these categories.

举个例子，当一个小孩子看到了一条狗，他可能会说“汪汪”，而不管这条狗是什么品种。我们自然地会从这些类别中看到世界。

In OO programming terminology, a category of objects like "dog" is called a class, and some specific object belonging to a class is called an instance of that class.

在**OO编程**的术语中，像“狗”这样的一类**对象**，被称为**类**，属于**类**的某些特定**对象**称为该**类**的一个**实例**。

Generally, to make an object in ruby or any other OO language, first one defines the characteristics of a class, then creates an instance. To illustrate the process, let's first define a simple Dog class.

通常，在Ruby或任何其他OO语言中，想要创造一个对象，第一步是定义一个**类**的特征，染成再创建一个**实例**。为了阐述这个过程，让我们先定义一个简单的**Dog**类。

```
ruby> class Dog
    |   def speak
    |     puts "Bow Wow"
    |   end
    | end
   nil
```

In ruby, a class definition is a region of code between the keywords class and end. 

在**Ruby**中，类定义是关键字`class`和`end`之间的代码区域。

A def inside this region begins the definition of a method of the class, which as we discussed in the previous chapter, corresponds to some specific behavior for objects of that class.

区域内的`def`是定义类方法的开始，正如我们在前一章中所讨论的，类方法对应于该类对象的某些特定行为。

Now that we have defined a Dog class, we can use it to make a dog:

现在我们已经定义类一个Dog类，我们可以用它来生成一条狗：

```
ruby> pochi = Dog.new
   #<Dog:0xbcb90>
```

We have made a new instance of the class Dog, and have given it the name pochi.

我们生成了类Dog的一个新实例，并且给它取名为**pochi**。

The new method of any class makes a new instance. Because pochi is a Dog according to our class definition, it has whatever properties we decided a Dog should have. Since our idea of Dog-ness was very simple, there is just one trick we can ask pochi to do.

任何类的`new`方法都是生成一个新实例。因为**pochi**是根据我们的类定义而来的一个**Dog**，它有任何我们认为**Dog**应该拥有的属性。因为我们对**Dog**的看法非常简单，只有一个小技巧可以让**pochi**去做。

```
ruby> pochi.speak
Bow Wow
   nil
```

Making a new instance of a class is sometimes called instantiating that class. We need to have a dog before we can experience the pleasure of its conversation; we can't merely ask the Dog class to bark for us.

一个类的新实例有时被称为实例化该类，在我们能体会到狗的乐趣之前，我们需要有一条狗才行。我们不能要求Dog类仅仅为了我们而吠叫。

```
ruby> Dog.speak
ERR: (eval):1: undefined method `speak' for Dog:class
```

It makes no more sense than trying to eat the concept of a sandwich.

吃三明治的概念是没有意义的。

On the other hand, if we want to hear the sound of a dog without getting emotionally attached, we can create (instantiate) an ephemeral, temporary dog, and coax a little noise out of it before it disappears.

换句话说，如果我们想要听到狗的叫声而无需感情上的依恋，我们可以生成(实例化)一个短暂的、临时的狗，在它消失之前，让它发出一点声音。

```
ruby> (Dog.new).speak   # 或者更常见的, Dog.new.speak
Bow Wow
   nil
```
"Wait," you say, "what's all this about the poor fellow disappearing afterwards?" 

“等等”，你说道：“这个可怜的家伙到底是怎么消失的呢?”

It's true: if we don't bother to give it a name (as we did for pochi), ruby's automatic garbage collection decides it is an unwanted stray dog, and mercilessly disposes of it. Really it's okay, you know, because we can make all the dogs we want.

事实是：如果我们不费心给它取一个名字(就像我们给它取名**pochi**)，**Ruby**的自动垃圾回收便判定它是一条不受欢迎的流浪狗，并且残忍地处理它。真的这没问题，你知道的，我们可以制造所有我们想要的狗。

[上一章 方法](./methods.md "Methods")
[下一章 继承](./inheritance.md "Inheritance")