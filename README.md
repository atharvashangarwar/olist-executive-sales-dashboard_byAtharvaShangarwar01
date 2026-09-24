# Executive Sales Dashboard & Decision Report

An end-to-end data analysis project on the **Olist Brazilian E-Commerce** dataset. It moves from **Data → Information → Insight → Decision → Action**: instead of showing many charts, it builds a decision dashboard that tells a CEO whether the business is healthy, what could go wrong, and what to do next.

**Author:** Atharva Shangarwar

## Dataset

[Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

About 100k orders (2016 to 2018) across linked tables: orders, order items, customers, products, reviews, payments, sellers and geolocation. This project uses six of them:

| File | Used for |
|---|---|
| `olist_orders_dataset.csv` | Order status, purchase and delivery dates |
| `olist_order_items_dataset.csv` | Price and freight per item |
| `olist_customers_dataset.csv` | Customer state and unique customer ID |
| `olist_products_dataset.csv` | Product category |
| `product_category_name_translation.csv` | English category names |
| `olist_order_reviews_dataset.csv` | Review scores |

The dataset is not included in this repository. Download it from Kaggle (link above).

## Project description

**Business question:** Is the business healthy, what could go wrong, and what should management do?

The analysis follows the 5-level dashboard hierarchy: KPIs (what is happening) → Trends (how is it changing) → Drivers (why) → Risk (what could go wrong) → Action (what should we do).

**Main steps**
1. Load and inspect the tables
2. Clean the data (delivered orders only, Jan 2017 to Aug 2018, remove duplicates)
3. Merge tables into an order-level table
4. Calculate executive KPIs: Revenue, Orders, Customers, Average Order Value, YoY Growth %, On-time delivery %
5. Analyse sales by category and state
6. Analyse risk: late deliveries vs review scores, and high-value customers inactive for 180+ days
7. Write insights in the Fact → Insight → Opportunity → Action format
8. Export CSVs for a 3-page dashboard (Executive Overview, Sales & Product, Customer & Risk)

**Note:** Olist has no Profit column, so Revenue means item price without freight.

## Technologies used

- Python 3.9+
- pandas, NumPy, matplotlib
- Jupyter Notebook
- Power BI or Tableau Public (dashboard)

## Setup and run

**Option A: Google Colab (recommended)**

1. Download the dataset from Kaggle (link above) and unzip it.
2. Open `AJ_OlistExecutiveDashboard.ipynb` in [Google Colab](https://colab.research.google.com/) (File → Upload notebook).
3. Open the Files panel on the left and drag all 9 CSV files into the `/content` folder.
4. Choose **Runtime → Run all**.

The notebook reads the files from `/content` and creates a `dashboard/` folder with the CSV files and a `dashboard/charts/` folder with PNG charts. Colab deletes files when the session ends, so download `dashboard/` before you close it.

**Option B: run locally**

```bash
git clone <your-repo-url>
cd <your-repo-folder>
pip install -r requirements.txt
jupyter notebook AJ_OlistExecutiveDashboard.ipynb
```

For a local run, change the `/content/` paths in the "Load the data" cell to the folder where you saved the CSV files.


## Dashboard
Interactive Tableau Public dashboard: https://public.tableau.com/app/profile/atharva.shangarwar/viz/OlistExecutiveDashboard_17902429603740/ExecutiveOverview


## Project structure

```
├── AJ_OlistExecutiveDashboard.ipynb   # Complete analysis code
├── requirements.txt                   # Python dependencies
├── AJ_ProjectReport.docx              # Project report
├── README.md
└── dashboard/                         # Output CSVs and charts (created on run)
```

## Key information

- Customers are counted by `customer_unique_id`, because `customer_id` changes with every order.
- Growth % compares the same months (Jan to Aug) in 2018 and 2017.
- "Churn risk" means high-value customers (top 20% by spend) with no order for 180+ days.
- All insight sentences in the notebook are generated from the computed numbers.
