# Analyst-Portfolio
The culmination of my work in my Data Analysis graduate course at American University.
This portfolio showcases two empirical research projects using R and Quarto.
Each project demonstrates core analytical skills including data cleaning, visualization, and interpretation of real-world datasets.
The goal of this portfolio is to present clear, reproducible research that answers substantive policy-relevant question.

It also showcases updated and cleaned versions of previous project that I have done in my graduate data analysis course at American University.

The edited versions of the research can be found in the `portfolio.pdf` file.


## Research Topics
1. U.S. Immigration Trends by Region (1999-2023)
This project examines how patterns of legal immigration to the United States have changed over time. It focuses on regional differences in Lawful Permanent Resident (LPR) admissions and explores both growth trends and shifts in the composition of immigration.
2. The Relationship Between War and Inflation
This project analyzes whether countries experiencing conflict face higher and more volatile inflation rates. It combines cross-national conflict data with macroeconomic indicators to evaluate the economic consequences of war.


## Data Sources

### Immigration Data
- Source: Migration Policy Institute (MPI)
- Description: Annual data on individuals granted LPR status by region of origin (1999-2023)
- Link: https://www.migrationpolicy.org

### Conflict Data
- Source: Uppsala Conflict Data Program (UCDP)
- Description: Country-year data on armed conflict incidence

### Inflation Data
- Source: World Bank Global Inflation Database
- Description: Cross-national inflation rates by country and year
- Link: https://www.worldbank.org


## Analytical Approach

### Data Preparation
- Cleaned and standardized datasets using `dplyr` and `janitor`
- Merged datasets at the country-yaer level
- Created key variables (e.g., binary conflit indicator)

  ### Visualizations and Analysis

  #### Immigration Project:
  - Created indexed trend plots to compare relative growth across regions
  - Developed area charts to show the composition of immigration over time
  - Used faceting and transformations to improve interpretability
 
  #### War and Inflation Project:
  - Compared inflation outcomes between conflict and non-conflict periods
  - Calculated summary statistics (mean, standard deviation
  - Introduced time-series analysis to examine global inflation trends

 
## Key Takeaways
- Immigration patterns very significantly by region, with some regions experiencing steady growth while others show long-term decline or volatility
- War is strongly associated with higher and more unstable inflation rates
- Time-based analysis suggests that conflict may contribute to broader global economic instability

## Reproducibility

All analyses in this repository are fully reproducible using the provided `.qmd` files and datasets. Code is written in R and uses packages including:

-`tidyverse`
-`ggplot2`
- `dplyr`
- `readr`
- `readxl`

## Exemplary Code Chunk: Summarizing Inflation by Conflict Status

### Overview

This code chunk highlights my ability to transform and summarize complex, merged datasets into interpretable statistics. 
Specifically, it calculates key summary measures of inflation-mean, standard deviation, and number of observations-grouped by whether a country is experiencing conflicts.

This function is central to my analysis of the relationship between war and inflation. 
By comparing both average inflation rate and its variability across conflict and non-conflict periods, the code provides a concise way to evaluate economic instability.
This approach is especially useful in policy analysis, where understanding both central tendencies and volatility is critical.


### What the Code Does

The code groups the dataset by a binary conflict variable (`war`) and computes:

- Mean Inflation: average prive level changes
- Standard Deviation: volatility of inflation (economic instability)
- Number of Observations: sample size for each group


### The Code

```{r}
sum_conflict <- conflict_inflation %>%
  group_by(war) %>%
  summarise(
    mean_inflation = mean(inflation, na.rm = TRUE),
    sd_inflation = sd(inflation, na.rm = TRUE),
    observations = n()
  )

conflict_tbl <- sum_conflict %>%
  mutate(
    war = ifelse(war == 1, "War", "No War")
  ) %>%
  rename(
    "Conflict Status" = war,
    "Average Inflation" = mean_inflation,
    "Standard Deviation" = sd_inflation,
    "Observations" = observations
  )

conflict_tbl
```

## Output

The output is a table that shows that countries experiencing conflict have, on average, more than double the inflation rate of countries not in conflict. 
Additionally, the higher standard deviation during conflict periods indicates greater volatility, suggesting increased economic instability. 

This code demonstrates the ability to produce meaningful, policy-relevant summaries from raw data.

