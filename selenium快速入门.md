# selenium快速入门

## 环境准备
- 安装Python3
- 安装selenium
- 下载安装对应的webdriver

## 上代码
### 发微博
```python
from selenium import webdriver
from time import sleep
#打开浏览器
driver = webdriver.Chrome()
#键入网址
driver.get("http://weibo.xx.cn/")
#输入邮箱//web元素中，有id的，可以用find_element_by_id方法寻找元素，用send_keys方法输入文本
driver.find_element_by_id("email").send_keys("真实邮箱")
#输入密码
driver.find_element_by_id("password").send_keys("真实密码")
#点击登录//没有id的元素，可以使用find_element_by_xpath，点击操作用click()方法
driver.find_element_by_xpath("/html/body/div[1]/div[3]/div[3]/div[2]/div[2]/form/div/button").click()
#输入微博发送内容
driver.find_element_by_xpath("/html/body/div[1]/div[2]/div[3]/div[2]/div[1]/div[1]/div/div[1]/div[1]/div/textarea").send_keys("xx")
#点击发表//还可以通过find_element_by_partial_link_text找到元素
driver.find_element_by_partial_link_text("发表").click()
#关闭浏览器
driver.quit()
```
### 发邮件
```python
from selenium import webdriver
from time import sleep
driver = webdriver.Chrome()
driver.get("http://mail.xx.cn/")
sleep(2)
#输入框输入内容
driver.find_element_by_id("username").send_keys("email@xx.cn")
sleep(2)
driver.find_element_by_id("password").send_keys("password")
sleep(2)
driver.find_element_by_xpath("/html/body/form/table/tbody/tr[2]/td[2]/table[1]/tbody/tr[7]/td/table/tbody/tr[3]/td/input[1]").click()
driver.find_element_by_id("newmsgc").click()
#处理新的窗口：获取所有窗口的句柄，再切换到其中一个
all_handles = driver.window_handles
print(all_handles)
print(all_handles[1])
driver.switch_to_window(all_handles[1])
driver.find_element_by_id("divTo").send_keys("mail@xx.cn")
sleep(2)
driver.find_element_by_id("txtSubj").click()
driver.find_element_by_id("txtSubj").send_keys("testmail")
sleep(2)
driver.find_element_by_id("divToolbarButtonsend").click()
sleep(5)
driver.quit()
```

## 元素查找方法

### 常用方法
- chrome浏览器，F12进入调试模式，可以找到元素的各种属性。

### xpath查找方法
- 1.火狐浏览器安装firebug插件；
- 2.对相应元素使用鼠标右键，选中“使用firebug查看元素”；
- 3.再对元素列表中的结果使用鼠标右键，选中“复制xpath”，粘贴到文本编辑器中。

## 参考资料
```
https://segmentfault.com/a/1190000007249396?_ea=1293878

```
