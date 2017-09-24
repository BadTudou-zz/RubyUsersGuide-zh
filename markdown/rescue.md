# 异常处理：rescue
**Exception processing: rescue**

**异常处理：rescue**

An executing program can run into unexpected problems. 

一个运行的程序可能会遇到意想不到的问题。

A file that it wants to read might not exist; the disk might be full when it wants to save some data; the user may provide it with some unsuitable kind of input.

一个想要读取的文件可能不存在；想要保存一些数据的时候磁盘却满了；用户可能会提供一些不合适的输入。

```
ruby> file = open("some_file")
ERR: (eval):1:in `open': No such file or directory - some_file
```

A robust program will handle these situations sensibly and gracefully. 

一个健壮的程序将会明智而优雅地处理这些情况。

Meeting that expectation can be an exasperating task. 

满足这种期望可能是一个令人恼火的任务。

C programmers are expected to check the result of every system call that could possibly fail, and immediately decide what is to be done:

**C**程序员期望检查每一个可能失败的系统调用的结果，并立即决定要做什么:

```
FILE *file = fopen("some_file", "r");
if (file == NULL) {
  fprintf( stderr, "File doesn't exist.\n" );
  exit(1);
}
bytes_read = fread( buf, 1, bytes_desired, file );
if (bytes_read != bytes_desired ) {
  /* do more error handling here ... */
}
...
```

This is such a tiresome practice that programmers can tend to grow careless and neglect it, and the result is a program that doesn't handle exceptions well. 

这是一种令人厌烦的做法，程序员可能会变得粗心大意，忽视它，结果是它成了一个不处理异常的程序。

On the other hand, doing the job right can make programs hard to read, because there is so much error handling cluttering up the meaningful code.

另一方面，做正确的工作可能会使程序难以阅读，因为有太多的错误处理会使有意义的代码变得混乱。

In ruby, as in many modern languages, we can handle exceptions for blocks of code in a compartmentalized way, thus dealing with surprises effectively but not unduly burdening either the programmer or anyone else trying to read the code later. 

在**Ruby**中，就像在许多现代语言中一样，我们可以用一种划分的方式处理代码块的异常，这样就可以有效地处理意外事件，但不会给程序员或其他试图阅读代码的人造成太大的负担。

The block of code marked with begin executes until there is an exception, which causes control to be transferred to a block of error handling code, which is marked with rescue. 

从有`begin`标记的代码块开始执行，直到有一个异常，这导致控制被转移到一个错误处理代码块，这个代码块被标记为`rescue`。

If no exception occurs, the rescue code is not used. The following method returns the first line of a text file, or nil if there is an exception:

如果没有异常发生，则不使用`rescue`代码。下面的方法返回文本文件的第一行，如果有异常，则返回`nil`：

```
def first_line( filename )
  begin
    file = open("some_file")
    info = file.gets
    file.close
    info  # Last thing evaluated is the return value
  rescue
    nil   # Can't read the file? then don't return a string
  end
end
```

There will be times when we would like to be able to creatively work around a problem. Here, if the file we want is unavailable, we try to use standard input instead:

有时候，我们希望能够创造性地解决一个问题。在这里，如果我们想要的文件不可用，我们尝试使用标准输入:

```
begin
  file = open("some_file")
rescue
  file = STDIN
end

begin
  # ... process the input ...
rescue
  # ... and deal with any other exceptions here.
end
```

retry can be used in the rescue code to start the begin code over again. It lets us rewrite the previous example a little more compactly:

可以在`rescue`代码中使用`retry`，以重新启动开始的代码。它让我们更简洁地重写上一个例子:

```
fname = "some_file"
begin
  file = open(fname)
  # ... process the input ...
rescue
  fname = "STDIN"
  retry
end
```

However, there is a flaw here. A nonexistent file will make this code retry in an infinite loop. You need to watch out for such pitfalls when using retry for exception processing.

然而，这里有一个缺陷。一个不存在的文件将使该代码在无限循环中重试。在使用重试进行异常处理时，需要注意这些缺陷。

Every ruby library raises an exception if any error occurs, and you can raise exceptions explicitly in your code too. 

如果出现任何错误，每个**Ruby**库都会抛出异常，并且你也可以在代码中显式地抛出异常。

To raise an exception, use raise. It takes one argument, which should be a string that describes the exception. 

使用`raise`来抛出一个异常。它可以接受一个描述异常的字符串作为参数。

The argument is optional but should not be omitted. It can be accessed later via the special global variable $!.

这个参数是可选的，但不应该省略。稍后可以通过特殊的全局变量`$!`来访问它。

```
ruby> raise "test error"
   test error
ruby> begin
    |   raise "test2"
    | rescue
    |   puts "An error occurred: #{$!}"
    | end
An error occurred: test2
   nil
```

[上一章 类常量](./constants.md "Class constants")
[下一章 异常处理：ensure](./ensure.md "Exception processing: ensure")
