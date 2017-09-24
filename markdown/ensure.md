# 异常处理：ensure
**Exception processing: ensure**

**异常处理：ensure**

There may be cleanup work that is necessary when a method finishes its work. 

当方法完成工作时，可能会有一些清理工作。

Perhaps an open file should be closed, buffered data should be flushed, etc. 

也许是一个打开的文件需要关闭，缓存的数据需要刷新，等等。

If there were always only one exit point for each method, we could confidently put our cleanup code in one place and know that it would be executed; 

如果每个方法总是只有一个出口点，那么我们可以自信地将我们的清理代码放在一个地方，并知道它将被执行；

however, a method might return from several places, or our intended cleanup code might be unexpectedly skipped because of an exception.

但是，一个方法可能从几个地方返回，或者我们准备的清理代码可能会因为异常而被意外地跳过。

```
file = open("/tmp/some_file", "w")
begin
  # ... write to the file ...
  file.close
end
```

In the above, if an exception occurred during the section of code where we were writing to the file, the file would be left open. And we don't want to resort to this kind of redundancy:

在上面，如果一个异常发生在我们写入文件的代码段中，那么这个文件就会被一直打开。我们不想采用这种冗余的方式：

```
file = open("/tmp/some_file", "w")
begin
  # ... write to the file ...
  file.close
rescue
  file.close
  fail # raise an exception
end
```

It's clumsy, and gets out of hand when the code gets more complicated because we have to deal with every return and break.

它很笨拙，当代码变得更加复杂的时候就会失去控制，因为我们必须处理每一个返回和中断。

For this reason we add another keyword to the "begin...rescue...end" scheme, which is ensure. 

出于这个原因，我们在`begin...rescue...end`中添加了另一个关键字：`ensure`。

The ensure code block executes regardless of the success or failure of the begin block.

无论`begin`块是成功还是失败，`ensure`代码块都将被执行。

```
file = open("/tmp/some_file", "w")
begin
  # ... write to the file ...
rescue
  # ... handle the exceptions ...
ensure
  file.close   # ... and this always happens.
end
```

It is possible to use ensure without rescue, or vice versa, but if they are used together in the same begin...end block, the rescue must precede the ensure.

可以在没有`rescue`的情况下使用`ensure`，反之亦然，但是如果它们在同一`begin...end`块中一起使用，`rescue`必须出现在`ensure`之前。

[上一章 异常处理：rescue](./rescue.md "Exception processing: rescue")
[下一章 访问器](./accessors.md "Accessors")
