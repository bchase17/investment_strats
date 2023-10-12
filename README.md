# investment_strats
Various algorithms for analyzing stock market movements and patterns

## Key variables as leading  indicators

### Overview
The first of these algorithms is a general exploration into how certain key variables perform for stock market movements as leading indicators across various time series. The reason for this analysis is to attempt to find a way to optimize investment decisions by maxmizing the likleihood of investing money ahead of the stock market rising and decrease risk when the market is expected to pull back from its current value.
These indicators include:
- The Volatility Index ETF (VXX)
- Index moving averages (50, 100 and 200 days)
- Treasury rates (2, 10 and 30 years)
- Relative Strength Index

### Files in Repository
'Key Indicators Market Analysis'.ipynb --> this has all of the code, from data aggregation/exploration to data analysis and machine learning training. The end of the code has the output of which indicators are most predictive for market movements and their respective weights.
'visuals.py' --> contains functions for visualizing the results of ML models

### Steps Taken:

Initial Collection and Exploration
- The library being used to pull in all stock market data is Alpha Vantage, which works by sending requests to its API for specific datapoints, like historic stock information, treasury rates and relative strength index historic values
- Each datapoint is pulled into a dataframe and then viewed to see what fields are included. From there, the dataframes are cleaned up by only including required fields and enhancing with any new fields needed for the analysis, such as moving averages

Further Cleanup/Data Enhancements
- In this section, we are adding binary variables for creating a discrete machine learning algorithm in a future step.
- We are adding moving averages for the main data points, which tells us the prior average for the datapoint over n_days
- Once those calculations are performed, we discretize the data by applying a value of 1 if the value is above its n_moving average and 0 if it is below
- This is repeated for each variable and for rates/RSI, we look at if the trailing n_days are rising or falling as our discretized value

Prepare DataFrames for Analysis
- The last step is to break out the data into a discrete dataframe and remove all continuous datapoints. We are also adding our dependent variables, which are how the market performed over n_days
- The market performance columns are added to the discrete dataframe and calculated so that we can train our model later on
- This is also done for the continuous dataset, however that analysis is not being done yet and will be a future task

Main Functions
- This section puts all of the above steps into one function for a more seamless execution of the code, where a user feeds in the stocks it wants to run the analysis for

Start Analysis
- Here we are actually creating our ML model and testing the predictability of each variable
- First we do an initial visualization of each variable for each n_day period we are trying to predict, where we chart how much more likley the market is to hae a positive return over n_days when the inidcator is true vs. when it is false. This ration is then visualized using a bar chart and is an indicator of what variables are most important
- Next we actually create and train our ML model by creating two dataframes: one for our independent variables and the other for our dependent variable
- The model breaks the dataset into a training and testing set, where 20% of the data is set aside for training
- Next we do some preliminary performance analysis and see what the naiave accuracy and f-score are
- Then we establish the function that will be used for actually training the model
- Once that is established, we test a few different models to see which are performing best for further tuning and training

Top Model Optimization
- The last steps are to optimize the best performing model, based on the previous step
- Here we train it by tuning different paramaters and seeing how we can increase the accuracy and f-scores the most
- Once that is finished, we visualize which variables have the most explanatory power for our model by printng the weights for the first 5 most predictive features
