# Problem and Solution
The existing developed models for predicting solar power generation have different characteristics, resulting in pros and cons in predicting performance by time zone. We aim to develop an ensemble technique that can improve prediction performance by understanding and utilizing the characteristics of these various prediction models.

# Process
- Dimensionally reduce the variables in weather data for each time period, and pre-classify each of the five provided models based on which prediction model performs best at a given time.
- Derive the final actual power generation prediction value by voting with RandomForest, Lasso, and Huber Regressor.

# Results
😍 8th / 150 teams
