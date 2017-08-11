# 字符串
**Strings**

**字符串**

Ruby deals with strings as well as numerical data. A string may be double-quoted ("...") or single-quoted ('...').

**Ruby**处理字符串就同处理数值数据一样优秀。定义字符串可以用**双引号**或者**单引号**。

```
ruby> "abc"
   "abc"
ruby> 'abc'
   "abc"
```
Double- and single-quoting have different effects in some cases. A double-quoted string allows character escapes by a leading backslash, and the evaluation of embedded expressions using #{}. A single-quoted string does not do this interpreting; what you see is what you get. Examples:

在某些场景中，双引号和单引号会产生不同的结果。双引号字符串允许通过反斜线对字符进行转义，以及对使用`#{}`嵌入的表达式进行求值。单引号字符串则不对这些进行解释，你所看到的便是其最终的结果。比如：
```
ruby> puts "a\nb\nc"
a
b
c
   nil
```

```
ruby> puts 'a\nb\n'
a\nb\nc
   nil
```

```
ruby> "\n"
   "\n"
```

```
ruby> '\n'
   "\\n"
```

```
ruby> "\001"
   "\t"
```

```
ruby> '\001'
   "\001"
```

```
ruby> "abcd #{5*3} efg"
   "abcd 15 efg"
```

```
ruby> var = " abc "
   " abc "
```

```
ruby> "1234#{var}5678"
   "1234 abc 5678"
```

Ruby's string handling is smarter and more intuitive than C's. For instance, you can concatenate strings with +, and repeat a string many times with *:

**Ruby**的字符串处理比**C语言**更智能，更直观。举个例子，你可以使用`+`把字符串连接起来，或者使用`*`将字符串重复多次。

```
ruby> "foo" + "bar"
   "foobar"
```

```
ruby> "foo" * 2
   "foofoo"
```

Concatenating strings is much more awkward in C because of the need for explicit memory management:

在**C语言**中连接字符串要显得更笨拙，因为它需要显式地进行内存管理：

```
char *s = malloc(strlen(s1)+strlen(s2)+1);
strcpy(s, s1);
strcat(s, s2);
/* ... */
free(s);
```

But using ruby, we do not have to consider the space occupied by a string. We are free from all memory management.

但是如果使用的是**Ruby**，我们则不需要考虑字符串占用的空间，由此从所有的内存管理工作中解放出来。

Here are some things you can do with strings.

这里有一些你可以用字符串完成的事情。

Concatenation:

连接：

```
ruby> word = "fo" + "o"
   "foo"
```

Repetition:

重复：
```
ruby> word = word * 2
   "foofoo"
```

Extracting characters (note that characters are integers in ruby):

取出字符(注意在**Ruby**中字符是整数)：

```
ruby> word[0]
   102            # 102是`f'的ASCII码 
ruby> word[-1]
   111            # 111是`o'的ASCII码
```

(Negative indices mean offsets from the end of a string, rather than the beginning.)

(负数的**索引**则表示从字符串末尾开始计算的偏移量，而不是从头开始计算。)

Extracting substrings:

取出子字符串：

```
ruby> herb = "parsley"
   "parsley"
ruby> herb[0,1]
   "p"
ruby> herb[-2,2]
   "ey"
ruby> herb[0..3]
   "pars"
ruby> herb[-5..-2]
   "rsle"
Testing for equality:

ruby> "foo" == "foo"
   true
ruby> "foo" == "bar"
   false
```

Now, let's put some of these features to use. This puzzle is "guess the word," but perhaps the word "puzzle" is too dignified for what is to follow ;-)

现在，让我们来使用一些这些特性。这个谜题是“猜单词”，但也许“谜”这个词太过凝重，不适合接下来的内容;-)

# save this as guess.rb

## 保存为guess.rb

```
words = ['foobar', 'baz', 'quux']
secret = words[rand(3)]

print "guess? "
while guess = STDIN.gets
  guess.chop!
  if guess == secret
    puts "You win!"
    break
  else
    puts "Sorry, you lose."
  end
  print "guess? "
end
puts "The word was ", secret, "."
```

For now, don't worry too much about the details of this code. Here is what a run of the puzzle program looks like.

现在，不要太担心这段代码的细节。下面是这个谜题程序的运行情况。

`% ruby guess.rb`
**guess? foobar**
**Sorry, you lose.**
**guess? quux**
**Sorry, you lose.**
**guess? ^D**
**The word was baz.**
(I should have done a bit better, considering the 1/3 probability of success.)

(考虑到1/3的成功概率，我应该可以做得更好一些。)