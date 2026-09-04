# Predicting Customer Transfer Service Adoption Using Logistic Regression
This project focuses on applying logistic regression algorithms to predict whether customers are likely to purchase a transfer service.

A company that manages a portfolio of tourist-oriented real estate properties is considering offering a transfer service to its clients. To support this decision, the project analyzes historical customer data to identify patterns and determine which customer profiles show the highest propensity to purchase the service.

The goal is to enable the company to proactively target these high-potential customers by sending early notifications or personalized offers, thereby increasing conversion rates and improving customer experience.

Note: This project is based on real-world data, which required additional care in the data preparation stage, including data cleaning, handling missing values, and feature engineering to ensure reliable and consistent modeling results.

# Background Overview

Feels Like Home is a property management company specialized in short-term rentals, offering personalized guest experiences including check-in services and optional transfer services from the airport to the accommodation.

With a growing portfolio and increasing competition in the tourism sector, the company aims to adopt a data-driven approach to enhance its service offering and marketing effectiveness. Specifically, the business challenge is to identify which customers are more likely to purchase transfer services, allowing for more targeted communication and improved service adoption.

This project was developed to support that strategic goal by building predictive models capable of profiling customers and estimating their likelihood of purchasing transfers.

# Data Structure Overview

The dataset used in this project is based on real operational data from Feels Like Home, reflecting actual customer reservations and service usage.

## Data Sources and Integration

The initial data was spread across three main tables:

* Reservations (core dataset)
*Apartments
* Transfers

These tables were merged using the common key ReservationId, resulting in a unified dataset with 22,662 records.

After data preparation, an additional dataset (NewReservations) with 393 records was appended, leading to a final dataset of 23,055 observations used for modeling.

## Data Preparation Decisions

Given the real-world nature of the data, several preprocessing steps were required:

1. Handling Missing and Inconsistent Data
Country: 636 missing values → replaced with “Unknown” and standardized to avoid duplicates
NumOfGuests: missing and invalid values (zeros) treated as nulls
Neighbourhood: 2,670 missing values → imputed using mode per region
2. Feature Engineering

New variables were created to improve model performance:

* CheckInTimeOfDay: derived from check-in time (Morning, Afternoon, Night, Late Night, Unknown)
* AirportDistanceKm: calculated based on apartment location
* HighSeason: defined as June–September
* TransferRequestTimeRange: time gap between reservation and check-in
3. Feature Selection

Variables were:

* Kept: ReservationValue, Length of Stay (relevant for transfer behavior)
* Removed: IDs, apartment characteristics, OTA origin, and irrelevant structural variables
* Target variable: Transfer (Y/N), converted into binary

These decisions ensured a clean, consistent, and model-ready dataset, reducing noise and improving predictive capability.

# Executive Summary
## Overview of Findings (Business Perspective)

The analysis shows that customer behavior regarding transfer purchases is highly dependent on contextual and behavioral factors, rather than purely demographic variables.

Key business insights include:

* Customers with shorter booking windows are more likely to purchase transfers
* Check-in timing plays a crucial role (late arrivals show higher propensity)
* Location and distance to airport significantly influence demand
* Seasonality effects (high season months) increase likelihood of purchase

From a business perspective, the project demonstrates that:
* It is possible to predict transfer demand with meaningful accuracy
* The company can move from reactive to proactive service offering
* Targeted notifications can significantly increase conversion rates

# Insights Deepdive (Technical Perspective)
## 1. Class Imbalance Challenge

The dataset presents a strong class imbalance, with significantly fewer transfer purchases compared to non-purchases.
To address this, the following techniques were applied:

* RandomOverSampler to balance the training data
* Focus on Recall and F1-score for the positive class (Transfer = 1)
* Reduced reliance on Accuracy as a primary metric
## 2. Models Implemented

The following classification models were tested:

* Decision Tree Classifier
* Bagging Classifier
* Random Forest Classifier
* Gradient Boosting Classifier
* XGBoost Classifier

Additionally, hyperparameter tuning was applied using:

GridSearchCV (for Bagging, Gradient Boosting, XGBoost, and Random Forest)

<img width="1570" height="790" alt="imagem" src="https://github.com/user-attachments/assets/e075b387-8501-4862-b3fa-21ffd463d684" />

## 3. Model Performance Summary
| Model | Accuracy | F1 (Macro) | Recall (Class 1) | F1 (Class 1) |
|------|----------:|------------:|-----------------:|-------------:|
| Decision Tree | 0.8729 | 0.5824 | 0.23 | 0.23 |
| Bagging | 0.8989 | 0.5987 | 0.21 | 0.25 |
| Random Forest | **0.9115** | 0.6165 | 0.21 | 0.28 |
| Gradient Boosting | 0.7807 | 0.6152 | **0.73** | **0.36** |
| XGBoost | 0.8515 | **0.6390** | 0.51 | 0.36 |

## 4. Key Findings

### Best Overall Model (Balanced Performance): XGBoost Classifier
* Highest F1 Macro (0.6390)
* Good balance between precision and recall
* More stable across both classes
### Best Model for Business Objective (Detect Buyers): Gradient Boosting Classifier
* Highest Recall for Class 1 (0.73)
* Best at identifying customers who will purchase transfers
* Strong F1-score for Class 1 (0.36)
* Highest Accuracy (But Misleading)

## 5. Technical Interpretation
###  Models like Decision Tree and Bagging underperformed in detecting the minority class
###  Random Forest favored majority class predictions, leading to high accuracy but poor recall
###  Boosting models (Gradient Boosting & XGBoost) showed superior performance by:
* Capturing non-linear relationships
* Better handling complex feature interactions
* Improving detection of rare events (transfer purchases)

## 6. Final Model Selection
Recommended Model: Gradient Boosting Classifier

Why?

* Maximizes detection of actual buyers (highest recall)
* Aligns with business objective: do not miss potential customers
* Acceptable trade-off between false positives and missed opportunities
  
