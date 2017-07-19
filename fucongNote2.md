富聪笔记2

# 20170717


elkadmin


## eclipse

修改字符集

java构建路径

重构：
（在项目开发中我们经常需要修改类名，但如果其他类依赖该类时，我们就需要花很多时间去修改类名。
但 Eclipse 重构功能可以自动检测类的依赖关系并修改类名，帮我们节省了很多时间。）右键--refactor（重构）
- 在 Package Explorer 视图中右击 Java 元素并选择Refactor(重构)菜单项
- 在 Java 编辑器中鼠标右击 Java 元素并选择Refactor(重构)菜单项
- 在 Package Explorer 视图中选择 Java 元素并按下 Shift + Alt + T
添加书签：
Eclipse 中可以在编辑器的任意一行添加书签。 您可以使用书签作为提示信息，或者使用书签快速定位到文件中的指定的行。
在垂直标尺上右击鼠标并选择能 "Add Bookmark" 即可。
代码模板：
Eclipse 提供了通过定义和使用代码模板来提高工作效率与代码可预测性的能力。
用Eclipse的代码提示快捷键(默认为Alt+/)，回车后，就可以看到Eclipse自动帮我们完成\*\*的完整定义：

Package Explorer 显示了新建的 Java 项目。项目图标中的 "J" 字母表示 Java 项目。 文件夹图标表示这是一个 java 资源文件夹。



Java构建路径用于在编译Java项目时找到依赖的类，包括以下几项：

- 源码包
- 项目相关的 jar 包及类文件
- 项目引用的的类库

Java 项目属性对话框可以通过在 Package Explorer 视图中鼠标右击指定的 Java 项目并选择 Properties(属性) 菜单项来调用。

然后 在左边窗口选择 Java Build Path(Java 构建路径)。



clipse 工作空间包含了多个项目。一个项目可以是关闭或开启状态。

项目打开过多影响有：

- 消耗内存
- 占用编译时间：在删除项目.class 文件（Clean All Projects）时并重新编译（在菜单上选择 Project > Clean > Clean all projects ）。


try catch 加上之后就会 ，如果没加 这个线程 跑到这里就会全部把异常爆出来，这个线程中止；下次再跑到这里时，这个线程继续如此。



Web应用开发好后，若想供外界访问，需要把web应用所在目录交给web服务器管理，这个过程称之为虚似目录的映射



工作空间路径查询：
eclipse ---- windows -------- preference---- general----- startup and shut down ------ workplace 



echarts



#20170718


**bam库**在生产环境中选择时 是第一个FarmsRO
今天问题：lisa查询时，日期的列都没有显示
测试库里的 把棉裤中的agreement鱼生产库中的以及farms库中的不一致 多了两个字段。

生产中的bam库里的表的使用，那么多表 先在用不用，我们倒库时该怎么导，问勋总。




## 注解（Annotation）与注释（comment）

注解是插入你代码中的一种注释或者说是一种元数据（meta data）。这些注解信息可以在编译期使用预编译工具进行处理（pre-compiler tools），也可以在运行期使用 Java 反射机制进行处理。下面是一个类注解的例子：




##廖雪峰 Java











#20170719






