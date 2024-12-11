## **Workshop on Web Scraping with Scrapy**

### **Introduction**

#### **What is Web Scraping?**
Web scraping is the process of extracting data from websites and converting it into a structured format like CSV, JSON, or databases.

**Why is Web Scraping Important?**
- Automates data collection from websites.
- Saves time and effort compared to manual data entry.
- Enables large-scale data gathering for analysis, market research, and application development.

**Applications:**
- Price monitoring and comparison.
- Sentiment analysis and social media monitoring.
- Content aggregation for blogs or apps.

---

### **Introduction to Scrapy**

#### **What is Scrapy?**
Scrapy is an open-source Python-based web scraping framework that simplifies the process of extracting data from websites.

**Why Use Scrapy?**
- Fast, efficient, and asynchronous.
- Provides built-in tools for crawling, data extraction, and processing.
- Highly customizable and extendable.

**Key Features:**
1. Support for asynchronous requests.
2. Built-in selectors for structured data extraction.
3. Flexible pipelines for data storage and processing.
4. Well-documented and supported by a strong community.

---

### **Key Components of Scrapy**

#### **1. Spiders**
- Custom scripts to define how and where to scrape data.

#### **2. Selectors**
- XPath and CSS Selectors for extracting specific elements from web pages.

#### **3. Pipelines**
- Process and store scraped data (e.g., cleaning, exporting).

#### **4. Items**
- Defines the structure of the data to be scraped, ensuring consistency and organization.

---

### **How Scrapy Works**

#### **Workflow:**
1. **Sending Requests:** Scrapy sends requests to target URLs.
2. **Receiving Responses:** It fetches the HTML of the pages.
3. **Extracting Data:** Uses spiders to parse and extract required data fields.
4. **Pipelines:** Processes and stores the extracted data.

---

### **Setting Up Scrapy**

#### **Requirements:**
1. Python 3.x
2. pip (Python package manager)

#### **Installation:**
```bash
pip install scrapy
```

#### **Starting a New Project:**
```bash
scrapy startproject myproject
```

**Project Structure Overview:**
- `spiders/`: Custom spiders for scraping.
- `items.py`: Defines data structure.
- `pipelines.py`: Processes scraped data.

---

### **Writing Your First Spider**

#### **Example: Scraping Quotes Website**

**Define a Spider:**
```python
import scrapy

class QuotesSpider(scrapy.Spider):
    name = "quotes"
    start_urls = ["http://quotes.toscrape.com"]

    def parse(self, response):
        for quote in response.css(".quote"):
            yield {
                'text': quote.css("span.text::text").get(),
                'author': quote.css("span small.author::text").get(),
                'tags': quote.css("div.tags a.tag::text").getall(),
            }
```

**Run the Spider:**
```bash
scrapy crawl quotes
```

---

### **Handling Complex Scraping Scenarios**

#### **1. Pagination:**
- Handling multi-page data with next-page links.
- Example Code:
```python
next_page = response.css("a.next::attr(href)").get()
if next_page:
    yield response.follow(next_page, self.parse)
```

#### **2. Authentication:**
- Sending login credentials for protected pages.
- Using Scrapy FormRequest.

#### **3. Avoiding Blocks:**
- Rotate User Agents and IP addresses.
- Add delays using `DOWNLOAD_DELAY`.

---

### **Storing Scraped Data**

#### **Built-in Storage Options:**
- Export data to CSV, JSON, or XML using command-line options.
- Example:
```bash
scrapy crawl quotes -o quotes.json
```

#### **Using Pipelines:**
- Store data directly in databases (e.g., MongoDB, PostgreSQL).

---

### **Best Practices for Web Scraping**

1. Respect website’s `robots.txt` and terms of service.
2. Avoid overloading servers with frequent requests.
3. Use proper headers and user agents to avoid detection.
4. Test your spiders regularly for broken selectors or structure changes.

---

### **Conclusion**

#### **Key Takeaways:**
- Scrapy is a versatile framework for efficient web scraping.
- Understand the core components: spiders, selectors, pipelines.
- Follow best practices for ethical and effective scraping.

**Questions?** Feel free to ask!