# BAT 
## 批处理的常见命令

1、REM 和 ::
2、ECHO 和 @
3、PAUSE
4、ERRORLEVEL
5、TITLE
6、COLOR
7、mode 配置系统设备
8、GOTO 和 :
9、FIND
10、START
11、assoc 和 ftype
12、pushd 和 popd
13、CALL
14、shift
15、IF
16、setlocal 与 变量延迟
17、ATTRIB 显示或更改文件属性

1、REM 和 ::

REM为注释命令，一般用来给程序加上注解，该命令后的内容不被执行，但能回显。
其次, :: 也可以起到rem 的注释作用, 而且更简洁有效; 但有两点需要注意：
第一, 任何以冒号:开头的字符行, 在批处理中都被视作标号, 而直接忽略其后的所有内容。
有效标号：冒号后紧跟一个以字母数字开头的字符串，goto语句可以识别。
无效标号：冒号后紧跟一个非字母数字的一个特殊符号，goto无法识别的标号，可以起到注释作用，
所以 :: 常被用作注释符号，其实 :+ 也可起注释作用。

第 二, 与rem 不同的是, ::后的字符行在执行时不会回显, 无论是否用echo on打开命令行回显状态, 
因为命令解释器不认为他是一个有效的命令行, 就此点来看, rem 在某些场合下将比 :: 更为适用; 另外, rem 可以用于 config.sys 文件中。

2、ECHO 和 @

@字符放在命令前将关闭该命令回显，无论此时echo是否为打开状态。

echo命令的作用列举如下：
（1）打开回显或关闭回显功能
格式:echo [{ on|off }]
如果想关闭“ECHO OFF”命令行自身的显示，则需要在该命令行前加上“@”。
（2）显示当前ECHO设置状态
格式:echo
（3）输出提示信息 
格式：ECHO 信息内容
上述是ECHO命令常见的三种用法，也是大家熟悉和会用的，但作为DOS命令淘金者你还应该知道下面的技巧：
（4）关闭DOS命令提示符 
在DOS提示符状态下键入ECHO OFF，能够关闭DOS提示符的显示使屏幕只留下光标，直至键入ECHO ON，提示符才会重新出现。
（5）输出空行，即相当于输入一个回车 
格式：ECHO．
值得注意的是命令行中的“．”要紧跟在ECHO后面中间不能有空格，否则“．”将被当作提示信息输出到屏幕。另外“．”可以用，：；”／[\]＋等任一符号替代。
命令ECHO．输出的回车，经DOS管道转向可以作为其它命令的输入，比如echo.|time即相当于在TIME命令执行后给出一个回车。所以执行时系统会在显示当前时间后，自动返回到DOS提示符状态
（6）答复命令中的提问 
格式：ECHO 答复语|命令文件名
上述格式可以用于简化一些需要人机对话的命令（如：CHKDSK／F；FORMAT Drive:；del *.*）的操作，它是通过DOS管道命令把ECHO命令输出的预置答复语作为人机对话命令的输入。下面的例子就相当于在调用的命令出现人机对话时输入“Y”回车：
C:>ECHO Y|CHKDSK/F
C:>ECHO Y|DEL A :*.*
（7）建立新文件或增加文件内容 
格式：ECHO 文件内容>文件名
ECHO 文件内容>>文件名

3、PAUSE

PAUSE，玩游戏的人都知道，暂停的意思
在这里就是停止系统命令的执行并显示下面的内容。
例：

PAUSE

运行显示：
请按任意键继续. . .
要显示其他提示语，可以这样用：
Echo 其他提示语 & pause > nul

4、errorlevel

程序返回码
echo %errorlevel%
每个命令运行结束，可以用这个命令行格式查看返回码
用于判断刚才的命令是否执行成功
默认值为0，一般命令执行出错会设 errorlevel 为1

5、title

设置cmd窗口的标题
title 新标题 #可以看到cmd窗口的标题栏变了

