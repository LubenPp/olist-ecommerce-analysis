# Olist e-commerce: late deliveries and bad reviews

An exploratory analysis of the Olist Brazilian e-commerce dataset. The question: **do late deliveries lead to bad reviews?**

## Dataset

[Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Kaggle): 9 linked tables covering orders, items, payments, reviews, customers, sellers, products, geolocation and category names.

The data is not included in this repo. Download it and put the CSV files in `data/archive/`.

## Main finding

Orders delivered after the promised date got a bad review (1-2 stars) **62%** of the time, compared with **9%** for on-time orders (95,545 delivered orders with a review, Jan 2017 - Aug 2018). The share of bad reviews rises with the delay:

| Delivery vs promised date | Bad reviews |
|---|---|
| Early | 9% |
| 1-3 days late | 32% |
| 4-7 days late | 68% |
| 8+ days late | 79% |

## Other results

- Orders and revenue grew fast through 2017 and then plateaued in 2018.
- About 97% of customers ordered only once.
- Late orders are about 7% of orders but about a third of all bad reviews. The other two thirds come from on-time orders, so delivery is a big driver, not the only one.
- Rio de Janeiro (RJ) has a late-delivery rate of about 12%, against 4-6% in the other four biggest states, and more bad reviews. Its freight cost is typical, so shipping price does not explain it.

## Method

- Cleaned the `orders` table: dropped 23 orders marked "delivered" with missing dates. Other missing dates (canceled or unfinished orders) were left as they are.
- Kept the latest review when an order had several.
- "Bad" review = 1-2 stars, 3 stars = neutral, 4-5 stars = good.
- "Late" = delivered on a later day than Olist's estimated delivery date.
- The data is complete only from Jan 2017 to Aug 2018, so the analysis is limited to that period.

## Limits

- Correlation, not causation: a bad seller could cause both a late delivery and a bad review.
- "Late" is measured against Olist's own estimate, not against an absolute delivery time.
- Only orders with a review are included in the review analysis.

## How to run

1. Download the dataset and put the CSV files in `data/archive/`.
2. Install the requirements: `pip install pandas matplotlib jupyter`
3. Open `olist.ipynb` in Jupyter and run all cells.