# Credit Card Fraud Detection

A CRISP-DM data science project that explores the detection of fraudulent credit card transactions in a hypothetical Italian banking context.

## Business Problem

The objective is to identify fraudulent transactions while limiting unnecessary verification requests for legitimate customers.

The initial business target was to detect at least 85% of fraudulent transactions. The model assigns a fraud risk score that could support three possible actions:

* Low risk: allow the transaction.
* Medium risk: require confirmation through 2FA.
* High risk: temporarily suspend the transaction for additional verification.

## Dataset

The project uses the [Credit Card Fraud Detection dataset](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud), containing European credit card transactions made in September 2013.

The original dataset contains:

* 284,807 transactions
* 31 variables
* 492 fraudulent transactions
* A fraud rate of approximately 0.173%

The dataset is highly imbalanced. The variables `V1`–`V28` are anonymized, while `Time`, `Amount` and `Class` are directly available.

The dataset file is not included in this repository and must be downloaded separately.

## Methodology

The project follows the CRISP-DM methodology:

1. Business Understanding
2. Data Understanding
3. Data Preparation
4. Modeling
5. Evaluation
6. Deployment Recommendations

Duplicate transactions were removed before modeling. The cleaned dataset contains 283,726 transactions, including 473 fraudulent cases.

## Models

Two models were evaluated:

* A baseline classifier that always predicts the majority class.
* A Logistic Regression model with class balancing and feature scaling.

A validation set was used to study different classification thresholds. A final decision threshold of `0.70` was selected to prioritize fraud detection while reducing false positives.

## Results

| Model                                      | Accuracy | Precision | Recall | F1-score | False Positives | Missed Frauds |
| ------------------------------------------ | -------: | --------: | -----: | -------: | --------------: | ------------: |
| Baseline                                   |   99.83% |     0.00% |  0.00% |    0.00% |               0 |            95 |
| Logistic Regression — threshold 0.50       |   97.53% |     5.64% | 87.37% |   10.59% |           1,389 |            12 |
| Tuned Logistic Regression — threshold 0.70 |   98.86% |    11.58% | 87.37% |   20.44% |             634 |            12 |

The final model detected 83 of the 95 fraudulent transactions in the test set, achieving a recall of 87.37% and meeting the initial business target.

Changing the threshold from `0.50` to `0.70` reduced false positives from 1,389 to 634 without reducing the number of detected fraudulent transactions.

## Technologies

* Python
* JupyterLab
* pandas
* NumPy
* Matplotlib
* Seaborn
* scikit-learn
* Git and GitHub

## Repository Structure

```text
credit-card-fraud-detection-italy/
├── data/
│   └── creditcard.csv          # Downloaded separately and ignored by Git
├── notebooks/
│   └── 01_credit_card_fraud_crisp_dm.ipynb
├── .gitignore
├── LICENSE
└── README.md
```

## Limitations

* The dataset contains transactions from 2013 and is not specifically related to Italian banks.
* The anonymized variables limit the interpretation of individual risk factors.
* The dataset does not identify whether fraud was caused by phishing, skimming or other methods.
* The model is an educational prototype and is not ready for deployment in a real banking system.
* A real implementation would require recent local data, model calibration, continuous monitoring and security, privacy and legal evaluations.

## Author

Vincenzo Ambrosino
