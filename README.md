scrapy-webdriver
================

Scrape using Selenium webdriver.

Installation
=============

For now it's not on pypi, but this should work:

    pip install https://github.com/sosign/scrapy-webdriver/archive/master.zip

Or something like this, in setup.py:

    setup(
        install_requires=[
            'scrapy_webdriver',
            ...,
        ],
        dependency_links=[
            'https://github.com/sosign/scrapy-webdriver/archive/master.zip#egg=scrapy_webdriver',
        ],
        ...,
        )

Configuration
=============

Add something like this in your scrapy project settings:

    DOWNLOAD_HANDLERS = {
        'http': 'scrapy_webdriver.download.WebdriverDownloadHandler',
        'https': 'scrapy_webdriver.download.WebdriverDownloadHandler',
    }

    SPIDER_MIDDLEWARES = {
        'scrapy_webdriver.middlewares.WebdriverSpiderMiddleware': 543,
    }

    WEBDRIVER_BROWSER = 'PhantomJS'  # Or any other from selenium.webdriver

Usage
=====

In order to have webdriver handle your downloads, use the provided
class `scrapy_webdriver.http.WebdriverRequest` in place of the stock scrapy
`Request`, like so:

    from scrapy_webdriver.http import WebdriverRequest
    yield WebdriverRequest('http://www.example.com')

Parameters not supported (yet?) are: `method`, `body`, `headers`, `cookies`.

Hacking
=======

Pull requests much welcome. Just make sure the tests still pass, and add to
them as necessary:

    python setup.py test
