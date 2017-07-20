

# 20170720

昨天装软件
1，安装jdk，配置对应的环境变量。
2，安装git和sourcetree（在sourcetree中指定git.exe路径）
3，gitlab地址[http://172.16.1.101/users/sign_in](http://172.16.1.101/users/sign_in)
对应项目路径
4，在Source Tree中拉取项目
安装STS
修改STS的启动参数（STS.init）：
-Xms2000m
-Xmx2000m
-XX:MaxPermSize=256m

STS.init:
(eclipse.ini是一个文本文件，其内容相当于在Eclipse运行时添加到 Eclipse.exe之后的命令行参数。)
其格式要求：
所有的选项及其相关的参数必须在单独的一行之内;
所有在-vmargs之后的参数将会被传输给JVM，所有如果所有对Eclipse 设置的参数必须写在-vmargs之前（就如同你在命令行上使用这些参数一样）
默认情况下，eclipse.ini的内容如下：
-showsplash
org.eclipse.platform
--launcher.XXMaxPermSize
256m
-vmargs
-Xms40m
-Xmx256m
上面的配置表示堆空间初始大小为40M，最大为256M，PermGen最大为256M。

(我的STS.ini的配置：
-startup
plugins/org.eclipse.equinox.launcher_1.3.100.v20150511-1540.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.300.v20150602-1417
-product
org.springsource.sts.ide
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
256M
-vmargs
-Dosgi.requiredJavaVersion=1.6
-Xms2000m
-Xmx2000m
-XX:MaxPermSize=256m
-Xverify:none
-Dorg.eclipse.swt.browser.IEVersion=10001
)

Eclipse配置Tomcat服务器
- 打开Eclipse，单击“window”菜单，选择下方的“Preferences”：
- 找到Server下方的Runtime Environment，单击右方的Add按钮：
- 选择已经成功安装的Tomcat版本，单击Next:
- 设置Tomcat的安装目录，设置完成后，单击OK即可完成设置！
Tomcat参数配置：
启动时间配置
Vm参数配置，-XX:MaxPermSize=256m -Xmx1500m
URI Encoding: UTF-8
<Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>



##学习任务

batch：
文件流动
BhlifeNewBusinessInJobCommand，
BhlifeNewBusinessOutJobCommand，
实时
InsuranceNewBusinessInJobCommand，
InsuranceNewBusinessOutJobCommand
TaLifeInsRealTimeTrans

UAT环境：
http://172.16.1.131:8080/aiaf/index?redirecting=false
uat2，http://172.16.1.127:8080/aiaf/index?redirecting=false
ust3，http://172.16.1.128:8080/aiaf/index?redirecting=false
ust4，http://172.16.1.1129:8080/aiaf/index?redirecting=false
h5,http://uat2.nfs.org/h5/Dashboard/Dashboard.html
h5,http://172.16.1.131/h5/Dashboard/Dashboard.html

接口：
DOC里的接口

实时

##Eclipse中快速输入代码的自动补全是按enter而不是tab。
alt+/：自动找到相关语句。
ctr+e：转换编辑器
ctr+O：outline
ctr+shift+R：快速打开资源


##eclipse  ctrl+左键 查看源代码 提示找不到源时

在eclipse进行java编程时，查看类源代码，这时ctrl+鼠标左键是个很常用的操作，但有时发现实现不了，经常显示找不到源码。
打开
点击连接源代码----选择”External location“----在此对话框下，选择”External location“---找到路径为安装java JDK时的路径，关键是在此路径下，找到src.zip,就行了。



