# Machine Learning Engineer Nanodegree
## Capstone Project
Projjol Banerji  
August 22nd, 2017

## I. Definition

### Project Overview
Stock price prediction has been an interesting and hard problem for quite a while now. The information it provides can give an individual or even a firm a strong overview of what is to come helping them plan for the same. My motivation for the project stems out of my interest in the 2008 economic crash. While I was quite young at that point, I remember it as a defining moment in our history. Later on, as I grew up, I tried to collect as much information about the event as possible. Throughout this process, all that was there in my mind was, how could Wall Street not see this coming? The answer to that I would think is cognitive bias. I think this is a blatant example of the normalcy bias, wherein even in moments of grave danger, one pretends as if everything is fine. With the knowledge that I acquired through the course of the nanodegree, I felt I could help create a prediction tool, which would provide people with data that can help them get over this bias, and help me understand the stock market better. 

In this project, I will be using technical analysis as a method to make sense of the data and make accurate predictions from it. In technical analysis past trading activity and price changes of a security are better indicators of the security's likely future price movements, which is the eventual goal in this project. Technical analysis derives from two underlying principles:
* Market price discounts every factor that may influence a security's price
* Market price movements are not purely random but move in identifiable patterns and trends that repeat over time
For technical analysis to be used, technical indicators will be used for forecasting future prices. More on this in the later sections.


The other forms of financial analysis that are available to us but not used in this project are :
* Fundamental Analysis: Evalutaion of a security via going through the financial statements of a company to determine the intrinsic value of the givne security. Once this has been determined, comparing the intrinsic value versus the market value, gives the investor insight as to whether the security is undervalued or overvalued, thereby letting him buy more or sell respectively. This sort of analysis will not help us, as the primary objective of fundamental analysis and this project are not the same
* Quantitative Analysis: It is a branch of financial analysis wherein events and behaviours are predicted using mathematical measurements and statistical modelling. Quantitative analysis is an important tool and is used in a variety of situations from the evaluation of an instrument to predicting changes in a country's GDP (Gross Domestic Product)

In this project I will be creating a stock market predictor, which has ingested data from 16 years and would predict the estimated value of the market on a given query date. 


### Problem Statement

The problem at hand is to accurately predict future market prices for a given index or asset. For this, I will use the S&P 500 index. Reasons for using this index over others are:
* Historic data dating back to the 1990s is easily available for this index, allowing the learning algorithm to see more examples and thereby more variations in the data
* Another popular index is the DOWJ 30 index, but the problem with that index is that it monitors the prices for only 30 selected companies. The S&P 500 index on the other hand is considered a litmus test for the American economy as a whole and trends followed in it affect not only the American business economy but global economies 
* Given the influence of the index and the far reaching data, it made sense to me to use the S&P 500 index

#### Concerning the random walk theory
In 1973, Burton Malkiel released a monumental book known as "A Random Walk Down Wall Street" in which he mentions how stock prices work as random walks, i.e. their current and past prices do not affect the future, i.e. they are non-deterministic in nature. 

Given this information, using index values as-is will not help us. To mitigate the problem, what the model will actually receive as input would be a set of technical indicator values over a given period of time. As the model learns the relationship that these indicators have for given index values, I do belive it can understand the underlying trend the data is following. 

#### Methodology behind the solution
In this section, I would like to breifly list out the steps taken out for the solution:

* Via the zipline package's load_bars_from_yahoo method get historical stock data espcially for Open, Close, High, Low and Volume
* Create values for the selected technical indicators using the datapoints received in the previous step
* Split the data into test and train datasets
* Build model and check for performance on the basis of the metrics that will be determined in the next section

### Metrics
I belive the fundamnetal problem at hand is one of regression and for regression models, predicting the Mean Absolute Error (MAE) is a good metric to determine the performance of the agent. To define MAE, it is a quantity used to measure how close forecasts or predictions are to the eventual outcomes. The formula is as follows: 

