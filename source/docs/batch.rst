.. _batch:

=====================================
批处理助记
=====================================

这部分笔记记录了平时工作中遇到的一些关于批处理文件编写的知识细节。

.. toctree::
   :hidden:
   :maxdepth: 1

   批处理总结教程 <batchtutorial>

获取文件所在路径
=====================================

在开发时，经常需要使用批处理运行一些程序，java程序犹其是这样，往往需要运行时根路径。Hardcode一个路径总是令自己觉得不自在，例如一个java程序从一台机copy到另外一台机，盘符往往发生变化，先修改一下bat里的路径再运行显然很麻烦。 

在批处理开头加入 ``cd /d %~dp0`` 一行代码就真真实实地做到“编写一次，到处运行”。%0是批处理文件本身的路径，
%~dp进行扩展，d向前扩展到驱动器，p往后扩展到路径。例如，你的bat文件在 `e:/mybat/test.bat` ,
则%0就是 `e:/mybat/test.bat` ,%~dp0是 `e:/mybat/` 。 
另外，%i提取第i个命令选项，例如%1提取第1个option，i可以取值从1到9 
        
	| %~0： 取文件名（名+扩展名） 
	| %~f0：取全路径 
	| %~d0：取驱动器名 
	| %~p0：只取路径（不包驱动器） 
	| %~n0：只取文件名 
	| %~x0：只取文件扩展名 
	| %~s0：取缩写全路径名 
	| %~a0：取文件属性 
	| %~t0：取文件创建时间 
	| %~z0：取文件大小 

.. note:: 
	
	- 以上选项可以组合起来使用
	- %1就是表示批处理的第一个参数
	- %~1表示删除参数外面的引号

比如有个批处理文件 ``test.bat`` , 在cmd中输入命令 ``test.bat "test"`` , %1表示的是 ``"test"`` 。%~1表示的是 ``test`` ，没有了双引号

参考链接： https://www.cnblogs.com/yang-hao/p/6002715.html

For循环命令
===================================

基本格式： FOR 参数 %%变量名 IN (相关文件或命令) DO 执行的命令

	- 参数: FOR有4个参数 /d /l /r /f 他们的作用我在下面用例子解释
	- %%变量名: 这个变量名可以是小写a-z或者大写A-Z,他们区分大小写,FOR会把每个读取到的值给他;
	- IN: 命令的格式,照写就是了;
	- (相关文件或命令): FOR要把什么东西读取然后赋值给变量,看下面的例子
	- do: 命令的格式,照写就是了!
	- 执行的命令: 对每个变量的值要执行什么操作就写在这.

可以在CMD输入 ``for /?`` 看系统提供的帮助，对照一下:

FOR %%variable IN (set) DO command [command-parameters]

	- %%variable		指定一个单一字母可替换的参数。
	- (set)		指定一个或一组文件。可以使用通配符。
	- command		指定对每个文件执行的命令。
	- command-parameters	为特定命令指定参数或命令行开关。
	  
无参数
---------------------------

格式：	FOR %variable IN (set) DO command [command-parameters]

	- %variable 指定一个单一字母可替换的参数。
	- (set)      指定一个或一组文件。可以使用通配符。
	- command    指定对每个文件执行的命令。
	- command-parameters	为特定命令指定参数或命令行开关。

