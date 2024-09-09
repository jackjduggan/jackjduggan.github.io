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
{% endhighlight %}

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
