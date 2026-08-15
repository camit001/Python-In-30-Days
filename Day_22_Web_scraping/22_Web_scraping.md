<div align="center">
  <h1>Python In 30 Days: Day 22 - Web Scraping</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>
</div>

[<< Day 21](../Day_21_Classes_and_objects/21_Classes_and_objects.md) | [Day 23 >>](../Day_23_Virtual_environment/23_Virtual_environment.md)

**Python In 30 Days**

- [📘 Day 22](#-day-22)
  - [Python Web Scraping](#python-web-scraping)
    - [What is Web Scraping](#what-is-web-scraping)
    - [Installing Required Packages](#installing-required-packages)
    - [Sending an HTTP Request](#sending-an-http-request)
    - [Parsing HTML with BeautifulSoup](#parsing-html-with-beautifulsoup)
    - [Finding HTML Elements](#finding-html-elements)
    - [CSS Selectors](#css-selectors)
    - [Extracting Links](#extracting-links)
    - [Extracting Tables](#extracting-tables)
    - [Handling Request Errors](#handling-request-errors)
    - [Respectful and Responsible Scraping](#respectful-and-responsible-scraping)
    - [Practical Data Engineering Example](#practical-data-engineering-example)
  - [💻 Exercises: Day 22](#-exercises-day-22)

# 📘 Day 22

## Python Web Scraping

### What is Web Scraping

The internet contains a huge amount of information that can be collected for many legitimate purposes. **Web scraping** is the process of programmatically requesting web pages, extracting useful information from their HTML or other response formats, and storing the results for later use.

A simple scraping workflow looks like this:

```text
Website
   ↓
HTTP Request
   ↓
HTML Response
   ↓
Parse HTML
   ↓
Find Required Data
   ↓
Clean Data
   ↓
Save as JSON / CSV / Database
```

In this lesson we use the `requests` and `BeautifulSoup` packages.

> **Important:** Always check a website's terms of service, `robots.txt`, rate limits, and applicable laws before scraping. Do not bypass authentication, access controls, CAPTCHAs, or other technical restrictions.

---

## Installing Required Packages

Install the required packages with:

```sh
python -m pip install requests beautifulsoup4
```

Check that the packages are installed:

```sh
python -m pip show requests
python -m pip show beautifulsoup4
```

Import them:

```py
import requests
from bs4 import BeautifulSoup
```

---

## Sending an HTTP Request

We can use `requests.get()` to retrieve a web page.

```py
import requests

url = "https://example.com"

response = requests.get(url, timeout=10)

print(response.status_code)
```

A status code of `200` generally means that the request succeeded.

We can inspect other useful response properties:

```py
print(response.status_code)
print(response.url)
print(response.headers.get("content-type"))
print(response.text[:200])
```

### Use a Timeout

Always consider specifying a timeout for network requests.

```py
response = requests.get(
    "https://example.com",
    timeout=10
)
```

Without a timeout, a network request can wait indefinitely in some failure situations. Computers already have enough opportunities to waste our time.

---

## Parsing HTML with BeautifulSoup

BeautifulSoup parses HTML and gives us convenient methods for finding elements.

```py
import requests
from bs4 import BeautifulSoup

url = "https://example.com"

response = requests.get(url, timeout=10)
response.raise_for_status()

soup = BeautifulSoup(response.text, "html.parser")

print(soup.title)
print(soup.title.get_text(strip=True))
```

Output:

```text
<title>Example Domain</title>
Example Domain
```

`response.raise_for_status()` raises an exception when the HTTP request returns an unsuccessful status code.

---

## Finding HTML Elements

### Find the First Matching Element

```py
heading = soup.find("h1")

print(heading)
print(heading.get_text(strip=True))
```

### Find All Matching Elements

```py
paragraphs = soup.find_all("p")

for paragraph in paragraphs:
    print(paragraph.get_text(strip=True))
```

### Find by Class

```py
items = soup.find_all("div", class_="item")

for item in items:
    print(item.get_text(" ", strip=True))
```

### Find by ID

```py
element = soup.find("div", id="main-content")

if element:
    print(element.get_text(" ", strip=True))
```

---

## CSS Selectors

BeautifulSoup supports CSS selectors through `select()` and `select_one()`.

```py
headings = soup.select("h1")

for heading in headings:
    print(heading.get_text(strip=True))
```

Select a class:

```py
items = soup.select(".item")
```

Select an ID:

```py
content = soup.select_one("#main-content")
```

Select links inside a navigation element:

```py
links = soup.select("nav a")

for link in links:
    print(link.get_text(strip=True))
```

CSS selectors are useful when the HTML structure is more complex than a simple `find()` call.

---

## Extracting Links

HTML links are represented by the `<a>` tag.

```py
import requests
from bs4 import BeautifulSoup

url = "https://example.com"

response = requests.get(url, timeout=10)
response.raise_for_status()

soup = BeautifulSoup(response.text, "html.parser")

for link in soup.find_all("a"):
    text = link.get_text(" ", strip=True)
    href = link.get("href")

    print(text, href)
```

### Extract Only Links with URLs

```py
for link in soup.find_all("a", href=True):
    print(link.get_text(" ", strip=True))
    print(link["href"])
```

The `href=True` condition ensures that only `<a>` elements containing an `href` attribute are returned.

---

## Extracting Tables

Tables are commonly used to present structured data.

Example HTML:

```html
<table>
    <tr>
        <th>Name</th>
        <th>City</th>
    </tr>
    <tr>
        <td>Amit</td>
        <td>Mumbai</td>
    </tr>
    <tr>
        <td>Priya</td>
        <td>Pune</td>
    </tr>
</table>
```

We can extract the rows:

```py
table = soup.find("table")

for row in table.find_all("tr"):
    cells = row.find_all(["th", "td"])

    values = [
        cell.get_text(" ", strip=True)
        for cell in cells
    ]

    print(values)
```

Output:

```text
['Name', 'City']
['Amit', 'Mumbai']
['Priya', 'Pune']
```

---

## Converting a Table to Dictionaries

A useful next step is to convert table rows into dictionaries.

```py
table = soup.find("table")

headers = [
    cell.get_text(" ", strip=True)
    for cell in table.find_all("th")
]

records = []

for row in table.find_all("tr")[1:]:
    cells = row.find_all("td")

    values = [
        cell.get_text(" ", strip=True)
        for cell in cells
    ]

    if len(values) == len(headers):
        records.append(dict(zip(headers, values)))

print(records)
```

Output:

```py
[
    {"Name": "Amit", "City": "Mumbai"},
    {"Name": "Priya", "City": "Pune"}
]
```

This structure is much easier to save as JSON, CSV, or load into a database.

---

## Saving Scraped Data as JSON

```py
import json

with open(
    "employees.json",
    "w",
    encoding="utf-8"
) as file:
    json.dump(
        records,
        file,
        indent=4,
        ensure_ascii=False
    )
```

### Saving as CSV

```py
import csv

if records:
    with open(
        "employees.csv",
        "w",
        encoding="utf-8",
        newline=""
    ) as file:

        writer = csv.DictWriter(
            file,
            fieldnames=records[0].keys()
        )

        writer.writeheader()
        writer.writerows(records)
```

---

## Handling Request Errors

Network requests can fail for many reasons.

```py
import requests

try:
    response = requests.get(
        "https://example.com",
        timeout=10
    )

    response.raise_for_status()

except requests.exceptions.Timeout:
    print("The request timed out.")

except requests.exceptions.ConnectionError:
    print("Could not connect to the website.")

except requests.exceptions.HTTPError as error:
    print("HTTP error:", error)

except requests.exceptions.RequestException as error:
    print("Request failed:", error)
```

Handling specific exceptions makes debugging and production code much easier.

---

## Request Headers

Some websites return different responses depending on the HTTP headers.

A simple request can include a descriptive User-Agent:

```py
import requests

headers = {
    "User-Agent": "Python-In-30-Days-Learning-Project/1.0"
}

response = requests.get(
    "https://example.com",
    headers=headers,
    timeout=10
)

print(response.status_code)
```

Do not use headers to impersonate a browser for the purpose of bypassing a site's protections.

---

## Scraping Multiple Pages

If a website has predictable page URLs, a loop can process multiple pages.

```py
import requests
from bs4 import BeautifulSoup

for page_number in range(1, 4):
    url = f"https://example.com/page/{page_number}"

    response = requests.get(
        url,
        timeout=10
    )

    if response.status_code != 200:
        print("Could not fetch:", url)
        continue

    soup = BeautifulSoup(
        response.text,
        "html.parser"
    )

    print("Processed:", url)
```

When scraping multiple pages, keep the request rate reasonable and follow the website's rules.

---

## Respectful and Responsible Scraping

Before scraping a website:

1. Read its terms of service.
2. Check its `robots.txt`.
3. Look for an official API.
4. Respect rate limits.
5. Add reasonable delays when appropriate.
6. Do not bypass authentication or access controls.
7. Do not overload the website with requests.
8. Store only the data you actually need.
9. Respect copyright, privacy, and applicable laws.
10. Prefer public datasets or official APIs when they are available.

A scraper should behave like a polite visitor, not like a very enthusiastic denial-of-service attack.

---

## When Web Scraping Is Not the Best Choice

If a website provides an official API, using the API is often better than scraping HTML.

For example:

```text
Official API
    ↓
Structured JSON
    ↓
Python
    ↓
Data Processing
```

is usually more reliable than:

```text
HTML
    ↓
CSS Selectors
    ↓
HTML Changes
    ↓
Scraper Breaks
```

APIs generally provide structured data and documented endpoints, while HTML layouts can change without warning.

---

## Practical Data Engineering Example

Web scraping can be one source in an ETL pipeline.

```text
Website
   ↓
requests
   ↓
BeautifulSoup
   ↓
Extract
   ↓
Clean
   ↓
Validate
   ↓
JSON / CSV
   ↓
Database / Data Lake
```

Example:

```py
import json
import requests
from bs4 import BeautifulSoup

url = "https://example.com"

response = requests.get(
    url,
    timeout=10
)

response.raise_for_status()

soup = BeautifulSoup(
    response.text,
    "html.parser"
)

records = []

for link in soup.find_all("a", href=True):
    records.append({
        "title": link.get_text(" ", strip=True),
        "url": link["href"]
    })

with open(
    "scraped_links.json",
    "w",
    encoding="utf-8"
) as file:
    json.dump(
        records,
        file,
        indent=4,
        ensure_ascii=False
    )

print(f"Saved {len(records)} records.")
```

In a production data pipeline, the output could then be uploaded to ADLS, loaded into a database, or processed by Spark/Databricks.

---

## Practical Tips for Reliable Scrapers

### Use Functions

Instead of putting everything in one large script:

```py
def fetch_page(url):
    response = requests.get(url, timeout=10)
    response.raise_for_status()
    return response.text


def parse_titles(html):
    soup = BeautifulSoup(html, "html.parser")

    return [
        heading.get_text(" ", strip=True)
        for heading in soup.find_all("h2")
    ]


html = fetch_page("https://example.com")
titles = parse_titles(html)

print(titles)
```

### Keep Extraction Separate from Storage

A useful design is:

```text
fetch()
   ↓
parse()
   ↓
clean()
   ↓
save()
```

This makes the code easier to test and maintain.

---

## 💻 Exercises: Day 22

### Exercises: Level 1

1. Install `requests` and `beautifulsoup4`.
2. Send a GET request to `https://example.com` and print the status code.
3. Print the page title using BeautifulSoup.
4. Extract all `<h1>` and `<h2>` headings from a page.
5. Extract all links from a page and print their text and URLs.
6. Find elements by class and by ID.
7. Use CSS selectors to extract a group of elements.

### Exercises: Level 2

1. Scrape a publicly available website and store selected data as a JSON file.
2. Extract a table from a publicly available HTML page and convert it into a list of dictionaries.
3. Save the extracted table to both JSON and CSV.
4. Handle `Timeout`, `ConnectionError`, and `HTTPError`.
5. Write a function named `fetch_page()` that accepts a URL and returns HTML.
6. Write a function named `extract_links()` that accepts HTML and returns a list of links.
7. Use `enumerate()` to add a sequence number to each scraped record.

### Exercises: Level 3

1. Build a scraper with separate `fetch()`, `parse()`, `clean()`, and `save()` functions.
2. Scrape multiple pages using a loop and combine their results.
3. Remove duplicate records before saving.
4. Add a timestamp to every scraped record.
5. Store the final data as JSON and CSV.
6. Add exception handling so one failed page does not stop the entire process.
7. Add a reasonable delay between requests.
8. Build a small ETL-style scraper that extracts public data, cleans it, validates it, and writes the final dataset to a file.

### Exercises: Level 4 - Data Engineering

1. Create a scraper that produces records with the following structure:

```py
{
    "source": "website",
    "title": "...",
    "url": "...",
    "scraped_at": "..."
}
```

2. Save the records as JSON.
3. Save the same records as CSV.
4. Add a unique record ID.
5. Remove duplicate URLs.
6. Create an error log containing failed URLs and error messages.
7. Create an output folder and archive previously processed files.
8. Design the scraper as:

```text
Extract
  ↓
Validate
  ↓
Transform
  ↓
Deduplicate
  ↓
Load
```

9. Explain why an official API might be preferable to scraping the same website.
10. Explain how you would schedule this scraper as part of an ADF or Databricks data pipeline.

🎉 CONGRATULATIONS! 🎉

[<< Day 21](../Day_21_Classes_and_objects/21_Classes_and_objects.md) | [Day 23 >>](../Day_23_Virtual_environment/23_Virtual_environment.md)
