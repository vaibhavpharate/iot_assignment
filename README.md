# IoT Assignment
This project focusses on the importance and uses of the weather data “Feels Like Temprature” which can be majorly used for Advertising. The aim of this project is to analyse the the difference between “Temperature” and “Feels LikeTemperature” of the Location “Hinjewadi, Pune” and find out a better hyper tuned model that can forecast the “Feels Like
**Title: Finding the Ideal way to Forecast the “Feels Like Temperature” of a Location by extracting the Data in Realtime**

**Purpose of the Project:** 

This project focusses on the importance and uses of the weather data “Feels Like Temprature” which can be majorly used for Advertising. The aim of this project is to analyse the the difference between “Temperature” and “Feels LikeTemperature” of the Location “Hinjewadi, Pune” and find out a better hyper tuned model that can forecast the “Feels Like Temperature” as accurately as possible.

**Why we considered “Feels Like Temperature” instead of temperature:** 

Temperature refers to the actual measure of the air temperature, usually recorded in degrees Celsius or Fahrenheit. Feels like temperature, on the other hand, takes into account other factors such as humidity, wind speed, and sunshine, which can affect how the temperature feels to the human body. It is a measure of the perceived temperature or how hot or cold it actually feels to a person.

**Why is forecasting “Feels Like Temperature” Necessary:**

Feels like temperature is often used in advertising to promote products or services that are related to weather conditions or seasonal activities. For example, a company that sells outdoor apparel or equipment may use feels like temperature in their advertising to emphasize the importance of their products in protecting customers from the elements. By highlighting the actual conditions that people experience, and how it feels to be outside in those conditions, feels like temperature can be a powerful marketing tool for brands that are targeting consumers who are sensitive to weather changes.

In addition to promoting products that are related to weather or outdoor activities, feels like temperature can also be used in advertising to create a sense of urgency or to encourage certain behaviors. For example, a travel company may use feels like temperature in their advertising to encourage people to book a warm weather vacation during a particularly cold or dreary time of year. By emphasizing the contrast between the actual temperature and the perceived temperature, they can make their offer seem more attractive and necessary.

Feels like temperature can be used in advertising for food and beverage products, especially during hot or cold weather. For instance, a beverage company may promote their cold drinks during a heatwave by highlighting how refreshing they are when it feels like the temperature is above 100 degrees Fahrenheit. Similarly, a coffee company may emphasize how comforting their hot drinks are during a cold snap when it feels like the temperature is below freezing.

Overall, feels like temperature is a useful tool for advertisers who want to create a connection between their product or service and the conditions that their target audience is experiencing. By using this metric, they can make their offer seem more relevant and compelling, and drive interest and engagement from potential customers.



**DataSet:**

Visual Crossing is a leading provider of weather data and enterprise analysis tools to data scientists, business analysts, professionals, and academics. Their weather API Tokens have been used to extract the weather data in real time. The extracted data consists of various factors like, Temperature, Feels like temperature, Precipitation, Due, Snow, wind, solar radiation, and many more of a slected locality of the requested timeline. Heat index of the dataset is the measure of how hot it feels combining the actual air temeperature with the relative humidity. Wind Chill is the measure of how cold it feels combining with the actual air temperature with the wind speed. Finally the star attribute “Feels Like Temperature”considered in this project is a combination of  heat index and wind chill.

**Methodolgy:**

The flow of this project goes like below:

1. Select Weather Data Perameters(Like Location, Start Date, Finish Date)
1. Extract the Data
1. Covert it into Usable Format
1. Read the Final Dastaset
1. Filter the required Columns
1. Scale the data
1. Analyse the difference between the Variables Temperature & Feels Like Temperature
1. Perform Dickey Fuller test to check if the time series data is Stationary
1. If  Data is Not Satationary Perform Data Transformation Techniques
1. ` `Find Optimal Seasonal & Non-seasonal paprameters of the ARIMA model suitable for this specific dataset
1. Fit the training data into ARIMA Model & Evaluate its Performance
1. ` `To Compare the performance of the Models Perform LSTM @epoch=30, optimiser=”Adam”, loss = “Mean Squared Error”
1. Evaluate the performace of the LSTM Model
1. Compare the performance of both the models & Conclude the findings

**Data Extraction:**

Using VisualCrossing API to extract the weather data

\1. Setup the Location As per your choice

\2. Give Start Date for historical data extraction in the format(YYYY-MM-DD)

\3. Give Start Date for historical data extraction in the format(YYYY-MM-DD)