6、COLOR

设置默认的控制台前景和背景颜色。
COLOR [attr]
attr 指定控制台输出的颜色属性
颜色属性由两个十六进制数字指定 -- 第一个为背景，第二个则为
前景。每个数字可以为以下任何值之一:
0 = 黑色 8 = 灰色
1 = 蓝色 9 = 淡蓝色
2 = 绿色 A = 淡绿色
3 = 湖蓝色 B = 淡浅绿色
4 = 红色 C = 淡红色
5 = 紫色 D = 淡紫色
6 = 黄色 E = 淡黄色
7 = 白色 F = 亮白色
如果没有给定任何参数，该命令会将颜色还原到 CMD.EXE 启动时
的颜色。这个值来自当前控制台窗口、/T 开关或
DefaultColor 注册表值。
如果用相同的前景和背景颜色来执行 COLOR 命令，COLOR 命令
会将 ERRORLEVEL 设置为 1。
例如: "COLOR fc" 在亮白色上产生亮红色

7、mode 配置系统设备

配置系统设备。
串行口:　　　 MODE COMm[:] [BAUD=b] [PARITY=p] [DATA=d] [STOP=s]
[to=on|off] [xon=on|off] [odsr=on|off]
[octs=on|off] [dtr=on|off|hs]
[rts=on|off|hs|tg] [idsr=on|off]
设备状态: MODE [device] [/STATUS]
打印重定向:　　 MODE LPTn[:]=COMm[:]
选定代码页:　　 MODE CON[:] CP SELECT=yyy
代码页状态:　　 MODE CON[:] CP [/STATUS]
显示模式:　　 MODE CON[:] [COLS=c] [LINES=n]
击键率:　 MODE CON[:] [RATE=r DELAY=d]
例：
mode con cols=113 lines=15 & color 9f
此命令设置DOS窗口大小：15行，113列

8、GOTO 和 :

GOTO会点编程的朋友就会知道这是跳转的意思。
在批处理中允许以“:XXX”来构建一个标号，然后用GOTO XXX跳转到标号:XXX处，然后执行标号后的命令。
例：

if {%1}=={} goto noparms
if "%2"=="" goto noparms

标签的名字可以随便起，但是最好是有意义的字符串啦，前加个冒号用来表示这个字符串是标签，goto命令就是根据这个冒号（:）来寻找下一步跳到到那里。最好有一些说明这样你别人看起来才会理解你的意图啊。

例：

```
@echo off
:start
set /a var+=1
echo %var%
if %var% leq 3 GOTO start
pause
```
运行显示：

1
2
3
4

9、find

在文件中搜索字符串。
FIND [/V] [/C] [/N] [/I] [/OFF[LINE]] "string" [[drive:][path]filename[ ...]]
/V 显示所有未包含指定字符串的行。
/C 仅显示包含字符串的行数。
/N 显示行号。
/I 搜索字符串时忽略大小写。
/OFF[LINE] 不要跳过具有脱机属性集的文件。
"string" 指定要搜索的文字串，
[drive:][path]filename
指定要搜索的文件。
如果没有指定路径，FIND 将搜索键入的或者由另一命令产生的文字。
Find常和type命令结合使用

Type [drive:][path]filename | find "string" [>tmpfile] #挑选包含string的行
Type [drive:][path]filename | find /v "string" #剔除文件中包含string的行
Type [drive:][path]filename | find /c #显示文件行数

以上用法将去除find命令自带的提示语（文件名提示）

例：
```
@echo off
echo 111 >test.txt
echo 222 >>test.txt
find "111" test.txt
del test.txt
pause
```
运行显示如下：

---------- TEST.TXT
111

请按任意键继续. . .

例：
```
@echo off
echo 111 >test.txt
echo 222 >>test.txt
type test.txt|find "111"
del test.txt
pause
```
运行显示如下：

111

请按任意键继续. . .

