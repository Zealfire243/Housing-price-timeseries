# Housing-price-timeseries

## Goals

Create an interface that helps the typical person decide where they want to buy a house in the United States. Take Zillow housing data to create many time series for different areas. Cross reference areas with census data to look for correlation. Use this information to create a user friendly app that allows someone to either browse with a map or use filters to see which place would best fit their interests. Eventually having the predictions change in real time.

## Overview

For this portion of the project I focused on a predictive time series for a small number of counties. My MVP project would be all 3000 or so counties in the US but I decided to start with a group of 27 to see if my idea would work. I sourced my housing data from Zillow and used it to get a time series from 2012 to 2021 for the typical home value for 27 different counties. I used what I found to create forecasts to see what the tpyical home value could be within the next 4 years.

## Data

Housing data sourced from [Zillow](https://www.zillow.com/research/data/) that dates from January 2000, to September 2021. The main resource that I am using to predict furture housing values is the Zillow Home Index Value. The main aspect of the Zillow Home Index Value (ZHVI) is the Zestimate. The Zestimate of a house is the estimated value of that individual house. Zestimates for on-market houses across the entire US have a median error of 2%. This means that for the on-market homes, half of the Zestimates are within 2% of the selling price, while the other half is not. Off-market Zestimates have a median error of 6.9%. One of the core functions of the ZHVI is calculating the weighted average of each home’s appreciation in the property universe. The homes Zestimate or zi,t-1 and ,zi,t , at time t-1 and t respectively, is used to calculate the individual home appreciation (ai,t).

![Appreciation](./imgs/z_appreciation.png)

Each individual home appreciation is then multiplied by a weight (wi,t-1). This weight is found by dividing a homes zestimate by the sum of all Zestimates in the region.

![Weight](./imgs/z_weight.png)

The total market appreciation, At, is the sum of the weighted appreciation of each home.
The total market appreciation is then used to find the previous typical home value in every period by dividing the mean Zestimate of the property universe at time t (It) by 1 plus the total market appreciation at time t.

![Total Appreciation](./imgs/z_total_appreciation.png)

There has been articles talking about the quality of the Zestimate, due to Zillow losing approx. 500 million from their house flipping business. Although critics say Zillow depended too much on its Zestimate, other experts are saying it has more to do with holding on to too many houses for too long and the expenses that come along with that.

## Methods

The data I sourced was seperated by RegionID and produced 26000 different regions. I decided to immediately change my focus to counties as there are only 3000. I started by taking the 27 values for the counties. I chose these 27 counties as the 27 middle counties according to the median. I cut data that predates 2012 due to the housing bubble that went from 2005 to 2012.

![Full Data Display](./imgs/typical_time_series.png)
![Post Housing Bubble Display](./imgs/post_housing_bubble.png)

I took steps to make the data stationary. I logged the data to normalize it. 

![Logged Time Series](./imgs/logged.png)

I subtracted the exponential rolling mean and differenced the data in order to detrend it.

![Differenced Time Series](./imgs/differenced.png)

I checked the autocorrelation and the partial autocorrelation. The autocorrelation looks great, starts with a high correlation but immediately drops and then flucuates around 0. For the partial autocorrelation, while most performed great, some of the time series didnt preform as well as others with spikes of correlation popping up towards the end as well as beginning. 

![Autocorrelation](./imgs/autocorr.png)

![Good Partial Autocorrelation](./imgs/part_autocorr_good.png)
![Bad Partial Autocorrelation](./imgs/part_autocorr_bad.png)

I put both the original data and my differenced data through a method that gave me the best combination of orders. I used these combinations to fit models on both sets of data.
Note: This is displaying a single result of the 27 different time series

![Preprocessed Cross Validation](./imgs/checking_pre_preds.png)
![Processsed Cross Validation](./imgs/checking_preds.png)

## Results

With these models I forecasted predictions that are usuable in my final project.
Note: This is displaying a single result of the 27 different time series

![Preprocessed Forecast](./imgs/pre_forecast.png)
![Processed Forecast](./imgs/forecast.png)

## Next Steps

The next steps would be to better optimize the individual model. With better optimized models one would be able to generate more accurate predictions. After applying those methods to the 2900 other counties, group census data by county to see if there are correlations. Build a map to display results and a filtering program to help the user review what they want to see. Have the program pull data from Zillow and any updates to the census information in real time. 

## For More Information

For a more detailed look into my project see my full report:

* [Report](./Notebooks/Report.ipynb)

For additional infomation see:

* [All in one Notebook](./Notebooks/MaidenVoyage.ipynb)

For a short presentation see:

* [Presentation](./Notebooks/Presentation.pdf)

## Repository Structure
- README.md                     <- The top-level README for reviewers of this project
- Notebooks                     
    - Report.ipynb              <- Narrative documentation of analysis in Jupyter notebook
    - MaidenVoyage.ipynb        <- Jupyter notebook containing all code that was used with documentation
- Presentation.pdf                  <- PDF version of project presentation
- dataraw                       <- Both sourced externally and generated with code
- imgs                          <- Both sourced externally and generated with code
