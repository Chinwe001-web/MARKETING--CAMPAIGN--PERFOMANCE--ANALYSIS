# MARKETING-CAMPAIGN-PERFOMANCE-ANALYSIS


## Overview
This project analyzes 200,000 marketing campaigns run across 5 companies, 6 channels and 5 customer segments in 2021 (about $2.5B in total ad spend). The goal was to answer five questions a marketing stakeholder would ask before setting next quarter's budget, and to test whether the differences in the data are real or just noise.

## Business questions
1. Which channel delivers the best ROI?
2. Which customer segment are the most responsive?
3. Which locations offer the strongest marketing opportunity?
4. Does higher engangement translate into stronger campaign performance?
5. Which companies are running the most effective campaign?

## Dataset
- **Records:** 200,000 campaigns, 16 columns
- **Period:** 1 Jan 2021 to 31 Dec 2021
- **Dimensions:** Company, Campaign_Type, Target_Audience, Channel_Used, Location,Customer_Segment, Duration
- **KPIs:** Total campaign, Total spend, AVG ROI, AVG Conversion rate, AVG CTR rate
- **Source:** [https://www.kaggle.com/datasets/manishabhatt22/marketing-campaign-performance-dataset]

## Tools
- **PostgreSQL:** table creation and data cleaning
- **Excel:** ANOVA validation (Analysis ToolPak)
- **Power BI:** DAX measures and dashboard

## Data cleaning
Two columns were stored as text and had to be converted before they could be summed or compared:

| Column | Problem | Fix |
|---|---|---|
| `Acquisition cost` | Currency text, e.g. "$16,174.00" | Strip `$` and `,`, changed to numeric |
| `Duration` | Text, e.g. "30 days" | Extracted the number, changed to integer |

No null values or duplicate `Campaign_ID`s were found. The full script is in `marketing_campaign_postgresql.sql`.

## Key findings

| Question | Finding |
|---|---|
| Best channel by ROI | There was no clear winner. ROI ranges from 4.99x to 5.02x (ANOVA p = 0.17) |
| Spend vs conversion | There was no relationship found. Correlation = 0.0007, so a 2.6x higher cost per campaign bought no extra conversion |
| Channel by segment | A modest tilt: Foodies and Outdoor Adventurers convert best on Google Ads, Tech Enthusiasts on Website, Health & Wellness on Email, Fashionistas on Instagram |
| Campaign duration | ROI was flat at about 5.0x. Engagement dips very slightly on longer campaigns |
| Company comparison | There was no  real difference in spend or ROI across the five companies (ANOVA p = 0.70) |

Overall averages: ROI 5.00x, conversion rate 8.01%, click-through rate 9.98%.

## Statistical testing
One-way ANOVA (Î± = 0.05) was used to check whether differences between groups are statistically significant.

| Test | P-value | Result |
|---|---|---|
| ROI by channel | 0.1711 | Not significant |
| ROI by company | 0.6950 | Not significant |
| Conversion rate by segment | 0.4634 | Not significant |



## Recommendations
-  Focus on channels that deliver better returns.Compare ROI and conversion rates across channels before increasing the marketing budget. Small differences alone are not enough to justify a major budget change, so test performance before shifting spend.
- Target the customer segments that respond best. Foodies had the highest average ROI among the customer segments in the initial analysis. Test more campaigns for this group and compare the results with other segments before scaling up.
- Review campaign performance by company. Innovate Industries had the highest average conversion rate, although the differences between companies were small. Look at its strongest campaigns to identify practices that could be useful elsewhere.
- Investigate location-level performance. Miami and Los Angeles showed slightly higher average ROI than New York. Run targeted tests in these locations to see whether the difference is consistent before reallocating budgets.
- Don't assume engagement automatically leads to conversions. Check whether campaigns with higher engagement scores also have stronger conversion rates. Use the findings to improve campaign messages and targeting.
## Limitations
One of the main limitations I faced was that the dataset only covered marketing campaigns from 2021, so the findings might not reflect current market trends. It also lacked some important details, such as actual sales revenue and the number of customers who converted.I also found that some differences in performance were quite small, so I had to be careful not to make strong recommendations based on limited evidence.




## Files in this repository
- `marketing_campaign_postgresql.sql`: table creation and cleaning script
- `marketing_campaign_clean.csv`: cleaned dataset
- `ANOVA_ready_data.xlsx`: grouped data for running the ANOVA in Excel
- `images/`: dashboard screenshots

---
*Built by Ibe Chinwe Peace | https://www.linkedin.com/in/chinweibe1/| *

