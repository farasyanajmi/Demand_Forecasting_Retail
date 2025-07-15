# Retail Product Demand Forecasting

## Project Overview

This project focuses on forecasting the daily demand for a specific retail product (Product ID: `P0001`) using historical sales data and other influencing factors. Accurate demand forecasts are crucial for optimizing inventory levels, reducing stockouts, and preventing overstock, thereby improving supply chain efficiency and reducing costs.

The solution employs a **Random Forest Regressor** machine learning model, implemented and demonstrated within a Jupyter Notebook.

## Dataset

The `retail_store_inventory.csv` dataset contains the following columns (relevant for this project):
- `Date`: Date of the record.
- `Product ID`: Unique identifier for the product.
- `Units Sold`: The daily quantity of the product sold (target variable).
- `Discount`: Discount applied on the product.
- `Price`: Selling price of the product.
- `Competitor Pricing`: Competitor's price for similar products.
- `Inventory Level`: Current stock level.
- `Units Ordered`: Number of units ordered from suppliers.
- `Demand Forecast`: Existing demand forecast (can be used as a feature or for comparison).
- `Holiday/Promotion`: Indicates if there was a holiday or promotion.
- `Weather Condition`: Weather on that day.
- `Seasonality`: General seasonality information.
- `Store ID`, `Category`, `Region`: Other identifiers.

## Methodology

The forecasting process, detailed step-by-step in the Jupyter Notebook (`notebooks/Demand_Forecasting_Analysis.ipynb`), involves the following key stages:

1.  **Data Loading & Preprocessing**:
    * Loading the `retail_store_inventory.csv` dataset.
    * Converting the `Date` column to datetime format.
    * Filtering data to focus specifically on `Product ID P0001`.
    * Sorting the data chronologically.

2.  **Feature Engineering**:
    * **Time-Based Features**: Extracting `year`, `month`, `day`, `dayofweek`, `dayofyear`, and `weekofyear` to capture seasonal patterns.
    * **Lagged Sales Features**: Creating lag features for `Units Sold` (1, 7, 14, and 28 days prior) to model time-series dependencies.
    * **Categorical Encoding**: One-hot encoding `Weather Condition` and `Seasonality` columns.
    * Including other numerical features (`Discount`, `Price`, `Competitor Pricing`, `Inventory Level`, `Units Ordered`, `Demand Forecast`) as predictors.

3.  **Data Splitting**:
    * The data is split chronologically into an 80% training set and a 20% testing set to simulate real-world forecasting scenarios (training on past data, predicting future data).

4.  **Model Training**:
    * A **Random Forest Regressor** is chosen for its ability to handle various data types, capture non-linear relationships, and provide robust predictions.
    * The model is trained on the engineered features from the training set.

5.  **Prediction**:
    * The trained model generates demand forecasts for the test set.
    * All negative predictions are clipped to zero, as demand cannot be negative.

6.  **Evaluation**:
    * The model's performance is assessed using:
        * **Mean Absolute Error (MAE)**
        * **Root Mean Squared Error (RMSE)**
        * **Mean Absolute Percentage Error (MAPE)**: Critically, MAPE is calculated *excluding* periods where actual sales were zero, to prevent division by zero errors and provide a more meaningful percentage error.

## Results

The Random Forest Regressor model achieved the following performance metrics on the test set for Product `P0001`:

* **Mean Absolute Error (MAE):** 7.32
* **Root Mean Squared Error (RMSE):** 8.76
* **Mean Absolute Percentage Error (MAPE):** **17.83%**

A MAPE of 17.83% indicates that, on average, the model's predictions deviate by approximately 17.83% from the actual sales. This is a strong result for daily demand forecasting in a retail environment, demonstrating the model's effectiveness in providing actionable insights for inventory management.

## Visualizations

The `results/` directory contains plots visualizing the model's performance:

* `historical_vs_forecasted_demand_P0001_rf_rerun.png`: Shows the actual historical demand, actual test demand, and the model's forecasted demand.
* `forecast_errors_P0001_rf_rerun.png`: Displays the difference between actual and forecasted demand over time.

## How to Run the Project (using Jupyter Notebook)

1.  **Clone the repository:**
    ```bash
    git clone (https://github.com/farasyanajmi/Demand_Forecasting_Retail)
    cd Demand_Forecasting_Retail
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Start Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```
4.  **Open and Run:**
    In your web browser, navigate to the `notebooks/` folder and click on `Demand_Forecasting_Analysis.ipynb` to open it. Execute all cells sequentially to run the analysis and generate the results and plots.

## Dependencies

The project relies on the following Python libraries:
* `pandas`
* `numpy`
* `scikit-learn`
* `matplotlib`
* `jupyter`

These can be installed via `pip` using the `requirements.txt` file.

## Acknowledgements

This project was developed with the assistance of an AI conversational assistant and by leveraging various online resources and documentation found on the internet. Their contributions were instrumental in the learning process, feature engineering, model selection, and overall project structure.
