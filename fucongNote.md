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

