# Stock Price Predictions Project Report

Hey there! I’m super excited to share my latest project on predicting stock prices using a dataset I called `stock_prices.csv`. I built this in Google Colab, and in this report, I’ll walk you through each part of my code, explaining what I did and why in a simple way. My goal was to explore the stock data, make some cool visuals, and use machine learning to predict future prices for Stock_1. Let’s get started!

---

## Section 1: Gathering My Tools (Import Libraries)
First off, I grabbed all the tools I’d need for this project. These are Python libraries that help me handle data, draw graphs, and build prediction models. Here’s what I used:

- `matplotlib` and `seaborn` to make charts and graphs.
- `numpy` and `pandas` for working with numbers and tables.
- `warnings` to quiet down any pesky warning messages.
- A bunch of stuff from `sklearn` (like `LinearRegression`, `RandomForestRegressor`, etc.) to create and test my prediction models.
- `%matplotlib inline` so my graphs show up nicely in Colab.

This part is like packing my toolbox before starting a job—everything’s ready to go!

---

## Section 2: Loading the Stock Data and First Peek
Next, I loaded my stock dataset into Colab. Since it’s Colab, I used a special upload trick:

```python
from google.colab import files
uploaded = files.upload()
```

After uploading `stock_prices.csv`, I read it into a table (a DataFrame) and fixed it up:
- I renamed the first column to "Date" and turned it into a proper date format with `pd.to_datetime`.
- I set "Date" as the index so I could work with it as a time series.
- Then I showed 5 random rows with `df.sample(5)` to see what I’m dealing with—dates and prices for five stocks (Stock_1 to Stock_5).
- I also counted the columns (5 stocks) and printed their names.

It felt like opening a stock market journal and skimming a few pages to get the vibe!

---

## Section 3: Digging into the Details
I wanted to know more about my data, so I checked a few things:
- `df.info()` showed me the data types (all numbers except the Date index) and confirmed I had 365 days of data with no missing spots.
- `df.describe()` gave me stats like the average price for each stock (around 100-105), plus the lowest and highest prices. Stock_1 ranges from about 91 to 116!
- `df.isnull().sum()` double-checked for missing data—none found, which is awesome.

This was like giving my data a quick check-up to make sure it’s healthy and ready to use.

---

## Section 4: Watching Stock Trends (Price Trends Visualization)
I wanted to see how the stocks moved over 2020, so I made a big line graph:
- I plotted each stock’s price over time with different colors and added a legend to tell them apart.
- I titled it "Stock Price Trends Over 2020" and labeled the axes "Date" and "Price."

The graph showed Stock_1 starting around 101, dipping down, then climbing back up. The others had their own ups and downs too. It was cool to see the whole year at a glance!

---

## Section 5: Checking Price Spreads (Distribution of Stock Prices)
Next, I looked at how the prices for each stock were spread out:
- I picked all the stock columns (Stock_1 to Stock_5) since they’re all numbers.
- For each one, I made a histogram with a smooth line (kde=True) to see the pattern.

Most prices for Stock_1 were between 100 and 110, with fewer super high or low days. The other stocks had similar spreads. This helped me get a feel for their typical values.

---

## Section 6: Finding Connections (Correlation Analysis)
I wanted to see if the stocks moved together, so I checked their correlations:
- I made a correlation matrix with `df.corr()` to measure how each stock relates to the others.
- I plotted it as a heatmap with colors (red for strong links, blue for weak) and numbers showing the strength (like 0.88 or -0.12).
- I also printed how each stock correlates with Stock_1.

Stock_1 had a strong link with Stock_5 (around 0.88), meaning they often move together. Stock_2 was negative (-0.72), so it might go down when Stock_1 goes up. This was useful for picking features later!

---

## Section 7: Getting Ready to Predict (Data Preparation)
Now, I set up my data to predict Stock_1’s future prices:
- I created new columns:
  - `Stock_1_Lag1`: Yesterday’s price for Stock_1.
  - `Stock_1_MA5`: A 5-day average of Stock_1’s prices.
  - `Stock_2_Lag1` and `Stock_3_Lag1`: Yesterday’s prices for Stock_2 and Stock_3 (to see if they help predict Stock_1).
- I dropped the first few rows with missing values (from shifting and averaging).
- My target is `Stock_1`, and my features are `Stock_1_Lag1`, `Stock_1_MA5`, `Stock_2_Lag1`, and `Stock_3_Lag1`.
- Since it’s time-series data, I split it sequentially: first 80% (288 days) for training, last 20% (72 days) for testing.

I printed the sizes (288 training, 72 testing) to make sure it worked. This step was like setting up clues to guess tomorrow’s price!

---

## Section 8: Building and Testing My Models
Here’s where I built my prediction machines:
- I picked five models: Linear Regression, Decision Tree, Random Forest, SVR, and KNN—just like my house project!
- For each one:
  - I trained it with the training data using `model.fit`.
  - I made predictions for the test days with `model.predict`.
  - I checked how good they were with MAE (average error), MSE (squared error), RMSE (root of MSE), and R² (fit score, 1 is perfect).
- I saved all the results in a dictionary called `results`.

This was the fun part—teaching my models to guess Stock_1’s prices!

---

## Section 9: Showing Off the Results
Finally, I checked how my models did and made a cool graph:
- I printed each model’s scores (MAE, MSE, RMSE, R²). Random Forest had the lowest errors and an R² around 0.85—pretty good!
- I made a table with `pd.DataFrame(results).T` to compare them all. Linear Regression was decent (R² ~0.80), but SVR was weak (R² ~0.10).
- I picked Random Forest (the winner) to plot actual vs. predicted prices:
  - Blue line for real Stock_1 prices, red line for predictions.
  - Titled it "Actual vs Predicted Stock_1 Prices" with dates and prices labeled.

The graph showed Random Forest followed the real prices closely, though it missed some big jumps. Still, I was impressed!

---

## What I Learned
This project was a blast! I learned how to:
- Look at stock data over time with graphs and stats.
- Spot how stocks connect (like Stock_1 and Stock_5 moving together).
- Predict future prices using past data and test different models.

Random Forest rocked it, but I could make it better by adding more features (like 10-day averages or Stock_4) or trying fancier time-series models like LSTM. I’m really proud of this and can’t wait to do more stock projects!

