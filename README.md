# DataCo Global Operations Analytics Using Chi-Square

**A supply chain analytics project investigating late deliveries and evaluating the relationship between shipping mode and delivery delays.**

This project analyzes DataCo Global's order and shipping records to identify patterns in delivery performance, test whether selected business factors are associated with late delivery, and develop operational recommendations based on the findings.

## Project Overview

Late deliveries can undermine customer experience and trust. This project examines the delivery performance of DataCo Global and investigates whether delivery delays are associated with shipping mode, product department, customer segment, or market.

The analysis uses exploratory data analysis (EDA), data cleaning, feature engineering, visualizations, and the Chi-Square test of independence.

## Business Questions

1. Is late delivery a significant operational issue for DataCo Global?
2. Which shipping approach is more effective based on actual delivery performance?
3. Would opening additional store branches help address the delivery-delay issue?

## Dataset

| Item | Description |
|---|---|
| Dataset | `DataCoSupplyChainDataset.csv` |
| Source | [DataCo Smart Supply Chain for Big Data Analysis – Kaggle](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis) |
| Format | CSV |
| Original size | 180,519 rows × 53 columns |
| Subject | Orders, customers, products, shipping, and delivery performance |

The notebook excludes records with suspected fraud from the main delivery analysis. The resulting analysis dataset contains **176,457 shipments**. The reported delivery-status percentages below refer to this filtered dataset unless stated otherwise.

> **Dataset note:** The source CSV is not included in this repository. Download it from Kaggle and place it in the same directory as the notebook before running the analysis.

## Tools & Libraries

- **Python** — data analysis
- **Pandas, NumPy** — data manipulation
- **Matplotlib, Seaborn, Plotly** — visualization
- **SciPy** — D'Agostino-Pearson normality test and Chi-Square test of independence
- **Scikit-learn** — categorical label encoding
- **Jupyter Notebook** — analysis workflow
- **Tableau Public** — interactive dashboard

## Project Workflow

### 1. Data Understanding

- Loaded the Kaggle dataset and reviewed its structure.
- Examined the 53 columns, data types, and descriptive statistics.
- Explored missing values, duplicate records, outliers, and variable distributions.

### 2. Data Cleaning

- Converted identifier-like columns to categorical data types.
- Converted order and shipping date columns to datetime.
- Removed `Product Description`, which was entirely missing.
- Retained other missing values where their proportion was very small or the field was not consistently applicable across countries.
- Checked for duplicate records; none were identified in the notebook.

### 3. Feature Engineering

Created additional fields to support the analysis:

- **`Hari_Telat`** — actual shipping days minus scheduled shipping days, representing the number of days early or late.
- **`Kategori_Diskon`** — groups discount rates into discount bands.
- **`Rugi`** — identifies transactions with a negative `Benefit per order`.

### 4. Exploratory Data Analysis

The analysis explores:

- Delivery status distribution.
- Late-delivery percentages by shipping mode.
- Scheduled versus actual shipping duration.
- Delivery performance by market, customer segment, and product department.
- Delivery patterns by order time.
- Store-country and customer-country combinations.
- Correlations between selected logistics variables.

### 5. Chi-Square Test of Independence

The Chi-Square test of independence was used to evaluate whether late delivery is associated with four categorical variables:

- `Shipping Mode`
- `Department Name`
- `Customer Segment`
- `Market`

The significance threshold used was **0.05**.

## Key Findings

### Overall delivery performance

After excluding records with suspected fraud, the analysis dataset contains **176,457 shipments**:

| Delivery status | Shipments | Share |
|---|---:|---:|
| Late delivery | 98,977 | 56.09% |
| Advance shipping | 41,592 | 23.57% |
| Shipping on time | 32,196 | 18.25% |
| Shipping canceled | 3,692 | 2.09% |

More than half of the analyzed shipments were delivered later than scheduled.

### Late delivery by shipping mode

