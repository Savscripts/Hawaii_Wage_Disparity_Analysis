# Hawaii Wage Disparity Analysis

Regression analysis of 2023 ACS PUMS microdata testing whether Native Hawaiian status is associated with lower wages, and whether education pays off equally across that status.

## Research questions

1. Does being Native Hawaiian correlate with income?
2. Do earnings for Native Hawaiians vary depending on whether they hold at least a bachelor's degree — i.e., does education pay off equally regardless of Native Hawaiian status?

## The data

2023 American Community Survey (ACS) Public Use Microdata Sample (PUMS) for Hawaii, from the U.S. Census Bureau. Starting sample of 15,019 observations, cleaned down to **7,355** after filtering missing values on wage, education, age, weeks worked, hours worked, sex, and industry code.

Key variables: wage (`WAGP`), Native Hawaiian status (`RACNH`), educational attainment (`SCHL`, recoded to a bachelor's-or-higher flag), age, sex, weeks worked, usual weekly hours, and 18 industry categories derived from Census industry codes (`INDP`).

## Methodology

Three nested log-wage regression models, each adding controls to isolate what's actually driving wage differences:

- **Model 1 (baseline):** Native Hawaiian status × bachelor's degree, controlling for age (with a quadratic term to capture the concave age-wage relationship)
- **Model 2 (expanded):** adds sex, weeks worked, and usual weekly hours (quadratic) to account for labor force participation
- **Model 3 (full):** adds 18 industry controls to test whether wage gaps are really about industry sorting rather than direct wage discrimination

Wages were log-transformed (right-skewed distribution — a small share of very high earners), so coefficients represent approximate percentage changes in wages. Breusch-Pagan tests were run on all three models to check for heteroskedasticity.

## Results

- **Native Hawaiian status alone is not a statistically significant predictor of wages.** In the full model, Native Hawaiians earned a statistically insignificant 2.02% *more* than non-Native Hawaiians (p > 0.1), holding other factors constant — i.e., no detectable direct wage penalty from Native Hawaiian status itself.
- **Education is the strongest driver of wages in the dataset.** A bachelor's degree is associated with a 38–46% wage increase depending on the model (p < 0.01) — by far the largest effect of any variable tested.
- **The Native Hawaiian × Bachelor's interaction is negative** (though not statistically significant at p<0.05 in every model), suggesting Native Hawaiians with a degree may see a somewhat smaller return to education than non-Native Hawaiians with the same credential.
- **Industry sorting explains more than direct discrimination.** Adding industry controls only nudged the Native Hawaiian coefficient and barely moved R² (0.61 → 0.62) — implying wage disparities are more about *which industries* Native Hawaiians are concentrated in than a wage penalty within the same job.
- **A persistent gender gap exists independent of the Native Hawaiian question:** men earned ~17% more than women, holding education, industry, and hours constant (p < 0.01).
- **Industry matters a lot:** Mining, Healthcare, Finance, and Construction paid significantly more than the Transportation reference category; Retail, Arts & Entertainment, and Agriculture paid significantly less.
- Model 3 (full model, with industry controls) had the best fit at **R² = 0.62**.

## Interpretation

Native Hawaiian status by itself doesn't show up as a direct wage penalty once you control for education, hours, and industry — but that's not the same as saying there's no disparity. The disparity shows up indirectly: through occupational sorting (which industries Native Hawaiians are concentrated in) and through a smaller wage return to the same bachelor's degree. That points toward a different kind of policy lever than "close a pay gap for the same job" — it points toward improving access to high-paying industries (Finance, Healthcare, Professional Services) through career development, mentorship, and networking programs targeted at Native Hawaiian workers.

## Repo contents

| File | Description |
|---|---|
| `hawaii_wages_regression.qmd` | Data cleaning, exploratory analysis, and all three regression models (Quarto/R) |
| `Hawaii_Wage_Disparity_Report.docx` | Full written report: introduction, descriptive statistics, results, conclusion |

Raw data isn't included — it's a public Census Bureau file (`psam_p15.csv`, the Hawaii person-level PUMS extract), available directly from the [Census Bureau's PUMS data page](https://www.census.gov/programs-surveys/acs/microdata.html).

## Tools

R (tidyverse, stargazer, lmtest, vtable, ggplot2), Quarto

## Author

Savgun Kaur ([savscripts](https://github.com/savscripts))
