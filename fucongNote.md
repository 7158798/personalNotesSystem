# 富聪笔记

# 20170405 第一天

中午开会任务
1，用python talkingdata数据获取
日报、周报
2，吴刚 SQL编程  BAM CRM
java后边再说 
3，车型数据获取，kun总 那边给出要求，可能会用火车头啥的 

完成的东西：安装

SourceTree

pycharm
anaconda
navicatPremium
git 自己的东西 把公司电脑ssh key加到了

pycharm背景颜色
pycharm -> setting -> Editor -> Colors&Fonts -> Font -> scheme:--

获取git fetch：相当于是从远程获取最新版本到本地，不会自动merge
拉取git pull：相当于是从远程获取最新版本并merge到本地
git pull origin master
上述命令其实相当于git fetch 和 git merge
在实际使用中，git fetch更安全一些
因为在merge前，我们可以查看更新情况，然后再决定是否合并



#  20170406

武刚未来，自己摸索navicat premium
mysql crash coourse
mysql 必知必会 文件 新建在navicat中数据库


talkingdata数据获取
产品研发部每日数据统计

fiddler web debugger


Python处理Excel文档（xlrd, xlwt, xlutils）
xlrd，xlwt和xlutils是用Python处理Excel文档(*.xls)的高效率工具。其中，xlrd只能读取xls，xlwt只能新建
xls（不可以修改），xlutils能将xlrd.Book转为xlwt.Workbook，从而得以在现有xls的基础上修改数据，并创
建一个新的xls，实现修改。

在网站:http://www.python-excel.org/, 提供了xlrd,xlwt,xlutils一套工具,xlrd是用来读取excl的,xlwt是用
来写入excel的xlutils,引用了xlrd和xlwt来做一些如合并,过滤,修改文件的操作,这个很多人推荐使用,但有一
个缺陷,就是,他的一个工作表sheet只能写入65535行,多了就不能写了,解决方法可以是,每65535行新建一个工作
表sheet或者向后移动几列,然后写入,他的列最大值为256,所以最多一个sheet文件可以写入:256 * 65535 个数
据
在网站:http://pythonhosted.org/openpyxl/,提供了工具openpyxl,


TalkingData:
------------
TalkingData（北京腾云天下科技有限公司）成立于2011年9月，是中国最大的独立第三方移动数据服务平台。2013年完成千万美元A轮融资（北极光领投），2014年完成数千万美元的B轮融资（软银，MileStone领投），总部位于北京，上海设有分公司，并在美国硅谷，日本东京成立了办事处。经过近4年高速发展，TalkingData形成了由开发者服务平台、数据服务平台、数据商业化平台为中心的数据生态体系，覆盖超过20亿独立智能设备，服务于10万款移动应用以及8万多应用开发者。
客户既有腾讯、百度、网易、搜狐、360、Google、Yahoo、Zynga、宝开、滴滴打车等知名互联网企业，又有中国银联、招商银行、中信银行、平安保险、国信证券、Orchirly、碧桂园、亨得利、全城热恋等传统行业巨头，我们正在利用移动互联网的数据价值，并逐步改变传统行业的未来。


fiddler web debugger:
---------------------
Fiddler是一款由C#语言开发的免费http调试代理软件，有.net 2 和 .net 4 两种版本。Fiddler能够记录所有的你电脑和互联网之间的http通讯，Fiddler 可以也可以让你检查所有的http通讯，设置断点，以及Fiddle 所有的“进出”的数据。


navicat
-----------------
利用MySQL Crash Course MySQL 必知必会王章上下载的mysql_scripts中的create.sql，populate.sql在navicat中建立数据库和数据表
检索数据 select products.prod_name from acrashmysql.products
排序检索数据 select prod_name from products order by prod_price DESC,prod_name LIMIT 1;
过滤数据 
select prod_name, prod_price from products where prod_price <10;
select prod_name, prod_price from products where prod_price BETWEEN 5 AND 10;
数据过滤 


将navicat for mysql 中查询出来的内容导出到xls文件中
保存查询结果，命名，导出向导，选择excel格式，然后点击下一步，填写好excel文件的存放路径，继续下一步。根据需要勾选附加选项，继续下一步。点击开始，等待完成即可。导出成功后，会有successful的提示。