10、start 命令

批处理中调用外部程序的命令（该外部程序在新窗口中运行，批处理程序继续往下执行，不理会外部程序的运行状况），如果直接运行外部程序则必须等外部程序完成后才继续执行剩下的指令

例：start explorer d:\

调用图形界面打开D盘

11、assoc 和 ftype

文件关联
assoc 设置'文件扩展名'关联，关联到'文件类型'
ftype 设置'文件类型'关联，关联到'执行程序和参数'
当你双击一个.txt文件时，windows并不是根据.txt直接判断用 notepad.exe 打开
而是先判断.txt属于 txtfile '文件类型'
再调用 txtfile 关联的命令行 txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1
可以在"文件夹选项"→"文件类型"里修改这2种关联
assoc #显示所有'文件扩展名'关联
assoc .txt #显示.txt代表的'文件类型'，结果显示 .txt=txtfile
assoc .doc #显示.doc代表的'文件类型'，结果显示 .doc=Word.Document.8
assoc .exe #显示.exe代表的'文件类型'，结果显示 .exe=exefile
ftype #显示所有'文件类型'关联
ftype exefile #显示exefile类型关联的命令行，结果显示 exefile="%1" %* 
assoc .txt=Word.Document.8
设置.txt为word类型的文档，可以看到.txt文件的图标都变了
assoc .txt=txtfile

恢复.txt的正确关联

ftype exefile="%1" %*

恢复 exefile 的正确关联
如果该关联已经被破坏，可以运行 command.com ，再输入这条命令

12、pushd 和 popd

切换当前目录

```
@echo off
c: & cd\ & md mp3 #在 C:\ 建立 mp3 文件夹
md d:\mp4 #在 D:\ 建立 mp4 文件夹
cd /d d:\mp4 #更改当前目录为 d:\mp4
pushd c:\mp3 #保存当前目录，并切换当前目录为 c:\mp3
popd #恢复当前目录为刚才保存的 d:\mp4
```
一般用处不大，在当前目录名不确定时，会有点帮助。（dos编程中很有用）

13、CALL

