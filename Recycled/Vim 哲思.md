说起来惭愧，作为一个程序员怎能不懂 Vim，一直以来对 Vim 只是略知皮毛，只在编辑小文本时偶尔用到。当初几次尝试使用 Vim 都感觉刻意使用反而增加了负担，再次入坑希望有所收获。<!-- more -->

## 模式

Vim 编辑程序有三种操作模式，分别称为编辑模式、插入模式 和 命令行模式。

**普通模式**：即 Normal 模式，Vim 的缺省模式，用以执行命令，在普通模式中可以快捷移动光标，使用剪切、复制、粘贴来处理文本数据，但无法编辑文本内容，vim 的大多数场景都是在这种模式下。

**插入模式**：即 Insert 模式，此模式下和一般的文本编辑器无多大区别，用来输入文本，在插入模式中，可以按 ESC 键回到普通模式。

**命令行模式**：用来执行命令。在编辑模式下输入『 : / ? 』三个中的任何一个按钮，就可以将光标移动到最底下那一行。在这个模式当中，可以进行保存、查找、替换、显示行号、退出、配置 Vim 操作等等的动作。

## 移动

### 文件中移动

在 vim 中提供了一些命令，可以方便的在文件中移动，命令 `gg` 移动到文件的第一行，而命令 `G` 则移动到文件的最后一行。可以在 `G` 之前加入数字表示需要跳转的行号，例如，"100G" 表示跳转到第 100 行。也可以使用百分比来进行跳转，`50%` 表示跳转到文件中间。

```bash
gg        移动到文件的第一行
G         则移动到文件的最后一行
```

可以在 `G` 之前加入数字表示需要跳转的行号，例如，"100G" 表示跳转到第 100 行。也可以使用百分比来进行跳转，`50%` 表示跳转到文件中间。

### 翻页

在 vim 中同样可以使用 `PageUp` 和 `PageDown` 进行翻页，不过通常使用 `CTRL-B` 和 `CTRL-F` 来进行翻页，它们的功能等同于 `PageUp` 和 `PageDown`。命令之前也可以加上数字，来表示向上或向下翻多少页。

`CTRL-U` 和 `CTRL-D` 可以让屏幕向上或向下移动半页，数字加 `CTRL-Y` 和 `CTRL-E` 可以让屏幕向上或向下移动指定行数。

```bash
CTRL-B        向上移动一页
CTRL-F        向下移动一页
CTRL-U        向上移动半页
CTRL-D        向下移动半页
CTRL-Y        向上移动指定行数
CTRL-E        向下移动指定行数
```

### 滚屏

在 vim 中可以使用 `zt、zz、zb` 命令让光标所在的位置滚动窗口的顶端、中间或底部，相较于翻页，滚屏的好处是始终以当前光标位置做为参照，不容易迷失方向。

```bash
zt        光标移动到窗口顶部
zz        光标移动到窗口中间
zb        光标移动到窗口底部
```

### 跳转

在 vim 中可以使用 `H、M、L` 命令让光标所在行跳到当前窗口的顶部、中间、和底部，并停留在第一个非空字符上。`H` 和 `L` 命令前也可以加一个数字指定跳转距窗口顶部、底部的行数。例如，"3H" 表示光标移动到距窗口顶部第3行的位置，"5L" 表示光标移动到距窗口底部5行的位置。

还可以使用 `(` 和 `)` 命令进行句间跳转，`{` 和 `}` 命令进行段间跳转。

```bash
H        光标所在行跳到顶部
M        光标所在行跳到中间
L        光标所在行跳到底部
)        跳转至前一句
(        跳转至后一句
}        跳转至前一段
{        跳转至后一段
```

### 上下左右

`h、j、k、l` 的移动方式，已经成为vim的标志之一，分别代表向左、下、上、右移动。
如同许多 vim 命令一样，可以在这些键前加一个数字，表示移动的倍数。例如，"10j" 表示向下移动 10行；"10l" 表示向右移动 10 列。

```bash
h        向左移动
j        向下移动
k        向上移动
l        向右移动
```

### 行首/行尾

在 vim 中移动到行首和行尾的命令分别是 `0` 和 `$`，另外还有一个命令 `^`，用它可以移动到行首的第一个非空白字符。联想到正则表达式中 `^` 字符代表行首，而 `$` 字符代表行尾。

