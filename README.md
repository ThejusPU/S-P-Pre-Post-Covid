## S&P 500 Covid Crash Analysis

To organize the companies on the S&P 500 into groups that flourished or struggled in different time frames in the times of Covid-19, based on OHLCV data (Open, High, Low, Close, Volume). companyFile is a file containing details on the 509 companies on the S&P500, including ticker symbol, company name, their sector, and their industry (individual industries make up sectors).

### Normalization
This method normalizes the data. SKLearn's Preprocessing's MinMaxScaler allows you to scale s ndarray of values between a desired range (we used (0, 1) and that is the default) by using the max and min value within the ndarray.

### Plus
We wanted all the output to open at the same number so we divided by the initial opening value, after adding 1 to the numerator and denomenator. The division makes values less than the opening value between 0 and 1 and the values greater than the opening value large. So we found the natural log of the division and to avoid accidentally finding the natural log of zero, we added 1 to the numberator and denominator in the division step.

We have decided to name this plus, because we don't know whether this step will provide any useful insight into our problem, or whether this will help us create a better solution. So this has been sprinkled on top.

### Normalization Pre-, Post-Covid and Crash (Pre Crash Post (PCP))

normPCP is a dictionary, key'd by the Ticker symbol, containing the set of three OHLCV data within the time frames and normalizes OHLC and Volume within those time frames.

#### Time Frames:
Pre-Covid: [start, preCrashHigh]

Crash: [preGrashHigh, postCrashLow]

Post-Covid: [postCrashLow, end]

### Insights

From these graphs we have given us a deeper understanding of how the market works and how we want to analyze the market for our problem. We analyzed these graphs by industry because the industries are an inbuilt clustering method, that allows us to gain insight into markets with high competition and markets that all respond simultaneously to external factors. There are a two key take-aways from these graphs

1. The Peak before the crash and the trough after the crash is different for each ticker. Because we used the dates for the peak and trough from the S&P 500, we couldn't see that until we created these graphs. For the Plus version of the normalization, this fact makes a big difference because the initial normalization is divided by the initial data point, and that can be exorbitantly low or high.

2. The Plus version doesn't seem to gleam much insight except for making market certainty and uncertainty in particular sectors and/or industries very apparent. However, once 1. is addrssed the plus version may give improved insights into the market conditions. Another solution to this problem could be to divide by every data-point in the time-series, which would technically end up analyzing every data point to every other datapoint which could become beneficial information-wise, but computationally costly.

But at the end of it all, the normalization of the market opens alone doesn't seem to provide enough information to make clean insights. The normal normalization doesn't provide insights into how some tickers outperform competitors week-to-week, day-to-day, or month-to-month because all the data is stuck between 0 and 1. On the other hand Normalization Plus seems promise a lot, and is now asking for more for those same promises. Feels a lot like corruption.

A good idea worth investing into is analyzing the day to day difference in opening values, or the daily difference is highs and lows and making them positives and negatives depending on the relativity of the opening and closing values.

## Finding Crash Peak and Trough

We need to analyze the data relative to their peaks and troughs, so for each ticker we need to find the date of their peak and the date of their trough during the crash time-frame. We're going to extend the crash time frame to start from the beginning of the year to the start of april so that we can ensure we've found the date of the highest high and the lowest low.

### Insight

If you were to analyze the crash off the basis of the S&P 500 timeline, the crash is very short, but the crash is very different on a ticker by ticker basis. The ticker 'A' had a very long draw out crash, 'AAL' had a very sharp crash, and 'AAPL' witnessed a price hike mid-crash, because people thought that might've been a good point in time to reenter the popular ticker Apple.

### Insights

This method has made the crash graphs crisper and they are ready to be used for clustering. The plus normalizations haven't gleamed any interesting insights, so we're not going to use that for the clustering algorithm.

## Time-series Clustering

tslearn has a clustering algorithm for time series which is well suited to look at general trends called Dynamic Time Warping (DTW). We are going to use tslearn to cluster and analyze thrends in the data.

### Insight

The inertial analysis shows us the number of clusters to look at to find the best clustering of the time series.

- Pre-Crash: 9, 11 clusters
- Crash: 5, 9, 11 clusters
- Post-Crash: 5, 7, 9, 11 clusters

We can look at each of these clustering to analyze trends in the market.

## Graph Clusters

In the future we should try clustering the pictures by their grouping and displayed the different paths the centers took. Unfortunately, we failed on the time management because the clustering algorithm was excruciatingly slow and therefore on the final clustering as well.

## Interactive Candle-Stick Graph
The first thing we tried to do was try to find patterns by looking at the Candle Stick Graph, which ended up taking too much time and couldn't overlay multiple candle-stick graphs on top of each other so we decided to use a line graph for this analysis instead.

Instead if we want to view any single graph we can use the cell two cells down to create an interactive candle-stick graph. This has proved useful in diagnosing problems, like the one we found with CARR, where the ticker only starts after the crash , so we end up lacking data points. Also in recognizing the highest highs and lowest lows worked correctly, this tool came in very useful.