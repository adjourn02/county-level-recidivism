# Predict recidivism rates in Wisconsin counties
This project models county-level recidivism rates in Wisconsin using Poisson regression with an offset term to account for population size.

## Goals
1. Predict recidivism rates across Wisconsin counties using available demographic and socioeconomic data.
2. Analyze the impact of individual-level characteristics, county unemployment rates, and county health indicators on recidivism.
3. Identify significant predictors associated with an increased risk of recidivism.
4. Evaluate model performance using fit metrics and conduct diagnostic testing to assess assumptions and robustness.

## Data Source
1. **WCLD: Curated Large Dataset of Criminal Cases from Wisconsin Circuit Courts**
- Description: A curated large dataset of 1.5 million criminal cases from circuit courts in the U.S. state of Wisconsin, consisting of data from 1970 to 2020 for every county, to include attributes like prior criminal counts and recidivism outcomes.
- Source: https://clezdata.github.io/wcld/.

2. **Job Center of Wisconsin: Labor Market Information**
- Description: State of Wisconsin's Department of Workforce Development provides labor market information to be queried from their website where Unemployment data from 1990 to 2025 is available for each each county.
- Source: This data can be queried on https://jobcenterofwisconsin.com/wisconomy/query.

3. **University of Wisconsin Population Health Institute: County Health Rankings & Roadmaps**
- Description: Based from the University of Wisconsin Population Health Institute Model of Health where collective health and well-being from 2010 to 2025 is summarized as a score based from multiple weighted factors captured within two focus areas: 1) Population Health and Well-being, and 2) Community Conditions.
- Source: Information on the factors comprising focus areas can be found on https://www.countyhealthrankings.org/what-impacts-health/model-of-health and the data can be downloaded on https://www.countyhealthrankings.org/health-data/wisconsin/data-and-resources.

## Exploratory Data Analysis

### Pairs Plot
![pairs_plot](images/pairs_plot.png)
From the plots in the top row, most variables show a non-linear relationship with recid_rate. Also, avg_prior_misdemeanor and avg_prior_felony have a strong linear relationship.

### Year vs Recidivism Rate
<img src="images/boxplot_year.png" alt="year_boxplot" width="400">
The boxes are overlapping making it hard to determine if the means are significantly different among groups.

### County vs Recidivism Rate
![county_boxplot](images/boxplot_county.png)
Most of the boxes are not overlapping indicating there is likely significant different means among groups.

## Prediction
Even after model adjustments, model does not fit the data indicating a non-parametric model is more appropriate to use. However, in terms of predictive power, the poisson model performs well with the following evaluation scores on a test dataset:
| Metric              | Score       |
|---------------------|-------------|
| MSE (Mean Squared Error)         | 6,844.17    |
| MAE (Mean Absolute Error)        | 40.64       |
| MAPE (Mean Absolute Percentage Error) | 14.33%      |
| PM (Prediction Match Rate)       | 0.00065     |
| R-squared                        | 0.9572      |
| Adjusted R-squared               | 0.9510      | 
