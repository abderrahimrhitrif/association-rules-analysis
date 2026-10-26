# Association Rules for Stroke Risk Factors

## Overview
A data mining and exploratory data analysis project applying association rule learning (Apriori algorithm) to a healthcare stroke dataset to identify clinical risk factor associations.

## Architecture & Pipeline
1. **Data Ingestion & Cleaning**: Loads healthcare stroke dataset (`healthcare-dataset-stroke-data.csv`), drops IDs, and imputes missing BMI values using median values.
2. **Discretization**: Bins continuous variables (age, BMI, average glucose level) into categorical intervals (`pd.cut`, `pd.qcut`).
3. **Association Mining**: Applies Transaction Encoding and the Apriori algorithm (`mlxtend`) to extract frequent itemsets and association rules.
4. **Filtering**: Filters and retains statistically meaningful association rules based on support, confidence, and lift.

## Data
- **Dataset**: Healthcare stroke dataset (`healthcare-dataset-stroke-data.csv`).
- **Features**: Age bins, BMI bins, glucose level bins, hypertension, heart disease, stroke occurrence.

## Method & Algorithms
- **Apriori Algorithm**: Frequent itemset mining and association rule generation.
- **Rule Evaluation**: Evaluates rules using support, confidence, and lift metrics, retaining 25 top rules.

## Verified Results & Metrics
- Successfully retained **20 filtered association rules** highlighting clinical risk factors associated with stroke occurrence.

## Limitations & Caveats
- Academic analysis on a public healthcare dataset; clinical utility requires professional validation.

## Run Instructions
```bash
jupyter notebook projet_BI.ipynb
```

## CV Bullet Points
- Applied association rule mining (Apriori algorithm) on a healthcare dataset to extract and validate 20 significant clinical risk factor rules for stroke prediction.
- Performed data preprocessing, median BMI imputation, and intelligent discretization (binning) of continuous medical attributes.

## Claims to Avoid
- Do not claim clinical diagnostic deployment or medical advisory validation.
