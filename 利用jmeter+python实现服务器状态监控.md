# 帆软服务器监控实践

## 主要步骤
- 1.使用badboy录制脚本，包括登录帆软服务后台，进入注册信息界面；
- 2.使用jmeter添加断言，输出断言结果；
- 3.使用python脚本执行jmx，并将结果发生邮件；

## python脚本
```python

#coding=utf-8
# 引用主要的py库文件
import os
import time
import smtplib
import email.mime.multipart
import email.mime.text

# 邮件发送函数
def send_email(SMTP_host, from_addr, password, to_addrs, subject='', content=''):
    msg = email.mime.multipart.MIMEMultipart()
    msg['from'] = from_addr
    msg['to'] = to_addrs
    msg['subject'] = subject
    content = content
    txt = email.mime.text.MIMEText(content)
    msg.attach(txt)
    smtp = smtplib.SMTP()
    smtp.connect(SMTP_host, '25')
    smtp.login(from_addr, password)
    smtp.sendmail(from_addr, to_addrs, str(msg))
    smtp.quit()

# 执行jmx文件，读取执行结果，发送邮件
def frstatus():
# 执行jmx文件
    os.system("D:\\webtest\\apache-jmeter-3.2\\bin\\jmeter -n -t D:\\webtest\\apache-jmeter-3.2\\bin\\FR8500.jmx")
# 读取执行结果
    with open("D:\\webtest\\apache-jmeter-3.2\\bin\\FR8500.csv","r",encoding="utf-8") as csvfile:
        readers = csvfile.readlines()
        countlines = len(readers)
        print(countlines)
        relusttype = readers[-1].split(',')[7]
        print('relusttype=',relusttype)
# 发送结果成功邮件
        if relusttype == 'true':
            print("registerSuccess")
            send_email('smtp.126.com', 'yuweixx@126.com', '******', 'yuwei@szewec.com', 'FR8500StatusOK', 'registerSuccess')
        else:
# 发送结果失败邮件
            print("registerFail")
            send_email('smtp.126.com', 'yuweixx@126.com', '******', 'yuwei@szewec.com', 'FR8500StatusFail', 'registerFail')
    return relusttype

# 与frstatus()类似，但结果为成功不发送邮件
def frfailstatus():
# 执行jmx文件
    os.system("D:\\webtest\\apache-jmeter-3.2\\bin\\jmeter -n -t D:\\webtest\\apache-jmeter-3.2\\bin\\FR8500.jmx")
# 读取执行结果
    with open("D:\\webtest\\apache-jmeter-3.2\\bin\\FR8500.csv","r",encoding="utf-8") as csvfile:
        readers = csvfile.readlines()
        countlines = len(readers)
        print(countlines)
        relusttype = readers[-1].split(',')[7]
        print('relusttype=',relusttype)
        if relusttype == 'true':
            print("registerSuccess")
        else:
# 发送结果失败邮件
            print("registerFail")
            send_email('smtp.126.com', 'yuweixx@126.com', '******', 'yuwei@szewec.com', 'FR8500StatusFail', 'registerFail')
    return relusttype

# 死循环，每100*144秒执行一次，如果成功，发送邮件并继续，如果失败，跳出，并发送邮件
while 1>0:
    i = 0
    typeB = frstatus()
    print('tpyeB=', typeB)
    if typeB == 'true':
        pass
    else:
        break
    time.sleep(100)
    while i<144:
# 每100秒检查一次，如果成功，发送邮件并继续，如果失败，跳出，并发送邮件
        typeA = frfailstatus()
        print('tpyeA=', typeA)
        print(time.strftime('%Y-%m-%d %H:%M:%S',time.localtime(time.time())))
        if typeA == 'true':
            pass
        else:
            break
        time.sleep(100)
        i = i+1

```
