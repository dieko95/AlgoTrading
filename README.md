<h1> Algorithmic Trading with Python </h1>

The following repo is based on the final project of the course "Algorithmic Trading" taught at Hult International Business School by professor Michael Rolleigh. The goal is to backtest a trading algorithm that receives the output from a machine learning model as a signal to perform the strategy. Please find the final results in <span style="color: #333399;"><strong><a style="color: #333399;" href="https://github.com/dieko95/AlgoTrading/blob/master/Algorithmic%20Trading%20in%20Python.pdf">Algorithmic Trading in Python.pdf</a></strong></span>

The corresponding tasks are divided into the following notebooks:
<h2 style="text-align: center;"><span style="color: #333399;"><a style="color: #333399;" href="https://github.com/dieko95/AlgoTrading/blob/master/Notebooks/AlgoTrading.ipynb">AlgoTrading.ipynb</a></span></h2>
Contains the data science workflow. This script was used as a research environment with the objective of extracting the signal from fundamental and alternative data. The signal extraction was done by ultimately developing a machine learning model that had as target returns in a particular stock (in this case Redhat [RHT] stocks).
<h4>Data Collection, Cleaning, and Exploration:</h4>
The Github repo <em>GetOldTweets</em> was used to web scrape all the mentions that Redhat had in the past 4 years (2014 - 2018). a total of 56,400 tweets were collected and cleaned. Sentiment analysis was undertaken by implementing <em>VaderSentimentAnalyzer</em>. After computing the sentiment score for each tweet, they were aggregated by adding the number of positive, negative and neutral tweets. Finally, these aggregated tweets were inner joined by timestamp with the fundamental data frame. These two data frames consisted of the following:
<h4>Fundamental Data:</h4>
<ul>
 	<li>Diluted EPS</li>
 	<li>EBIT Margin</li>
 	<li>EBITDA Margin Revenue % Growth</li>
 	<li>EBITDA % Growth</li>
 	<li>EBIT % Growth</li>
 	<li>NetIncome % Growth</li>
 	<li>Net Debt to Equity</li>
 	<li>Alternative Data:</li>
</ul>
<h4>Alternative Data</h4>
<ul>
 	<li>Favourites</li>
 	<li>retweets</li>
 	<li>Compound</li>
 	<li>Positive</li>
 	<li>Neutral</li>
 	<li>Negative</li>
</ul>
<h4>Machine Learning:</h4>
The data was split into training and Test Set (85% | 15%). The target consisted of the stock returns and the features consisted of the previously stated Fundamental and Alternative data. After having the target and features correctly split, the baseline model was created. This model consisted of a simple decision tree with no constraints in its max depth. Thus, it was hugely overfitted. After this, 5-fold cross-validation was done in order to assess how overfitted this model was. Finally, a cross-validated grid search was used with the purpose of finding the best hyperparameters and the optimized decision tree was created. The same process was done with a random forest with the difference of performing feature selection. This process was repeated with Gradient Booster and Neural Nets in order to compare and contrast different machine learning models.

The baseline model (hugely overfit decision tree) was used for the backtesting in order to exemplify the dangers of overfitting in trading.
<h2 style="text-align: center;"><span style="color: #333399;"><a style="color: #333399;" href="https://github.com/dieko95/AlgoTrading/blob/master/Notebooks/Backtesting.ipynb">Backtesting.ipynb</a></span></h2>
Backtesting consists of creating a trading strategy and going back in time simulating 'what would have happened' if the strategy was implemented in such a time frame. The time frame selected in this script ranged from 2014-01-02 to 2018-12-30. Finally, `bt` was used as the backtesting library for this project.
3 different strategies were implemented:

<strong>1. Baseline Strategy</strong>
<ul>
 	<li>If the predicted return is greater than 2% buy all the stocks with the available funds that we have (e.g. $1,000,000 in stocks).</li>
 	<li>If the predicted return is greater than 1% buy half the stocks with the available funds that we have (e.g. $500,000 in stocks).</li>
 	<li>If the predicted return is less than -2% sell all the stocks with the available funds that we have (e.g. $1,000,000 in stocks).</li>
 	<li>If the predicted return is greater than -1% sell half the stocks with the available funds that we have (e.g. $500,000 in stocks).</li>
</ul>
<strong>2. Baseline Strategy + Limiting the change of position by a max of 10% a day</strong>
<ul>
 	<li> The limit in the change of position was implemented due to the fact that is not plausible to assume that we will be able to buy or sell 100% of our stocks in just 1 day.</li>
</ul>
<strong>3. Baseline Strategy + Limiting the change of position by a max of 10% a day + 1 Day Lag</strong>
<ul>
 	<li>The 1 Day Lag was incorporated due to the fact that the library `bt` used the closing price in its backtesting.</li>
</ul>
<h2 style="text-align: center;"><span style="color: #333399;"><a style="color: #333399;" href="https://github.com/dieko95/AlgoTrading/blob/master/Notebooks/Backtesting_only_test_data.ipynb">Backtesting_only_test_data.ipynb</a></span></h2>
This notebook backtests the previously mentioned strategies only in the test data time range (2018-04-01 to 2018-12-30).
<h2 style="text-align: center;"> Considerations</h2>
Please find more information about further development of the current project in the file <strong><span style="color: #0000ff;"><a style="color: #0000ff;" href="https://github.com/dieko95/AlgoTrading/blob/master/Limitations%20and%20Recommendations.pdf">Limitations and Recommendations.pdf</a></span></strong>
<h2 style="text-align: center;">Authors</h2>
Diego Giménez, Jorge Betancourt, Myungsung Kim, Piya Thavornwong, Xuan Lu, Yoon Hee Bae
