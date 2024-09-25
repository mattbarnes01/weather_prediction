# weather_prediction
Weather prediction in Python using Ridge Regression and Random Forest Regressor. Time Series of daily weather used to predict the maximum temperature for tomorrow.
The dataset used is for Dallas Fort-Worth, Texas. The model is therefore designed to predict temperatures for this specific location. Data spans from the 1st January 1975 to 17th September 2024 and was downloaded from the National Center of Environmental Information.

# model
The final model can be found in the weather_predictor file. The model is a random forest regressor trained on data from Dallas Fort-Worth, Texas.
The model is trained using a walk-forward cross validation to preserve the chronological order of the time-series data.
Accuracy of the model is calculated with mean absolute error. The model has a mean absolute error of around 4.95 degrees farenheit when predicting tomorrows daily maximum temperature. This mean absolute error is roughly 6.4% of the average daily maximum temperature (target variable).

# weather_prediction_workings file
This file was the main file i used to perform EDA, feature engineering, hyperparameter tuning, data visualisation etc. It displays my methods and working that led to the final model found in the weather_predictor file. Initially, as seen in the file, I experimented with a ridge regression model since the dataset contained features that have multicolinearity however later I experiment with a random forest regressor and find mean absolute error is reduced (hence this becomes the final model).

# Other files
The original downloaded dataset is the Fort_Worth_weather_data csv file. After manipulating the dataset for use, the final dataset the model is trained on is found in the final_clean_data csv file. The requirements.txt file contains the required packages to run the code. The walk_forward_validation_function file contains the function to cross validate the model whilst keeping the chronological order of the dataset and is imported into the weather_predictor file.

# Additional
Accuracy of the model may be improved in a variety of ways. I noticed that the distribution of features was not normal and began thinking of ways to transform the data into a distribution more closely resembling a normal distribution however the positively skewed features contain many 0.0 values and therefore cannot be log transformed. In addition, the data contains negativly skewed and bimodal features. Handling these proved tricky when using the ridge regression model which is why using a random forest regressor was also more favourable since rfr does not require normalization or scaling. 
Accuracy could be improved by containing additional features and more variables describing other atmospheric conditions. The Fort Worth dataset had many null values in other atmospheric predictors so I decided not to include these predictors as it would mean either dropping or filling a large proportion of the dataset. Instead I created rolling features and percentage change features of the existing predictors with the intent of reducing the effects of any anomolous datapoints (days with dramatic change in temp with no apparent reason as an example).
Outliers could be handled differently to increase accuracy. I removed outliers with a z-score of 3 and above, however many outliers were still present in many different features. I did not remove all outliers due to the risk of removing too much data. I suspect the large amount of outliers is due to data being taken from Dallas, Texas; it is usually hot and rarely experiences precipitation and snow, hence most non zero prcp and snow datapoints will be considered outliers. Using data from another area may be more favourable.
