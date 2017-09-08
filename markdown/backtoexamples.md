# 再读“简单示例”
**Back to the simple examples**

**再读“简单示例”**

Now let's take apart the code of some of our previous example programs.

现在，让我们把之前“示例代码”中的代码剖析一下。

The following appeared in the simple examples chapter.

“简单示例”中有以下代码。

```
def fact(n)
  if n == 0
    1
  else
    n * fact(n-1)
  end
end
puts fact(ARGV[0].to_i)
```

Because this is the first explanation, we examine each line individually.

由于这是对代码的第一个解释说明，所以我们为每一行代码都做了单独的解释。

**Factorials**
**阶乘**

```
def fact(n)
```

In the first line, def is a statement to define a function (or, more precisely, a method; we'll talk more about what a method is in a later chapter).

第1行中，`def`是定义函数的声明(或者更确切地说，是一个方法。我们将在后面的章节中更多地讨论方法是什么)。

Here, it specifies that the function fact takes a single argument, referred to as n.

这里，它指定了函数在实际运行中将接收一个称之为n的参数。

```
if n == 0
```

The if is for checking a condition. When the condition holds, the next bit of code is evaluated; otherwise whatever follows the else is evaluated.

`if`用于检查条件。当条件成立时，执行`if`之后的代码块，否则执行`else`之后的代码块。

`1`
The value of if is 1 if the condition holds.

如果条件成立，则值为1.

`else`
If the condition does not hold, the code from here to end is evaluated.

如果条件不成立，从这里到`end`之间的代码将被执行。

`n * fact(n-1)`
If the condition is not satisfied, the value of if is the result of n times fact(n-1).

如果条件不满足，则`if`的值是`n`乘以`fact(n-1)`的结果。

`end`
The first end closes the if statement.

第1个`end`用于结束`if`语句。

`end`
The second end closes the def statement.

第2个`end`用于结束`def`语句。

`puts fact(ARGV[0].to_i)`
This invokes our fact() function using a value specified from the command line, and prints the result.

此处调用了我们的`fact()`函数，它从命令行接收一个值，然后将结果输出。

ARGV is an array which contains command line arguments. The members of ARGV are strings, so we must convert this into a integral number by to_i. Ruby does not convert strings into integers automatically like perl does.

`ARGV`是一个包含了命令行参数的数组。`ARGV`的成员都是字符串，所以我们必须用`to_i`将其转换成整数。**Ruby**不会像**Perl**那样自动将一个字符串转换为整数。

What would happen if we fed this program a negative number? Do you see the problem? Can you fix it?
如果我们给这个程序一个负数，会发生什么呢?
你找到问题所在了么？能够完善它么？

Strings
字符串

Next we examine the puzzle program from the chapter on strings. As this is somewhat longer, we number the lines for reference.
接下来，我们将从字符串的章节中研究这个谜题程序。由于话费的时间更长，所以我们为代码标注了行号。

```
01 words = ['foobar', 'baz', 'quux']
02 secret = words[rand(3)]
03
04 print "guess? "
05 while guess = STDIN.gets
06   guess.chop!
07   if guess == secret
08     puts "You win!"
09     break
10   else
11     puts "Sorry, you lose."
12   end
13   print "guess? "
14 end
15 puts "the word is ", secret, "."
```

In this program, a new control structure, while, is used. 

这个程序中使用了一个新的控制结构`while`。

The code between while and its corresponding end will execute repeatedly as long as some specified condition remains true.

当指定的条件满足时，`while`和它对应的`end`之间的代码就会一直被执行。

In this case, guess=STDIN.gets is both an active statement (collecting a line of user input and storing it as guess), and a condition (if there is no input, guess, which repesents the value of the whole guess=STDIN.gets expression, has a nil value, causing while to stop looping).

在这里，`guess=STDIN.gets`既是一个活动语句(收集用户输入并将其保存在guess中)，又是一个条件(如果没有输入，执行表达式guess=STDIN.gets所得到的guess，其值将为nil，进行导致循环被终止)。

STDIN is the standard input object. Usually, guess=gets does the same thing as guess=STDIN.gets.

`STDIN`是**标准输入设备**，通常情况下，`guess=gets`与`guess=STDIN.gets`是等价的。

rand(3) in line 2 returns a random number in the range 0 to 2. This random number is used to extract one of the members of the array words.

第2行的`rand(3)`将返回一个0到2之间的随机数，这个随机数被用来提取单词数组的一个成员。

In line 5 we read one line from standard input by the method STDIN.gets. If EOF (end of file) occurs while getting the line, gets returns nil. So the code associated with this while will repeat until it sees ^D (try ^Z or F6 under DOS/Windows), signifying the end of input.

在第5行，我们通过`STDIN.gets`方法从`标准输入设备`中读取1行内容，当读取的内容为`EOF`(end of file)时，`gets`返回`nil`。所以与`while`有关的代码会重复执行，直到遇到`^D`(在**DOS**/**Windows**上为`^Z`或`F6`)才结束。

guess.chop! in line 6 deletes the last character from guess; in this case it will always be a newline character, gets includes that character to reflect the user's Return keystroke, but we're not interested in it.

第6行的`guess.chop!`将会删除`guess`的最后一个字符，在这里，它将始终为换行符，`gets`包含该字符以反映用户的返回键，但我们对它不感兴趣。

In line 15 we print the secret word. We have written this as a puts (put string) statement with two arguments, which are printed one after the other; but it would have been equally effective to do it with a single argument, writing secret as #{secret} to make it clear that it is a variable to be evaluated, not a literal word to be printed:

在第15行我们打印出了机密单词，我们将它写成了一个有2个参数的`puts`（put string）语句，它们都会依次打印出来。但是它完全可以用一个语句来完成，将`secret`写作`#{secret}`，以明确表示它是一个被计算的变量，而不是一个被原样打印的单词。

`puts "the word is #{secret}."`

Many programmers feel this is a cleaner way to express output; it builds a single string and presents it as a single argument to puts.

许多程序员觉得这是一种更清晰地表达输出的方式，它构建了一个单独的字符串，并将其作为一个单独的参数来表示。

Also, we are by now used to the idea of using puts for standard script output, but this script uses print instead, in lines 4 and 13. 

而且，我们现在已经习惯了使用`puts`来作为脚本输出的概念，但是我们在第4行和第13行仍然使用的是`print`。

They are not quite the same thing. print outputs exactly what it is given; puts also ensures that the output line ends. Using print in lines 4 and 13 leaves the cursor next to what was just printed, rather than moving it to the beginning of the next line. This creates a recognizable prompt for user input. In general, the four output calls below are equivalent:

它们并不是完全相同，`print`将给它的东西完全输出，`puts`确保会输出行结束符。在第4行和第13行中使用`print`将光标放在刚刚打印的内容旁边，而不是把它移到下一行的开头，以为用户输入创建一个可辨别的提示。通常情况下，下面4个输出调用是等价的：

```
 # 隐式地添加新行:
puts  "Darwin's wife, Esmerelda, died in a fit of penguins."
```
```
 # 新行必须显式地在print命令中给出
print "Darwin's wife, Esmerelda, died in a fit of penguins.\n"
```
```
 # 你可以使用+将输出连接起来
print 'Darwin's wife, Esmerelda, died in a fit of penguins.'+"\n"
```

```
 # 或者通过提供多个字符串来将它们连接起来:
print 'Darwin's wife, Esmerelda, died in a fit of penguins.', "\n", "
One possible gotcha: sometimes a text window is programmed to buffer output for the sake of speed, collecting individual characters and displaying them only when it is given a newline character. So if the guessing game script misbehaves by not showing the prompt lines until after the user supplies a guess, buffering is the likely culprit. To make sure this doesn't happen, you can flush the output as soon as you have printed the prompt. It tells the standard output device (an object named STDOUT), don't wait; display what you have in your buffer right now."
```

```
04 print "guess? "; STDOUT.flush
  ...
13 print "guess? "; STDOUT.flush
```

And in fact, we were more careful with this in the next script.

事实上，在下一个脚本中我们显得更小心。

**Regular expressions**

**正则表达式**

Finally we examine this program from the chapter on regular expressions.

最后，我们将从**正则表达式**的章节来研究这个程序。

```
01 st = "\033[7m"
02 en = "\033[m"
03
04 puts "Enter an empty string at any time to exit."
05
06 while true
07   print "str> "; STDOUT.flush; str=gets.chop
08   break if str.empty?
09   print "pat> "; STDOUT.flush; pat=gets.chop
10   break if pat.empty?
11   re = Regexp.new(pat)
12   puts str.gsub(re, "#{st}\\&#{en}")
13 end
```

In line 6, the condition for while is hardwired to true, so it forms what looks like an infinite loop. 

在第6行中，`while`的条件始终为`true`，所以它形成了一个`无限循环`。

However we put break statements in the 8th and 10th lines to escape the loop. 

然后我们在第8行和第10行放置了`break`语句来跳出循环。

These two breaks are also an example of "if modifiers." An if modifier executes the statement on its left hand side if and only if the specified condition is satisfied. 

这2个`break`也是`if`修饰符的一个例子。当指定条件得到满足时，`if`修饰符将执行它左边的语句。

This construction is unusual in that it operates logically from right to left, but it is provided because for many people it mimics a similar pattern in natural speech. 

这种在逻辑上是从右到左的结构并不常用，但是我们仍提供了它，是因为对许多人来说，它模仿了自然语言中所存在的类似的模式。

It also has the advantage of brevity, as it needs no end statement to tell the interpreter how much of the following code is supposed to be conditional. 

它同样也有简洁的优点，因为它不需要`end`语句来告诉解释器其下有多少代码是有条件的。

An if modifier is conventionally used in situations where a statement and condition are short enough to fit comfortably together on one script line.

如果语句和条件足够短，可以在一个脚本行中轻松地组合在一起，就使用`if`修饰符。

Note the difference in the user interface compared to the string-guessing script. This one lets the user quit by hitting the Return key on an empty line. We are testing for emptiness of the input string, not for its nonexistence.

请注意用户界面与"猜测字符串"脚本的区别。这个允许用户在空行上输入回车键来退出，我们正在测试的是输入的字符串为空，而不是没有任何输入。

In lines 7 and 9 we have a "non-destructive" chop; again, we're getting rid of the unwanted newline character we always get from gets. 

在第7行和第9行，我们有一个“非破坏性”的`chop`。再一次，我们去掉了从`gets`中得到的不需要的换行符。

Add the exclamation point, and we have a "destructive" chop. What's the difference?

加上感叹号`!`，我们就得到了一个“破坏性”的`chop`，它们有何不同？

 In ruby, we conventionally attach '!' or '?' to the end of certain method names. The exclamation point (!, sometimes pronounced aloud as "bang!") indicates something potentially destructive, that is to say, something that can change the value of what it touches. 

在**Ruby**中，我们习惯于给某些方法名的末尾加上`!`或者`?`，感叹号`!`(!，有时也被读作"bang!")表示可能具有破坏性，也就是说，可以改变它所访问的值。

chop! affects a string directly, but chop gives you a chopped copy without damaging the original. Here is an illustration of the difference.

`chop!`直接更改一个字符串，而`chop`会给你一个截好的副本而不会破坏原始的文本。这里是一个解释它们差异的例子：

```
ruby> s1 = "forth"
  "forth"
ruby> s1.chop!       # 改变了s1.
  "fort"
ruby> s2 = s1.chop   # 这会在s2中放置一个修改过的副本,
  "for"
ruby> s1             # ... 没有修改s1.
  "fort"
```

You'll also sometimes see chomp and chomp! used. These are more selective: the end of a string gets bit off only if it happens to be a newline. So for example, "XYZ".chomp! does nothing.

有时你会看到`chomp`和`chomp!`都被使用，这是可以选择的：只有当字符串的末尾是换行符时，才会认为它已经结束了。举个例子，`"XYZ".chomp!"`就会什么也不做。

If you need a trick to remember the difference, think of a person or animal tasting something before deciding to take a bite, as opposed to an axe chopping indiscriminately.

如果你需要一个技巧来记住它们的不同，想想一个人或动物在品尝什么东西之前，会决定咬一口，而不是不加选择地使用砍斧。

The other method naming convention appears in lines 8 and 10. A question mark (?, sometimes pronounced aloud as "huh?") indicates a "predicate" method, one that can return either true or false.

另一种方法命名约定出现在第8行和第10行中。一个问号`?`(?，有时也被读作“huh?”)表明一个`断言`方法，即是可以返回`true`或`false`。

Line 11 creates a regular expression object out of the string supplied by the user. The real work is finally done in line 12, which uses gsub to globally substitute each match of that expression with itself, but surrounded by ansi markups; also the same line outputs the results.

第11行从用户提供的字符串中创建了一个**正则表达式**对象，真正的工作最终在第12行完成，使用`gsub`来全局地替换该表达式的每个匹配，但是被ANSI标记所包围。然后在同一行中输出结果。

We could have broken up line 12 into separate lines like this:

我们可以把第12行分解成这样的单独的行:

```
highlighted = str.gsub(re,"#{st}\\&#{en}")
puts highlighted
```

or in "destructive" style:

或者使用“破坏性”风格：

```
str.gsub!(re,"#{st}\\&#{en}")
puts str
```

Look again at the last part of line 12. st and en were defined in lines 1-2 as the ANSI sequences that make text color-inverted and normal, respectively. 

再看看第12行的最后一部分。在1-2行中，**st**和**en**被定义为**ANSI**序列，其文本颜色分别为颠倒和正常。

In line 12 they are enclosed in #{} to ensure that they are actually interpreted as such (and we do not see the variable names printed instead). 

在第12行中，它们被用`#{}`封闭起来以确保它们被解释为变量(我们没有看到变量名被打印出来)。

Between these we see \\&. This is a little tricky. Since the replacement string is in double quotes, the pair of backslashes will be interpreted as a single backslash; 

在这些之间我们可以看到`\&`，这有点棘手。由于替换字符串被包含在双引号中，因此`\\`将被解释为一个反斜杠。

What gsub actually sees will be \&, and that happens to be a special code that refers to whatever matched the pattern in the first place.

**gsub**实际上看到的将是`\&`，而这恰好是一种特殊的代码，它指的是一种首先匹配的模式。

So the new string, when displayed, looks just like the old one, except that the parts that matched the given pattern are highlighted in inverse video.

因此当新的字符串被显示时，除了那些与给定模式匹配的部分将在显示器中被高亮显示外，其他的看起来和旧的字符串是一样的。

[上一章 数组](./arrays.md "Arrays")
[下一章 流程控制](./control.md "Control structures")
