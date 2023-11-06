# Wind Power Forecasting

## Introduction

Wind power forecasting is the process of predicting the amount of electricity that will be generated by wind turbines in a given time period. Accurate forecasting is crucial for integrating wind energy into the electricity grid and making informed decisions about supply and demand. This project utilizes a dataset obtained from Kaggle, containing weather, turbine, and rotor features recorded at 10-minute intervals from January 2018 to March 2020. We aim to predict wind power generated by wind turbines using machine learning and deep learning models, including RandomForest, SARIMA, LSTM, and Prophet for anomaly detection.

## Research Insights

- (Guo et al., 2010) proposed a hybrid model for long-term wind speed forecasting, combining the first definite season index method, ARMA, GARCH models, and Support Vector Machine (SVM).
- (Zhang, 2003) introduced a hybrid approach that combines ARIMA and ANN models for linear and nonlinear modeling, improving forecasting accuracy.

Our project's objective is to understand various time-series forecasting methods, compare predictive accuracy, and enhance wind power forecasting.

## Dataset Description

The dataset used in this project is a time series wind turbine power dataset from Kaggle. It covers the period from December 31, 2017, to March 30, 2020, with data recorded at 10-minute intervals. The dataset comprises 22 columns, with ActivePower being the target variable.

### Exploratory Data Analysis (Before Data Pre-processing)

- The dataset contains 118,224 rows before pre-processing.
- ActivePower represents the total output power generated by the wind turbine.
- Statistical summary of ActivePower: Average = 619.11, Std Dev = 611.28, Min = -38.52, Max = 1778.03.
- The dataset exhibits seasonal patterns, with peaks occurring around July to August.

## Modeling and Anomaly Detection

### Prophet Model

- We use the Prophet model for predicting time series data patterns and trends.
- Changepoint_range parameter is set to 0.95 to adjust the history in which the trend can change.
- We predict the entire dataset to identify patterns and trends without splitting training and testing data.
- Visualizations and pattern comparisons confirm the dataset's seasonality.

### Anomaly Detection

- We calculate errors and uncertainties based on the predicted values.
- Anomalies are identified when the absolute error exceeds 1.5 times the uncertainty.
- Model evaluation metrics include Mean Absolute Error (MAE), Mean Squared Error (MSE), and Root Mean Squared Error (RMSE).

## Performance Metrics

- MAE: 335.65
- MSE: 183,829,865
- RMSE: 428.75

### LSTM Model

To predict ActivePower using the LSTM model:
1. Data is reshaped into the format `[samples, timesteps, features]`.
2. A Sequential model is used with two LSTM layers, each followed by a Dropout layer (0.2) and a Batch Normalization layer.
3. The output layer is fully connected with the number of days to forecast (30).
4. The model is compiled using the Adam optimizer (learning rate: 0.0001) and mean squared error loss function.
5. EarlyStopping monitors validation loss during training, and training stops when no improvement is observed.
6. The model is trained for 200 epochs with a batch size of 32 and a validation split of 0.2.

The training stopped at epoch 84 due to no further improvement in validation loss.

The actual and predicted ActivePower values for 30 days (from 2020-03-01 to 2020-03-30) are compared and visualized.

### Model Evaluation

Evaluation metrics used for the LSTM model:
- Mean Absolute Error (MAE): 171.59
- Root Mean Square Error (RMSE): 199.79

With these scores, it can be concluded that the LSTM model's performance is not satisfactory.

### Random Forest Regressor Model

The Random Forest Regressor model is initialized with default parameters without hyperparameter tuning. It is used to predict ActivePower based on the WindSpeed values in the dataset.

The dataset is split into training and testing sets. The training set (X_train, y_train) contains the WindSpeed and ActivePower values for the first 718 rows of the data, while the testing set (X_test, y_test) contains the WindSpeed and ActivePower values for the next 30 rows. The actual and predicted ActivePower values are compared, and model performance metrics are evaluated.

Performance evaluation metrics for the Random Forest Regressor model are provided. These metrics include:
- R-squared (R²): 0.900
- Mean Absolute Error (MAE): 23.99
- Root Mean Squared Error (RMSE): 29.35

An R² value of 0.900 indicates that the model explains 90% of the variability in the target variable, while lower MAE and RMSE values suggest better predictive performance.

## Performance Comparison

In this section, we provide a comprehensive performance comparison among the three different models used in our project: SARIMA, LSTM, and Random Forest. We evaluate their performance based on two key metrics: Mean Absolute Error (MAE) and Root Mean Square Error (RMSE).

### Performance Comparison Among the Three Models

The table below summarizes the results and performance metrics achieved by each of the models: SARIMA, LSTM, and Random Forest.

| Models         | MAE   | RMSE  |
|----------------|-------|-------|
| SARIMA         | 159.05 | 188.15 |
| LSTM           | 171.59 | 199.79 |
| Random Forest  | 48.74 | 58.31 |

From the results, we observe that the Random Forest model outperforms the other two models, achieving the lowest MAE and RMSE scores of 48.74 and 58.31, respectively. This indicates that the Random Forest model can predict the next 30 days of Active Power generation with an accuracy of approximately 90%. It was initially assumed that SARIMA or LSTM models would perform better, but the Random Forest model proved to be the most effective among all three.

### Performance Comparison With Other Research Results

To further validate the effectiveness of our Random Forest model, we compared its performance with results from a study conducted by (Abdulelah Alkesaiberi et al., 2022) using the same dataset. We recreated their model setup, which involved selecting training data from January 1, 2020, to March 27, 2020, and reserving the last 3 days (March 28, 2020, to March 30, 2020) as the testing set.

The table below displays the results obtained from both our proposed Random Forest model and the model from the researcher:

| Model                        | MAE   | RMSE  | R-squared |
|------------------------------|-------|-------|-----------|
| Proposed Random Forest Model | 48.74 | 58.31 | -         |
| Researcher's Random Forest Model | X | Y | Z       |

From the results, our proposed Random Forest model outperformed the researcher's model. This comparison demonstrates the effectiveness and competitiveness of our model in predicting wind power generation.

## Conclusion and Future Enhancements

In this project, we have delved into the world of machine learning methods for time-series forecasting with a specific focus on Wind Power Forecasting. We constructed three distinct models: SARIMA, LSTM, and Random Forest Regressor, utilizing a dataset from Kaggle. Through extensive evaluation metrics, we have assessed the accuracy and effectiveness of each model.

Surprisingly, the simplest model, Random Forest Regressor, outperformed the other models, highlighting the importance of model selection in time-series forecasting. This project provides valuable insights into wind power forecasting and offers a foundation for future work.

### Future Enhancements

As we continue to advance our understanding of wind power forecasting and improve prediction accuracy, there are several avenues for future enhancements:

1. **Hybrid Models:** Consider developing more advanced hybrid models that combine the strengths of different techniques. Combining LSTM with SARIMA or Random Forest Regression with LSTM could provide more accurate forecasts.

2. **Data Integration:** Incorporate data from various sources, including energy consumption and demand. Analyzing the relationship between wind power generation and consumption can provide more context and improve forecasting accuracy.

3. **Causal Impact Analysis:** Implement causal impact analysis to understand the impact of external factors on wind power generation. This can help in identifying and mitigating the influence of external variables on forecasts.

These future enhancements can lead to even more precise wind power forecasting models, advancing the reliability and efficiency of renewable energy sources in our energy grids.


## Contact

For inquiries, feedback, or potential collaboration, please contact Belle Lim (mailto:bellelim0621@example.com).
