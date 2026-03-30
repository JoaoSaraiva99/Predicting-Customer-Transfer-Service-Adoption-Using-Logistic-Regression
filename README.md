# Predicting-Customer-Transfer-Service-Adoption-Using-Logistic-Regression
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

*Kept: ReservationValue, Length of Stay (relevant for transfer behavior)
*Removed: IDs, apartment characteristics, OTA origin, and irrelevant structural variables
*Target variable: Transfer (Y/N), converted into binary

These decisions ensured a clean, consistent, and model-ready dataset, reducing noise and improving predictive capability.
