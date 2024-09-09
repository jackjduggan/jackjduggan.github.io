---
layout: post
title: Web Application testing in Python with Selenium
---

![_config.yml]({{ site.baseurl }}/images/config.png)

{% highlight powershell %}
python3 -m venv ./venv
.\venv\Scripts\activate
{% endhighlight %}

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

![_config.yml]({{ site.baseurl }}https://github.com/user-attachments/assets/c8fcdc62-2a94-4f6e-943a-a19bbc224187)
![image](https://github.com/user-attachments/assets/c8fcdc62-2a94-4f6e-943a-a19bbc224187)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
