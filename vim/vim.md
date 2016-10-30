# frontend 前端
## vim 编辑文件
![章节目录简介](http://www.denglm.com/images/backtotop.png)

### 1. 参考地址

    1. http://www.cnblogs.com/softwaretesting/archive/2011/07/12/2104435.html

### 2. 打开vim并创建文件

#### 2.1 打开vim并创建名为filename的文件

    vim filename

#### 2.2 打开单个文件

    vim file

#### 2.3 同时打开多个文件

    vim file1 file2 file3 ...

#### 2.4 在vim窗口中打开一个新文件

    :open file

#### 2.5 在新窗口中打开文件

    :split file

#### 2.6 切换到下一个文件

    :bn

#### 2.7 切换到上一个文件

    :bp

#### 2.8 查看当前打开的文件列表，当前正在编辑的文件会用[]括起来。

    :args

#### 2.9 打开远程文件，比如ftp或者share folder

    :e ftp://192.168.10.76/abc.txt
    :e \\qadrive\test\1.txt

### 3. vim 插入命令
#### 3.1 在当前位置前插入

    i

#### 3.2 在当前行首插入

    I

#### 3.3 在当前位置后插入

    a

#### 3.4 在当前行尾插入

    A

#### 3.5 在当前行之后插入一行

    o

#### 3.6 在当前行之前插入一行

    O

### 4.保存和退出命令

#### 4.1 保存并退出

    :wq

#### 4.2 保存并退出

    ZZ

#### 4.3 强制退出并忽略所有更改

    :q!

#### 4.4 放弃所有修改，并打开原来文件

    :e!


### 5.查找命令

#### 5.1 查找text，按n健查找下一个，按N健查找前一个

    /text　　

#### 5.2 查找text，反向查找，按n健查找下一个，按N健查找前一个

    ?text　　

#### 5.3

    vim中有一些特殊字符在查找时需要转义　　.*[]^%/?~$

#### 5.4 忽略大小写的查找

    :set ignorecase　　

#### 5.5 不忽略大小写的查找

    :set noignorecase　　

#### 5.6 查找很长的词

    如果一个词很长，键入麻烦，可以将光标移动到该词上，按*或#键即可以该单词进行搜索，相当于/搜索。而#命令相当于?搜索。

#### 5.7 高亮搜索结果，所有结果都高亮显示，而不是只显示一个匹配

    :set hlsearch　　

#### 5.8 关闭高亮搜索显示

    :set nohlsearch　　

#### 5.9

    :nohlsearch　关闭当前的高亮显示，如果再次搜索或者按下n或N键，则会再次高亮
    :set incsearch　　逐步搜索模式，对当前键入的字符进行搜索而不必等待键入完成。
    :set wrapscan　　重新搜索，在搜索到文件头或尾时，返回继续搜索，默认开启。

### 6 拷贝和粘贴

    yy 拷贝当前行

    nyy 拷贝当前后开始的n行，比如2yy拷贝当前行及其下一行。

    p  在当前光标后粘贴,如果之前使用了yy命令来复制一行，那么就在当前行的下一行粘贴。

    shift+p 在当前行前粘贴

    :1,10 co 20 将1-10行插入到第20行之后。

    :1,$ co $ 将整个文件复制一份并添加到文件尾部。

    正常模式下按v（逐字）或V（逐行）进入可视模式，然后用jklh命令移动即可选择某些行或字符，再按y即可复制

    ddp交换当前行和其下一行

    xp交换当前字符和其后一个字符

### 7 剪切命令

    正常模式下按v（逐字）或V（逐行）进入可视模式，然后用jklh命令移动即可选择某些行或字符，再按d即可剪切

    ndd 剪切当前行之后的n行。利用p命令可以对剪切的内容进行粘贴

    :1,10d 将1-10行剪切。利用p命令可将剪切后的内容进行粘贴。

    :1, 10 m 20 将第1-10行移动到第20行之后。

### 8 删除命令

    x 删除当前字符

    3x 删除当前光标开始向后三个字符

    X 删除当前字符的前一个字符。X=dh

    dl 删除当前字符， dl=x

    dh 删除前一个字符

    dd 删除当前行

    dj 删除上一行

    dk 删除下一行

    10d 删除当前行开始的10行。

    D 删除当前字符至行尾。D=d$

    d$ 删除当前字符之后的所有字符（本行）

    kdgg 删除当前行之前所有行（不包括当前行）

    jdG（jd shift + g）   删除当前行之后所有行（不包括当前行）

    :1,10d 删除1-10行

    :11,$d 删除11行及以后所有的行

    :1,$d 删除所有行

    J(shift + j)　　删除两行之间的空行，实际上是合并两行。

### 9 撤销和重做

    u 撤销（Undo）

    U 撤销对整行的操作

    Ctrl + r 重做（Redo），即撤销的撤销。