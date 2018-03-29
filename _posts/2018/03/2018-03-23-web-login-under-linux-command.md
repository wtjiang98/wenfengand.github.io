---
layout: postcn
title: "在python中实现模拟网页认证"
date: 2018-03-23 08:00:00 +0800
lang: cn
nav: post
stickie: false
comments: true
category: python
tags: [ python]
---

一个用来在命令行下进行网页认证的脚本。
<!-- more -->

* 需要把url 更换为实际的 请求url才可以*

使用示例
```sh
python web-login.py in
python web-login.py out
```

```python
import urllib.parse
import urllib.request
import argparse
import getpass

url = your_url
username = None
password = None
user_agent = 'Mozilla/4.0 (compatible; MSIE 5.5; Windows NT)'


def request_input(type):
    if type == 'username':
        return input("Please enter username:")
    elif type == 'password' :
        return getpass.getpass("Please enter password:")
parser = argparse.ArgumentParser()
parser.add_argument('op_type', type = str, help = 'for login: in, for logout: out')
parser.add_argument('--user_name', type = str, help = 'Enter your account\' name')

result, unparsed = parser.parse_known_args()


headers = { 'User-Agent' : user_agent }

# enter the user name
if result.user_name:
    username = result.user_name
else:
    username = request_input('username')

# enter password when login
if True == (result.op_type == 'in'):
    password = request_input('password')


login_values = {
    'action':'login',
    'username' : username,
    'password' : password,
    'ac_id':'20',
    'save_me':'0',
    'ajax':'1'
}
logout_values = {
    'action':'logout',
    'username': username,
    'ajax':'1'
}
# login or logout?
if True == (result.op_type == 'in'):
    data = urllib.parse.urlencode(login_values).encode(encoding='UTF8')
else:
    data = urllib.parse.urlencode(logout_values).encode(encoding='UTF8')


req = urllib.request.Request(url, data, headers)
response = urllib.request.urlopen(req)
the_page = response.read()
print(the_page.decode("utf8"))
```