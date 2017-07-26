# Jmeter性能测试介绍

## Jmeter介绍

jmeter是现在比较热门的web性能测试工具，由于具有开源、免费、轻巧等特点，现在较多的测试人员选择用jmeter来替代loadrunner做自动化测试。

jmeter除了能做web性能测试，还能做web接口测试。

我这里只简单介绍一下环境准备、用例录制、加压和结果查看。


## 环境准备

### java环境安装

最新的jmeter-3.2需要java 8支持，所以，要先安装java 8。

官方下载地址：
http://www.oracle.com/technetwork/java/javase/downloads/index.html

### jmeter安装

官网下载地址：
http://jmeter.apache.org/download_jmeter.cgi
下载后只需解压，不需安装。

### badboy安装

badboy是一个web请求录制工具，可以用来录制http请求
官方下载地址：
http://www.badboy.com.au/download/index

## 用例录制

- 主界面有个大红点按钮，就是录制开关，打开录制开关，在地址栏输入测试网址，就可以录制用例了；
- 录制完成后，在File菜单中选择export to jmeter，保存为.jmx文件即可。
- 在badboy主界面使用Play All按钮，可以重放录制的用例。

## 使用jmeter进行压力测试

- 在~\apache-jmeter-3.2\bin目录下双击jmeter.bat启动jmeter
- 打开用badboy录制的.jmx文件；
- 选中Thread Group，在Threads Properties中填入合适的数值；
	- Number of Threads(users):代表测试线程数，与loadrunner中的虚拟用户数相同；
	- Ramp-Up Period（in seconds）：在指定秒数内启动所有线程；
	- Loop Count:循环次数
- 点击start按钮开始执行测试。

## 结果查看

Jmeter的界面是没有默认展示结果的区域，需要在Thread Group下创建监听器来查看测试结果。

- 右键选中Thread Group；
- Add-Listener,选中合适的测试报告试图;
- 常用的测试报告试图：View Results Tree、View Results in Table、Aggregate Report。
- 注：每次执行测试，都会刷新结果，注意保存结果。

## 相关资料推荐：

jmeter官网：
http://jmeter.apache.org/usermanual/get-started.html

jmeter-tutorial：
https://aimer1124.gitbooks.io/jmeter-tutorial/content/

badboy录制：
https://jingyan.baidu.com/article/5d368d1ef548d43f61c05761.html



