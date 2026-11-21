# Online Retail Analysis

From raw transactions to business intelligence: an end-to-end analysis of one year of online retail sales.

The findings are presented as an interactive slide deck (`index.html`). The full analysis is in the notebook `Online_Retail_Full_Data_Analysis.ipynb`.

## Objective

To identify which products, countries, months and customers generate revenue, and to assess how reliable the raw transaction data is before drawing conclusions.

## Dataset

[Online Retail, Kaggle](https://www.kaggle.com/datasets/vijayuv/onlineretail): 541,909 invoice lines and 8 columns, covering December 2010 to early December 2011.

| Measure | Value |
|---|---|
| Invoices | 25,900 |
| Customer IDs | 4,372 |
| Product codes | 4,070 |
| Countries | 38 |
| Share of lines from the United Kingdom | 91.4% |

Each row is one product line on one invoice.

## Data quality

| Issue | Extent |
|---|---|
| Missing customer ID | 135,080 lines (24.9%) |
| Exact duplicate lines | 5,268 (1.0%) |
| Negative quantities | 10,624 lines, of which 9,288 are on cancellation invoices |
| Zero unit price | 2,515 lines |
| Negative unit price | 2 lines, both "Adjust bad debt" entries |
| Product codes with several descriptions | 650 |
| Non-product codes in the data | Discount, bad-debt adjustment, postage, manual entries |

## Cleaning decisions

- Removed only exact duplicates (541,909 to 536,641 lines), since repeated lines would inflate sales.
- Filled 1,342 missing descriptions using the most common description for the same product code. 112 remain missing.
- Kept lines without a customer ID. They are valid for sales, product, country and time analysis and are excluded only from customer analysis.
- Kept and flagged cancellations, negative quantities and unusual prices, so that returns reduce revenue instead of disappearing.
- Defined revenue as quantity multiplied by unit price, with date features added for time analysis.

## Findings

**Revenue.** Gross sales are 10,642,110.80. Cancellations remove 893,979.73 (8.4%), and two bad-debt entries remove a further 22,124.12, giving net revenue of 9,726,006.95.

**Products.** Only 5 of the top 10 products by units sold are also in the top 10 by revenue. Postage and manual entries rank among the top earners (31% of the top-10 revenue total), so they were separated from real products. The top real product by revenue is the Regency Cakestand 3 Tier (174,156.54).

**Returns.** Cancellations are 1.7% of lines but 14.8% of invoices (3,836 of 25,900). The two best-selling products by units were almost entirely returned: 80,995 units sold and 80,995 returned for one, 78,033 sold and 74,494 returned for the other. This suggests large orders that were reversed, which overstates their demand.

**Invoices.** The 99th percentile of invoice value is 4,106.87, and 259 invoices (1.0%) exceed it. The largest invoice is 168,469.60 for a single product.

**Countries.** The United Kingdom contributes 84.6% of sales revenue (8,979,619.97). The next four countries (Netherlands, Ireland, Germany, France) together contribute 9.5%.

**Time.** Monthly revenue rose from September to November 2011, peaking at 1,456,145.80. September to November accounts for 36% of the 13 months analysed.

**Customers.** The top 10 customers account for 14.1% of net revenue. They fall into two patterns: frequent smaller orders (customer 14911: 248 invoices, about 534 each) and infrequent large orders (customer 12415: 26 invoices, about 4,759 each).

## Recommendations

1. Report products separately from postage and manual entries.
2. Rank products after returns rather than before.
3. Validate the autumn peak against a second year of data.
4. Treat frequent and large-order customers differently.
5. Investigate why a quarter of lines have no customer ID.

These are proposals drawn from the analysis and have not been implemented.

## Limitations

- Country-level invoice counts and average invoice values in the notebook are unreliable (every country shows the same count), so only country revenue is reported.
- December 2011 is a partial month, and its low revenue does not indicate a decline.
- One year of data cannot separate seasonality from growth.
- Product rankings are based on sales lines before returns.
- Interpretations and recommendations are the author's reading of the data and are not proven by it.

## Tools

Python, pandas, Matplotlib, Seaborn and Plotly for the analysis. The presentation is plain HTML, CSS and JavaScript.
