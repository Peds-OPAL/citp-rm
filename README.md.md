# Chronic ITP Prediction Model


## Welcome

This repository contains an example of how to use the Chronic Immune
Thrombocytopenia Purpura Risk Model (cITP-RM).

``` r
#install.packages("rms")
library(rms)
mod <- readRDS("cITP-RM-public.rds")
```

## Required Variables

-   **`chronic_itp`**: Target outcome (factor: 0 = No, 1 = Yes)
-   **`age`**: Age at diagnosis (numeric, years)
-   **`male`**: Sex (factor: 0 = Female/Other, 1 = Male)
-   **`platelet_count`**: Platelet count (numeric, ×10³/μL)
-   **`lymphocyte_count`**: Absolute lymphocyte count (numeric, 1000
    cells/μL)
-   **`igg_level`**: IgG level (numeric, 100 mg/dL)
-   **`iga_level`**: IgA level (numeric, 100 mg/dL)
-   **`igm_level`**: IgM level (numeric, 100 mg/dL)
-   **`secondary_cause`**: Secondary cause present (factor: 0 = No, 1 =
    Yes)
-   **`dat_positive`**: Direct Antiglobulin Test (factor: 0 = Negative,
    1 = Positive)

**Note**: Variable names are case-sensitive and must match exactly.

## Example Dataset Structure

``` r
# Create example dataset
example_data <- data.frame(
  age = c(5, 1, 10),
  male = factor(c(1, 0, 1), levels = c(0, 1)),
  platelet_count = c(75, 15, 2),
  lymphocyte_count = c(1.2, 0.8, 2.5),
  igg_level = c(1, 2, 3),
  iga_level = c(2.1, 1.8, 3.2),
  igm_level = c(1.1, 3, 1.8),
  secondary_cause = factor(c(0, 1, 0), levels = c(0, 1)),
  dat_positive = factor(c(1, 0, 0), levels = c(0, 1))
)

# Make predictions (probability of chronic ITP)
predictions <- predict(mod, newdata = example_data, type = "fitted")

# Display results
results <- data.frame(
  Patient = 1:3,
  Probability_Chronic_ITP = round(predictions, 3)
)

print(results)
```

      Patient Probability_Chronic_ITP
    1       1                   0.380
    2       2                   0.218
    3       3                   0.051
