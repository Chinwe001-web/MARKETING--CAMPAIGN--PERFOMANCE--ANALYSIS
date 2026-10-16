# MARKETING-CAMPAIGN-PERFOMANCE-ANALYSIS
# Marketing Campaign Performance Analysis

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
| `Acquisition_Cost` | Currency text, e.g. "$16,174.00" | Strip `$` and `,`, cast to numeric |
| `Duration` | Text, e.g. "30 days" | Extract the number, cast to integer |

No null values or duplicate `Campaign_ID`s were found. The source file also held two duplicate sheets with the same data, so only one was used. The full script is in `marketing_campaign_postgresql.sql`.

## Key findings

| Question | Finding |
|---|---|
| Best channel by ROI | No clear winner. ROI ranges from 4.99x to 5.02x (ANOVA p = 0.17) |
| Spend vs conversion | No relationship. Correlation = 0.0007, so a 2.6x higher cost per campaign bought no extra conversion |
| Channel by segment | A modest tilt: Foodies and Outdoor Adventurers convert best on Google Ads, Tech Enthusiasts on Website, Health & Wellness on Email, Fashionistas on Instagram |
| Campaign duration | ROI is flat at about 5.0x. Engagement dips very slightly on longer campaigns |
| Company comparison | No real difference in spend or ROI across the five companies (ANOVA p = 0.70) |

Overall averages: ROI 5.00x, conversion rate 8.01%, click-through rate 9.98%.

## Statistical testing
One-way ANOVA (Î± = 0.05) was used to check whether differences between groups are statistically significant.

| Test | P-value | Result |
|---|---|---|
| ROI by channel | 0.1711 | Not significant |
| ROI by company | 0.6950 | Not significant |
| Conversion rate by segment | 0.4634 | Not significant |



## Recommendations
- Do not choose channels or companies on ROI, because the data shows no real gap.
- Do not assume bigger budgets per campaign will lift conversion.
- Use the segment-to-channel pairings only as a tie-breaker when allocating budget.
- Favor shorter campaigns (15 to 30 days). Results are equivalent and budget can be redeployed sooner.

## Limitations
Every cut of the data was statistically flat. This is consistent with a synthetic or randomly generated dataset rather than real campaign results. The findings are reported as they are and in a live business setting "none of these levers makes a significant difference" is itself a useful result.




## Files in this repository
- `marketing_campaign_postgresql.sql`: table creation and cleaning script
- `marketing_campaign_clean.csv`: cleaned dataset
- `ANOVA_ready_data.xlsx`: grouped data for running the ANOVA in Excel
- `images/`: dashboard screenshots

---
*Built by Ibe Chinwe Peace | https://www.linkedin.com/in/chinweibe1/| *

