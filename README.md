# Udacity AI Trading Strategies: Data Transformation for Trading Models

This repo is a fork of `udacity/CD13649-Project` repo. The parent repo is part of Udacity AI Trading Strategies Nanodegree Course 3: Preparing for Data Analysis. This repo includes Exercises and skeleton Jupyter notebook for project Data Transformation for Trading Models

The key modifications in this fork repo include:
- Updated repo [README](https://github.com/sharan-naribole/finance-data-exploration/blob/main/README.md)
- Completed Project [Jupyter Notebook](https://github.com/sharan-naribole/finance-data-exploration/blob/main/Project/Preparing-for-data-analysis-project-student.ipynb)

The course project is a an excellent hands-on training in data engineering pipeline using historical financial data including macroeconomic indicators and stock prices.

## Project Dependencies

### Key dependencies

- `jupyter`
- `pandas`
- `matplotlib`

### Optional Dependencies

- `seaborn`
- `numpy`
- `os`
- `scikit-learn`
- `datetime`

## Trace files

The [Project](https://github.com/sharan-naribole/finance-data-exploration/tree/main/Project) directory includes pre-loaded trace files in CSV format.

- GDP quarterly data
- Inflation monthly data
- Apple and Microsoft daily stock price info
    - Open
    - Close
    - High
    - Low
    - Volume

## Data Preprocessing

- Loaded the data into `pandas` DataFrames
- Bonus :star: Updated the column names for convenience
    - Inflation column `CORESTICKM159SFRBATL` -> `INFLATION`
    - Stock price column `Close/Last` -> `Close`
    - Make all the column names to Title case for consistency
- Checked for missing data and forward filled missing values
  - Missing AAPL Closing price data was filled using `ffill` operation
- Removed special characters and converted to numeric/datetime
    - Stock price data had `$` prefix in most columns
    - Implemented a utility method `convert_dollar_columns_to_numeric` to remove the currency prefix and convert the data type to `numeric` to enable computations.
- Bonus :star: Sorted the stock price date based on Date
    - Stock price data was recorded in reverse order of time with latest date on top of DataFrame. Implemented a utility method `sort_date_order` and applied to the stock DataFrames.
- Aligned datetime data using `pandas` `offsets` method
    - Aligned the inflation data so that it falls on the last day of the month instead of the first
- Resampled the Inflation data
    - Created a new quarterly inflation DataFrame by downsampling the monthly inflation data to quarterly using the mean.
    - Created a new weekly inflation DataFrame by upsampling the monthly inflation data. Used `interpolate` `time` method to account for the unequal time difference between monthly inflation data due to the varying number of days in different months.
- Standardized the GDP data
    -  Used `scikit-learn` `StandardScaler` approach
    -  Bonus :star: Transformed the GDP data directly using mean and standard deviation.

## Feature Engineering
- Bonus :star: Computed the Intra Day Return from daily Opening and Closing price data
- Computed the daily returns for stock Closing price using `pct_change` method
- Computed the monthly change in Inflation using `pct_change` method
- Explored different approaches of Monthly Returns in Stock prices
    - **Method 1**: Change from first Open price in month to last Close price in the month
    - **Method 2**: Simple average of computed daily returns across the month
    - **Method 3**: Compounded monthly returns across the month using computed daily returns
- Compute correlation matrix between stock price and Inflation data
- Compute Volatility in stock price by applying `pandas` `rolling` method on Closing price window
- Bonus :star: Compute correlation between rolling volatility and stock price

## Exploratory Data Analysis

Used `matplotlib` and `seaborn` libraries for plotting.

- Filtered stock price data for last 3 months using `pandas` `DateOffset`
- Plotted time series of adjusted open vs close price

- Bonus :star: Plotted and analyzed histogram of Intra day returns
- Plotted histogram of Closing Price 
- Plotted correlation matrix of stock price and inflation as heatmap
- Plotted Volatility and Close price on the same plot with different Y-axis
- Plotted correlation matrix between Volatility and Close price

## Data Storage

To avoid reperforming all the preprocessing steps, exported the processed DataFrames to CSV files.

- Implemented a utility method `export_to_csv` to reuse the operation for multiple DataFrames.

## License

[License](LICENSE.txt)
