# How to Scrape with Scrapy: A Step-by-Step Guide with Homegate.ch

Scraping websites can be a powerful tool for gathering data, and Scrapy is one of the most popular frameworks to help you do this efficiently. Here's a comprehensive guide on setting up Scrapy and creating your first spider.

---
# Summary

Here’s a quick recap of the steps we followed in this guide:

## 1. Setting Up the Environment

- Installed Python and Pip.
- Created a virtual environment to isolate project dependencies.
- Installed Scrapy using Pip.

## 2. Creating a Scrapy Project

- Generated a new Scrapy project using `scrapy startproject`.
- Created a spider using `scrapy genspider`.

## 3. Building the Spider

- Updated the spider to target property listings on [Homegate.ch](http://homegate.ch/).
- Used the Scrapy shell to test CSS selectors and extract data.
- Extracted property details (price, rooms, living space, and address) from each card.
- Added pagination logic to scrape all pages.

## 4. Running the Spider

- Ran the spider using `scrapy crawl`.
- Saved the scraped data to a CSV file (`properties.csv`).

## 5. Key Takeaways

- **CSS Selectors**: Used to extract specific elements from HTML.
- **Pagination**: Handled by finding and following the "Next" button.
- **Data Export**: Saved data in JSON or CSV format for further analysis.

## **1. Setting Up Your Environment**

1. **Installing Python**

First, download and install Python from the [official Python website](https://www.python.org/downloads/). Verify your installation by running the following in VS Code’s integrated terminal or in Windows PowerShell Terminal:

```python
python --version
```

2. **Installing Pip**

Pip is included with last versions of Python, but you can double-check its installation:

```bash
pip --version
```

If you have not pip install, you can installed from here: [https://pip.pypa.io/en/stable/installation/](https://pip.pypa.io/en/stable/installation/)

3. **Setting Up a Virtual Environment**

Virtual Env is already installed in Python 3.9 and above but if you have a previous version it can be installed manually using “pip install virtualenv”.

In VS Code, create and open your project folder and go to the terminal and create a virtual environment:

```bash
python -m venv myenv
```

Once created, you may activate the virtual environment in the terminal:

```python
myenv\Scripts\activate
```

To check if it is activated, you can see at the start of the terminal (myenv), now every package will be install into this folder and be specific to this project.

4. **Scrapy Instalation**

To create a new Scrapy project, first run in the terminal:

```bash
pip install scrapy
```

Verify the installation by running:

```bash
scrapy
```

You should see a list of Scrapy commands.

---

## **2. Creating a Scrapy Project in VS Code**

1. **Start a New Scrapy Project**

In the VS Code terminal, run:

```bash
scrapy startproject homegate_scraper
```

This creates a new Scrapy project named `homegate_scraper`.

2. **Navigate into your project folder:**

```python
cd homegate_scraper
```

## **3. Building Your First Spider with [Homegate.ch](http://Homegate.ch) website**

1. **Create a Scrapy Spider**
    
    Navigate to the `spiders` directory in your terminal:
    
    ```python
    cd myproject\spiders
    ```
    
    Now, generate a new spider using the following command:
    
    ```python
    scrapy genspider homegate_spider homegate.ch
    ```
    
    This creates a spider file named `homegate_spider.py`. Open this file in your editor. The spider will look something like this:
    
    ```python
    import scrapy
    
    class HomegateSpider(scrapy.Spider):
        name = "homegate_spider"
        allowed_domains = ["homegate.ch"]
        start_urls = ["https://www.homegate.ch"]
    
        def parse(self, response):
            pass
    ```
    
2. **Update the Spider to Target Property Listings**
    
    **Step 1**: Update start_urls
    Change the start_urls to target the property listings page for Zurich:
    
    ```python
    start_urls = ["[https://www.homegate.ch/buy/real-estate/canton-zurich/matching-list](https://www.homegate.ch/buy/real-estate/canton-zurich/matching-list)"]
    ```
    
    **Step 2**: Add a Basic parse Function
    The parse function will handle the response from the start_urls. For now, let’s just print the page title to verify that the spider is working:
    
    ```python
    def parse(self, response):
    print(response.css('title::text').get())
    ```
    
    Run the spider to test it:
    
    ```python
    scrapy crawl homegate_spider
    ```
    
    You should see the title of the [Homegate.ch](http://homegate.ch/) page printed in the terminal.
    
    ---
    
3. **Extract Property Cards**
    
    **Step 1**: Identify Property Cards
    Inspect the page (using your browser’s developer tools) to find the HTML structure of the property cards. Suppose each property card is inside a `<div>` with the class `HgCardElevated_cardElevated_M4Ozt`.
    
    **Step 2**: Extract All Property Cards
    Update the parse function to extract all property cards:
    
    ```python
    def parse(self, response):
    cards = response.css('.HgCardElevated_cardElevated_M4Ozt')
    print(f"Found {len(cards)} property cards")
    ```
    
    Run the spider again to verify that it correctly identifies the number of property cards on the page.
    
    ---
    
4. **Extract Data from Each Card**
    
    **Step 1**: Inspect the Data to Extract
    For each property card, we want to extract:
    
    **Price**: Inside a `<span>` with the class `HgListingCard_price_JoPAs`.
    
    **Rooms**: Inside a `<span>` within a `<div>` with the class `HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq`.
    
    **Living Space**: Also inside the same `<div>` as the rooms.
    
    **Address**: Inside an `<address>` tag within a `<div>` with the class `HgListingCard_address_JGiFv`.
    
    **Step 2**: Extract Data for One Card
    
    Let’s start by extracting data for the first card to test our selectors:
    
    ```python
    def parse(self, response):
    cards = response.css('.HgCardElevated_cardElevated_M4Ozt')
    
    if cards:
        first_card = cards[0]
        price = first_card.css('span.HgListingCard_price_JoPAs::text').get()
        rooms = first_card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(1) strong::text').get()
        living_space = first_card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(2) strong::text').get()
        address = first_card.css('div.HgListingCard_address_JGiFv address::text').get()
    
        print({
            'Price': price,
            'Rooms': rooms,
            'Living_Space': living_space,
            'Address': address,
        })
    ```
    
    Run the spider to verify that it extracts the data for the first card correctly.
    

---

5. **Extract Data for All Cards**
    
    Now that we’ve tested the selectors for one card, let’s loop through all the cards and extract the data for each one:
    
    ```python
    def parse(self, response):
        cards = response.css('.HgCardElevated_cardElevated_M4Ozt')
    
        for card in cards:
            yield {
                'Price': card.css('span.HgListingCard_price_JoPAs::text').get(),
                'Rooms': card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(1) strong::text').get(),
                'Living_Space': card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(2) strong::text').get(),
                'Address': card.css('div.HgListingCard_address_JGiFv address::text').get(),
            }
    ```
    

Run the spider again. This time, it will extract and print the data for all property cards on the page.

---

6. **Handle Pagination**
    
    To scrape all pages, we need to find the "Next" button and follow it to the next page.
    
    **Step 1**: Find the "Next" Button
    
    Inspect the "Next" button on the page. Suppose it’s an `<a>` tag with the class `HgPaginationSelector_nextPreviousArrow__Mlz2` and an `aria-label="Go to next page"`.
    
    **Step 2**: Extract the "Next" Page URL
    Update the parse function to find the "Next" button and extract its URL:
    
    ```python
    def parse(self, response):
        cards = response.css('.HgCardElevated_cardElevated_M4Ozt')
    
        for card in cards:
            yield {
                'Price': card.css('span.HgListingCard_price_JoPAs::text').get(),
                'Rooms': card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(1) strong::text').get(),
                'Living_Space': card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(2) strong::text').get(),
                'Address': card.css('div.HgListingCard_address_JGiFv address::text').get(),
            }
    
        next_page = response.css('a.HgPaginationSelector_nextPreviousArrow__Mlz2[aria-label="Go to next page"]::attr(href)').get()
        if next_page:
            next_page_url = response.urljoin(next_page)
            yield response.follow(next_page_url, callback=self.parse)
    ```
    
    **Step 3**: How Pagination Works
    
    - The spider extracts the `href` attribute of the "Next" button.
    - If a "Next" button exists, it constructs the full URL using `response.urljoin`.
    - It then follows the URL and calls the parse function again to scrape the next page.

---

7. **Run the Spider and Save the Data**
    
    Finally, run the spider and save the scraped data to a file:
    
    ```bash
    scrapy crawl homegate_spider -o properties.csv
    ```
    
    This will create a `properties.csv` file containing all the scraped data from all pages. The data will be organized into columns based on the keys in the `yield` dictionary (`Price`, `Rooms`, `Living_Space`, and `Address`).
    

---

## 4. Final Spider Code

Here’s the complete code for the spider:

```python
import scrapy

class HomegateSpider(scrapy.Spider):
    name = "homegate_spider"
    allowed_domains = ["homegate.ch"]
    start_urls = ["https://www.homegate.ch/buy/real-estate/canton-zurich/matching-list"]

    def parse(self, response):
        cards = response.css('.HgCardElevated_cardElevated_M4Ozt')

        for card in cards:
            yield {
                'Price': card.css('span.HgListingCard_price_JoPAs::text').get(),
                'Rooms': card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(1) strong::text').get(),
                'Living_Space': card.css('div.HgListingRoomsLivingSpace_roomsLivingSpace_GyVgq span:nth-child(2) strong::text').get(),
                'Address': card.css('div.HgListingCard_address_JGiFv address::text').get(),
            }

        next_page = response.css('a.HgPaginationSelector_nextPreviousArrow__Mlz2[aria-label="Go to next page"]::attr(href)').get()
        if next_page:
            next_page_url = response.urljoin(next_page)
            yield response.follow(next_page_url, callback=self.parse)
```

---

## 5. Conclusion

Congratulations! You’ve successfully built a Scrapy spider to scrape property listings from [Homegate.ch](http://homegate.ch/). By following this guide, you’ve learned how to:

1. Set up a Scrapy project and create a spider.
2. Extract data from web pages using CSS selectors.
3. Handle pagination to scrape multiple pages.
4. Save the scraped data in CSV formats.

Scrapy is a powerful tool that can handle even more complex scraping tasks, such as:

- Logging into websites.
- Handling JavaScript-rendered content (using tools like Splash or Selenium).
- Scraping data from APIs.
- Storing data in databases (e.g., PostgreSQL, MongoDB).

This project is just the beginning. As you continue to work with Scrapy, you’ll discover more advanced features and techniques to tackle even more challenging scraping tasks.