CALL命令可以在批处理执行过程中调用另一个批处理，当另一个批处理执行完后，再继续执行原来的批处理
CALL command
调用一条批处理命令，和直接执行命令效果一样，特殊情况下很有用，比如变量的多级嵌套，见教程后面。在批处理编程中，可以根据一定条件生成命令字符串，用call可以执行该字符串，见例子。
CALL [drive:][path]filename [batch-parameters]
调用的其它批处理程序。filename 参数必须具有 .bat 或 .cmd 扩展名。
CALL :label arguments
调用本文件内命令段，相当于子程序。被调用的命令段以标签:label开头
以命令goto :eof结尾。
另外，批脚本文本参数参照(%0、%1、等等)已如下改变:
批脚本里的 %* 指出所有的参数(如 %1 %2 %3 %4 %5 ...)
批参数(%n)的替代已被增强。您可以使用以下语法:（看不明白的直接运行后面的例子）
%~1 - 删除引号(")，扩充 %1
%~f1 - 将 %1 扩充到一个完全合格的路径名
%~d1 - 仅将 %1 扩充到一个驱动器号
%~p1 - 仅将 %1 扩充到一个路径
%~n1 - 仅将 %1 扩充到一个文件名
%~x1 - 仅将 %1 扩充到一个文件扩展名
%~s1 - 扩充的路径指含有短名
%~a1 - 将 %1 扩充到文件属性
%~t1 - 将 %1 扩充到文件的日期/时间
%~z1 - 将 %1 扩充到文件的大小
%~PATH:1−查找列在PATH环境变量的目录，并将PATH:1 - 在列在 PATH 环境变量中的目录里查找 %1，
并扩展到找到的第一个文件的驱动器号和路径。
%~ftza1 - 将 %1 扩展到类似 DIR 的输出行。
在上面的例子中，%1 和 PATH 可以被其他有效数值替换。
%~ 语法被一个有效参数号码终止。%~ 修定符不能跟 %*使用
注意：参数扩充时不理会参数所代表的文件是否真实存在，均以当前目录进行扩展
要理解上面的知识，下面的例子很关键。

例：
```
@echo off
Echo 产生一个临时文件 > tmp.txt
Rem 下行先保存当前目录，再将c:\windows设为当前目录
pushd c:\windows
Call :sub tmp.txt
Rem 下行恢复前次的当前目录
Popd
Call :sub tmp.txt
pause
Del tmp.txt
exit
:sub
Echo 删除引号： %~1
Echo 扩充到路径： %~f1
Echo 扩充到一个驱动器号： %~d1
Echo 扩充到一个路径： %~p1 
Echo 扩充到一个文件名： %~n1
Echo 扩充到一个文件扩展名： %~x1
Echo 扩充的路径指含有短名： %~s1 
Echo 扩充到文件属性： %~a1 
Echo 扩充到文件的日期/时间： %~t1 
Echo 扩充到文件的大小： %~z1 
Echo 扩展到驱动器号和路径：%~dp1
Echo 扩展到文件名和扩展名：%~nx1
Echo 扩展到类似 DIR 的输出行：%~ftza1
Echo.
Goto :eof
```
例：

set aa=123456
set cmdstr=echo %aa%
call %cmdstr%
pause

本例中如果不用call，而直接运行%cmdstr%，将显示结果%aa%，而不是123456

14、shift

更改批处理文件中可替换参数的位置。
SHIFT [/n]
如果命令扩展名被启用，SHIFT 命令支持/n 命令行开关；该命令行开关告诉
命令从第 n 个参数开始移位；n 介于零和八之间。例如:
SHIFT /2
会将 %3 移位到 %2，将 %4 移位到 %3，等等；并且不影响 %0 和 %1。

15、IF

IF 条件判断语句，语法格式如下：
IF [NOT] ERRORLEVEL number command
IF [NOT] string1==string2 command
IF [NOT] EXIST filename command
下面逐一介绍，更详细的分析请看后面章节。

(1) IF [NOT] ERRORLEVEL number command
IF ERRORLEVEL这个句子必须放在某一个命令的后面，执行命令后由IF ERRORLEVEL 来判断命令的返回值。
Number的数字取值范围0~255，判断时值的排列顺序应该由大到小。返回的值大于等于指定的值时，条件成立
例：

```
@echo off
dir c:
rem退出代码为>=1就跳至标题1处执行，>=0就跳至标题0处执行
IF ERRORLEVEL 1 goto 1
IF ERRORLEVEL 0 goto 0
Rem 上面的两行不可交换位置，否则失败了也显示成功。
:0
echo 命令执行成功！
Rem 程序执行完毕跳至标题exit处退出
goto exit
:1
echo 命令执行失败！
Rem 程序执行完毕跳至标题exit处退出
goto exit
:exit
pause
```
运行显示：命令执行成功！

(2) IF [NOT] string1==string2 command
string1和string2都为字符的数据，英文内字符的大小写将看作不同，这个条件中的等于号必须是两个（绝对相等的意思）
条件相等后即执行后面的command
检测当前变量的值做出判断，为了防止字符串中含有空格，可用以下格式
if [NOT] {string1}=={string2} command
if [NOT] [string1]==[string2] command
if [NOT] "string1"=="string2" command
这种写法实际上将括号或引号当成字符串的一部分了，只要等号左右两边一致就行了，比如下面的写法就不行：
if {string1}==[string2] command

(3) IF [NOT] EXIST filename command
EXIST filename为文件或目录存在的意思
echo off
IF EXIST autoexec.bat echo 文件存在！
IF not EXIST autoexec.bat echo 文件不存在！
这个批处理大家可以放在C盘和D盘分别执行，看看效果

16、setlocal 与 变量延迟

本条内容引用[英雄出品]的批处理教程：
要想进阶，变量延迟是必过的一关！所以这一部分希望你能认真看。
为了更好的说明问题，我们先引入一个例子。

例1:
```
@echo off
set a=4
set a=5 & echo %a%
pause
```
结果：4

解说：为什么是4而不是5呢？在echo之前明明已经把变量a的值改成5了？
让我们先了解一下批处理运行命令的机制：
批 处理读取命令时是按行读取的（另外例如for命令等，其后用一对圆括号闭合的所有语句也当作一行），在处理之前要完成必要的预处理工作，这其中就包括对该 行命令中的变量赋值。我们现在分析一下例1，批处理在运行到这句“set a=5 & echo %a%”之前，先把这一句整句读取并做了预处理——对变量a赋了值，那么%a%当然就是4了！（没有为什么，批处理就是这样做的。）
而为了能够感知环境变量的动态变化，批处理设计了变量延迟。简单来说，在读取了一条完整的语句之后，不立即对该行的变量赋值，而会在某个单条语句执行之前再进行赋值，也就是说“延迟”了对变量的赋值。
那么如何开启变量延迟呢？变量延迟又需要注意什么呢？举个例子说明一下：

例2:
```
@echo off
setlocal enabledelayedexpansion
set a=4
set a=5 & echo !a!
pause
```
结果：5

解说：启动了变量延迟，得到了正确答案。变量延迟的启动语句是“setlocal enabledelayedexpansion”，并且变量要用一对叹号“!!”括起来（注意要用英文的叹号），否则就没有变量延迟的效果。
分析一下例2，首先“setlocal enabledelayedexpansion”开启变量延迟，然后“set a=4”先给变量a赋值为
4，“set a=5 & echo !a!”这句是给变量a赋值为5并输出（由于启动了变量延迟，所以批处理能够感知到动态变化，即不是先给该行变量赋值，而是在运行过程中给变量赋值，因此此时a的值就是5了）。
再举一个例子巩固一下。

例3:
```
@echo off
setlocal enabledelayedexpansion
for /l %%i in (1,1,5) do (
set a=%%i
echo !a!
)
pause
```
结果：

1
2
3
4
5

解说：本例开启了变量延迟并用“!!”将变量扩起来，因此得到我们预期的结果。如果不用变量延迟会出现什
么结果呢？结果是这样的：
ECHO 处于关闭状态。
ECHO 处于关闭状态。
ECHO 处于关闭状态。
ECHO 处于关闭状态。
ECHO 处于关闭状态。
即没有感知到for语句中的动态变化。
提示：在没有开启变量延迟的情况下，某条命令行中的变量改变，必须到下一条命令才能体现。这一点也可以加以利用，看例子。
例：交换两个变量的值，且不用中间变量
``` 
@echo off
::目的：交换两个变量的值，但是不使用临时变量
::Code by JM 2007-1-24 [email=CMD@XP]CMD@XP[/email]
::出处：http://www.cn-dos.net/forum/viewthread.php?tid=27078
set var1=abc
set var2=123
echo 交换前： var1=%var1% var2=%var2%
set var1=%var2%& set var2=%var1%
echo 交换后： var1=%var1% var2=%var2%
pause
```
17、ATTRIB 显示或更改文件属性

ATTRIB [+R|-R] [+A|-A] [+S|-S] [+H|-H] [[drive:] [path] filename] [/S [/D]]
+ 设置属性。
- 清除属性。
R 只读文件属性。
A 存档文件属性。
S 系统文件属性。
H 隐藏文件属性。
[drive:][path][filename]
指定要处理的文件属性。
/S 处理当前文件夹及其子文件夹中的匹配文件。
/D 也处理文件夹。

例：
```
md autorun
attrib +a +s +h autorun
```
上面的命令将建立文件夹autorun，然后将其设为存档、系统、隐藏属性


