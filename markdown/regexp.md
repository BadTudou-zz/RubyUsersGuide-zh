# 正则表达式
**Regular expressions**

**正则表达式**

Let's put together a more interesting program. This time we test whether a string fits a description, encoded into a concise pattern.

让我们把一个更有趣的程序放在一起。这次我们用简洁的模式来测试一个字符串是否符合描述。

There are some characters and character combinations that have special meaning in these patterns, including:

在这些模式中有一些特殊的字符和字符组合，包括:

[]	range specificication (e.g., [a-z] means a letter in the range a to z)

**[]**	**范围(比如[a-z]表示a到z范围内的字母)**

\w	word character; same as [0-9A-Za-z_]

**\w**	**word字符，等同于[0-9A-Za-z_]**

\W	non-word character

**\W**	**非word字符**

\s	space character; same as [ \t\n\r\f]

**\s**	**间隔符号，等同于[ \t\n\r\f]**

\S	non-space character

**\S**	**非间隔符号**

\d	digit character; same as [0-9]

**\d**	**数字字符，等同于[0-9]**

\D	non-digit character

**\D**	**非数字字符**

\b	backspace (0x08) (only if in a range specification)

**\b**	**退格(0x08) (只有在一个范围规范中)**

\b	word boundary (if not in a range specification)

**\b**	**word边界(如果不在范围规范中)**

\B	non-word boundary

**\B**	**非word边界**

\* zero or more repetitions of the preceding

**\*** **前述字符的0次或多次重复**

\+ one or more repetitions of the preceding

**\+** **前述字符的1次或多次重复**

{m,n} at least m and at most n repetitions of the preceding

**{m,n}** **前述字符的重复次数在m和n之间**

?at most one repetition of the preceding; same as {0,1}

**?** **前述字符的重复次数最多1次，等同于{0,1}**

|either preceding or next expression may match

**|** **匹配其前后2个表达式中的任意一个**

()grouping

**()** **分组**

The common term for patterns that use this strange vocabulary is regular expressions. In ruby, as in Perl, they are generally surrounded by forward slashes rather than double quotes.

使用这种奇怪词汇表的模式的常用术语是**正则表达式**。**Ruby**和**Perl**一样，**正则表达式**通常被**斜线**包围，而不是**双引号**。

If you have never worked with regular expressions before, they probably look anything but regular, but you would be wise to spend some time getting familiar with them. 

如果你以前从未使用过**正则表达式**，那么它们可能看起可能来和其他字符串并没有什么不同，但是你最好花些时间熟悉它们。

They have an efficient expressive power that will save you headaches (and many lines of code) whenever you need to do pattern matching, searching, or other manipulations on text strings.

当你需要对文本字符串进行模式匹配、搜索或其他操作时，它们具有一种有效的表达能力，可以为你省去繁琐(以及许多行代码)。

For example, suppose we want to test whether a string fits this description: "Starts with lower case f, which is immediately followed by exactly one upper case letter, and optionally more junk after that, as long as there are no more lower case characters." 

举个例子，假设我们想测试一个字符串是否符合如下的描述：*以小写字母f开头，紧随其后的是一个大写字母，之后还有其他除了小写字母的字符*。

If you're an experienced C programmer, you've probably already written about a dozen lines of code in your head, right? Admit it; you can hardly help yourself. But in ruby you need only request that your string be tested against the regular expression /^f[A-Z][^a-z]*$/.

如果你是一个有经验的C语言程序员，你可能已经在脑子里写了十几行代码了，是吧？承认吧，你几乎不能帮到自己。但是在**Ruby**中，你只需要使用**正则表达式**对你的字符串进行测试即可。

How about "Contains a hexadecimal number enclosed in angle brackets"? No problem.

又该如何测试“*包含一个用尖括号括起来的十六进制数字*”的字符串呢？很简单。

```
ruby> def chab(s)   # "contains hex in angle brackets"
    |    (s =~ /<0(x|X)(\d|[a-f]|[A-F])+>/) != nil
    | end
  nil
ruby> chab "Not this one."
  false
ruby> chab "Maybe this? {0x35}"    # wrong kind of brackets
  false
ruby> chab "Or this? <0x38z7e>"    # bogus hex digit
  false
ruby> chab "Okay, this: <0xfc0004>."
  true
```

Though regular expressions can be puzzling at first glance, you will quickly gain satisfaction in being able to express yourself so economically.

尽管**正则表达式**会让初次见到它的人感到很疑惑，但你很快就会感到满意，因为它能让你更精简地表达自己。

Here is a little program to help you experiment with regular expressions. Store it as regx.rb and run it by typing "ruby regx.rb" at the command line.

这里有一个小程序可以帮助你尝试正则表达式。将它保存为regx.rb，然后在命令行中输入"ruby regx.rb"来运行它。

# Requires an ANSI terminal!

## 需要一个ANSI终端！

```
st = "\033[7m"
en = "\033[m"

puts "Enter an empty string at any time to exit."

while true
  print "str> "; STDOUT.flush; str = gets.chop
  break if str.empty?
  print "pat> "; STDOUT.flush; pat = gets.chop
  break if pat.empty?
  re = Regexp.new(pat)
  puts str.gsub(re,"#{st}\\&#{en}")
end
```

The program requires input twice, once for a string and once for a regular expression. The string is tested against the regular expression, then displayed with all the matching parts highlighted in reverse video. Don't mind details now; an analysis of this code will come soon.

这个程序要求你输入2次，一次是输入**字符串**，另一次是输入**正则表达式**。字符串是根据正则表达式进行测试的，然后在显示器中突出显示所有的匹配部分。现在不要在意细节，很快你就会看到对这段代码的分析。

```
str> foobar
pat> ^fo+
**foo**bar
​~~~
```

What you see above as red text will appear as reverse video in the program output. The "~~~" lines are for the benefit of those using text-based browsers.

你在上面看到的`****`中的文本会在在程序输出中突出显示，“~~~”用于使用基于文本浏览器的用户。

Let's try several more inputs.

让我们再尝试几个输入。

```
str> abc012dbcd555
pat> \d
abc**012***dbcd**555**
   ~~~    ~~~
```
If that surprised you, refer to the table at the top of this page: \d has no relationship to the character d, but rather matches a single digit.

如果结果让你感到很意外，请回过头去看看参考页面顶部的表格：\d与字符d没有关系，它仅仅匹配一个数字。

What if there is more than one way to correctly match the pattern?

还有其他方法可以正确地匹配该模式吗？

```
str> foozboozer
pat> f.*z
**foozbooz**er
​~~~~~~~~
```
foozbooz is matched instead of just fooz, since a regular expression matches the longest possible substring.

匹配到了foozbooz，而不是fooz，因为**正则表达式**匹配尽可能长的子字符串。

Here is a pattern to isolate a colon-delimited time field.

这里有一种模式，可以分离一个以冒号分隔的时间字段。

```
str> Wed Feb  7 08:58:04 JST 1996
pat> [0-9]+:[0-9]+(:[0-9]+)?
Wed Feb  7 **08:58:04** JST 1996
           ~~~~~~~~
```

"=~" is a matching operator with respect to regular expressions; it returns the position in a string where a match was found, or nil if the pattern did not match.

`=~`是**正则表达式**的匹配操作符。如果找到匹配的字符串，就返回字符串的位置，如果模式不匹配，则不返回。

```
ruby> "abcdef" =~ /d/
   3
ruby> "aaaaaa" =~ /d/
   nil
```

[上一章 字符串](./strings.md "Strings")
[下一章 数组](./arrays.md "Arrays")
