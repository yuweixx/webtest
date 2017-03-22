# selenium2python自动化测试学习笔记

最近开始学习selenium，未后续项目的自动化做准备。

## 主要参考资料
- 《selenium2 python 自动化测试实战》

  这本书是由虫师编写（[作者博客](http://fnng.cnblogs.com/)），是一本适合selenium入门的书籍。

- [Python菜鸟教程](http://www.runoob.com/python/python-tutorial.html) 

  一个很好基础学习网站，除了python还有其它很多教程。

## 环境准备
### 系统环境
Win10-64bit

### python
书中用的是python2.x，为了加强学习效果，我选用的是python3.x，已更书中有所区别，避免自己完全照抄代码。

- python下载

  [python下载地址](https://www.python.org/downloads/)

- python安装

  python安装完成后，需要检查环境变量是否配置ok，如果ok，cmd中键入py，会显示出py版本

### selenium
- selenium下载 

  [selenium下载地址](http://www.seleniumhq.org/download/)，注意选择python对应的selenium。

- selenium安装

  解压selenium-3.3.1.tar.gz，cmd键入到 ``~/selenium-3.3.1``目录下，使用``python setup.py install``命令进行安装。

  注：如果系统中python2和python3同时存在，要检查一下是否安装到了python3下，注意看安装过程文件移动到哪个路径。

- webdriver下载

  webdriver是为了调用浏览器存在的组件，不同的浏览器有不同的webdriver

  [IE64bit-webdriver下载地址](http://selenium-release.storage.googleapis.com/3.3/IEDriverServer_x64_3.3.0.zip)

  [chrome-webdriver下载地址](https://chromedriver.storage.googleapis.com/2.28/chromedriver_win32.zip)

- webdriver安装

  将下载好的``IEDriverServer.exe``和``chromedriver.exe``放的python安装目录下即可，我的python安装目录在``C:\Users\yuwei\AppData\Local\Programs\Python\Python36-32``

- 环境检查

  cmd中键入以下命令，如果能启动IE或者chrome，说明环境已经准备完成：

```python
py
from selenium import webdriver
driver=webdriver.Ie()
driver=webdriver.Chrome()
```
## selenium基础

### 元素定位的常用方法

### 示例1-登录
