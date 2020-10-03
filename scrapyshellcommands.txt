# Scrapy Shell commands

these are the commands run inside the scrapy shell to find elements and text from the website.

## basic working, get method returns first match
response.css('title')
response.css('title').get()
response.css('title::text').get()

## get all method returns a list
response.css('h3')
response.css('h3').getall()
response.css('h3::text').getall()

## using a dot to match
response.css('div.f-grid prod-row')
response.css('div.f-grid.prod-row')

## get some proper data
products = response.css('div.details-pricing')
products.css('a::text').get()

## get all links
products.css('a::attr(href)').getall()

## get first link
products.css('a::attr(href)').get()

## get price
products.css('p.price.larger')
products.css('p.price.larger').get()
products.css('p.price.larger::text').get()

# generate new spider

scrapy genspider drones jessops.com/drones

note start urls and name, class etc. this is a basic template

under PARSE:

products = response.css('div.details-pricing')
        for item in products:
            drone = {
            'name' : item.css('a::text').get(),
            'price' : item.css('p.price.larger::text').get(),
            }
            yield drone

# run the spider
scrapy crawl dronespider (name)

scrapy crawl dronespider (name) -o drones.csv

saving to same file will add to it
