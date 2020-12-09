# Scrapy框架

## 1.创建项目

`scrapy startproject 'projectname'`

## 2.项目结构

```
tutorial/
    scrapy.cfg            # deploy configuration file

    tutorial/             # project's Python module, you'll import your code from here
        __init__.py

        items.py          # project items definition file

        middlewares.py    # project middlewares file

        pipelines.py      # project pipelines file

        settings.py       # project settings file

        spiders/          # a directory where you'll later put your spiders
            __init__.py
```

## 3.First Demo

Spiders are classes that you define and that Scrapy uses to scrape information from a website (or a group of websites). They must subclass [`Spider`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider) and define the initial requests to make, optionally how to follow links in the pages, and how to parse the downloaded page content to extract data.

This is the code for our first Spider. Save it in a file named `quotes_spider.py` under the `tutorial/spiders` directory in your project:

```
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes"

    def start_requests(self):
        urls = [
            'http://quotes.toscrape.com/page/1/',
            'http://quotes.toscrape.com/page/2/',
        ]
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)

    def parse(self, response):
        page = response.url.split("/")[-2]
        filename = f'quotes-{page}.html'
        with open(filename, 'wb') as f:
            f.write(response.body)
        self.log(f'Saved file {filename}')
```

As you can see, our Spider subclasses [`scrapy.Spider`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider) and defines some attributes and methods:

- [`name`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.name): identifies the Spider. It must be unique within a project, that is, you can’t set the same name for different Spiders.

- [`start_requests()`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.start_requests): must return an iterable of Requests (you can return a list of requests or write a generator function) which the Spider will begin to crawl from. Subsequent requests will be generated successively from these initial requests.

- [`parse()`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.parse): a method that will be called to handle the response downloaded for each of the requests made. The response parameter is an instance of [`TextResponse`](https://docs.scrapy.org/en/latest/topics/request-response.html#scrapy.http.TextResponse) that holds the page content and has further helpful methods to handle it.

  The [`parse()`](https://docs.scrapy.org/en/latest/topics/spiders.html#scrapy.spiders.Spider.parse) method usually parses the response, extracting the scraped data as dicts and also finding new URLs to follow and creating new requests ([`Request`](https://docs.scrapy.org/en/latest/topics/request-response.html#scrapy.http.Request)) from them.

  ## 4.How to run the spider

  `scrapy crawl 'projectname'`