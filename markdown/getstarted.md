# 起步
**Getting started**

**起步**

First, you'll want to check whether ruby is installed. From the shell prompt (denoted here by "%", so don't type the %), type

首先，如果你想检测**Ruby**是否已经安装，在**提示符**中输入:

`ruby -v`

(-v tells the interpreter to print the version of ruby), then press the Enter key. If ruby is installed, you will see a message something like the following:

(`-v`表示让**解释器**打印出当前**Ruby**的版本)

然后按下**回车键**。如果**Ruby**已经安装，你将会看到类似下面这样的信息:

```
ruby -v
ruby 2.1.0p0 (2013-12-25 revision 44422) [x86_64-linux]
```

If ruby is not installed, you can ask your administrator to install it, or you can do it yourself, since ruby is free software with no restrictions on its installation or use.

如果**Ruby**还没有安装，那么你可以选择自己动手安装，或者向计算机管理员寻求帮助。**Ruby**是一个**自由软件**，任何人都可以随意安装和使用。

Now, let's play with ruby. You can place a ruby program directly on the command line using the -e option:

现在，让我们来把玩一下**Ruby**。你可以在**命令行中**用`-e`选项来直接执行**Ruby**程序。

```
ruby -e 'puts "hello world"'
hello world
```

More conventionally, a ruby program can be stored in a file.

更传统一点，**Ruby**程序可以被保存在文件中。

```
echo "puts 'hello world'" > hello.rb
ruby hello.rb
hello world**
```

When writing more substantial code than this, you will want to use a real text editor!

你编写的代码量远超上面的示例时，你可能想到是时候使用一个**文本编辑器**了。

Some surprisingly complex and useful things can be done with miniature programs that fit in a command line. 

命令行中的小程序可以用来完成一些非常复杂和有用的操作。

For example, this one replaces foo with bar in all C source and header files in the current working directory, backing up the original files with ".bak" appended:

举个例子，这个程序会将当前目录中的**C语言源文件**和**头文件**中的**foo**替换为**bar**。

`ruby -i.bak -pe 'sub "foo", "bar"' *.[ch]`

This program works like the UNIX cat command (but works slower than cat):

而这个程序的作用则有点像**UNIX**中的**cat**命令(但是处理过程比**cat**慢)。

`ruby -pe 0 file`

[上一章 Ruby是什么？](./index.md "Ruby是什么？") 
[下一章 简单示例](./examples.md "简单示例")
