# 类常量
**Class constants**

**类常量**

A constant has a name starting with an uppercase character. 

常量的名称以大写字母开头。

It should be assigned a value at most once. 

它应该最多赋值一次。

In the current implementation of ruby, reassignment of a constant generates a warning but not an error (the non-ANSI version of eval.rb does not report the warning):

在**Ruby**的当前实现中，重新给一个常量赋值将产生一个警告，而不是一个错误(非ansi版本的eval.rb不报告警告):

```
ruby>fluid=30
   30
ruby>fluid=31
   31
ruby>Solid=32
   32
ruby>Solid=33
   (eval):1: warning: already initialized constant Solid
   33
```

Constants may be defined within classes, but unlike instance variables, they are accessible outside the class.

常量可能在类中被定义，但是不同于实例变量，它们可以在类外部被访问。

```
ruby> class ConstClass
    |   C1=101
    |   C2=102
    |   C3=103
    |   def show
    |     puts "#{C1} #{C2} #{C3}"
    |   end
    | end
   nil
ruby> C1
ERR: (eval):1: uninitialized constant C1
ruby> ConstClass::C1
   101
ruby> ConstClass.new.show
101 102 103
   nil
```

Constants can also be defined in modules.

常量同样可以在模块中被定义。

```
ruby> module ConstModule
    |   C1=101
    |   C2=102
    |   C3=103
    |   def showConstants
    |     puts "#{C1} #{C2} #{C3}"
    |   end
    | end
   nil
ruby> C1
ERR: (eval):1: uninitialized constant C1
ruby> include ConstModule
   Object
ruby> C1
   101
ruby> showConstants
101 102 103
   nil
ruby> C1=99  # 这不是一个好主意
   99
ruby> C1
   99
ruby> ConstModule::C1
   101
ruby> ConstModule::C1=99   # 更早的版本中不允许这样做
   (eval):1: warning: already initialized constant C1
   99
ruby> ConstModule::C1  # "enough rope to shoot yourself in the foot"
   99
```