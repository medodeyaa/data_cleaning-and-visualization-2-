# E-commerce Electronic Products Scraping and Data Analysis

## Overview
This project is an end-to-end data pipeline that begins with web scraping electronic products from an e-commerce website, moves through data cleaning, and finishes with Exploratory Data Analysis (EDA) to understand product pricing distributions.

## Libraries and Dependencies
The project is built using Python and requires the following libraries:
* `pandas` - For data manipulation and DataFrame handling.
* `requests` - For making HTTP requests to the target website.
* `bs4` (`BeautifulSoup`) - For parsing HTML and scraping web page elements.
* `matplotlib.pyplot` - For data visualization.
* `seaborn` - For enhanced statistical data visualizations.
* `numpy` - For numerical operations.

## Project Workflow

### 1. Pre-Scraping Verification
Before initiating the scraper, the script sends a request to the target website's `robots.txt` (`https://www.ram-e-shop.com/robots.txt`) to verify that web scraping is permitted.

### 2. Web Scraping Execution
Using `requests` and `BeautifulSoup`, the script iterates through multiple pages (pages 1 to 49) of the e-commerce store's catalog. For each product card, it extracts the following information:
* **Name**: The title of the electronic product.
* **Price**: The listed price of the item.
* **Description (det)**: A brief overview or specific details about the item.
* **Link**: The URL extension directing to the product's individual page.

The extracted raw data (amounting to 1,470 products) is compiled into a pandas DataFrame and successfully saved as `Electronic scraping.csv`.

### 3. Data Cleaning
To prepare the dataset for analysis, the raw data undergoes several cleaning procedures:
* **Price Formatting**: Using Regular Expressions (Regex) `r'[^\d.]'`, non-numeric characters (like currency symbols) are stripped from the `price` column, allowing it to be cast as a `float`.
* **Handling Missing Data**: Any rows containing missing product descriptions (`NaN` values) are dropped from the dataset.
* **Filtering Invalid Entries**: Rows where the description explicitly states "No description" (case-insensitive) are removed to maintain data quality.

### 4. Exploratory Data Analysis (EDA)
With a clean dataset of 891 valid products, the notebook performs price-focused data analysis:
* **Price Range Binning**: Products are categorized into custom price brackets (`0-500`, `500-1000`, `1000-2000`, `2000-5000`, `5000-10000`, `10000-20000`, and `20000+` EGP).
* **Distribution Visualization**: A bar chart is generated using `seaborn` to display the total number of products that fall into each specific price range, highlighting the store's inventory distribution.
* **Pricing Statistics**: Analyzes overall price points across the catalog, checking metrics like minimum price, maximum price, and identifying high-end outlier items (e.g., thermal cameras and AI hardware).

## Execution Instructions
1. Install all required dependencies using `pip install pandas requests beautifulsoup4 matplotlib seaborn numpy`.
2. Run the web scraping cells first if you wish to pull the latest product data, which will generate `Electronic scraping.csv`.
3. Update the local file path in the `pd.read_csv()` function to match the location of your `Electronic scraping.csv` file.
4. Run the data cleaning and EDA cells to generate the cleaned datasets and statistical visualizations.