MySQL命令行导出数据库


命令行导出数据库：
----------------
导出数据库：mysqldump -u 用户名 -p 数据库名 > 导出的文件名 
如我输入的命令行:mysqldump -u root -p news > news.sql   (输入后会让你输入进入MySQL的密码)
（如果导出单张表的话在数据库名后面输入表名即可）


命令行导入数据库：
----------------
导入文件：mysql>source 导入的文件名; 
如我输入的命令行：mysql>source news.sql; 

MySQL备份和还原,都是利用mysqldump、mysql和source命令来完成的。 


mysql：
右键连接-->命令列界面：可以可以在像在命令行中运行一样
右键连接-->运行SQL文件







20170407
====================================================================================================================
-


WIN7 的系统缩放比例在哪里改？
---------------------
1,在Win7桌面点击鼠标右键，选择“屏幕分辨率”。
2,打开Win7屏幕分辨率设置窗口，在“屏幕分辨率”窗口点击下方的“放大或缩小文本和其它项目”。
3,选择“放大或缩小文本和其他项目，在“显示”设置窗口，选择要放大的位数。一般来说屏幕较小的笔记本电脑可以放大到125%，
台式机可以放大的更多一些，达到150%甚至200%。　
4,调整放大倍数　 选好之后点击“应用”按钮保存退出，注销后重新登录系统，就会发现所有地方的字体都变大了。




 Office 2010 中打开多个Excel文件只能在同一窗口中显示的问题
--------------------------
Start：
打开“运行”窗口（快捷键：Win + R），输入regedit编辑注册表。
定位到【HKEY_CLASSES_ROOT\Excel.Sheet.12\shell\Open】，展开Open，将ddeexec删除，然后选中command，双击右侧窗格的”默
认“，将末尾的/dde改为”%1“（注意有双引号）；再双击command，同样将末尾的/dde改为”%1“。
定位到【HKEY_CLASSES_ROOT\Excel.Sheet.8\shell\Open】，做和上面一样的改动。
End


数据每日拉取
--------

可以考虑execfile()函数进行多个 XXX.py文件放到一个python main文件中一起执行。

在python代码里执行其他python程序
听起来很绕口，其实就是在一个python代码里直接运行另外一个.py文件
exec("anotherprogram.py")




PV、UV、IP的区别
---------------
网站推广需要一个网站访问统计工具，常用的统计工具有百度统计、51la、量子恒道统计等。网站访问量常用的指标为PV、UV、IP。
那么什么是PV、UV和IP，PV、UV、IP的区别是什么？
PV(访问量)：即Page View, 即页面浏览量或点击量，在一定统计周期内用户每次刷新网页一次即被计算一次。 
UV(独立访客)：即Unique Visitor,访问您网站的一台电脑客户端为一个访客。00:00-24:00内相同的客户端只被计算一次。
IP(独立IP)：即Internet Protocol,指独立IP数。00:00-24:tf8').encode('gbk')




公司业务概况--自媒体运营
--------------------------


python 中 exec、 eval、 execfile 和 compile 用法
------------------
exec语句用来执行储存在字符串或文件中的Python语句。
例如，我们可以在运行时生成一个包含Python代码的字符串，然后使用exec语句执行这些语句。下面是一个简单的例子。
>>> exec 'print "Hello World"'
>>> Hello World
>>> eval语句用来计算存储在字符串中的有效Python表达式。下面是一个简单的例子。
>>> eval('2*3')
>>> 6

eval(expression[, globals[, locals]])
eval(str [ globals [ locals ]])函数将字符串str当成有效python表达式来求值，并返回计算结果。
同样地, exec语句将字符串str当成有效Python代码来执行.提供给exec的代码的名称空间和exec语句的名称空间相同.
最后，execfile(filename [,globals [,locals ]])函数可以用来执行一个文件,看下面的例子:
>>> eval_r('3+4')
>>> 7
>>> exec 'a=100' 
>>> a 
>>> 100 
>>> execfile(r'd:\code\ex\test.py')
>>> hello world!
>>>

