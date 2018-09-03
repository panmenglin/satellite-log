# 基于 selenium、 chromedriver 模拟登录

我们可以通过 selenium 测试脚本实现 chrome 浏览器下模拟用户的实际操作

来实现网页访问，点击输入框，输入用户名、密码，点击登录等一系列操作

## 依赖

python

我这里直接使用的 python 2.7

pip

```
sudo easy_install pip
```

selenium

```
pip install -U selenium
```

chromedriver

下载 chromedriver

[下载地址](https://sites.google.com/a/chromium.org/chromedriver/downloads)

## 模拟用户行为

```python
from selenium import webdriver
browser = webdriver.Chrome()
```