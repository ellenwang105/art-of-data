---
layout: post
title: Groundhog Day Analysis
tags: [lab, dataset]
comments: true
cover-img: /assets/img/groundhog.jpeg
---

In this lab, I used Seaborn and Pandas to analyze the Groundhog Day Forecasts and Temperatures dataset from Kaggle (https://www.kaggle.com/datasets/groundhogclub/groundhog-day), which provides Punxsutawney Phil's annual predictions and the subsequent temperatures in February and March.

By analyzing this dataset, I hoped to find whether or not the groundhog's predictions were meaningful or accurate, i.e. a shadow meaning there will be a longer winter and no shadow predicting an early spring. Moreover, I wanted to see if there was a trend in the general temperatures in Febraury and March, with global warming increasing each year.

First, I created dataframes for each prediction outcome (no shadow, full shadow, partial shadow). The majority of results predicted a "Full Shadow," which was interesting to me - maybe Groundhog day is too early in the year and an early spring is always unlikely? Then, I used Seaborn to visualize histogram plots of the February and March average temperatures for each prediction outcome. For the Full Shadow prediction, February and March Average Temperatures were pretty normally distributed. However, possibly due to the small amount of data, the temperatures for a no shadow prediction looked to be relatively uniform, which was surprising.

![plot](https://ellenwang105.github.io/art-of-data/assets/img/Full_Shadow_February.png)

Next, to address my main objective of figuring out whether or not Phil's predictions have any value, I calculated the mean temperatures for each prediction. By using these numbers, it seemed that there was a slight correlation between the prediction and Febraury temperatures, but the March temperature means were pretty similar.

|| Full Shadow | Partial Shadow | No Shadow |
| :------ |:--- | :--- |
| February Average Temperature                |  33.712  | 30.74 | 35.58 |
| February Average Temperature (Northeast)    |  22.7270 | 20.10 | 23.49 |
| February Average Temperature (Midwest)      |  32.7990 | 29.70 | 33.85 |
| February Average Temperature (Pennsylvania) |  26.6310 | 23.20 | 27.29 | 
| March Average Temperature                   |  41.6698 | 41.31 | 42.97 |
| March Average Temperature (Northeast)       |  32.3690 | 35.70 | 32.97 |
| March Average Temperature (Midwest)         |  42.6200 | 44.10 | 43.03 |
| March Average Temperature (Pennsylvania)    |  35.9470 | 37.80 | 36.32 |

I also created a scatter plot of year vs. February Average Temperature, with color-coded points to indicate the prediction. Consistent with the mean of the February Average Temperatures, No Shadow temperatures tended to be higher than Full Shadow Temperatures.

![plot2](https://ellenwang105.github.io/art-of-data/assets/img/Scatter_Plot_February.png)

However, with a scatter plot of the March Average Temperatures, it seemed like there was a correlation between the prediction and temperature, which was inconsistent with my conclusions using the mean value, demonstrating that the mean is not always the best way of analyzing data, as a lot of information is lost.

![plot3](https://ellenwang105.github.io/art-of-data/assets/img/Scatter_Plot_March.png)

With these plots, there seemed to be a very slight upwards trajectory of temperature over time, but not enough to make any concrete conclusions.

Overall, this dataset provided a lot of good information about the temperatures in February and March in various parts of the United States, however, because the overwhelming majority of predictions were "Full Shadow," much of the analyses may have been skewed and it was difficult to find whether or not the predictions have any merit. However, I had a lot of fun playing around with the visualizations in seaborn, and I think pandas and seaborn are really helpful tools for analyzing data.
