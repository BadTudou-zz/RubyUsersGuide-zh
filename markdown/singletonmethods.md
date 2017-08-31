# 单例方法
**Singleton methods**

 **单例方法**

The behavior of an instance is determined by its class, but there may be times we know that a particular instance should have special behavior. 

一个实例的行为是由它所属的类决定的，但是我们也有可能知道，特定的实例有自己特定的行为。

In most languages, we must go to the trouble of defining another class, which would then only be instantiated once. 

在大多数语言中，我们必须去定义另一个类，这样就只会实例化一次。

In ruby we can give any object its own methods.

在**Ruby**中，我们可以给任何对象它自己的方法。

```
ruby> class SingletonTest
    |   def size
    |     25
    |   end
    | end
   nil
ruby> test1 = SingletonTest.new
   #<SingletonTest:0xbc468>
ruby> test2 = SingletonTest.new
   #<SingletonTest:0xbae20>
ruby> def test2.size
    |    10
    | end
   nil
ruby> test1.size
   25
ruby> test2.size
   10
```

In this example, test1 and test2 belong to same class, but test2 has been given a redefined size method and so they behave differently. A method given only to a single object is called a singleton method.

在这个示例中，test1和test2都属于同一个类，但是test2重定义了`size`方法，因此它们有不同的行为。只属于一个对象的**方法**被称为**单例方法**。

Singleton methods are often used for elements of a graphic user interface (GUI), where different actions need to be taken when different buttons are pressed.

**单例方法**经常用于图形用户界面(GUI)的元素，当不同的按钮被按下时，需要采取不同的行动。

Singleton methods are not unique to ruby, as they appear in CLOS, Dylan, etc. Also, some languages, for example, Self and NewtonScript, have singleton methods only. These are sometimes called prototype-based languages.

**单例方法**并不是**Ruby**独有的，它出现于**CLOS**、**Dylan**等，同样，也出现于许多语言中，例如，**Self**和**NewtonScript**只有**单例方法**。它们有时被称为**基于原型的语言**。