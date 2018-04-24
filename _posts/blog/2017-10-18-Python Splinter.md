---
layout: post
title: Python Splinter 入门
category: blog
---
Splinter是一个使用Python开发的开源Web应用测试工具。它可以帮你实现自动浏览站点和与其进行交互。

splinter下载地址：https://pypi.python.org/pypi/splinter/

官方文档：http://splinter.readthedocs.io/en/latest/index.html

目前最新版本是0.7.5，测试平台是window7 64位。

在pip install splinter 之前需要 install Cython、lxml、selenium 这三个插件，听说install了selenium就不用install splinter，我也没试过。

 

Splinter默认使用的firefox,如果你使用chrome，需要下载Chrome Driver，并放在chrome安装目录下。

For Example:C:\Program Files (x86)\Google\Chrome\Application

并把C:\Program Files (x86)\Google\Chrome\Application 添加到系统环境变量中。

官方不提供Windows的下载，但我们可以用第三方的。

下载地址：http://chromedriver.storage.googleapis.com/index.html

下载地址：http://splinter.readthedocs.io/en/latest/drivers/chrome.html

在notes.txt中寻找与你Chrome浏览器对应的版本。

 

代码实现：
```
from splinter import Browser
import time
with Browser('chrome') as browser:
    # Visit URL
    url = "https://www.baidu.com"
    browser.visit(url)
    time.sleep(3)
    browser.fill('wd', 'splinter - python acceptance testing for web applications')
    time.sleep(3)
    # Find and click the 'search' button
    button = browser.find_by_id('su')
    # Interact with elements
    button.click()
    time.sleep(3)
    if browser.is_text_present('splinter.readthedocs.org'):
        print("Yes, the official website was found!")
    else:
        print ("No, it wasn't found... We need to improve our SEO techniques")
```

常用定位元素：
```
browser.find_by_css('.h1')
browser.find_by_xpath('//h1')
browser.find_by_tag('h1')
browser.find_by_name('name')
browser.find_by_text('Hello World!')
browser.find_by_id('firstheader')
browser.find_by_value('query')

first_found = browser.find_by_name('name').first
last_found = browser.find_by_name('name').last
second_found = browser.find_by_name('name')[1]

links_found = browser.find_link_by_text('Link for Example.com')
links_found = browser.find_link_by_partial_text('for Example')

links_found = browser.find_link_by_href('http://example.com')
links_found = browser.find_link_by_partial_href('example')

divs = browser.find_by_tag("div")
within_elements = divs.first.find_by_name("name")
```

浏览器操作

```
browser.windows              # all open windows
browser.windows[0]           # the first window
browser.windows[window_name] # the window_name window
browser.windows.current      # the current window
browser.windows.current = browser.windows[3]  # set current window to window 3

window = browser.windows[0]
window.is_current            # boolean - whether window is current active window
window.is_current = True     # set this window to be current window
window.next                  # the next window
window.prev                  # the previous window
window.close()               # close this window
window.close_others()        # close all windows except this one

browser.reload()
browser.visit('http://cobrateam.info')
browser.visit('https://splinter.readthedocs.io')
browser.back()
browser.forward()
```

