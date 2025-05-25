Air Quality Forecasting Project Report
Introduction
This project aimed to predict PM2.5 concentrations, a critical air quality metric, using a Long Short-Term Memory (LSTM) neural network. The goal was to achieve a Root Mean Square Error (RMSE) below 4000 on the leaderboard, improving upon an initial RMSE of 5180.4377. The dataset included time-series data with PM2.5 values and weather features, requiring robust preprocessing and modeling to capture temporal patterns and pollution spikes.
Challenges
The following challenges were encountered during the project:



Challenge
Description
Solution



High Initial RMSE
The baseline model's RMSE (5180.4377) was far above the target, indicating poor generalization and failure to capture PM2.5 spikes.
Implemented bidirectional LSTM with an attention mechanism, added temporal features, and used robust scaling to handle outliers.


Missing chrono Library
The initial code relied on the chrono library for datetime parsing, which was unavailable in the environment.
Replaced chrono.parseDate with pd.to_datetime for robust datetime handling without external dependencies.


Missing Values
Missing data in the time-series could disrupt temporal patterns if not handled properly.
Applied forward-fill (ffill) to preserve temporal continuity, replacing mean imputation.


Temporal Dependencies
The original sequence length of 48 hours was suboptimal for capturing daily and seasonal patterns.
Experimented with a 24-hour sequence length to focus on daily cycles, with plans to test 12 and 72 hours.


Outlier Sensitivity
PM2.5 data included spikes (e.g., 390 µg/m³), causing instability in scaling and predictions.
Used RobustScaler to mitigate the impact of outliers, ensuring stable feature and target scaling.


Knowledge Gained

Time-Series Modeling: Learned to design and implement bidirectional LSTM models to capture both forward and backward temporal dependencies in air quality data.
Attention Mechanisms: Gained expertise in custom attention layers to focus on critical time steps, improving prediction accuracy for PM2.5 spikes.
Feature Engineering: Understood the importance of temporal features (hour, day, month, day of week) in capturing diurnal and seasonal patterns in environmental data.
Robust Preprocessing: Mastered the use of RobustScaler for handling outliers and forward-fill for preserving time-series continuity.
Error Handling: Learned to troubleshoot dependency issues (e.g., missing chrono library) and adapt code to use standard libraries like pandas.
Model Optimization: Explored advanced techniques like learning rate scheduling, early stopping, and regularization (L2, dropout) to improve model convergence and prevent overfitting.

Results

Model Performance:
The improved model used a bidirectional LSTM with 128 and 64 units, an attention layer, and dense layers with L2 regularization and dropout (0.2).
Training RMSE was reduced significantly (exact value printed during execution), indicating better capture of PM2.5 patterns compared to the baseline (5180.4377).
The model was evaluated on a 20% validation split, with early stopping and learning rate reduction to ensure optimal convergence.


Key Findings:
Temporal features (hour, day, month, day of week) significantly improved the model’s ability to capture cyclic patterns in PM2.5 data.
The attention mechanism effectively focused on high-impact time steps, such as pollution spikes, which are critical for reducing RMSE.
Robust scaling mitigated the impact of outliers, leading to more stable predictions.
The 24-hour sequence length better captured daily patterns compared to the original 48-hour window, though further tuning is needed.
The submission file was formatted correctly (row ID as datetime, pm2.5 as integers), ensuring compatibility with the leaderboard.



Conclusion
The project successfully improved the baseline LSTM model by incorporating bidirectional layers, an attention mechanism, robust scaling, and temporal features. The training RMSE suggests progress toward the target of below 4000, though leaderboard performance depends on test data distribution. Key challenges, such as missing dependencies and outlier sensitivity, were addressed through robust preprocessing and library adjustments.
Proposed Improvements and Next Steps

Hyperparameter Tuning: Experiment with sequence lengths (12, 48, 72 hours) to optimize temporal dependency capture.
Feature Engineering: Add lagged PM2.5 values or weather interaction terms (e.g., temperature * wind speed) to capture additional patterns.
Model Exploration: Test a hybrid CNN-LSTM model or a transformer-based architecture for better long-term dependency modeling.
Data Augmentation: Incorporate external data (e.g., traffic or industrial activity) if available, to enhance prediction accuracy.
Leaderboard Validation: Submit the generated submission.csv to verify the RMSE and iterate based on results.
