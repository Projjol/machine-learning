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
In this section, you will need to clearly define the metrics or calculations you will use to measure performance of a model or result in your project. These calculations and metrics should be justified based on the characteristics of the problem and problem domain. Questions to ask yourself when writing this section:
- _Are the metrics you’ve chosen to measure the performance of your models clearly discussed and defined?_
- _Have you provided reasonable justification for the metrics chosen based on the problem and solution?_


## II. Analysis
_(approx. 2-4 pages)_

### Data Exploration
In this section, you will be expected to analyze the data you are using for the problem. This data can either be in the form of a dataset (or datasets), input data (or input files), or even an environment. The type of data should be thoroughly described and, if possible, have basic statistics and information presented (such as discussion of input features or defining characteristics about the input or environment). Any abnormalities or interesting qualities about the data that may need to be addressed have been identified (such as features that need to be transformed or the possibility of outliers). Questions to ask yourself when writing this section:
- _If a dataset is present for this problem, have you thoroughly discussed certain features about the dataset? Has a data sample been provided to the reader?_
- _If a dataset is present for this problem, are statistics about the dataset calculated and reported? Have any relevant results from this calculation been discussed?_
- _If a dataset is **not** present for this problem, has discussion been made about the input space or input data for your problem?_
- _Are there any abnormalities or characteristics about the input space or dataset that need to be addressed? (categorical variables, missing values, outliers, etc.)_

### Exploratory Visualization
In this section, you will need to provide some form of visualization that summarizes or extracts a relevant characteristic or feature about the data. The visualization should adequately support the data being used. Discuss why this visualization was chosen and how it is relevant. Questions to ask yourself when writing this section:
- _Have you visualized a relevant characteristic or feature about the dataset or input data?_
- _Is the visualization thoroughly analyzed and discussed?_
- _If a plot is provided, are the axes, title, and datum clearly defined?_

### Algorithms and Techniques
In this section, you will need to discuss the algorithms and techniques you intend to use for solving the problem. You should justify the use of each one based on the characteristics of the problem and the problem domain. Questions to ask yourself when writing this section:
- _Are the algorithms you will use, including any default variables/parameters in the project clearly defined?_
- _Are the techniques to be used thoroughly discussed and justified?_
- _Is it made clear how the input data or datasets will be handled by the algorithms and techniques chosen?_

### Benchmark
In this section, you will need to provide a clearly defined benchmark result or threshold for comparing across performances obtained by your solution. The reasoning behind the benchmark (in the case where it is not an established result) should be discussed. Questions to ask yourself when writing this section:
- _Has some result or value been provided that acts as a benchmark for measuring performance?_
- _Is it clear how this result or value was obtained (whether by data or by hypothesis)?_


## III. Methodology
_(approx. 3-5 pages)_

### Data Preprocessing
In this section, all of your preprocessing steps will need to be clearly documented, if any were necessary. From the previous section, any of the abnormalities or characteristics that you identified about the dataset will be addressed and corrected here. Questions to ask yourself when writing this section:
- _If the algorithms chosen require preprocessing steps like feature selection or feature transformations, have they been properly documented?_
- _Based on the **Data Exploration** section, if there were abnormalities or characteristics that needed to be addressed, have they been properly corrected?_
- _If no preprocessing is needed, has it been made clear why?_

### Implementation
In this section, the process for which metrics, algorithms, and techniques that you implemented for the given data will need to be clearly documented. It should be abundantly clear how the implementation was carried out, and discussion should be made regarding any complications that occurred during this process. Questions to ask yourself when writing this section:
- _Is it made clear how the algorithms and techniques were implemented with the given datasets or input data?_
- _Were there any complications with the original metrics or techniques that required changing prior to acquiring a solution?_
- _Was there any part of the coding process (e.g., writing complicated functions) that should be documented?_

### Refinement
In this section, you will need to discuss the process of improvement you made upon the algorithms and techniques you used in your implementation. For example, adjusting parameters for certain models to acquire improved solutions would fall under the refinement category. Your initial and final solutions should be reported, as well as any significant intermediate results as necessary. Questions to ask yourself when writing this section:
- _Has an initial solution been found and clearly reported?_
- _Is the process of improvement clearly documented, such as what techniques were used?_
- _Are intermediate and final solutions clearly reported as the process is improved?_


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

## VI References
* [Techinal Analysis](http://www.investopedia.com/terms/t/technicalanalysis.asp)
* [Fundamental Analysis](http://www.investopedia.com/terms/f/fundamentalanalysis.asp)
* [Quantitative Analysis](http://www.investopedia.com/terms/q/quantitativeanalysis.asp)
* [Mean Absolute Error](https://www.kaggle.com/wiki/MeanAbsoluteError)
* [Techical Indicators](http://stockcharts.com/school/* doku.php?id=chart_school:technical_indicators:introduction_to_technical_indicators_and_oscillators)

**Before submitting, ask yourself. . .**

- Does the project report you’ve written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Analysis** and **Methodology**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your analysis, methods, and results?
- Have you properly proof-read your project report to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
- Is the code that implements your solution easily readable and properly commented?
- Does the code execute without error and produce results similar to those reported?
