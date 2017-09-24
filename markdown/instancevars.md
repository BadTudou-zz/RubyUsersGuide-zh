# 实例变量
**Instance variables**

**实例变量**

An instance variable has a name beginning with @, and its scope is confined to whatever object self refers to. 

一个**实例变量**的名称以`@`开头，而且它的作用域仅限于该对象自身。

Two different objects, even if they belong to the same class, are allowed to have different values for their instance variables. 

2个不同的对象，尽管它们属于同一个类，允许对**实例变量**有不同的值。

From outside the object, instance variables cannot be altered or even observed (i.e., ruby's instance variables are never public) except by whatever methods are explicitly provided by the programmer. 

对于外部对象，除了由程序员明确提供的方法之外，**实例变量**不可改变，甚至不可见(即，**Ruby**的实例变量从来不是公开的)。

As with globals, instance variables have the nil value until they are initialized.

与**全局变量**一样，**实例变量**在初始化之前的值为`nil`。

Instance variables do not need to be declared. 

**实例变量**不需要声明。

This indicates a flexible object structure; in fact, each instance variable is dynamically appended to an object when it is first assigned.

这表明了一个灵活的对象结构，事实上，每个**实例变量**都是在第一次被赋值时被动态地追加到一个对象中。

```
ruby> class InstTest
    |   def set_foo(n)
    |     @foo = n
    |   end
    |   def set_bar(n)
    |     @bar = n
    |   end
    | end
   nil
ruby> i = InstTest.new
   #<InstTest:0x83678>
ruby> i.set_foo(2)
   2
ruby> i
   #<InstTest:0x83678 @foo=2>
ruby> i.set_bar(4)
   4
ruby> i
   #<InstTest:0x83678 @foo=2, @bar=4>
```
Notice above that i does not report a value for @bar until after the set_bar method is invoked.

注意，上面的`i`在调用`set-bar`方法之前并没有返回@bar的值。

[上一章 全局变量](./globalvars.md "Global variables")
[下一章 局部变量](./localvars.md "Local variables")
