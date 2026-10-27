# Calculated Fields & Dashboard Logic

This document explains the calculated fields, binning configurations, metric selection, aggregations, and interactive behaviour used in the **Digital Wellness & Sleep Debt Analytics Dashboard** built with Google Looker Studio.

## 1. Calculated Fields

### 1.1 Bed-time Phone Usage Band

**Purpose:** Categorises bedtime phone usage into four bands to make it easier to compare users across different levels of bedtime phone activity.

**Formula:**

```text
IF(
  bedtime_phone_minutes <= 30,
  "0 - 30 min",
  IF(
    bedtime_phone_minutes <= 60,
    "31 - 60 min",
    IF(
      bedtime_phone_minutes <= 90,
      "61 - 90 min",
      "Above 90 min")))
```

**Categories produced:**

| Condition | Category |
|---|---|
| `bedtime_phone_minutes <= 30` | 0 - 30 min |
| `bedtime_phone_minutes > 30` and `<= 60` | 31 - 60 min |
| `bedtime_phone_minutes > 60` and `<= 90` | 61 - 90 min |
| `bedtime_phone_minutes > 90` | Above 90 min |

**Used in:** Page 2 — *Bedtime Habits & Sleep Quality Analysis*, in the chart showing the number of users by bedtime phone usage band.

### 1.2 Total Sleep Min

**Purpose:** Converts total sleep duration from hours to minutes so that it can be compared with other sleep measurements recorded in minutes.

**Formula:**

```text
total_sleep_hours * 60
```

**Logic:** One hour contains 60 minutes. Multiplying the source field by 60 converts the duration to minutes.

**Used in:** Calculations for deep sleep duration and REM sleep duration.

### 1.3 Deep Sleep Min

**Purpose:** Estimates the duration of deep sleep in minutes from the total sleep duration and the percentage of sleep attributed to deep sleep.

The source field `deep_sleep_pct` represents the percentage of total sleep spent in deep sleep.

**Formula:**

```text
(total_sleep_min * deep_sleep_pct) / 100
```

**Logic:** Total sleep duration in minutes is multiplied by the deep-sleep percentage and divided by 100.

**Example:** If total sleep duration is 360 minutes and deep sleep accounts for 20% of that duration, the calculated deep sleep duration is 72 minutes.

**Used in:** Page 2 — the scatter plot exploring the relationship between bedtime phone usage and deep sleep duration; and Page 3 — the scatter plot exploring evening caffeine intake and deep sleep duration.

### 1.4 REM Sleep Min

**Purpose:** Estimates the duration of REM sleep in minutes from the total sleep duration and the percentage of sleep attributed to REM sleep.

The source field `rem_sleep_pct` represents the percentage of total sleep spent in REM sleep.

**Formula:**

```text
(total_sleep_min * rem_sleep_pct) / 100
```

**Logic:** Total sleep duration in minutes is multiplied by the REM-sleep percentage and divided by 100.

**Used for:** Converting the source REM-sleep percentage into a duration expressed in minutes.

### 1.5 Sleep Latency Min Band

**Purpose:** Groups sleep-latency values into numeric intervals to support comparisons across latency ranges.

**Configuration:**

| Setting | Value |
|---|---|
| Binning method | Numeric bins |
| Bin size | 30 |
| Minimum observed value | 6 |
| Maximum observed value | 123.3 |

The minimum and maximum values were obtained automatically from the data.

**Used in:** Page 2 — *Bedtime Habits & Sleep Quality Analysis*, in the chart comparing average bedtime phone usage and average next-day fatigue across sleep-latency ranges.

### 1.6 Age Range

**Purpose:** Groups users into five-year age intervals to support age-group comparisons.

**Configuration:**

| Setting | Value |
|---|---|
| Binning method | Numeric bins |
| Bin size | 5 |
| Minimum age | 18 |
| Maximum age | 65 |

**Used in:** Page 1 — *Sleep & Digital Wellness Overview*, in the chart comparing the selected metric across age groups and chronotypes.

---

## 2. Optional Metric Selector

The age-group chart on Page 1 includes an optional metric selector that allows viewers to switch between two metrics.

