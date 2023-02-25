---
title: 'Scrapy project intro'
date: 2023-02-25
permalink: /posts/2025/02/blog-post-scrapy/
tags:
  - scrapy
  - tech posts
  - data analysis
---

Scraping Introduction
====

Web scraping refers to the process of extracting data from websites. It involves using software tools or scripts to automate the process of collecting information from the internet. Web scraping can be useful for a variety of purposes, including market research, data analysis, and content aggregation.

There are several techniques for web scraping, including using APIs provided by websites or using web scraping libraries and tools such as BeautifulSoup, Scrapy, and Selenium. Web scraping can be done for various types of data, such as text, images, videos, and other media.

It's important to note that web scraping may violate the terms of use of some websites, and it can be illegal in some cases. Therefore, it's important to check the legality of web scraping before engaging in it. Additionally, web scraping can be resource-intensive and may require expertise in programming and data analysis to be effective.

In its simplest form, web scraping comprises of making HTTP GET (or POST) requests, manipulating the output received to obtain the required data. Every time one visits any website, a HTTP request is sent to that website, and the browser interprets the output (normally HTML), and displays it visually. In Python, we can make HTTP requests with the Requests library, but unlike using a browser, it will simply return the raw form of the output (such as HTML), rather than any visual interpretation.

Below is an example of a simple HTTP GET request

~~~
{
python
import requests
r = requests.get('https://google.com')
}
~~~

From here, several attributes of the request such as the status code received, header, contents can be queried. Usually a HTML document if it is a website or a JSON dictionary if the URL is an API. From here, one can use other libraries such as BeautifulSoup (to parse HTML into a more friendly data structure), or JSON to parse JSON. For some websites, more advanced techniques may be required to circumvent scraping restrictions, such as rate limiting the requests sent (in order to not spam the website). On the other hand, multiprocessing can be used to speed up the scraping process by sending multiple requests simultaneously. Such intricacies can be troublesome to set-up from scratch, which is where the Scrapy library comes in.

[Scrapy]("https://scrapy.org/")
======

Scrapye is designed to extract data from websites in a fast, simple, and extensible way. Scrapy provides an integrated way for handling requests, managing responses, and parsing the web page content.

With Scrapy, you can easily define and customize spiders (also known as crawlers or bots) to extract data from websites, and store it in various formats such as CSV, JSON, or XML. You can also use Scrapy to scrape large amounts of data, follow links between pages, and handle web page authentication.


Setting Up
======
Here we use pipenv to create a vitual environment. Ensure you have pipenv installed. Optionally install pyenv to automatically install the right version of python, otherwise use 3.7 or later. Then install the dependencies to a virtualenv by being in the directory with this file and running pipenv install


Main Components
======

Settings 
=======
Location: /settings.py

Settings are the configuration options that control Scrapy's behavior. They can be used to set global options such as the user-agent string, the number of concurrent requests, and the maximum depth of crawling.

Items
=======
Location: /items.py

Items are the objects that Scrapy extracts from websites. They are essentially containers that hold the data you want to scrape. You define the structure of the items using Python classes.

Pipelines
=======
Location: /pipelines.py

Item pipelines are responsible for processing the extracted data. They can be used for cleaning, validation, and storing data in various formats, such as JSON, CSV, or databases. After an item has been scraped by a spider, it is sent to the Item Pipeline which processes it through several components that are executed sequentially. 

Spiders
=======
Location: /spiders/

Spiders are the heart of the Scrapy framework. They are responsible for defining how to navigate websites, what data to extract and how to store it. A spider is a class that defines how to start a request and what to do with the response.

Creating a New Spider
=======
Generating a new Spider is fairly straightforward. Apart from simply copying the format of a pre-existing Spider, the command prompt line.

~~~
{
$ scrapy genspider <spider name> <scrape web domain>
}
~~~

Running a Spider Locally
=======
Firstly, running scrapy list will show a list of spiders that are currently available to run. Next, take the name of the scrape you wish to run from above and run the following command 
  
~~~
{
$ scrapy crawl <spider name> 
}
~~~


Uploading Data to MongoDB（TBD)
======= 
While the individual Spiders run through the SplitCSVExportPipeline and output a CSV file each, a separate script, that can be build to run all the Spiders and uploads the contents of each CSV into MongoDB. We will discuss it in the future.

  
  
