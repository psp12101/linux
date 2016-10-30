# linux
## shell  脚本
![章节目录简介](http://www.denglm.com/images/backtotop.png)

### 1. 参考地址

    1. http://www.runoob.com/linux/linux-shell.html

### 2. 第一个脚本

#### 2.1 创建第一个脚本文件

    vi helloworld.sh

#### 2.2 编辑第一个脚本文件

    #!/bin/bash
    echo "Hello World !"

#### 2.3 运行第一个脚本文件(方法 1)

##### 2.3.1 定位到 helloworld.sh 当前路径, 使脚本 helloworld.sh 具有执行权限

    chmod +x ./helloworld.sh

##### 2.3.2 执行第一个脚本

    ./helloworld.sh

#### 2.4 运行第一个脚本文件(方法 2)

    /bin/sh helloworld.sh

### 3. 使用变量

    首个字符必须为字母（a-z，A-Z）。
    中间不能有空格，可以使用下划线（_）。
    不能使用标点符号。
    不能使用bash里的关键字（可用help命令查看保留关键字）。

#### 3.1 定义变量

    your_name="tony deng"

#### 3.2 使用变量 $your_name ${your_name},推荐给所有变量加上{}，这是个好的编程习惯

    使用一个定义过的变量，只要在变量名前面加美元符号即可,
    your_name="tony deng"
    echo $your_name
    echo "my name is ${your_name}"

    变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，比如下面这种情况
    for skill in Ada Coffe Action Java
    do
        echo "I am good at ${skill}Script"
    done

    输出结果:
    I am good at AdaScript
    I am good at CoffeScript
    I am good at ActionScript
    I am good at JavaScript

#### 3.3 只读变量 readonly ,不能修改

    myName="tony Deng"
    readonly myName
    myName="Jack Smith"
    会提示:myName: readonly variable

#### 3.4 删除变量 unset

    myName="tony Deng"
    unset myName
    echo $myName

    以上实例执行将没有任何输出。

### 4. 单引号和双引号

#### 4.1 单引号

    单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；

    your_name="tony deng"
    echo 'my name is ${your_name}'

    输出的还是 my name is ${your_name} 而不是 my name is tony deng, 如果想输出 my name is tony deng,
    需要将单引号改成双引号,像下面这样

    your_name="tony deng"
    echo "my name is ${your_name}"

    单引号字串中不能出现单引号（对单引号使用转义符后也不行）。

#### 4.2 双引号

    双引号里可以有变量
    双引号里可以出现转义字符

    your_name='tony deng'
    str="Hello, I know your are \"$your_name\"! \n"

#### 4.3 拼接字符串,获取字符串长度,提取子字符串

    name="tony"
    familyname="deng"
    echo $name $familyname
    echo ${#familyname}
    echo ${familyname:1:3}

### 5 数组

    my_array=(value0 value1 value2 value3)
    echo ${my_array[1]}

#### 5.1  取得数组元素的个数

    length=${#array_name[@]}
    # 或者
    length=${#array_name[*]}

#### 5.2 取得数组单个元素的长度

    lengthn=${#array_name[n]}

### 6 向脚本文件传递参数

    我们向脚本传递三个参数，并分别输出，其中 $0 为执行的文件名

     /bin/sh helloworld.sh 1 2 3
     echo "Shell 传递参数实例！";
     echo "执行的文件名：$0";
     echo "第一个参数为：$1";
     echo "第二个参数为：$2";
     echo "第三个参数为：$3";
     echo "参数个数为：$#";
     echo "传递的参数作为一个字符串显示：$*";

### 6.1 将所有参数在一个字符串里

    for i in "$*"; do
        echo $i
    done

### 6.2 将所有参数在一个字符数组里

    for i in "$@"; do
        echo $i
    done

### 7 Shell 基本运算符

    原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用
    表达式和运算符之间要有空格，例如 2+2 是不对的，必须写成 2 + 2
    完整的表达式要被 ` ` 包含，注意这个字符不是常用的单引号，在 Esc 键下边

    val=`expr 2 + 2`
    echo "两数之和为 : $val"

#### 7.1 + 加

    val=`expr 2 + 2`
    echo "result : $val"

#### 7.2 - 减

    val=`expr 2 - 2`
    echo "result : $val"

#### 7.3 \* 乘

    乘号(*)前边必须加反斜杠(\)才能实现乘法运算；
    val=`expr 2 \* 2`
    echo "result : $val"

#### 7.4 / 除

    val=`expr 2 / 2`
    echo "result : $val"

#### 7.5 % 取余数

    val=`expr 7 % 2`
    echo "result : $val"

#### 7.6 == 相等

    a=12
    b=13
    if [ $a == $b ]
    then
        echo "a == b"
    fi

#### 7.1 != 不相等

    if [ $a != $b ]
    then
        echo "a != b"
    fi

### 8 关系运算符

    假定变量 a 为 10，变量 b 为 20

    | 运算符 |	说明 |	举例
    | -eq	| 检测两个数是否相等，相等返回 true。	| [ $a -eq $b ] 返回 false。|
    | -ne	| 检测两个数是否相等，不相等返回 true。	| [ $a -ne $b ] 返回 true。|
    | -gt	| 检测左边的数是否大于右边的，如果是，则返回 true。	| [ $a -gt $b ] 返回 false。|
    | -lt	| 检测左边的数是否小于右边的，如果是，则返回 true。	| [ $a -lt $b ] 返回 true。|
    | -ge	| 检测左边的数是否大于等于右边的，如果是，则返回 true。	| [ $a -ge $b ] 返回 false。|
    | -le	| 检测左边的数是否小于等于右边的，如果是，则返回 true。	| [ $a -le $b ] 返回 true。|

    a=10
    b=20

    if [ $a -eq $b ]
    then
       echo "$a -eq $b : a 等于 b"
    else
       echo "$a -eq $b: a 不等于 b"
    fi
    if [ $a -ne $b ]
    then
       echo "$a -ne $b: a 不等于 b"
    else
       echo "$a -ne $b : a 等于 b"
    fi
    if [ $a -gt $b ]
    then
       echo "$a -gt $b: a 大于 b"
    else
       echo "$a -gt $b: a 不大于 b"
    fi
    if [ $a -lt $b ]
    then
       echo "$a -lt $b: a 小于 b"
    else
       echo "$a -lt $b: a 不小于 b"
    fi
    if [ $a -ge $b ]
    then
       echo "$a -ge $b: a 大于或等于 b"
    else
       echo "$a -ge $b: a 小于 b"
    fi
    if [ $a -le $b ]
    then
       echo "$a -le $b: a 小于或等于 b"
    else
       echo "$a -le $b: a 大于 b"
    fi

### 9 布尔运算符

    假定变量 a 为 10，变量 b 为 20
    !	非运算，表达式为 true 则返回 false，否则返回 true。	[ ! false ] 返回 true。
    -o	或运算，有一个表达式为 true 则返回 true。	[ $a -lt 20 -o $b -gt 100 ] 返回 true。
    -a	与运算，两个表达式都为 true 才返回 true。	[ $a -lt 20 -a $b -gt 100 ] 返回 false。

    a=10
    b=20

    if [ $a != $b ]
    then
       echo "$a != $b : a 不等于 b"
    else
       echo "$a != $b: a 等于 b"
    fi
    if [ $a -lt 100 -a $b -gt 15 ]
    then
       echo "$a -lt 100 -a $b -gt 15 : 返回 true"
    else
       echo "$a -lt 100 -a $b -gt 15 : 返回 false"
    fi
    if [ $a -lt 100 -o $b -gt 100 ]
    then
       echo "$a -lt 100 -o $b -gt 100 : 返回 true"
    else
       echo "$a -lt 100 -o $b -gt 100 : 返回 false"
    fi
    if [ $a -lt 5 -o $b -gt 100 ]
    then
       echo "$a -lt 100 -o $b -gt 100 : 返回 true"
    else
       echo "$a -lt 100 -o $b -gt 100 : 返回 false"
    fi

### 10 逻辑运算符

    &&	逻辑的 AND	[[ $a -lt 100 && $b -gt 100 ]] 返回 false
    ||	逻辑的 OR	[[ $a -lt 100 || $b -gt 100 ]] 返回 true

    a=10
    b=20

    if [[ $a -lt 100 && $b -gt 100 ]]
    then
       echo "返回 true"
    else
       echo "返回 false"
    fi

    if [[ $a -lt 100 || $b -gt 100 ]]
    then
       echo "返回 true"
    else
       echo "返回 false"
    fi

### 11 字符串运算符

    变量 a 为 "abc"，变量 b 为 "efg"
    =	检测两个字符串是否相等，相等返回 true。	[ $a = $b ] 返回 false。
    !=	检测两个字符串是否相等，不相等返回 true。	[ $a != $b ] 返回 true。
    -z	检测字符串长度是否为0，为0返回 true。	[ -z $a ] 返回 false。
    -n	检测字符串长度是否为0，不为0返回 true。	[ -n $a ] 返回 true。
    str	检测字符串是否为空，不为空返回 true。	[ $a ] 返回 true。


    假定变量 a 为 10，变量 b 为 20：
    运算符	说明	举例
    +	加法	`expr $a + $b` 结果为 30。
    -	减法	`expr $a - $b` 结果为 -10。
    *	乘法	`expr $a \* $b` 结果为  200。
    /	除法	`expr $b / $a` 结果为 2。
    %	取余	`expr $b % $a` 结果为 0。
    =	赋值	a=$b 将把变量 b 的值赋给 a。
    ==	相等。用于比较两个数字，相同则返回 true。	[ $a == $b ] 返回 false。
    !=	不相等。用于比较两个数字，不相同则返回 true。	[ $a != $b ] 返回 true。
    注意：条件表达式要放在方括号之间，并且要有空格，例如: [$a==$b] 是错误的，必须写成 [ $a == $b ]。


    算术运算符实例如下：

    a=10
    b=20

    val=`expr $a + $b`
    echo "a + b : $val"

    val=`expr $a - $b`
    echo "a - b : $val"

    val=`expr $a \* $b`
    echo "a * b : $val"

    val=`expr $b / $a`
    echo "b / a : $val"

    val=`expr $b % $a`
    echo "b % a : $val"

    if [ $a == $b ]
    then
       echo "a 等于 b"
    fi
    if [ $a != $b ]
    then
       echo "a 不等于 b"
    fi
    执行脚本，输出结果如下所示：
    a + b : 30
    a - b : -10
    a * b : 200
    b / a : 2
    b % a : 0
    a 不等于 b
    注意：
    乘号(*)前边必须加反斜杠(\)才能实现乘法运算；
    if...then...fi 是条件语句，后续将会讲解。
    在 MAC 中 shell 的 expr 语法是：$((表达式))，此处表达式中的 "*" 不需要转义符号 "\" 。
    关系运算符
    关系运算符只支持数字，不支持字符串，除非字符串的值是数字。
    下表列出了常用的关系运算符，假定变量 a 为 10，变量 b 为 20：
    运算符	说明	举例
    -eq	检测两个数是否相等，相等返回 true。	[ $a -eq $b ] 返回 false。
    -ne	检测两个数是否相等，不相等返回 true。	[ $a -ne $b ] 返回 true。
    -gt	检测左边的数是否大于右边的，如果是，则返回 true。	[ $a -gt $b ] 返回 false。
    -lt	检测左边的数是否小于右边的，如果是，则返回 true。	[ $a -lt $b ] 返回 true。
    -ge	检测左边的数是否大于等于右边的，如果是，则返回 true。	[ $a -ge $b ] 返回 false。
    -le	检测左边的数是否小于等于右边的，如果是，则返回 true。	[ $a -le $b ] 返回 true。
    实例
    关系运算符实例如下：

    a=10
    b=20

    if [ $a -eq $b ]
    then
       echo "$a -eq $b : a 等于 b"
    else
       echo "$a -eq $b: a 不等于 b"
    fi
    if [ $a -ne $b ]
    then
       echo "$a -ne $b: a 不等于 b"
    else
       echo "$a -ne $b : a 等于 b"
    fi
    if [ $a -gt $b ]
    then
       echo "$a -gt $b: a 大于 b"
    else
       echo "$a -gt $b: a 不大于 b"
    fi
    if [ $a -lt $b ]
    then
       echo "$a -lt $b: a 小于 b"
    else
       echo "$a -lt $b: a 不小于 b"
    fi
    if [ $a -ge $b ]
    then
       echo "$a -ge $b: a 大于或等于 b"
    else
       echo "$a -ge $b: a 小于 b"
    fi
    if [ $a -le $b ]
    then
       echo "$a -le $b: a 小于或等于 b"
    else
       echo "$a -le $b: a 大于 b"
    fi
    执行脚本，输出结果如下所示：
    10 -eq 20: a 不等于 b
    10 -ne 20: a 不等于 b
    10 -gt 20: a 不大于 b
    10 -lt 20: a 小于 b
    10 -ge 20: a 小于 b
    10 -le 20: a 小于或等于 b
    布尔运算符
    下表列出了常用的布尔运算符，假定变量 a 为 10，变量 b 为 20：
    运算符	说明	举例
    !	非运算，表达式为 true 则返回 false，否则返回 true。	[ ! false ] 返回 true。
    -o	或运算，有一个表达式为 true 则返回 true。	[ $a -lt 20 -o $b -gt 100 ] 返回 true。
    -a	与运算，两个表达式都为 true 才返回 true。	[ $a -lt 20 -a $b -gt 100 ] 返回 false。
    实例
    布尔运算符实例如下：
    #!/bin/bash
    # author:菜鸟教程
    # url:www.runoob.com

    a=10
    b=20

    if [ $a != $b ]
    then
       echo "$a != $b : a 不等于 b"
    else
       echo "$a != $b: a 等于 b"
    fi
    if [ $a -lt 100 -a $b -gt 15 ]
    then
       echo "$a -lt 100 -a $b -gt 15 : 返回 true"
    else
       echo "$a -lt 100 -a $b -gt 15 : 返回 false"
    fi
    if [ $a -lt 100 -o $b -gt 100 ]
    then
       echo "$a -lt 100 -o $b -gt 100 : 返回 true"
    else
       echo "$a -lt 100 -o $b -gt 100 : 返回 false"
    fi
    if [ $a -lt 5 -o $b -gt 100 ]
    then
       echo "$a -lt 100 -o $b -gt 100 : 返回 true"
    else
       echo "$a -lt 100 -o $b -gt 100 : 返回 false"
    fi
    执行脚本，输出结果如下所示：
    10 != 20 : a 不等于 b
    10 -lt 100 -a 20 -gt 15 : 返回 true
    10 -lt 100 -o 20 -gt 100 : 返回 true
    10 -lt 100 -o 20 -gt 100 : 返回 false
    逻辑运算符
    以下介绍 Shell 的逻辑运算符，假定变量 a 为 10，变量 b 为 20:
    运算符	说明	举例
    &&	逻辑的 AND	[[ $a -lt 100 && $b -gt 100 ]] 返回 false
    ||	逻辑的 OR	[[ $a -lt 100 || $b -gt 100 ]] 返回 true
    实例
    逻辑运算符实例如下：
    #!/bin/bash
    # author:菜鸟教程
    # url:www.runoob.com

    a=10
    b=20

    if [[ $a -lt 100 && $b -gt 100 ]]
    then
       echo "返回 true"
    else
       echo "返回 false"
    fi

    if [[ $a -lt 100 || $b -gt 100 ]]
    then
       echo "返回 true"
    else
       echo "返回 false"
    fi
    执行脚本，输出结果如下所示：
    返回 false
    返回 true
    字符串运算符
    下表列出了常用的字符串运算符，假定变量 a 为 "abc"，变量 b 为 "efg"：
    运算符	说明	举例
    =	检测两个字符串是否相等，相等返回 true。	[ $a = $b ] 返回 false。
    !=	检测两个字符串是否相等，不相等返回 true。	[ $a != $b ] 返回 true。
    -z	检测字符串长度是否为0，为0返回 true。	[ -z $a ] 返回 false。
    -n	检测字符串长度是否为0，不为0返回 true。	[ -n $a ] 返回 true。
    str	检测字符串是否为空，不为空返回 true。	[ $a ] 返回 true。

    实例

    a="abc"
    b="efg"

    if [ $a = $b ]
    then
       echo "$a = $b : a 等于 b"
    else
       echo "$a = $b: a 不等于 b"
    fi
    if [ $a != $b ]
    then
       echo "$a != $b : a 不等于 b"
    else
       echo "$a != $b: a 等于 b"
    fi
    if [ -z $a ]
    then
       echo "-z $a : 字符串长度为 0"
    else
       echo "-z $a : 字符串长度不为 0"
    fi
    if [ -n $a ]
    then
       echo "-n $a : 字符串长度不为 0"
    else
       echo "-n $a : 字符串长度为 0"
    fi
    if [ $a ]
    then
       echo "$a : 字符串不为空"
    else
       echo "$a : 字符串为空"
    fi

### 12 文件测试运算符

    -b file	检测文件是否是块设备文件，如果是，则返回 true。	[ -b $file ] 返回 false。
    -c file	检测文件是否是字符设备文件，如果是，则返回 true。	[ -c $file ] 返回 false。
    -d file	检测文件是否是目录，如果是，则返回 true。	[ -d $file ] 返回 false。
    -f file	检测文件是否是普通文件（既不是目录，也不是设备文件），如果是，则返回 true。	[ -f $file ] 返回 true。
    -g file	检测文件是否设置了 SGID 位，如果是，则返回 true。	[ -g $file ] 返回 false。
    -k file	检测文件是否设置了粘着位(Sticky Bit)，如果是，则返回 true。	[ -k $file ] 返回 false。
    -p file	检测文件是否是有名管道，如果是，则返回 true。	[ -p $file ] 返回 false。
    -u file	检测文件是否设置了 SUID 位，如果是，则返回 true。	[ -u $file ] 返回 false。
    -r file	检测文件是否可读，如果是，则返回 true。	[ -r $file ] 返回 true。
    -w file	检测文件是否可写，如果是，则返回 true。	[ -w $file ] 返回 true。
    -x file	检测文件是否可执行，如果是，则返回 true。	[ -x $file ] 返回 true。
    -s file	检测文件是否为空（文件大小是否大于0），不为空返回 true。	[ -s $file ] 返回 true。
    -e file	检测文件（包括目录）是否存在，如果是，则返回 true。	[ -e $file ] 返回 true。

    file="/var/www/runoob/test.sh"
    if [ -r $file ]
    then
       echo "文件可读"
    else
       echo "文件不可读"
    fi
    if [ -w $file ]
    then
       echo "文件可写"
    else
       echo "文件不可写"
    fi
    if [ -x $file ]
    then
       echo "文件可执行"
    else
       echo "文件不可执行"
    fi
    if [ -f $file ]
    then
       echo "文件为普通文件"
    else
       echo "文件为特殊文件"
    fi
    if [ -d $file ]
    then
       echo "文件是个目录"
    else
       echo "文件不是个目录"
    fi
    if [ -s $file ]
    then
       echo "文件不为空"
    else
       echo "文件为空"
    fi
    if [ -e $file ]
    then
       echo "文件存在"
    else
       echo "文件不存在"
    fi

### 13 echo 命令

#### 13.1 显示普通字符串

    echo "这个测试了"

#### 13.2 显示转义字符

    echo "\"这个测试了\""

#### 13.3 显示变量

    name=12;
    echo ${name}

#### 13.4 显示换行

    name=12;
    echo ${name} "haha\n"
    echo ${name} "tony"

#### 13.5 不换行

    echo "我就 \c"
    echo "哈哈了"

#### 13.6 显示结果定向至文件

    echo "显示结果定向至文件" > text.sh

### 14 printf 命令

    $ printf "打印结果\n"

    printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg
    printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234
    printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543
    printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876

    输出结果:
    姓名     性别   体重kg
    郭靖     男      66.12
    杨过     男      48.65
    郭芙     女      47.99

### 15 Shell test 命令

    Shell中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。

#### 15.1 数值测试

    -eq	等于则为真
    -ne	不等于则为真
    -gt	大于则为真
    -ge	大于等于则为真
    -lt	小于则为真
    -le	小于等于则为真

    a=12
    b=13
    if test $a -eq $b
    then
        echo 'a 等于 b'
    else
        echo 'a 不等于 b'
    fi

#### 15.2 字符串测试

    =	等于则为真
    !=	不相等则为真
    -z 字符串	字符串的长度为零则为真
    -n 字符串	字符串的长度不为零则为真

    str1="runoob"
    str2="runoob"
    if test str1=str2
    then
        echo '两个字符串相等!'
    else
        echo '两个字符串不相等!'
    fi

#### 15.3 文件测试

    -e 文件名	如果文件存在则为真
    -r 文件名	如果文件存在且可读则为真
    -w 文件名	如果文件存在且可写则为真
    -x 文件名	如果文件存在且可执行则为真
    -s 文件名	如果文件存在且至少有一个字符则为真
    -d 文件名	如果文件存在且为目录则为真
    -f 文件名	如果文件存在且为普通文件则为真
    -c 文件名	如果文件存在且为字符型特殊文件则为真
    -b 文件名	如果文件存在且为块特殊文件则为真

    判断文件是否存在
    if test -e ./bash
    then
        echo '文件已存在!'
    else
        echo '文件不存在!'
    fi

    判断文件是否可写
    if test -w text.sh
    then
        echo '文件可写!'
    else
        echo '文件不可写!'
    fi

### 16 Shell 流程控制

#### 16.1 if 语句语法格式

    if condition
    then
        command1
        command2
        ...
        commandN
    fi

#### 16.2 if else 语法格式

    if condition
    then
        command1
        command2
        ...
        commandN
    else
        command
    fi

#### 16.3 if else-if else 语法格式

    if condition1
    then
        command1
    elif condition2
    then
        command2
    else
        commandN
    fi

#### 16.4 for 循环

    for var in item1 item2 ... itemN
    do
        command1
        command2
        ...
        commandN
    done

    for i in 1 2 3 4 5 6
    do
        echo $i
    done

#### 16.5 case  加用户输入

    echo '输入 1 到 4 之间的数字:'
    echo '你输入的数字为:'
    read aNum
    case $aNum in
        1)  echo '你选择了 1'
        ;;
        2)  echo '你选择了 2'
        ;;
        3)  echo '你选择了 3'
        ;;
        4)  echo '你选择了 4'
        ;;
        *)  echo '你没有输入 1 到 4 之间的数字'
        ;;
    esac

    结果显示:
    输入 1 到 4 之间的数字:
    你输入的数字为:
    3
    你选择了 3

