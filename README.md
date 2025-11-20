# Stripe Dataset
Stripe Connect Payout Analysis

Goal: Analyze payout behavior for Stripe Connect platforms, then estimate:
1. Payouts to each country on Jan 1, 2019.
2. Typical daily payout volume in 2019 from three industries under a given platform count scenario.
3. Metrics that product and business teams should track to understand progress and behavior.
   
Data:
* payouts.csv: daily payout amounts in cents, with platform_id and recipient_id.
* countries.csv: maps merchant id to country.
* industries.csv: maps merchant id to industry.
  
Questions to answer:
1. Estimate total payout to each country on Jan 1, 2019, the first day after the dataset ends.
2. Assume that one year after the dataset end there are 15 Education platforms, 5 Hotels Restaurants and Leisure platforms, and 40 Food and Beverage platforms. Estimate the typical daily payout volume in 2019 from these three industries.
3. Propose metrics to help product and business teams monitor Connect health and behavior.

Approach:

Preparation:
* Normalize schemas, check duplicates and missing values, validate date ranges.
* Join payouts to countries and industries through merchant ids, create daily country and industry aggregates, compute platform level features.

Forecast for Jan 1, 2019:
* Build country level daily time series from historical totals.
* Use a baseline method such as seasonal naive or rolling seasonal mean as a starting point; compare against a simple ARIMA or ETS model for stability.
* Select the method per country using cross validation on the last K weeks; report MAE and MAPE; output the country forecast table for Jan 1, 2019.

Industry scenario for 2019:
* Estimate per platform payout intensity for each industry from history, for example median daily payout per active platform after outlier trimming.
* Scale by the assumed platform counts, adjust for seasonality with a monthly or weekly index if required, output the typical daily payout expected for Education, Hotels Restaurants and Leisure, and Food and Beverage, and the total across the three.

Metrics to track:
* Volume: total payouts per day, per country, per industry, per platform.
* Activity: active platforms per day, active recipients per day, activation rate, churn rate.
* Concentration and risk: top N platform share, Herfindahl index of payouts, large payment flags.
* Efficiency and stability: payout volatility, payout failure rate, processing lag from charge to payout, payout success rate by corridor and currency.
* Growth levers: new platform cohort performance, L28 and L90 payout trends, platform lifetime value proxy from payout streams.

Communication:
* Provide a business facing slide deck with plain language takeaways, forecast tables, and clear charts.
* Include caveats and assumptions next to each estimate.

Deliverables:
* notebooks/ or src/: Python or R code for preparation, modeling, and reporting.
* outputs/: forecast tables and charts.
* deck/: slides for a business audience.
* README.md: this document.

Assumptions:
* Payout amounts are final settled values in cents.
* Merchant ids are consistent across files; a merchant may act as a platform or recipient depending on context.
* Scenario counts for 2019 platforms are taken as given; intensity estimates are derived from historical per platform distributions.
* Forecasts are point estimates with error bands; methods are selected for stability and simplicity given time constraints.
