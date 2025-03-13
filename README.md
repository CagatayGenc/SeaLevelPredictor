```python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_plot():
    # Load the data
    data = pd.read_csv('epa-sea-level.csv')

    # Create scatter plot
    plt.figure(figsize=(10, 6))
    plt.scatter(data['Year'], data['CSIRO Adjusted Sea Level'], color='blue', label='Sea Level Data')

    # Calculate the line of best fit for all data
    slope_all, intercept_all, _, _, _ = linregress(data['Year'], data['CSIRO Adjusted Sea Level'])
    years_all = range(1880, 2051)  # Extend to 2050
    plt.plot(years_all, slope_all * years_all + intercept_all, color='red', label='Best Fit Line (1880-2050)')

    # Calculate the line of best fit for data from 2000 onwards
    data_recent = data[data['Year'] >= 2000]
    slope_recent, intercept_recent, _, _, _ = linregress(data_recent['Year'], data_recent['CSIRO Adjusted Sea Level'])
    years_recent = range(2000, 2051)  # Extend to 2050
    plt.plot(years_recent, slope_recent * years_recent + intercept_recent, color='green', label='Best Fit Line (2000-2050)')

    # Add labels and title
    plt.xlabel('Year')
    plt.ylabel('Sea Level (inches)')
    plt.title('Rise in Sea Level')
    plt.legend()

    # Save the plot
    plt.savefig('sea_level_rise.png')

    # Return the plot
    return plt.gca()
```