示例： ::

	for %%i in (t*.*) do echo %%i --显示当前目录下与t*.*相匹配的文件(只显示文件名，不显示路径) 
	for %%i in (d:/mydocuments/*.doc) do @echo %%i --显示d:/mydocuments/目录下与*.doc相匹配的文件

D参数
--------------------------

格式：	FOR /D %variable IN (set) DO command [command-parameters]

这个参数主要用于目录搜索,不会搜索文件,/D 参数只能显示当前目录下的目录名字。(特别说明：只会搜索指定目录下的目录，不会搜索再下一级的目录。)

示例： ::

	for /d %%i in (c:/*) do echo %%i --显示c盘根目录下的所有目录
	for /d %%i in (???) do echo %%i --显示当前目录下名字只有1-3个字母的目录

L参数
---------------------------

格式：	FOR /L %variable IN (start,step,end) DO command [command-parameters]

该集表示以增量形式从开始到结束的一个数字序列。可以使用负的 Step

示例： ::

	for /l %%i in (1,1,5) do @echo %%i --输出1 2 3 4 5
	for /l %%i in (1,2,10) do @echo %%i --输出1,3，5,7，9 
	for /l %%i in (100,-20,1) do @echo %%i --输出100,80,60,40,20
	for /l %%i in (1,1,5) do start cmd --打开5个CMD窗口
	for /l %%i in (1,1,5) do md %%i --建立从1~5共5个文件夹
	for /l %%i in (1,1,5) do rd /q %%i --删除从1~5共5个文件夹
	
R参数
------------------------------

格式：	FOR /R [[drive:]path] %variable IN (set) DO command [command-parameters]

此命令会搜索指定路径及所有子目录中与set相符合的所有文件，注意是指定路径及所有子目录。

	1.	set中的文件名如果含有通配符(？或*)，则列举/R参数指定的目录及其下面的所用子目录中与set相符合的所有文件，无相符文件的目录则不列举。
	2.	如果set中为具体文件名，不含通配符，则枚举该目录树（即列举该目录及其下面的所有子目录）(并在后面加上具体的文件名)，而不管set中的指定文件是否存在。

示例： ::

	for /r c:/ %%i in (boot.ini) do echo %%i --枚举了c盘所有目录
	for /r d:/backup %%i in (1) do echo %%i --枚举d/backup目录
	for /r c:/ %%i in (boot.ini) do if exist %%i echo %%i --很好的搜索命令，列举boot.ini存在的目录
	for /r c:/ %%i in (*.exe) do echo %%i --把C盘根目录,和每个目录的子目录下面全部的EXE文件都列出来了!!!!

F参数
---------------------------------

这个参数是最难的，参数又多，先简单的解释一下：for命令带这个参数可以分析文件内容，字符串内容或某一命令输出的结果，并通过设置option得我们想要的结果。

以下是某高手的解释，感觉有点太专业了，自认为不太容易理解，也列一下：

	迭代及文件解析--使用文件解析来处理命令输出、字符串及文件内容。使用迭代变量定义要检查的内容或字符串，
	并使用各种options选项进一步修改解析方式。使用options令牌选项指定哪些令牌应该作为迭代变量传递。
	请注意：在没有使用令牌选项时，/F 将只检查第一个令牌。文件解析过程包括读取输出、字符串或文件内容，
	将其分成独立的文本行以及再将每行解析成零个或更多个令牌。然后通过设置为令牌的迭代变量值，
	调用 for 循环。	默认情况下，/F 传递每个文件每一行的第一个空白分隔符号。跳过空行。

格式：

	| FOR /F ["options"] %variable IN (file-set) DO command [command-parameters]
	| FOR /F ["options"] %variable IN ("string") DO command [command-parameters]
	| FOR /F ["options"] %variable IN ('command') DO command [command-parameters]

1. OPTION关键字详解:

	| eol=c：指一个行注释字符的结尾(就一个)。例如：eol=; --忽略以分号打头的那些行;
	| skip=n：指在文件开始时忽略的行数。例如：skip=2 --忽略2行；
	| delims=xxx：指分隔符集。这个替换了空格和跳格键的默认分隔符集。例如：[delims=, ] --指定用逗号，空格对字符串进行分隔。
	| tokens=x,y,m-n：指每行的哪一个符号被传递到每个迭代的 for 本身。这会导致额外变量名称的分配。m-n格式为一个范围。通过 nth 符号指定 mth。如果符号字符串中的最后一个字符是星号，那么额外的变量将在最后一个符号解析之后分配并接受行的保留文本。例如：tokens=2,3* --将每行中的第二个和第三个符号传递给 for 程序体；tokens=2,3* ... i% --将会把取到的第二个字符串赋给i%,第三个赋给j%,剩下的赋给k%。

#. file-set

	为一个或多个文件名。继续到 file-set 中的下一个文件之前，每份文件都已被打开、读取并经过处理。
	处理包括读取文件，将其分成一行行的文字，然后将每行解析成零或更多的符号。然后用已找到的符号
	字符串变量值调用 For 循环。以默认方式，/F 通过每个文件的每一行中分开的第一个空白符号。
	跳过空白行。您可通过指定可选 "options"参数替代默认解析操作。这个带引号的字符串包括一个或
	多个指定不同解析选项的关键字。

#. %i

	专门在 for 语句中得到说明，%j 和 %k 是通过tokens= 选项专门得到说明的。您可以通过 tokens= 一行指定最多 26 个符号，
	只要不试图说明一个高于字母 'z' 或'Z' 的变量。请记住，FOR 变量是单一字母、分大小写和全局的；而且，同时不能有 52 个以上都在使用中。

#. 补充说明

	| 一般在tokens后只指定第一个参数，如%%i或%%a，在后面使用第二个及两个以上的参数，自动按顺序往下排即可。
	  如前面指定的是%%a，后面则用%%b代表第二个结果，%%c代表第 三个结果。。。测试了一下tokens后指定多个变量名，
	  没有测试成功，应该是不可以的。所以token后只能跟要使用的第一个变量名
	| 如果使用的变量名超过了%z或%Z，就无法使用了，曾经以为会循环过来：如%%z后可以使用%%a或%%A，但经测试，这是不可以的。
	| 如：for /f "tokens=1,2,3* delims=-, " %%y in ("aa bb,cc-dd ee") do echo %%y %%z %%A %%a --只会输出前两个字符串，后面的两个变量是无效的。

示例1： ::

	FOR /F "eol=; tokens=2,3* delims=, " %i in (myfile.txt) do @echo %i %j %k --
		分析 myfile.txt 中的每一行，
		eol=; --忽略以分号打头的那些行;
		tokens=2,3* --将每行中的第二个和第三个符号传递给 for 程序体；
		delims= , --用逗号和/或空格定界符号。
		%i --这个 for 程序体的语句引用 %i 来取得取得的首个字符串(本例中为第二个符号)，引用 %j 来取得第二个字符串(本例中为第三个符号)引用 %k来取得第三个符号后的所有剩余符号。

示例2： ::

	1. 分析文件的例子: for /f "eol=; tokens=1,2* delims=,- " %%i in (d:/test.txt) do echo %%i %%j %%k
	2. 分析字符串的例子： for /f "tokens=1,2,3* delims=-, " %%i in ("aa bb,cc-dd ee") do echo %%i %%j %%k %%l
	3. 分析命令输出的例子： for /f "tokens=1* delims==" %%i IN ('set') DO @echo [%%i----%%j]

FOR命令中的变量: ::

	~I         - 删除任何引号(")，扩充 %I
	%~fI        - 将 %I 扩充到一个完全合格的路径名
	%~dI        - 仅将 %I 扩充到一个驱动器号
	%~pI        - 仅将 %I 扩充到一个路径
	%~nI        - 仅将 %I 扩充到一个文件名
	%~xI        - 仅将 %I 扩充到一个文件扩展名
	%~sI        - 扩充的路径只含有短名
	%~aI        - 将 %I 扩充到文件的文件属性
	%~tI        - 将 %I 扩充到文件的日期/时间
	%~zI        - 将 %I 扩充到文件的大小
	%~$PATH:I   - 查找列在路径环境变量的目录(TTT提示：是环境变量path的目录)，并将 %I 扩充到找到的第一个完全合格的名称。如果环境变量名未被定义，或者没有找到文件，此组合键会扩充到空字符串
	%~dpI       - 仅将 %I 扩充到一个驱动器号和路径
	%~nxI       - 仅将 %I 扩充到一个文件名和扩展名
	%~fsI       - 仅将 %I 扩充到一个带有短名的完整路径名
	%~dp$PATH:i - 查找列在路径环境变量的目录，并将 %I 扩充到找到的第一个驱动器号和路径。 
	%~ftzaI     - 将 %I 扩充到类似输出线路的 DIR

.. note:: 在以上例子中，%I 和 PATH 可用其他有效数值代替。%~ 语法用一个有效的 FOR 变量名终止。选取类似 %I 的大写变量名比较易读，而且避免与不分大小写的组合键混淆。

set命令
==========================

| [设置变量]
| 格式：set 变量名=变量值
| 详细：被设定的变量以 `%变量名%` 引用

| [取消变量]
| 格式：set 变量名=
| 详细：取消后的变量若被引用 `%变量名%` 将为空

| [展示变量]
| 格式：set 变量名
| 详细：展示以变量名开头的所有变量的值

| [列出所有可用的变量]
| 格式：set

| [计算器]
| 格式：set /a 表达式
| 示例：set /a 1+2*3 输出 7

.. attention:: 

	set不能用在复合语句里面比如 ``if 1==1 set a=2`` 或者 ``for %%i in (a) do set a=2`` 


预定义的变量
--------------------------------------

下面是些已经被底层定义好可以直接使用的变量：不会出现在 SET 显示的变量列表中: ::

	- %CD% - 扩展到当前目录字符串。
	- %DATE% - 用跟 DATE 命令同样的格式扩展到当前日期。
	- %TIME% - 用跟 TIME 命令同样的格式扩展到当前时间。
	- %RANDOM% - 扩展到 0 和 32767 之间的任意十进制数字。
	- %ERRORLEVEL% - 扩展到当前 ERRORLEVEL 数值。
	- %CMDEXTVERSION% - 扩展到当前命令处理器扩展名版本号。
	- %CMDCMDLINE% - 扩展到调用命令处理器的原始命令行。
	- %0 bat的完整路径名如"C:\Windows\system32\xxx.bat"
	- %1 bat参数1依次类推%2参数2...
	- %path% - 当前的环境变量。以分号隔开的路径列表，路径可包含空格，可以以'\'结尾, 可以以双引号包围之。


扩展变量
----------------------------------------

与%i相关的变量
````````````````````````````````````````````````
包括bat参数或者for循环的%i

假设文件为 ``C:\Documents and Settings\jinsun\桌面\ParseSinglePkgs.bat`` ::

	%0	C:\Documents and Settings\jinsun\桌面\ParseSinglePkgs.bat
	%~dp0 	C:\Documents and Settings\jinsun\桌面\
	%cd%	C:\Documents and Settings\jinsun\桌面
	%~nx0	ParseSinglePkgs.bat
	%~n0	ParseSinglePkgs
	%~x0	.bat

与%VAR%相关的变量
```````````````````````````````````````````````````````````````````````
::

	%VAR:str1=str2%	会将VAR中的str1替换为str2(str2如果为空则达到删除的效果,str1前可以加*，变量%ABC:*B=%是C)
	%VAR:~0,-2%	会提取VAR 变量的所有字符，除了最后两个
	%VAR:~-2%	会提取VAR 变量的最后两个

 

系统变量
-------------------------------------

他们的值由系统将其根据事先定义的条件自动赋值,我们只需要调用而已： ::

	%ALLUSERSPROFILE% （allusersprofile)本地 返回“所有用户”配置文件的位置。 C:Documents and SettingsAll Users 
	%APPDATA% (appdata)本地返回默认情况下应用程序存储数据的位置。 C:Documents and SettingsAdministratorApplication Data 
	%CD% (cd)本地返回当前目录字符串。 C:Documents and SettingsAdministrator桌面 
	%CMDCMDLINE% (cmdcmdline)本地返回用来启动当前的 Cmd.exe 的准确命令行。 cmd /c ""C:Documents and SettingsAdministrator桌面a.bat" " 
	%CMDEXTVERSION%(cmdextversion)系统返回当前的“命令处理程序扩展”的版本号。2 
	%COMPUTERNAME% (computername)系统返回计算机的名称。 xxxx 
	%COMSPEC% (comspec) 系统返回命令行解释器可执行程序的准确路径。 C:WINDOWSsystem32cmd.exe 
	%DATE% 系统返回当前日期。使用与 date /t 命令相同的格式。由 Cmd.exe 生成。有关 date 命令的详细信息，请参阅 Date。 
	%ERRORLEVEL% (errorlevel) 系统返回上一条命令的错误代码。通常用非零值表示错误。 
	%HOMEDRIVE% (homedrive)系统返回连接到用户主目录的本地工作站驱动器号。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。 C: 
	%HOMEPATH% (homepath) 系统返回用户主目录的完整路径。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。 Documents and SettingsAdministrator 
	%HOMESHARE% (homeshare) 系统返回用户的共享主目录的网络路径。基于主目录值而设置。用户主目录是在“本地用户和组”中指定的。 
	%LOGONSERVER% (logonserver) 本地返回验证当前登录会话的域控制器的名称 \ xxxx 
	%NUMBER_OF_PROCESSORS% (numeer_of_processors) 系统指定安装在计算机上的处理器的数目。 
	%OS% (os)系统返回操作系统名称。Windows 2000 显示其操作系统为 Windows_NT。 Windows_NT 
	%PATH% (path)系统指定可执行文件的搜索路径。 C:WINDOWSsystem32;C:WINDOWS;C:WINDOWSSystem32Wbem;C:Program FilesVc++ToolsWinNT;C:Program FilesVc++MSDev98Bin;C:Program FilesVc++Tools;C:Program FilesVC98in 
	%PATHEXT% (pathext)系统返回操作系统认为可执行的文件扩展名的列表。 .COM .EXE .BAT .CMD .VBS .VBE .JS .JSE .WSF .WSH 
	%PROCESSOR_ARCHITECTURE% (processor_architecture) 系统返回处理器的芯片体系结构。值：x86 或 IA64 基于Itanium x86 
	%PROCESSOR_IDENTFIER% (processor_identfier)系统返回处理器说明。 
	%PROCESSOR_LEVEL% (processor_level)系统返回计算机上安装的处理器的型号。 15 
	%PROCESSOR_REVISION% (processor_revision)系统返回处理器的版本号。 4f02 
	%PROMPT% (prompt)本地 返回当前解释程序的命令提示符设置。由 Cmd.exe 生成。$P$G 
	%RANDOM% (random)系统返回 0 到 32767 之间的任意十进制数字。由 Cmd.exe 生成。 30580 
	%SYSTEMDRIVE% (systemdrive)系统返回包含 Windows server operating system 根目录（即系统根目录）的驱动器。 C: 
	%SYSTEMROOT% (systemroot)系统返回 Windows server operating system 根目录的位置。C:WINDOWS 
	%TEMP%(temp) C:DOCUME~1ADMINI~1LOCALS~1Temp和 %TMP% (tmp）C:DOCUME~1ADMINI~1LOCALS~1Temp系统和用户返回对当前登录用户可用的应用程序所使用的默认临时目录。有些应用程序需要 TEMP，而其他应用程序则需要 TMP。 
	%TIME% 系统 返回当前时间。使用与 time /t 命令相同的格式。由 Cmd.exe 生成。有关 time 命令的详细信息，请参阅 Time。 
	%USERDOMAIN% （userdomain)本地返回包含用户帐户的域的名称。 xxxx 
	%USERNAME% (username)本地返回当前登录的用户的名称。 Administrator 
	%USERPROFILE% (userprofile)本地返回当前用户的配置文件的位置。 C:Documents and SettingsAdministrator 
	%WINDIR%(windir) 系统 返回操作系统目录的位置。 C:WINDOWS 
	
echo输出多行内容到文件
===========================================

执行echo时，如果用 ``>`` 输出到文件，会将文件内容清空并输出, 如: ::

	name=bash
	echo “my name is $name” > file.txt
	cat  file.txt
	“my name is bash”

因此这种情况下，输出字符串后面带不带'\n'都不会换行

如果用 ``>>`` 输出到文件，会将内容从文件最后面另起一行输出。

https://blog.csdn.net/ly890700/article/details/53470265

注释语句
=================================

写bat批处理也一样，都要用到注释的功能，这是为了程式的可读性

在批处理中，段注释有一种比较常用的方法： ::

	goto start
	 = 可以是多行文本，可以是命令
	 = 可以包含重定向符号和其他特殊字符
	 = 只要不包含 :start 这一行，就都是注释
	:start

另外，还有其他各种注释形式，比如：

	1. :: 注释内容（第一个冒号后也可以跟任何一个非字母数字的字符）
	#. rem 注释内容（不能出现重定向符号和管道符号）
	#. echo 注释内容（不能出现重定向符号和管道符号）〉nul
	#. if not exist nul 注释内容（不能出现重定向符号和管道符号）
	#. :注释内容（注释文本不能与已有标签重名）
	#. %注释内容%（可以用作行间注释，不能出现重定向符号和管道符号）
	#. goto 标签 注释内容（可以用作说明goto的条件和执行内容）
	#. :标签 注释内容（可以用作标签下方段的执行内容）
	
https://blog.csdn.net/wh_19910525/article/details/8125762
	
	
参考链接
=================================

1. 很好的 `批处理总结 <http://www.cnblogs.com/yang-hao/p/6003376.html>`_ 。
#. `For循环详细讲解一 <https://blog.csdn.net/fool2009/article/details/52265966>`_。
#. `For循环详细讲解二 <http://www.cnblogs.com/yang-hao/p/6003923.html>`_。
#. https://blog.csdn.net/wh_19910525/article/details/8125762
#. https://www.cnblogs.com/adforce/p/3282591.html