### 17 Shell 函数

#### 17.1 第一个函数

    myfunc(){
    echo '我的第一个shell 函数'
    }
    echo '开始运行第一个函数'
    myfunc
    echo '运行结束'

#### 17.2 带有用户输入和return返回的函数

    myadd(){
        echo '加法函数'
        echo '输入第一个加数：\n'
        read num1
        echo '输入第一个加数：\n'
        read num2
        echo '两个加法的和为：\n'
        echo '两个数之和为：\n'
        echo `expr $num1 + $num2`
        return $(($num1 + $num2))
    }
    myadd
    echo "输入的两个数字之和为 $? !"

    输入10 和 20
    结果为:
    30
    输入的两个数字之和为 30 !

#### 17.3 带参数函数

    funWithParam(){
        echo "第一个参数为 $1 !"
        echo "第二个参数为 $2 !"
        echo "第十个参数为 $10 !"
        echo "第十个参数为 ${10} !"
        echo "第十一个参数为 ${11} !"
        echo "参数总数有 $# 个!"
        echo "作为一个字符串输出所有参数 $* !"
    }
    funWithParam 1 2 3 4 5 6 7 8 9 34 73

    结果:
    第一个参数为 1 !
    第二个参数为 2 !
    第十个参数为 10 !
    第十个参数为 34 !
    第十一个参数为 73 !
    参数总数有 11 个!
    作为一个字符串输出所有参数 1 2 3 4 5 6 7 8 9 34 73 !

    $10 不能获取第十个参数，获取第十个参数需要${10}。当n>=10时，需要使用${n}来获取参数。
    $#	传递到脚本的参数个数
    $*	以一个单字符串显示所有向脚本传递的参数
    $$	脚本运行的当前进程ID号
    $!	后台运行的最后一个进程的ID号
    $@	与$*相同，但是使用时加引号，并在引号中返回每个参数。
    $-	显示Shell使用的当前选项，与set命令功能相同。
    $?	显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。

### 18 Shell 函数

#### 18.1 输出重定向

    echo "输入的两个数字之和为 $? !" >text.sh

#### 18.2 输出重定向,追加到文件末尾

    echo "输入的两个数字之和为 $? !" >>text.sh

### 19 Shell 文件包含

#### 19.1 text.sh 代码如下:

    str1=10
    str2=20

#### 19.2 helloworld.sh 代码如下:

    source ./text.sh
    echo "从外部引入文件 text.sh"
    echo $str1 "\n"$str2

    注: 被包含的文件 test1.sh 不需要可执行权限