**Available metrics:**

- Average `next_day_fatigue_score`
- Average `bedtime_phone_minutes`

**Chart configuration:**

| Setting | Field or value |
|---|---|
| Dimension | `Age Range` |
| Breakdown dimension | `chronotype` |
| Primary metric | Average `next_day_fatigue_score` |
| Optional metric | Average `bedtime_phone_minutes` |

The selector allows viewers to examine fatigue scores or bedtime phone usage across age groups, with results broken down by chronotype.

Because fatigue scores and phone usage are measured in different units, the selected metric should be interpreted independently. Their values should not be compared directly as if they shared a common scale.

---

## 3. Interactive Dashboard Behaviour

### 3.1 Cross-Filtering

Cross-filtering is enabled on the report charts.

When viewers select a chart element, related visualisations can be filtered to focus on the selected subset of data. This allows users to explore relationships between categories and metrics without creating a separate report for every combination.

### 3.2 Page-Level Filters

The report includes the following controls:

- Gender
- Age range
- Sleep-debt category

These controls allow viewers to explore the displayed metrics for selected groups.

### 3.3 Drill-Down Analysis

The occupation chart on Page 3 supports drill-down in the following order:

1. Occupation
2. Sleep-debt category

This hierarchy lets viewers begin with an occupational comparison and then examine the data at the sleep-debt-category level.

The interactive drill-down behaviour is available in the Looker Studio report. A static PDF export does not preserve the interactive controls.

---

## 4. Aggregation Logic

Different aggregation methods are used depending on the analytical question.

| Analytical question | Field or metric | Aggregation |
|---|---|---|
| How many distinct users are represented? | `user_id` | Count Distinct |
| What is the average sleep duration? | `total_sleep_hours` | Average |
| What is the average next-day fatigue score? | `next_day_fatigue_score` | Average |
| What is the average bedtime phone usage? | `bedtime_phone_minutes` | Average |
| What is the average evening caffeine intake? | `caffeine_post_5pm_mg` | Average |
| What is the average sleep outcome within a category? | Relevant sleep metric | Average |

Distinct user counts are used for user-distribution charts. Averages are used for comparisons of typical values across groups.

The aggregation must match the business question. For example, average bedtime phone usage describes typical usage per record, whereas a sum describes the total recorded minutes across records.

---

## 5. Interpretation and Data-Quality Considerations

### 5.1 Average Fatigue by Chronotype

The report explores differences in average next-day fatigue scores across chronotypes.

If the averages are displayed as percentages of their combined sum, the percentages represent each chronotype's share of the sum of the group-average scores. They do not represent the percentage of users in each chronotype or the share of all individual fatigue observations.

### 5.2 Scatter Plots and Trendlines

Scatter plots are used to explore relationships between numeric variables, including:

- Bedtime phone usage and deep sleep duration.
- Evening caffeine intake and deep sleep duration.
- Alarm snoozing, fatigue, and sleep duration.

Trendlines indicate the overall direction of a relationship in the displayed data. They do not establish causation, and a visible trendline alone does not establish the statistical strength or significance of the relationship.

### 5.3 Binning

Numeric bins simplify continuous fields by grouping values into intervals. This makes category comparisons easier but can conceal variation among observations within each interval.

### 5.4 Dual-Axis Charts

Some charts compare metrics with different units, such as sleep duration in hours and fatigue scores. Where separate axes are used, the bar heights should not be interpreted as directly comparable quantities.

### 5.5 Simulated Dataset

The dashboard uses the original dataset from Kaggle, connected to Looker Studio, with calculated fields and binned dimensions created in Looker Studio.

The findings describe patterns within this dataset. They should not be interpreted as medical advice or proof that any particular behaviour causes a sleep outcome.

---

## 6. Data Source

**Dataset:** [Sleep Debt and Screen Time: Late Night Phone Habits — Kaggle](https://www.kaggle.com/datasets/samartalwar/sleep-debt-and-screen-time-late-night-phone-habits)

The original dataset was used without modifying the source data. Calculated fields and binning configurations were created in Looker Studio to support the analysis.
