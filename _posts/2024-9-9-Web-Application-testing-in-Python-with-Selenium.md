---
layout: post
title: (WIP) Web Application testing in Python with Selenium
---

![Image]({{ site.baseurl }}/images/selenium-partone-header.png)

## 1. Set up your Python environments.
In most cases, when running Python code, the preferred approach is to set up a 'virtual environment'. There are multiple ways to do this, with my preferred method being:
{% highlight powershell %}
python3 -m venv ./venv
.\venv\Scripts\activate
{% endhighlight %}
You'll know the virtual environment is set up and running when you a green '(venv)' in front of your prompt.
![image](https://github.com/user-attachments/assets/63dd6147-2fc3-4091-9f6d-c57d89be6be2)

{% highlight powershell %}
pip install selenium
{% endhighlight %}

{% highlight python %}
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.service import Service

## Create an instance of WebDriver to interacte with a browser, in our case, Chrome.
service = Service(executable_path=r'chromedriver-win64\chromedriver.exe')
driver =  webdriver.Chrome(service=service)

## Choose a website to interact with, I've chosen this blog.
driver.get("https://jackjduggan.github.io/")

## Let's interact with the website by getting the title.
print(driver.title)

## Remember to close the browser after you're finished interacting with it!
driver.quit()
{% endhighlight %}

![image](https://github.com/user-attachments/assets/c8fcdc62-2a94-4f6e-943a-a19bbc224187)
