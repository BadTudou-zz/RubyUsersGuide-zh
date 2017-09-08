# 对象初始化
**Object initialization**

**对象初始化**

Our Fruit class from the previous chapter had two instance variables, one to describe the kind of fruit and another to describe its condition. 

我们上一章节中的`Fruit`类有2个实例变量，其中一个描述了水果的种类，另外一个描述了环境。

It was only after writing a custom inspect method for the class that we realized it didn't make sense for a piece of fruit to lack those characteristics. 

只有在为类写了一种自定义的`inspect`方法之后，我们才意识到，一种水果缺乏这种特性是没有意义的。

Fortunately, ruby provides a way to ensure that instance variables always get initialized.

幸运的是，**Ruby**提供了一种方法来确保实例变量总是被初始化。

The initialize method

`initialize`方法

Whenever Ruby creates a new object, it looks for a method named initialize and executes it. 

当**Ruby**创建一个新的对象时，它会查找并运行一个名为`initialize`的方法。

So one simple thing we can do is use an initialize method to put default values into all the instance variables, so the inspect method will have something to say.

因此，我们可以做的一件简单的事情是使用`initialize`方法将默认值放入所有的实例变量中，因此`inspect`方法将会有一些内容。

```
ruby> class Fruit
    |   def initialize
    |     @kind = "apple"
    |     @condition = "ripe"
    |   end
    | end
   nil
ruby> f4 = Fruit.new
   "a ripe apple"
```

Changing assumptions to requirements

改变需求的假设

There will be times when a default value doesn't make a lot of sense. 

在某些情况下，默认值没有什么意义。

Is there such a thing as a default kind of fruit? It may be preferable to require that each piece of fruit have its kind specified at the time of its creation. 

有什么东西是一种默认的水果吗?最好是要求每一种水果都在其诞生之时指定种类。

To do this, we would add a formal argument to the initialize method. 

为了做到这一点，我们将向`initialize`方法添加一个正式的参数。

For reasons we won't get into here, arguments you supply to new are actually delivered to initialize.

出于我们不会深入到这里，你提供给新用户的参数实际上是被交付给`initalize`的。

```
ruby> class Fruit
    |   def initialize( k )
    |     @kind = k
    |     @condition = "ripe"
    |   end
    | end
   nil
ruby> f5 = Fruit.new "mango"
   "a ripe mango"
ruby> f6 = Fruit.new
ERR: (eval):1:in `initialize': wrong # of arguments(0 for 1)
```

**Flexible initialization**

**灵活的初始化**

Above we see that once an argument is associated with the initialize method, it can't be left off without generating an error. 

上面我们看到，一旦一个参数与`initialize`方法相关联，如果不产生错误，它就不能被关闭。

If we want to be more considerate, we can use the argument if it is given, or fall back to default values otherwise.

如果我们想要更加周到，我们可以使用参数，如果给定了参数则使用参数，或者返回默认值。

```
ruby> class Fruit
    |   def initialize( k="apple" )
    |     @kind = k
    |     @condition = "ripe"
    |   end
    | end
   nil
ruby> f5 = Fruit.new "mango"
   "a ripe mango"
ruby> f6 = Fruit.new
   "a ripe apple"
```

You can use default argument values for any method, not just initialize. 

不仅仅是在`initialize`中，你可以给任何方法指定默认值。

The argument list must be arranged so that those with default values come last.

必须对参数列表进行安排，以便那些有缺省值的是最后一个。

Sometimes it is useful to provide several ways to initialize an object. 

有时，提供几个方法来初始化一个对象是很有用的。

Although it is outside the scope of this tutorial, ruby supports object reflection and variable-length argument lists, which together effectively allow method overloading.

虽然它超出了本教程的范围，但是**Ruby**支持**对象反射**和**变长参数列表**，这两者一起有效地允许方法重载。

[上一章 访问器](./accessors.md "Accessors")
[下一章 其他](./misc.md "misc")