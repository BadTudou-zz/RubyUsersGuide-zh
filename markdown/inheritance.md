# 继承
**Inheritance**

**继承**

Our classification of objects in everyday life is naturally hierarchical.

我们在日常生活中对物品的分类是自然分层的。

We know that all cats are mammals, and all mammals are animals. Smaller classes inherit characteristics from the larger classes to which they belong. If all mammals breathe, then all cats breathe.

我们知道，所有的**猫**(Cat)都是**哺乳动物**(Mammal)，而所有的**哺乳动物**都是**动物**。较小的类继承了它们所属的较大类的特征。如果所有的**哺乳动物**都呼吸，那么所有的**猫**也都需要呼吸。

We can express this concept in ruby:

我们可以用**Ruby**来表达这个概念：

```
ruby> class Mammal
    |   def breathe
    |     puts "inhale and exhale"
    |   end
    | end
   nil
ruby> class Cat<Mammal
    |   def speak
    |     puts "Meow"
    |   end
    | end
   nil
```

Though we didn't specify how a `Cat` should breathe, every cat will inherit that behavior from the `Mammal` class since `Cat` was defined as a subclass of `Mammal`. (In OO terminology, the smaller class is a *subclass* and the larger class is a *superclass*.) Hence from a programmer's standpoint, cats get the ability to breathe for free; after we add a `speak` method, our cats can both breathe and speak.

尽管我们没有具体说明一只`Cat`应该如何呼吸，但每只`Cat`都会继承`Mammal`的行为，因为`Cat`被定义为`Mammal`的一个子类。(在**OO**的术语中，较小的类是`子类`，较大的类是`父类`。)因此，从程序员的角度来看，猫咪可以自由地呼吸。在我们添加了`speak`方法之后，我们的猫既可以呼吸也可以叫了。

```
ruby> tama = Cat.new
   #<Cat:0xbd80e8>
ruby> tama.breathe
inhale and exhale
   nil
ruby> tama.speak
Meow
   nil
```

There will be situations where certain properties of the superclass should not be inherited by a particular subclass. Though birds generally know how to fly, penguins are a flightless subclass of birds.

在某些情况下，**父类**的某些属性不应该由特定的**子类**继承。尽管鸟类一般都知道如何飞行，但是企鹅是鸟类的一个不能飞行的子类。

```
ruby> class Bird
​    |   def preen
​    |     puts "I am cleaning my feathers."
​    |   end
​    |   def fly
​    |     puts "I am flying."
​    |   end
​    | end
   nil
ruby> class Penguin<Bird
​    |   def fly
​    |     fail "Sorry. I'd rather swim."
​    |   end
​    | end
   nil
```
Rather than exhaustively define every characteristic of every new class, we need only to append or to redefine the differences between each subclass and its superclass. 

相比详尽地定义每一个新类的每一个特征，我们仅仅需要**添加**或者**重定义**每个和它的父类之间的差异。

This use of inheritance is sometimes called *differential programming*. It is one of the benefits of object-oriented programming.

这种**继承**的使用有时被称为**微分编程**，这是面向对象编程的好处之一。

[上一章 类](./classes.md "Classes")
[下一章 重新定义方法](./redefinemethods.md "Redefinition of methods")
