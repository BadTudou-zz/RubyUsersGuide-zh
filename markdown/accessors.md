# 访问器
**Accessors**

**访问器**

What is an accessor?

**访问器**是什么？

We briefly discussed instance variables in an earlier chapter, but haven't done much with them yet. 

我们在前面的章节中简要地讨论了**实例变量**，但是还没有对它们对过多的讨论。

An object's instance variables are its attributes, the things that distinguish it from other objects of the same class. 

对象的实例变量是它的属性，它将它与同类的其他对象区分开来。

It is important to be able to write and read these attributes; doing so requires methods called attribute accessors. 

能够编写和读取这些属性是很重要的，这样做需要称为属性访问器的方法。

We'll see in a moment that we don't always have to write accessor methods explicitly, but let's go through all the motions for now. The two kinds of accessors are writers and readers.

稍后我们会看到，我们并不总是需要显式地编写访问器方法，现在让我们来看看所有的动作。这两种读写方法是**writers**和**readers**。

```
ruby> class Fruit
    |   def set_kind(k)  # a writer
    |     @kind = k
    |   end
    |   def get_kind     # a reader
    |     @kind
    |   end
    | end
   nil
ruby> f1 = Fruit.new
   #<Fruit:0xfd7e7c8c>
ruby> f1.set_kind("peach")  # use the writer
   "peach"
ruby> f1.get_kind           # use the reader
   "peach"
ruby> f1                    # inspect the object
   #<Fruit:0xfd7e7c8c @kind="peach">
```

Simple enough; we can store and retrieve information about what kind of fruit we're looking at. But our method names are a little wordy. The following is more concise, and more conventional:

很简单;我们可以储存和获取关于我们正在研究的水果的信息。但是我们的方法名称有点冗长。下面的内容更简洁，更传统：

```
ruby> class Fruit
    |   def kind=(k)
    |     @kind = k
    |   end
    |   def kind
    |     @kind
    |   end
    | end
   nil
ruby> f2 = Fruit.new
   #<Fruit:0xfd7e7c8c>
ruby> f2.kind = "banana"
   "banana"
ruby> f2.kind
   "banana"
```

The inspect method

**inspect**方法

A short digression is in order. You've noticed by now that when we try to look at an object directly, we are shown something cryptic like #<anObject:0x83678>. 

小小的题外话。你已经注意到当我们试着直接看对象时，我们会看到一些像`#<anObject:0x83678> `这样神秘的东西。

This is just a default behavior, and we are free to change it. 

这只是一个默认的行为，我们可以自由地改变它。

All we need to do is add a method named inspect. 

我们所要做的便是添加一个名为`inspect`的方法。

It should return a string that describes the object in some sensible way, including the states of some or all of its instance variables.

它应该返回一个以某种合理方式描述对象的字符串，包括一些或全部实例变量的状态。

```
ruby> class Fruit
    |   def inspect
    |     "a fruit of the #{@kind} variety"
    |   end
    | end
   nil
ruby> f2
   "a fruit of the banana variety"
```

A related method is to_s (convert to string), which is used when printing an object. 

一个相关的方法是`to_s`(转换成字符串)，在打印对象时使用该方法。

In general, you can think of inspect as a tool for when you are writing and debugging programs, and to_s as a way of refining program output. eval.rb uses inspect whenever it displays results. You can use the p method to easily get debugging output from programs.

一般来说，你可以将`inspect`看作是编写和调试程序时的工具，并将`to_s`作为改进程序输出的一种方法。eval.rb在显示结果时使用`inspect`。你可以使用`p`方法轻松地从程序中调试输出。

```
# These two lines are equivalent:
p anObject
puts anObject.inspect
```

Making accessors the easy way

使访问器变得简单

Since many instance variables need accessor methods, Ruby provides convenient shortcuts for the standard forms.

由于许多实例变量需要访问器方法，所以**Ruby**为标准样式提供了方便的快捷方式。

|                 快捷方法 |                                 效果 |
| -------------------: | ---------------------------------: |
|       attr_reader :v |                     def v; @v; end |
|       attr_writer :v |       def v=(value); @v=value; end |
|     attr_accessor :v |     attr_reader :v; attr_writer :v |
| attr_accessor :v, :w | attr_accessor :v; attr_accessor :w |

Let's take advantage of this and add freshness information. 

让我们利用这一点并添加新鲜信息。

First we ask for an automatically generated reader and writer, and then we incorporate the new information into inspect:

首先，我们自动生成的**reader**和**writer**，然后我们将这些新信息整合到`inspect`中:

```
ruby> class Fruit
    |   attr_accessor :condition
    |   def inspect
    |     "a #{@condition} #{@kind}"
    |   end
    | end
   nil
ruby> f2.condition = "ripe"
   "ripe"
ruby> f2
   "a ripe banana"
```

More fun with fruit

给水果添加更多乐趣

If nobody eats our ripe fruit, perhaps we should let time take its toll.

如果没有人吃我们成熟的水果，也许我们应该让时间来慢慢腐烂它。

```
ruby> class Fruit
    |   def time_passes
    |     @condition = "rotting"
    |   end
    | end
   nil
ruby> f2
   "a ripe banana"
ruby> f2.time_passes
   "rotting"
ruby> f2
   "a rotting banana"
```

But while playing around here, we have introduced a small problem. 

但是在这里玩的时候，我们已经引入了一个小问题。

What happens if we try to create a third piece of fruit now? Remember that instance variables don't exist until values are assigned to them.

如果我们现在尝试制作第3种水果，会发生什么呢?记住，实例变量在赋值给它们之前是不存在的。

```
ruby> f3 = Fruit.new
ERR: failed to convert nil into String
```

It is the inspect method that is complaining here, and with good reason. 

这是是在抱怨`inspect`方法，而且有很好的理由。

We have asked it to report on the kind and condition of a piece of fruit, but as yet f3 has not been assigned either attribute. 

我们已经要求它报告一种水果的种类和状况，但是迄今为止，`f3`还没有被分配到任何一种属性。

If we wanted to, we could rewrite the inspect method so it tests instance variables using the defined? method and then only reports on them if they exist, but maybe that's not very useful; 

如果我们想，我们可以重写`inspect`方法，以便它使用`defined?`方法测试实例变，然后只报告它们是否存在，但也许这不是很有用;

since every piece of fruit has a kind and condition, it seems we should make sure those always get defined somehow. That is the topic of the next chapter.

因为每一种水果都有种类和环境，似乎我们应该确保它们总是被定义的。这是下一章的主题。

[上一章 异常处理：ensure](./ensure.md "Exception processing: ensure")
[下一章 对象初始化](./objinitialization.md "Object initialization")