# AlgoTrading

This repo is based on the final project of the course "Algorithmic Trading" taught at Hult International Business School by professor Michael Rolleigh. The goal is to backtest a trading algorithm that recieves the output from a machine learning model as a signal to perform the strategy. Please find the final results in `Algorithmic Trading in Python.pdf`  

The corresponding tasks are divided in the following notebooks: 


## `AlgoTrading.ipynb`:

Contains the data science workflow. This script was used as a research environment with the objective of extracting the signal from fundamental and alternative data. The signal extraction was done by ultimately developing a machine learning model that had as target returns in a particular stock (in this case Redhat [RHT] stocks).

* <b> Data Collection, Cleaning, and Exploration: </b>
The Github repo `GetOldTweets` was used to webscrape all the mentions that Redhat had in the past 4 years (2014 - 2018). a total of 56,400 tweets were collected and cleaned. A sentiment analysis was undertaken by implementing `VaderSentimentAnalyzer`. After computing the sentiment score for each tweet, they were aggregated by adding the number of positive, negative and neutral tweets. Finally, these aggrageted tweetes were inner joined by time stamp with the fundamental data data frame. These two dataframes consisted of the following: 

  * Fundamental Data: 

    * Diluted EPS
    * EBIT Margin
    * EBITDA Margin	Revenue % Growth
    * EBITDA % Growth
    * EBIT % Growth
    * NetIncome % Growth
    * Net Debt to Equity

  * Alternative Data: 

    * Favourites	
    * retweets	
    * Compound	
    * Positive	
    * Neutral	
    * Negative

* <b> Machine Learning: </b>

 The data was splitted into training and Test Set (85% | 15%). The target consisted of the stock returns and the features consisted of the previously stated Fundamental and Alternative data. After having the target and features correctly splitted, the baseline model was created. This model consisted of a simple decision tree with no constraints in its max depth. Thus, it was hugely overfit. After this, a 5-fold cross validation was done in order to assess how overfit this model was. Finally, a cross validated gridsearch was used with the purpose of finding the best hyperparameters and the optimized decision tree was created. The same process was done with a random forest with the difference of performing feature selection. This process was repeated with Gradient Booster and Neural Nets in order to compare and contrast different machine learning models. 
 
The baseline model (hugely overfit decision tree) was used for the backtesting in order to exemplify the dangers of overfitting in trading. 

 
## `Backtesting.ipynb`

Backtesting consists of creating a trading strategy and going back in time simulating 'what would have happened' if the strategy was implemented in such time frame. The time frame selected in this script ranged from 2014-01-02 to 2018-12-30. Finally, `bt` was used as the backtesting library for this project.   
3 different strategies were implemented: 

1. Baseline Strategy 
    * If predicted return is greater than 2% buy all the stocks with the available funds that we have (e.g. $1,000,000 in stocks).
    * If predicted return is greater than 1% buy half the stocks with the available funds that we have (e.g. $500,000 in stocks).
    * If predicted return is less than -2% sell all the stocks with the available funds that we have (e.g. $1,000,000 in stocks).
    * If predicted return is greater than -1% sell half the stocks with the available funds that we have (e.g. $500,000 in stocks).
    
2. Baseline Strategy + Limiting the change of position by a max of 10% a day
    * The limit in change of position was implemented due to the fact that is not plausible to assume that we will be able to buy or sell 100% of our stocks in just 1 day. 
    
3. Baseline Strategy + Limiting the change of position by a max of 10% a day + 1 Day Lag 
    * The 1 Day Lag was incorporated due to the fact that `bt` used the closing price in its backtesting.  


## `Backtesting_only_test_data.ipynb`

This notebook backtests the previously mentioned strategies only in the test data time range (2018-04-01 to 2018-12-30).

## Considerations

Please find more information about further development of the current project in the file `Limitations and Recommendations.pdf`

## Authors

Diego Giménez, Jorge Betancourt, Myungsung Kim, Piya Thavornwong, Xuan Lu, Yoon Hee Bae







