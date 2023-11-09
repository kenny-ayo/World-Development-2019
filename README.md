# World-Development-2019

**Introduction**

The data, sourced from Gapminder, includes population, life expectancy, and GDP per capita data, all merged for this analysis

**code**
``` python
# import and load the excel file into pandas dataframe
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
df_2019 = pd.read_excel("gap_minder_2019.xlsx")
df_2019.head()
```
![pd excel](https://github.com/kenny-ayo/World-Development-2019/assets/92790075/a442ddde-0efc-43a7-b559-979d8fe91f6e)


``` python
#Create a dictionary to color the colors for the continent
dict = {
    'Asia':'red',
    'Europe':'green',
    'Africa':'blue',
    'Americas':'yellow',
    'Oceania':'black'
}
```

``` python
# pop as a numpy array : np_pop
np_pop = np.array(df_2019['population'])

# Adjust the width and height
plt.figure(figsize=(12, 6))  

# Create a dictionary to map regions to colors
col = [dict[region] for region in df_2019['Cont']]

# Basic scatterplot with population-based point sizes and region-based colors
plt.scatter(df_2019['gdp_cap'], df_2019['life_exp'], s=np_pop / 1000000, c=col, alpha=0.5)

# Strings
plt.xscale('log')
xlab = 'GDP per Capita'
ylab = 'Life Expectancy'
title = 'World Development in 2019'

# Add axis labels
plt.xlabel(xlab)
plt.ylabel(ylab)

# Add title
plt.title(title)

# Create the legend with region labels and colors
for region, color in dict.items():
    plt.scatter([], [], c=color, label=region)

# Customize the x-axis ticks for better distribution
x_ticks = [100, 1000, 10000, 100000]
x_tick_labels = ['100', '1,000', '10,000', '100,000']

plt.xscale('log')
plt.xticks(x_ticks, x_tick_labels)

# Label the bubbles for India and China
india_idx = df_2019[df_2019['country'] == 'India'].index[0]
china_idx = df_2019[df_2019['country'] == 'China'].index[0]

plt.text(df_2019['gdp_cap'][india_idx], df_2019['life_exp'][india_idx], 'India', fontsize=12, ha='center')
plt.text(df_2019['gdp_cap'][china_idx], df_2019['life_exp'][china_idx], 'China', fontsize=12, ha='center')

# Display the legend
plt.legend()

# Add grid() call
plt.grid(True)

# Display the plot
plt.show()
```

![world_devt_19](https://github.com/kenny-ayo/World-Development-2019/assets/92790075/b7e4e13e-0aa7-4a3e-999b-5d854df3a2d9)
