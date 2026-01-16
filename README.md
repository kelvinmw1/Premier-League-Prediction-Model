# Premier League Match Outcome Prediction

This project aims to predict the outcomes of Premier League football matches using historical match data and a RandomForestClassifier model.

## Dataset

The dataset used for this project is `premier_league.csv`, which contains detailed statistics for Premier League matches across multiple seasons. The data includes information such as:

-   Date and time of the match
-   Competition round
-   Venue (Home/Away)
-   Match result (Win, Loss, Draw)
-   Goals scored (gf) and conceded (ga)
-   Expected Goals (xg) and Expected Goals Against (xga)
-   Possession (poss)
-   Shots (sh) and Shots on Target (sot)
-   Distance of shots (dist)
-   Free kicks (fk), penalties (pk), and penalty attempts (pkatt)
-   Team names and opponents

## Methodology

The prediction model was built using the following steps:

1.  **Data Loading and Initial Exploration**: The `premier_league.csv` file was loaded into a Pandas DataFrame. Initial exploration included checking data types, value counts for key columns, and filtering data for specific teams.

2.  **Feature Engineering**: Several features were engineered from the raw data to be used as predictors:
    *   `date`: Converted to datetime objects.
    *   `venue_code`: Categorical encoding for home/away venues.
    *   `opp_code`: Categorical encoding for opponent teams.
    *   `hour`: Extracted from the match time.
    *   `day_code`: Day of the week extracted from the date.
    *   `target`: A binary target variable, `1` for a win and `0` otherwise.
    *   **Rolling Averages**: Rolling averages over the last 3 matches for 'goals for', 'goals against', 'shots', 'shots on target', 'distance of shots', 'free kicks', 'penalties', and 'penalty attempts' were calculated for each team to capture recent performance trends.

3.  **Model Training**: A `RandomForestClassifier` from `sklearn.ensemble` was used for training. The model was configured with `n_estimators=50` and `min_samples_split=10` to balance performance and prevent overfitting.
    *   The data was split into training and testing sets based on date (`train` before '2022-01-01', `test` after '2022-01-01').
    *   Predictors included engineered features like `venue_code`, `opp_code`, `hour`, `day_code`, and all the `_rolling` average features.

4.  **Model Evaluation**: The model's performance was evaluated using:
    *   `accuracy_score`: Overall prediction accuracy.
    *   `precision_score`: Precision of predicting wins.
    *   A confusion matrix (crosstab of actual vs. predicted) was generated to understand the distribution of correct and incorrect predictions.

## Results

After training and evaluating the model, the following performance metrics were observed:

*   **Accuracy**: 61.23%
*   **Precision**: 62.5%

The confusion matrix also provided insights into true positives, true negatives, false positives, and false negatives, indicating areas where the model performed well and where it could be improved.

## How to Run the Notebook

To run this project, follow these steps:

1.  **Open in Google Colab**: Click on the 'Open in Colab' badge (if available) or upload the `.ipynb` file to your Google Colab environment.
2.  **Mount Google Drive**: The notebook will prompt you to mount your Google Drive. This is necessary to access the `premier_league.csv` file.
3.  **Place Data File**: Ensure that `premier_league.csv` is located in the root directory of your Google Drive (or modify the `pd.read_csv` path accordingly).
4.  **Run All Cells**: Execute all cells in the notebook sequentially. The code will perform data loading, preprocessing, model training, and evaluation.
5.  **Review Outputs**: Observe the outputs of each cell to see data transformations, model training progress, and evaluation metrics.



