# 数组

**Arrays**

**数组**

You can create an array by listing some items within square brackets ([]) and separating them with commas. Ruby's arrays can accomodate diverse object types.

您可以通过在**方括号**中列出一些以逗号分隔的项来创建**数组**。

```
ruby> ary = [1, 2, "3"]
   [1, 2, "3"]
```
Arrays can be concatenated or repeated just as strings can.

**数组**可以同**字符串**一样被连接或重复。

```
ruby> ary + ["foo", "bar"]
   [1, 2, "3", "foo", "bar"]
ruby> ary * 2
   [1, 2, "3", 1, 2, "3"]
```
We can use index numbers to refer to any part of a array.

我们可以通过数字索引来引用**数组**的任何部分。

```
ruby> ary[0]
   1
ruby> ary[0,2]
   [1, 2]
ruby> ary[0..1]
   [1, 2]
ruby> ary[-2]
   2
ruby> ary[-2,2]
   [2, "3"]
ruby> ary[-2..-1]
   [2, "3"]
```
(Negative indices mean offsets from the end of an array, rather than the beginning.)

(负数的索引代表从数组的末尾开始，而不是从头开始。)

Arrays can be converted to and from strings, using join and split respecitvely:

数组可以与字符串相互转换，请参考join和split。

```
ruby> str = ary.join(":")
   "1:2:3"
ruby> str.split(":")
   ["1", "2", "3"]
```

**Hashes**

**哈希**

An associative array has elements that are accessed not by sequential index numbers, but by keys which can have any sort of value. Such an array is sometimes called a hash or dictionary; 

关联数组有一些元素，这些元素不是通过顺序索引号访问的，而是通过**键**来访问，这些**键**可以是任何类型的值。这样的数组有时被称为**散列**或**字典**。

In the ruby world, we prefer the term hash. A hash can be constructed by quoting pairs of items within curly braces ({}). You use a key to find something in a hash, much as you use an index to find something in an array.

在**Ruby**的世界里，我们更喜欢将它称之为**哈希**。可以通过在**花括号中**引用成对的哈希项来构造**哈希**。你通过**键**在**哈希**中查找哈希项，就如同你用**索引**在**数组中**查找**数组元素**一样。

```
ruby> h = {1 => 2, "2" => "4"}
   {1=>2, "2"=>"4"}
ruby> h[1]
   2
ruby> h["2"]
   "4"
ruby> h[5]
   nil
ruby> h[5] = 10    # appending an entry 添加一个哈希项
   10
ruby> h
   {5=>10, 1=>2, "2"=>"4"}
ruby> h.delete 1   # deleting an entry by key 通过键删除一个哈希项
   2
ruby> h[1]
   nil
ruby> h
   {5=>10, "2"=>"4"}
```

[上一章 正则表达式](./regexp.md "Regular expressions")
[下一章 再读“简单示例”](./backtoexamples.md "Back to the simple examples")