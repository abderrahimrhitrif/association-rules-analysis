# Association Rules for Stroke Prediction

This project implements an association rule mining approach to identify risk factors associated with stroke occurrence. The workflow leverages the Apriori algorithm and several evaluation metrics to extract and validate statistically significant associations from a healthcare dataset.

## Table of Contents
- [Introduction](#introduction)
- [Dataset and Preprocessing](#dataset-and-preprocessing)
- [Transaction Construction and Encoding](#transaction-construction-and-encoding)
- [Parametric Analysis](#parametric-analysis)
- [Association Rule Mining](#association-rule-mining)
- [Evaluation Metrics](#evaluation-metrics)
- [Results and Filtering](#results-and-filtering)
- [Usage](#usage)
- [Resources](#resources)

## Introduction
Stroke is the second leading cause of mortality worldwide and results in significant morbidity. Early prediction is critical for effective prevention. This project focuses on identifying combinations of risk factors (demographic, clinical, and lifestyle) using association rules to help flag high-risk patients.

## Dataset and Preprocessing
The analysis is based on the "Stroke Prediction Dataset" from Kaggle. The dataset includes various attributes such as age, BMI, glucose levels, and more, with the target variable `stroke` indicating stroke occurrence (0/1). Key preprocessing steps include:
- Dropping non-informative columns (e.g., `id`)
- Imputing missing values (e.g., using the median for `bmi`)
- Discretizing continuous variables into clinically meaningful bins:
  - Age into groups such as `0-30`, `31-45`, `46-60`, `61+`
  - BMI into categories: `Underweight`, `Normal`, `Overweight`, `Obese`
  - Glucose levels into quartiles labeled `Low`, `Mid-low`, `Mid-high`, `High`

## Transaction Construction and Encoding
After preprocessing, each record is transformed into a transaction record containing attribute-value pairs (e.g., `gender=Male`, `age_bin=31-45`) with the target appended as `stroke=0` or `stroke=1`. These transactions are encoded using the `TransactionEncoder`, producing a binary matrix for further analysis with the Apriori algorithm.

## Parametric Analysis
To explore the impact of various support and confidence thresholds on rule generation, a parametric analysis was performed. The following levels were tested:
- **Support Levels:** [0.001, 0.002, 0.003, 0.005] (corresponding to 0.1% to 0.5%)
- **Confidence Levels:** [0.2, 0.4, 0.6, 0.7, 0.8]

A plot is generated to visualize the number of rules (specifically those with `stroke=1` in the consequents) as the thresholds vary. This analysis helped to determine an optimal balance between rule reliability and coverage.

## Association Rule Mining
The Apriori algorithm from the `mlxtend` package is used to mine frequent itemsets and generate association rules. Rules with consequents containing `stroke=1` are isolated for further analysis. In a separate section, the notebook generates all such rules before applying additional filtering based on evaluation metrics.

## Evaluation Metrics
Beyond support and confidence, the project incorporates several advanced metrics to evaluate the quality of the association rules:
- **Lift:** Measures how much more likely `stroke=1` is to occur in the presence of a given antecedent compared to random chance.
- **Bayes Factor (BF):** Compares the probability of stroke in the presence versus the absence of the antecedent.
- **Predictive Dependency Index (PDI):** Quantifies the absolute dependency between the antecedent and stroke occurrence.
- **Interest Improvement (INTIMP):** Assesses the relative improvement in predicting `stroke` when the antecedent is considered.

These metrics help in filtering out rules that are statistically weak or not clinically significant.

## Results and Filtering
After calculating the evaluation metrics, the final filtering retains rules that satisfy the following minimum criteria:
- **Lift ≥ 1.0**
- **BayesFactor ≥ 1.0**
- **PDI ≥ 0.0**

Due to the nature of the data, the `INTIMP` metric was not used in the final filtering as it did not meet the minimum threshold for any rule. The final rules, which number 20 following the chosen thresholds (support = 0.1%, confidence = 60%), exhibit very high average lift (≈15.8) and Bayes Factors (≈14.4).

## Usage
1. **Preprocessing:** Run the preprocessing section to load the dataset, clean the data, and discretize continuous variables.
2. **Transaction Construction:** Convert the cleaned dataset into transaction format.
3. **Rule Mining:** Execute the parametric analysis followed by association rule extraction with the Apriori algorithm.
4. **Evaluation:** Compute the evaluation metrics and apply the filtering criteria.
5. **Output:** The final set of rules is saved to `stroke_association_rules.csv`.

To reproduce the analysis, open the provided Jupyter Notebook `projet_BI.ipynb` and run the cells sequentially.

## Resources
- [Tableau Dashboard](https://public.tableau.com/app/profile/abderrahim.rhitrif/viz/ClasseurBI/Dashboard1)
- [Reference Article on Interestingness Measures](https://www.sciencedirect.com/science/article/abs/pii/S0377221706011465)
- [Stroke Prediction Dataset on Kaggle](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)
