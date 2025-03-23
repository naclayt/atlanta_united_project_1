**Atlanta United Data Scientist Project 1 - Predicting Player Outcomes**

- Name: Nathan Clayton
- Email: nathanaclayton25@gmail.com
- Date Created: March 18, 2025
- Last Modified: March 23, 2025

**Overview**

This project aims to predict player performance outcomes for MLS players using historical match data and machine learning techniques. The model is trained on rolling averages of key performance metrics to estimate expected contributions (non-penalty xG + xA) for upcoming matches.

**Dependencies**

The script requires the following R packages:
 - tidyverse
 - slider
 - lubridate
 - caret
 - zoo
 - dplyr
 - randomForest
 - ggthemes
 - teamcolors

To ensure all required packages are installed, the script includes a function install_and_load() that installs missing packages and loads them.

**Data Sources**

The script loads two primary datasets:

- Match Log: Contains detailed player performance metrics.
- Schedule: Contains match dates and opponents.

Both datasets are loaded from CSV files stored locally.

**Data Processing**

1. Data Cleaning

Ensures season_name values are consistent.

Joins match logs with schedule data to include match_date.

2. Compute Rolling Averages

Calculates 5-match rolling averages for key performance metrics:

 - avg_np_xg_5 (non-penalty expected goals over last 5 matches)

 - avg_xa_5 (expected assists over last 5 matches)

 - avg_np_xg_xa_5 (sum of the above metrics)

Computes expected player volume (average minutes, shots, key passes).

3. Compute Defensive Team Stats

Aggregates opponent defensive metrics (goals/assists allowed, xG conceded) for the 2025 season.

4. Merge Player Data with Schedule

Links player rolling averages to upcoming match schedule.

Joins defensive stats for the opponent team.

**Machine Learning Model**

A Random Forest model is trained to predict non-penalty xG + xA based on:

 - avg_np_xg_5
 - avg_xa_5
 - avg_shots
 - avg_key_passes
 - avg_xg_xa_conceded (opponent's expected goals conceded)

The model is trained using randomForest() with 200 trees and 3 variables per split.

**Visualization**

The script generates a bar chart ranking the top 10 predicted players for the upcoming match using ggplot2, with:

 - Player names
 - Predicted np_xG + xA values
 - Team colors (using teamcolors package)
 - Usage

Run the script in RStudio or any R environment. Ensure the required datasets (matchlog_data.csv and schedule.csv) are available in the specified directory.