```bash
0        移动到行尾
$        移动到行首
^        移动到行首第一个非空字符
```

### 移动到指定字符

在 vim 中可以使用 `f、t、F、T` 命令进行行内快速移动到指定字符。

`f` 命令移动光标到右边的指定字符上，`F` 命令则反方向查找，也就是移动光标到左边的指定字符上。例如：`fc` 移动到光标右边字符 "c" 上，而 `Fx` 则移动到光标左边字符 “c” 上。

`t、T` 命令与 `f、F` 命令的唯一区别就在于不是移动到指定字符上，而是移动到之前或之后。`t` 命令移动光标到右边的指定字符之前，`F` 命令移动到光标左边的指定字符之后。

这四个命令只在当前行中移动光标，光标不会跨越回车换行符。并且都可以在前面加上数字来表示移动的倍数。

```bash
f        移动到右边指定字符上
F        移动到左边指定字符上
t        移动到右边指定字符之前
T        移动到左边指定字符之后
```

### 按单词移动

在 vim 中，`w` 命令移动光标到下一个单词的词首，`e` 命令移动光标到下一个单词的结尾；`b` 命令移动光标到上一个单词的词首，`ge` 命令移动光标到上一个单词的结尾。

空白字符可以把代码分成字串，同上，`W` 命令移动光标到下一个字串首，`E` 命令移动光标到下一个字串尾；`B` 命令移动光标到上一个字串首，`gE` 命令移动光标到上一个字串尾i。

`*` 和 `#` 会在文件内搜索并匹配当前光标所在单词，并向下或向上跳转到匹配的单词上。

```bash
w       移动到下一个单词首
W       移动到下一个字串首
e       移动到下一个单词尾
E       移动到下一个字串尾
b       移动到上一个单词首
B       移动到上一个字串首
ge      移动到上一个单词尾
gE      移动到上一个字串尾
*       移动到下一个匹配的单词
#       移动到上一个匹配的单词
```

### 查找

在 vim 中使用查找可以进行快速移动，在 `Normal` 模式下，键入 `\` 或 `？` 分别进行向下、向上查找，然后输入需要查找的字符串并回车，光标跳转到第一个匹配的地方，之后可以使用命令 `n` 重复上一次的查找，命令 `N` 反向重复上一次的查找。

vim 保存了查找的历史记录，可以在输入 `/` 或 `?` 后，用上、下光标键翻看历史记录，然后再次执行这个查找。

### 折叠

代码折叠可以减少对空间的占用，移动速度，在 vim 中可以使用以下命令快速进行代码折叠：

 ```bash
zo        打开光标下的折叠
zO        循环打开光标下的折叠，也就是说，如果存在多级折叠，每一级都会被打开
zc        关闭光标下的折叠
zC        循环关闭光标下的折叠
```

## 编辑

### 插入

在 Vim 中，通过使用如下任意一个插入命令可以从普通模式进入插入模式，使用 `ESC` 键从插入模式切换回普通模式。

```bash
i        在当前字符的左边插入
I        在当前行首插入
a        在当前字符的右边插入
A        在当前行尾插入
o        在当前行下面插入一个新行
O        在当前行上面插入一个新行
```

### 选择文本

在使用剪切、删除、拷贝之前可以使用 `v` 或 `V` 选择文本。

```bash
v        按字符选择
V        按行选择
```

### 删除和剪贴

在 Vim 中通过 `X` 命令进行删除字符，加上数字可以删除多个字符，例如: "6x" 删除当前光标所在处起始地 6 个字符。

```bash
x        删除光标处所在的字符
```

### 剪切和拷贝

通过 `d` 命令可以按块进行剪贴，在使用 `v` 或 `V` 命令选中文本之后，`d` 命令可以将选中的文本剪贴，`dd` 可以剪贴当前光标所在行，加上数字可以进行多行删除。`d$` 和 `d^` 可以剪贴光标所在位置到行尾或行首的内容。

```bash
d        剪贴选中文本
dd       剪贴光标所在行
d$       剪贴光标到行尾的内容
d^       删除光标到行首的内容
y        拷贝选择的内容
p        粘贴剪贴板的内容
```

Just enjoy it ฅ●ω●ฅ

参考文章：  
[vi/vim使用进阶: 指随意动，移动如飞](//blog.easwy.com/archives/advanced-vim-skills-basic-move-method/)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM4MjMzNTQwXX0=
-->