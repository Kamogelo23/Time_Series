# Time_Series
Time Series analysis of sales data
# Load necessary libraries
library(forecast)
library(ggplot2)

# Set seed for reproducibility
set.seed(123)

# Generate a time series with a linear trend and seasonality
time <- 1:365
trend <- 0.05 * time
seasonality <- sin(2 * pi * time / 365)
noise <- rnorm(365, mean = 0, sd = 0.5)
demand <- trend + seasonality + noise

# Convert to a time series object
demand_ts <- ts(demand, start = c(2020, 1), frequency = 365)

# Plot the time series
autoplot(demand_ts) +
  ggtitle("Simulated Electricity Demand") +
  xlab("Time") +
  ylab("Demand")

# Decompose the time series
decomposed <- stl(demand_ts, s.window="periodic")

# Plot the decomposed time series
autoplot(decomposed)

# Forecast the next 30 days
forecasted <- forecast(decomposed, h=30)

# Plot the forecast
autoplot(forecasted)
