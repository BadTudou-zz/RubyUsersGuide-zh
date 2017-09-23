# 变量
**Variables**

**变量**

Ruby has three kinds of variables, one kind of constant and exactly two pseudo-variables. 

**Ruby**有3种类型的变量，一种是**常量**，另外两种是**伪变量**。

The variables and the constants have no type. While untyped variables have some drawbacks, they have many more advantages and fit well with ruby's quick and easy philosophy.

变量和常量都没有类型。尽管没有类型的变量有一些缺点，但是它们有远远更多的优点，并且与**Ruby**的快速和简单的哲学相适应。

Variables must be declared in most languages in order to specify their type, modifiability (i.e., whether they are constants), and scope; since type is not an issue, and the rest is evident from the variable name as you are about to see, we do not need variable declarations in ruby.

变量在大多数语言中必须声明，以指定它们的类型、可修改性(即:它们是否是常数)和作用域；因为类型不是问题，剩下的就是从变量名中可以看到的，正如你即将要看到的，在**Ruby**中使用变量不需要声明。

The first character of an identifier categorizes it at a glance:

标识符的第一个字符对它进行了分类:

| 标识符       |  类型  |
| --------- | :--: |
| $         | 全局变量 |
| @         | 实例变量 |
| [a-z] 或 _ | 局部变量 |
| [A-Z]     |  常量  |

The only exceptions to the above are ruby's pseudo-variables: self, which always refers to the currently executing object, and nil, which is the meaningless value assigned to uninitialized variables. 

上面的唯一例外是**Ruby**的伪变量:总是指向当前运行对象的`self`和被赋给未初始化变量的无意义的值`nil`。

Both are named as if they are local variables, but self is a global variable maintained by the interpreter, and nil is really a constant. 

虽然两者都像是局部变量一样被命名，但是`self`是由解释器维持的一个全局变量，而`nil`实际上是一个常量。

As these are the only two exceptions, they don't confuse things too much.

因为这是仅有的2个例外，他们不会把事情搞得太混乱。

You may not assign values to self or nil. main, as a value of self, refers to the top-level object:

你不能给`self`或`nil`赋值。`main`，作为`self`的值，指的是顶级对象:

```
ruby> self
   main
ruby> nil
   nil
```

[上一章 过程对象](./procobjects.md "Procedure objects")
[下一章 全局变量](./globalvars.md "Global variables")