![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.001.png)

**Scaling the Data:**

- MinMaxScaler is used to scale the data, 
- This scaling helps in briging the data into the range 0-1, avoiding any kind of bias in the forecasting.

**Analyse the difference between the Variables Temperature & Feels Like Temperature**

**Blue: Represents Feels Like Temperature**

**Red: Represesnts Actual Temperature**

![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.002.png)

From the above graph it can be seen that in Hinjewadi, Pune Druing the months of Summer(March, April,May) the Feels Like Temperature is lower than the actual Temperature. However, during the months of Rainy Season(August, September, October) Feels like temperature is higher than the actual temperature. 

**Dickey Fuller Test:**

ARIMA cannot be applied in case of Non-stationary Datasets. So to get the best output of ARIMA Models it is necessary to do stationary test on the time series dataset

Following is the output of Dickey Fuller Test:

![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.003.png)![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.004.png)

The results show that  Time series data is not Stationary

**Data Transformation Methods:**

Time Series Data Transformation from Non Stationary data to Stationary Data through Differencing Techniques. In this technique the following steps are followed, 

1. Use NumPy’s square root function to transform the required column
1. Then shift the transformation by one using the “shift’ function.
1. Take the difference between both the original transformation and shift.

Perform the Dickey Fuller test to check if the data is Transformed or not:

![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.005.png)![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.006.png)

Therefore, it can be seen that the time series data has now become statioanry, making it ideal to perform ARIMA on it

Cons of this Transformation Technique:

- Using this technique modifies the feels like temperature so much, making it hard to caluculate back to the original temperature of Hinjewadi. Resulting in forecasting temperature values that are not understandale by the users/audience.

**Alternative method of Data Transformation:**

Another way of dealing with Non stationary Data in ARIMA Models using Integrate(I) concept

In Auto ARIMA(p,d,q)(P,D,Q), the model itself will generate the optimal p, d, and q values which would be suitable for the data set to provide better forecasting even for Non stationary Data.

1. p — the number of autoregressive
1. d — degree of differencing
1. q — the number of moving average terms
1. (P, D, Q )— represents the (p,d,q) for the seasonal part of the time series
1. m — refers to the number of periods in each season

Note: In the Auto ARIMA model, note that small p,d,q values represent non-seasonal components, and capital P, D, Q represent seasonal components

This transformation method is ideal for “Feels Like temperature” data we are dealing with as the only change in the data done through this method is taking log of the values which is easily reversible for forecasted values and the temperature values can be understood by the audience.

**Division of Training& Testing Data: (@90:10) Ratio**

![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.007.png)

**Hyper Tuning Parameter of ARIMA Model to find optimal p,q,d parameters:** 

![](Aspose.Words.3d4c9f2c-11a5-4111-b9ef-6a0f7965e7ab.008.png)

Optimal Values Found out during Analysis are: p: 2, q: 1, d: 1, P: 0,Q: 0, D:0, M:0

**LSTM Models:**

Parameters Chosen for the LSTM Model are:

Neurons in Layer-1: 128

Neurons in Layer-2: 64

Optimizer: Adam

Loss: Mean Squared Error

Epochs: 30

**Evaluating the Performace of both ARIMA & LSTM Models:**

|**Model**|**RMSE**|**MAE**|**MAPE**|
| - | - | - | - |
|ARIMA|0.14|0.11|0.04|
|LSTM|0.53|0.40|0.02|

MAPE means Mean Absolute Percentage Error it explains the average difference, lower the value of MAPE, better is the prediction of the model

**Conclusion:** Lesser MAPE Value for LSTM Indicates that it has an accuracy of 98% in forecasting the feels like temperature of Hinjewadi i.e, better than the performance of ARIMA Model with a MAPE Value of 0.04 i.e., 96% Accurate

Therefore For forecasting the future “Feels Like Temperature” of Hinjewadi, LSTM model can be deployed based on which personolised regional mobile advertisement can be sent.

**Future Study:**

This part of the project covers solving the baseline problem of how to approach the temperature forecasting problem of a locality. As the code provided in this project is Dynamic. A web interface can be developed where user can choose the location, starting date, Ending date of his Choice. The forecasted values values can be connected to Clothing Database to suggest the user outfits he can wear through the week. Or the the forecasted values connected to a Recommendation model, can pop up some temperature appropriate advertisements in his mobile. Like Zomato Sends Ice Cream Ads during the hottest temperature of the day.