| Shipping mode | Late-delivery rate |
|---|---:|
| First Class | 97.73% |
| Second Class | 78.30% |
| Same Day | 46.80% |
| Standard Class | 38.94% |

First Class and Second Class have the highest late-delivery rates, both above the overall rate of 56.09%.

### Scheduled versus actual delivery duration

The notebook reports the following average delivery durations for late shipments:

| Shipping mode | Average scheduled duration | Average actual duration |
|---|---:|---:|
| First Class | About 1 day | About 2 days |
| Second Class | About 2 days | About 4 days |
| Standard Class | About 4 days | About 5 days |
| Same Day | 0 days (same day) | About 1 day |

The results indicate a mismatch between promised and observed delivery times, particularly for First Class and Second Class.

### Chi-Square test results

| Variable tested against late delivery | p-value | Result at α = 0.05 |
|---|---:|---|
| Shipping Mode | 0.0000 (reported to 4 decimals) | Statistically significant association |
| Department Name | 0.6903 | No statistically significant evidence of association |
| Customer Segment | 0.4169 | No statistically significant evidence of association |
| Market | 0.0595 | No statistically significant evidence of association |

Among the four variables tested, **Shipping Mode is the only variable with a statistically significant association with late delivery** at the 0.05 significance level.

A statistically significant association does not, by itself, establish causation. The result identifies a relationship in this dataset, not proof that shipping mode alone causes delays.

### Additional observations

- First Class and Second Class show high late-delivery rates across markets.
- The analysis found that Same Day orders placed before 12:00 were not late in the observed data, while orders placed from 12:00 onward had late deliveries.
- In the notebook's delivery-promise simulation, changing the First Class promise to two days reduced its simulated late rate to 0%. A five-day promise for Second Class and Standard Class reduced their simulated late rates to approximately 20%; a six-day promise reduced them to 0%.

These are findings and simulations based on the historical dataset, not guaranteed future outcomes.

## Conclusions & Business Recommendations

Based on the analysis:

1. **Review First Class delivery promises.** The observed average actual duration is around two days, compared with a one-day scheduled promise. Consider revising the promised delivery time to better reflect observed performance.
2. **Reassess Second Class.** Its observed delivery duration is similar to Standard Class despite a shorter scheduled promise. Review whether the service level and its delivery promise are sufficiently differentiated.
3. **Set a Same Day order cut-off.** The observed data suggests that orders placed before 12:00 performed better. Consider a noon cut-off, subject to operational validation.
4. **Prioritize shipping operations over branch expansion.** Late-delivery rates for First Class and Second Class remain high across different customer locations. The analysis therefore does not identify additional store branches as the primary solution.
5. **Monitor delivery performance continuously.** Track late-delivery rates by shipping mode, promised duration, and order time to evaluate whether operational changes improve service reliability.

## Dashboard

Explore the interactive Tableau Public dashboard:

[**DataCo Global Operations Analytics Dashboard – Tableau Public**](https://public.tableau.com/app/profile/ahmad.malik.ibrahim6201/viz/DashboardDataCoGlobalOperationsAnalyticsDenganChi-SquareAhmadMalikIbrahim/Dashboard1)

## Repository Contents

```text
.
├── DataCo Global Operations Analytics Using Chi-Square Ahmad Malik Ibrahim.ipynb
└── README.md
```

The source dataset must be downloaded separately from Kaggle and placed alongside the notebook.

## How to Run

1. Clone or download this repository.
2. Download `DataCoSupplyChainDataset.csv` from the [Kaggle dataset page](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis).
3. Place the CSV file in the same directory as the notebook.
4. Install the required Python libraries:

   ```bash
   pip install pandas numpy matplotlib seaborn scipy scikit-learn plotly jupyter
   ```

5. Open Jupyter Notebook and run the notebook cells.

## Author

**Ahmad Malik Ibrahim**

- [LinkedIn](https://www.linkedin.com/in/ahmad-malik-ibrahim)
- [GitHub](https://github.com/ahmad2129)

---

*This project was created as a Data Analytics portfolio project (November 2026).*
