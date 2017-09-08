# 重新定义方法
**Redefinition of methods**

**重新定义方法**

In a subclass, we can change the behavior of the instances by redefining superclass methods.

在**子类**中，我们可以通过重定义继承自**父类**的方法来改变实例的行为。

```
ruby> class Human
    |   def identify
    |     puts "I'm a person."
    |   end
    |   def train_toll(age)
    |     if age < 12
    |       puts "Reduced fare.";
    |     else
    |       puts "Normal fare.";
    |     end
    |   end
    | end
   nil
ruby> Human.new.identify
I'm a person.
   nil
ruby> class Student1<Human
    |   def identify
    |     puts "I'm a student."
    |   end
    | end
   nil
ruby> Student1.new.identify
I'm a student.
   nil
```

Suppose we would rather enhance the superclass's identify method than entirely replace it. For this we can use super.

假如我们想要增强父类的的**identify**方法，而不是完全替换它。为此我们可以使用`super`。

```
ruby> class Student2<Human
    |   def identify
    |     super
    |     puts "I'm a student too."
    |   end
    | end
   nil
ruby> Student2.new.identify
I'm a person.
I'm a student too.
   nil
```

super lets us pass arguments to the original method. It is sometimes said that there are two kinds of people...

`super`让我们将传递参数给原始的方法。有时会说，有两种人...

```
ruby> class Dishonest<Human
    |   def train_toll(age)
    |     super(11) # 我们想要便宜的车票
    |   end
    | end
   nil
ruby> Dishonest.new.train_toll(25)
Reduced fare. 
   nil

ruby> class Honest<Human
    |   def train_toll(age)
    |     super(age) # 传递我们给的参数
    |   end
    | end
   nil
ruby> Honest.new.train_toll(25)
Normal fare. 
   nil
```

[上一章 继承](./inheritance.md "Inheritance")
[下一章 访问控制](./accesscontrol.md "Access control")