默认的，eval(),exec,execfile()所运行的代码都位于当前的名字空间中. eval(), exec 和 execfile()函数也可以接受一个或两个
可选字典参数作为代码执行的全局名字空间和局部名字空间. 例如:
globals={'x':7,'y':10,'birds':['parrot','swallow','albatross']}
locals={}
# 将上边的字典作为全局和局部名称空间
a=eval("3*x+4*y",globals,locals)
exec "for b in birds:print b" in globals,locals # 注意这里的语法 
parrot
swallow
albatross
execfile("foo.py", globals, locals)

注意例子中exec语句的用法和eval(), execfile()是不一样的. exec是一个语句(就象print或while), 而eval_r()和execfile()则是
内建函数.
exec(str) 这种形式也被接受，但是它没有返回值。

当一个字符串被exec,eval(),或execfile()执行时,解释器会先将它们编译为字节代码，然后再执行.这个过程比较耗时,所以如果需
要对某段代码执行很多次时,最好还是对该代码先进行预编译,这样就不需要每次都编译一遍代码，可以有效提高程序的执行效率。
compile(str ,filename ,kind )函数将一个字符串编译为字节代码, str是将要被编译的字符串, filename是定义该字符串变量的文
件，kind参数指定了代码被编译的类型-- 'single'指单个语句, 'exec'指多个语句, 'eval'指一个表达式. cmpile()函数返回一个
代码对象，该对象当然也可以被传递给eval()函数和exec语句来执行,例如:
>>> str = 'for i in range(0, 10): print i'
>>> c = compile(str,'','exec')
>>> exec c 
>>> 0
>>> 1
>>> 2
>>> 3
>>> 4
>>> 5
>>> 6
>>> 7
>>> 8
>>> 9
>>>  str2 = '3*6 + 4*8'
>>> c2 = compile(str2,'','eval')        # 编译为表达式 
>>> result = eval_r(c2)                    # 执行
>>> result
>>> 50






foo还有bar都是无意义的代名词，就好像中文里面的“某某“，“张三李四”差不多。
foo bar baz = 无名氏 = 张三李四小明小张





20170410
=============================================================================================================

172.16.1.114:3306
root
Hubin123
http://git.nfs.org/wangxun/aiaf-spi.git
http://git.nfs.org/wangxun/aiaf-spi.git


3306是MySQL的默认端口。


fiddler
-----------
Fiddler是最强大最好用的Web调试工具之一，它能记录所有客户端和服务器的http和https请求，允许你监视，设置断点，甚至修改
输入输出数据，Fiddler包含了一个强大的基于事件脚本的子系统，并且能使用.net语言进行扩展
　　你对HTTP 协议越了解， 你就能越掌握Fiddler的使用方法。你越使用Fiddler，就越能帮助你了解HTTP协议。
　　Fiddler无论对开发人员或者测试人员来说，都是非常有用的工具。

Fiddler是一款由C#语言开发的免费http调试代理软件，有.net 2 和 .net 4 两种版本。Fiddler能够记录所有的你电脑和互联网之
间的http通讯，Fiddler 可以也可以让你检查所有的http通讯，设置断点，以及Fiddle 所有的“进出”的数据。

安装完成后，在开始菜单中找到Fiddler 2并运行，打开IE浏览器，访问某个网站，此时在Fiddler中就可以看到抓取的数据了

获取cookies，以某开源站为例，先清空Fiddler的抓取记录，然后在网页中输入用户名、密码登录，显示登录成功后，查看Fiddler
捕捉到的第1条记录，点击右侧[Raw]

在新弹出的程序窗口中我们就可以看到详细的信息记录，其中就包括了cookies




武刚：
C语言爬虫比较多，java少。

公司后台开发基于现成的模块框架，sql
因为其实软件发展到现在大多东西前人都搞过相关功能，我们要么直接拿来用，要么修修补补，
和我用python感觉一样，我们主要学习的是如何用，至于底层的为什么，是什么我们只要了解，他的意思，不需要具体指导底层是如
何实现的，等有需要时再看。这其实也是学习的途径、方法论。

数据是app端写入的，我们后台数据库，需要查询 分析，交易、对账、图形化等。

我们这边数据量很小的，服务器主机是4T，也就是说 根本用不到大数据，不够用了加一个就好了。


版本不同，excel的最大行数和列数不同。2003版最大行数是65536行，最大列数是256列。Excel2007及以后的版本最大行数是
1048576行，最大列数是16384列。


python、 fiddler、cookie
request和response，session和cookie
