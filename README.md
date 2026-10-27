# Digital Wellness & Sleep Debt Analytics Dashboard

An interactive business intelligence dashboard built using **Google Looker Studio** to explore the relationships between bedtime phone usage, sleep quality, sleep debt, lifestyle habits, and next-day fatigue.

This project uses a dataset sourced from Kaggle and demonstrates dashboard development, calculated fields, data aggregation, interactive filtering, optional metrics, drill-down analysis, and analytical storytelling.

## Dashboard Preview

### Page 1 — Sleep & Digital Wellness Overview

![Page 1 - Sleep and Digital Wellness Overview](<screenshots/Page 1 - Sleep & Digital Wellness Overview.jpg>)

This page provides a high-level overview of digital wellness and sleep-related metrics.

**Key elements:**
- KPI scorecards for total users, average next-day fatigue, average sleep duration, and average bedtime phone usage.
- User distribution by chronotype.
- Average next-day fatigue comparison across chronotypes.
- Average sleep duration by chronotype and blue-light-filter status.
- Total bedtime phone usage by primary bedtime application.
- Age-group analysis with an optional metric selector and chronotype breakdown.

### Page 2 — Bedtime Habits & Sleep Quality Analysis

![Page 2 - Bedtime Phone Habits and Sleep Quality](<screenshots/Page 2 - Bedtime Phone Habits & Sleep Quality.jpg>)

This page investigates bedtime phone usage and its association with sleep outcomes.

**Key elements:**
- User distribution across bedtime phone usage bands.
- Average phone usage and average fatigue across sleep-latency ranges.
- Scatter plot exploring the relationship between bedtime phone usage and deep sleep duration, including a trendline.

### Page 3 — Lifestyle Factors, Sleep Debt & Fatigue

![Page 3 - Lifestyle Factors, Sleep Debt and Fatigue](<screenshots/Page 3 - Lifestyle Factors, Sleep Debt & Fatigue.jpg>)

This page explores sleep debt alongside occupational and lifestyle factors.

**Key elements:**
- User distribution by sleep-debt category.
- User distribution by occupation.
- Average sleep duration and next-day fatigue by occupation, with drill-down from occupation to sleep-debt category.
- Relationship between evening caffeine intake and deep sleep duration.
- Relationship between alarm snoozing, next-day fatigue, and average sleep duration.
- Average evening caffeine intake and next-day fatigue by sleep-debt category.

## Business Questions

The dashboard was designed to investigate the following questions:

1. What does the overall sleep and digital-wellness profile look like in the dataset?
2. How does bedtime phone usage vary across usage bands and age groups?
3. How are bedtime phone usage, sleep latency, deep sleep, and next-day fatigue associated?
4. How are sleep-debt categories distributed across the dataset?
5. How do sleep-related metrics differ across occupational groups?
6. How are evening caffeine intake and morning alarm snoozing associated with sleep outcomes?

## Key Observations

The following observations describe patterns in the dataset. They should not be interpreted as causal conclusions.

- The dashboard reports **8,500 users**, average sleep duration of **6.3 hours**, average next-day fatigue score of **3.8**, and average bedtime phone usage of **59.3 minutes**.
- The intermediate chronotype is the largest group in the dataset.
- The 31–60 minute bedtime phone usage band contains the largest number of users among the four usage bands.
- The sleep-latency comparison shows higher average phone usage and fatigue in the longer-latency groups.
- The scatter plot suggests a negative association between bedtime phone usage and deep sleep duration, with substantial variation across users.
- The sleep-debt distribution is concentrated in the moderate-debt category.
- In the displayed occupational comparison, the healthcare/shift-worker group has lower average sleep duration and a higher average fatigue score than the other occupational groups.

These findings describe the patterns displayed in the report and are limited to the dataset used for this project.

## Interactive Features

- **Cross-filtering:** Selecting chart elements filters related visualisations, allowing users to explore subsets of the data.
- **Page-level filters:** Gender, age range, and sleep-debt category filters support interactive exploration.
- **Optional metric selector:** The age-group chart switches between average next-day fatigue score and average bedtime phone usage.
- **Chronotype breakdown:** The age-group chart compares results across morning larks, intermediate chronotypes, and night owls.
- **Drill-down analysis:** The occupation chart supports drill-down from occupation to sleep-debt category.
- **Calculated fields and bins:** Custom fields categorise phone usage, convert sleep measurements into minutes, and group continuous variables into ranges.

## Tools & Technologies

- Google Looker Studio
- Data visualisation and dashboard design
- Calculated fields and conditional logic
- Data aggregation and distinct counts
- Interactive filters and cross-filtering
- Optional metrics and drill-down dimensions
- Scatter plots and trendline analysis

## Dataset

**Source:** [Sleep Debt and Screen Time: Late Night Phone Habits — Kaggle](https://www.kaggle.com/datasets/samartalwar/sleep-debt-and-screen-time-late-night-phone-habits)

The original dataset was connected to Looker Studio. Calculated fields and binned dimensions were created within Looker Studio for the analysis.

## Repository Contents

- `README.md` — Project overview, business questions, dashboard screenshots, key observations, and report access.
- `screenshots/` — Screenshots of all three dashboard pages, with a folder-level README.
- `documentation/calculated-fields-and-logic.md` — Calculated fields, binning configurations, optional metric selector, and interactive dashboard logic.
- `Sleep-Debt-Screen-Time-Report.pdf` — Static PDF export of the complete three-page report.

## Access the Report

**Interactive Looker Studio Report:** [Open the interactive dashboard](https://datastudio.google.com/reporting/2e9c5bd1-fbfa-43b4-9bcc-27b6a8c64eee)

**PDF Report:** [View the complete three-page report](Sleep-Debt-Screen-Time-Report.pdf)

The interactive report supports browser-based exploration. The PDF provides a static view of all three pages.

## Limitations

- The dashboard explores distributions and associations; it does not establish causation.
- Average values can conceal individual differences within groups.
- Results depend on the dataset's definitions, sampling, and data quality.
- Binning makes comparisons easier but can conceal variation within ranges.
- Dual-axis charts use different units and scales, so bar heights should not be interpreted as directly comparable quantities.
- The dashboard is an analytical portfolio project, not a medical assessment or source of health advice.

## Author

Created as a business intelligence portfolio project to demonstrate practical dashboard development, data analysis, and analytical storytelling using Google Looker Studio.