![MAE formula](http://i.imgur.com/q8lQz2c.gif )

In this case, the MAE calculates the mean difference in values over the predicted and correct values. A high MAE shows that the model is not working the way it should and has not learnt the trend of the underlying data. A low MAE shows the very opposite of that, i.e the model has learnt the trend of the underlying data and fit itself well to it. 

## II. Analysis

### Data Exploration
The data being used in this project is sourced via the Yahoo Finance API. Since the API in itself is not well documented and several parts of it have been depracted, I have used the zipline python package that loads historical data from the API without an issue. The total package expects certain parameters to be provided to it for fetching data, such as time period and index to be monitored. The time period I have specified is from the 1st of Jan 2000 - 1st of Jan 2017, a total of 17 years. 

![data.describe()] (http://i.imgur.com/enEy3gf.png)

The package returns data with multiple features that are :
* Open: Price of the stock [in our case value of the index] in the beginning of the day
* High: Highest recorded price/value recorded in that day of trading           
* Low: Lowest recorded price/value recorded in that day of trading                     
* Close: Price/value recorded at the end of the day
* Price: Adjusted price for stock splits/joins in the day [note: this feature is more important when considering specific companies and not entire indexes such as the S&P 500]
* Volume: Total number of shares traded in that day

### Exploratory Visualization
Below are plots of all the features that we get from zipline:

![Open](http://i.imgur.com/r0G3RqL.png)
![Close](http://i.imgur.com/1mrJQxJ.png)
![High](http://i.imgur.com/wYpiaKv.png)
![Low](http://i.imgur.com/K0752Pi.png)
![Price](http://i.imgur.com/1fEXx5c.png)
![Volume](http://i.imgur.com/AdsMEHR.png)

All the features together:
![Together](http://i.imgur.com/aMMCAG1.png)

An interesting observation is that all the values of the features returned by zipline are quite similar. The reason for this is that in a stable index such as the S&P 500, individual parameters don't stray afar from each other, as a whole the index does well or poorly. It's worthwhile to note the spike in the graphs around 2008-2009 which corresponds to the global economic meltdown, very low volumes for very high prices.

### Algorithms and Techniques
Given that this is a regression problem, I would like to use linear regression as my learner for a given input. The input itself will be a set of technical indicators. The dependant value, or the value that needs to be predicted would be the 'price' variable. Linear regression helps us model the relationship between a scalar dependant variable [y] and a set of explanatory variables [X]. If the learner is successfull, it would understand the trend of the underlying data and the corresponding MAE would be small. For further refinement and improvement I would like to try a SVM implementation. 


### Benchmark
Luckily, there exists an industry standard that monitors the fluctuaions in the value of the 'price' component of our data. It is the CBOE VIX [Chicago Board Options Exchange Volatility Index] value. The VIX value changes everyday and is a benchmark to analysts and traders as to how much volatility one might see in the data for that trading day. From the CBOE's website, I downloaded VIX values from 1998-2017. Computing an average VIX value on these inputs, I got the value as : 19.81. Thus, the goal for the linear regression learner is to predict prices that are better/lower than the average VIX value. To carry out this comparision, the metric defined above, the MAE will be useful.


## III. Methodology

### Data Preprocessing
The first step in data preprocessing would be to parse the historic data into the selected technical indicators which can then be used for prediction. Following is a summary of the technical indicators being used:

- Momentum: It measures the securities rate-of-change. Like in physics, it is a measurement that provides details of the acceleration/deceleration of the stock in question. On the basis of whether the speed is upwards/downwards bullish/bearish interpretations might be made
- Relative Strength Index: The RSI creates a measure of value between 0-100, key points being above 70 and below 30. On the basis of these two keypoints one can determine whether the stock is overbought or undersold. If a particular stock is above 70, it can be considered as overbought, similarly for a stock below 30, it is considered to be undersold
- On Balance Volume: Another momentum indicator, it uses volume flow to predict changes in stock price. The belief is that when volume increases sharply without a significant change in the stock's price, the price will eventually jump upward, and vice versa.
- Simple Moving Average: It is an arithmetic moving average calculated by adding the closing price of the security for a number of time periods and then dividing this total by the number of time periods. This is important to traders, as when short-term SMAs cross long-term SMAs it gives them a signal to buy/sell
- Exponential Moving Average: It is similar to a simple moving average, except that more weight is given to the latest data, this gives traders a better idea about day-to-day nuances but can also give false buy/sell signals, which is why it is used alongside SMA
- Weighted Moving Average: Similar to EMA, however WMA assigns a unique weight to every element in the period, not just the latest observations. Additionally, the sum of all weights is 1
- Double Exponential Moving Average: It is an attempt to reduce the amount of lag time found in traditional moving averages. It is a composite implementation of single and double EMAs producing another EMA with less lag than either of the original two 
- Average Directional Index: is an indicator used in technical analysis as an objective value for the strength of a trend. ADX is non-directional, so it quantifies a trend's strength regardless of whether it is up or down. Higher the number, stronger the trend, lower the number, weaker it is
- Rate of Change Percentage: It is a momentum indicator that measures the percentage change in price between the current price and the price n periods in the past
- Williams %R: It has values on an inverted scale, i.e. 0 at the top and 100 at the bottom. Similar to RSI, it has two keypoints, 20 and 80. Stock values below 20 are considered overbought and those over 80 as oversold

After selecting all the technical indicators, they're normalized between -1 and 1 to bring all the values to the same scale. Following are plots of multiple indicators post normalization:

![5 indicators](http://i.imgur.com/ph8deHu.png)
![rocp willr](http://i.imgur.com/903t9Zb.png)
![mom dx rsi](http://i.imgur.com/kbtqOvW.png)

As it can be seen, normalizing these values or using technical indicators instead of the input historic data has not removed the underlying trend that can be seen [one can still see major peaks and troughs in the 2008-09 period]

### Implementation
It is time to implement the linear regression learning model. The linear regression formula used will be simple: 

![linear regression](http://i.imgur.com/xacSGaE.gif)

In this equation, y is predicted price, xi is the technical indicator and ki and b are co-effcients that need to be tuned to get the right value. 

Once the regression model is fixed, I would split the data into two parts, the training set and the test set. The need to do this as has been made clear during the nanodegree is to overcome the problems of overfitting and to check how accurate our predictions are. 

### Refinement
The previous section saw the implementation of a simple learning model using linear regression. In this section, I will buid a new learning agent using SVM. A major difference in my approach to SVM vis-a-vis the linear regression model would be the selection of hyperpaarameters. The best way for to choose hyperparameters for the model are via cross-validation I feel. In cross validation one creates ultiple train-test sets or folds and runs the model on many combinations of these folds. One point that needs to be kept in mind here is that during the course, cross-validation was used by running random training data on the model, however, given the time sensitive information held by this dataset random selection is not possible. To mitigate this issue for every nth fold, the train set should run on 1..n and the test set should run on the n+1th fold. For example :

If there are 3 folds,
* Train should run on fold 1, fold 2
* Test should run on fold 3


## IV. Results
_(approx. 2-3 pages)_

### Model Evaluation and Validation
In this section, the final model and any supporting qualities should be evaluated in detail. It should be clear how the final model was derived and why this model was chosen. In addition, some type of analysis should be used to validate the robustness of this model and its solution, such as manipulating the input data or environment to see how the model’s solution is affected (this is called sensitivity analysis). Questions to ask yourself when writing this section:
- _Is the final model reasonable and aligning with solution expectations? Are the final parameters of the model appropriate?_
- _Has the final model been tested with various inputs to evaluate whether the model generalizes well to unseen data?_
- _Is the model robust enough for the problem? Do small perturbations (changes) in training data or the input space greatly affect the results?_
- _Can results found from the model be trusted?_

### Justification
In this section, your model’s final solution and its results should be compared to the benchmark you established earlier in the project using some type of statistical analysis. You should also justify whether these results and the solution are significant enough to have solved the problem posed in the project. Questions to ask yourself when writing this section:
- _Are the final results found stronger than the benchmark result reported earlier?_
- _Have you thoroughly analyzed and discussed the final solution?_
- _Is the final solution significant enough to have solved the problem?_


## V. Conclusion
_(approx. 1-2 pages)_

### Free-Form Visualization
In this section, you will need to provide some form of visualization that emphasizes an important quality about the project. It is much more free-form, but should reasonably support a significant result or characteristic about the problem that you want to discuss. Questions to ask yourself when writing this section:
- _Have you visualized a relevant or important quality about the problem, dataset, input data, or results?_
- _Is the visualization thoroughly analyzed and discussed?_
- _If a plot is provided, are the axes, title, and datum clearly defined?_

### Reflection
In this section, you will summarize the entire end-to-end problem solution and discuss one or two particular aspects of the project you found interesting or difficult. You are expected to reflect on the project as a whole to show that you have a firm understanding of the entire process employed in your work. Questions to ask yourself when writing this section:
- _Have you thoroughly summarized the entire process you used for this project?_
- _Were there any interesting aspects of the project?_
- _Were there any difficult aspects of the project?_
- _Does the final model and solution fit your expectations for the problem, and should it be used in a general setting to solve these types of problems?_

### Improvement
In this section, you will need to provide discussion as to how one aspect of the implementation you designed could be improved. As an example, consider ways your implementation can be made more general, and what would need to be modified. You do not need to make this improvement, but the potential solutions resulting from these changes are considered and compared/contrasted to your current solution. Questions to ask yourself when writing this section:
- _Are there further improvements that could be made on the algorithms or techniques you used in this project?_
- _Were there algorithms or techniques you researched that you did not know how to implement, but would consider using if you knew how?_
- _If you used your final solution as the new benchmark, do you think an even better solution exists?_

-----------

## VI. References
* [Techinal Analysis](http://www.investopedia.com/terms/t/technicalanalysis.asp)
* [Fundamental Analysis](http://www.investopedia.com/terms/f/fundamentalanalysis.asp)
* [Quantitative Analysis](http://www.investopedia.com/terms/q/quantitativeanalysis.asp)
* [Mean Absolute Error](https://www.kaggle.com/wiki/MeanAbsoluteError)
* [Techical Indicators](http://stockcharts.com/school/doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators)
* [Exponential Moving Average](http://www.investopedia.com/terms/e/ema.asp)
* [Simple Moving Average](http://www.investopedia.com/terms/s/sma.asp)
* [Double Exponential Moving Average](http://www.investopedia.com/articles/trading/10/double-exponential-moving-average.asp)

**Before submitting, ask yourself. . .**

- Does the project report you’ve written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Analysis** and **Methodology**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your analysis, methods, and results?
- Have you properly proof-read your project report to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
- Is the code that implements your solution easily readable and properly commented?
- Does the code execute without error and produce results similar to those reported?
