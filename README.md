# Housing-price-timeseries

## Goals

Create an interface that helps the typical person decide where they want to buy a house in the United States. Take Zillow housing data to create many time series for different areas. Cross reference areas with census data to look for correlation. Use this information to create a user friendly app that allows someone to either browse with a map or use filters to see which place would best fit their interests. Eventually having the predictions change in real time.

## Overview

For this portion of the project I focused on a predictive time series for a small number of counties. My MVP project would be all 3000 or so counties in the US but I decided to start with a group of 27 to see if my idea would work. I sourced my housing data from Zillow and used it to get a time series from 2012 to 2021 for the typical home value for 27 different counties. I used what I found to create forecasts to see what the tpyical home value could be within the next 4 years.

## Data

Housing data sourced from Zillow that dates from January 2000, to September 2021. I cut data that predates 2012 due to the housing bubble that went from 2005 to 2012. The main resource that I am using to predict furture housing values is the Zillow Home Index Value. The main aspect of the Zillow Home Index Value (ZHVI) is the Zestimate. The Zestimate of a house is the estimated value of that individual house. Zestimates for on-market houses across the entire US have a median error of 2%. This means that for the on-market homes, half of the Zestimates are within 2% of the selling price, while the other half is not. Off-market Zestimates have a median error of 6.9%. One of the core functions of the ZHVI is calculating the weighted average of each home’s appreciation in the property universe. The homes Zestimate or zi,t-1 and ,zi,t , at time t-1 and t respectively, is used to calculate the individual home appreciation (ai,t). Each individual home appreciation is then multiplied by a weight (wi,t-1). This weight is found by dividing a homes zestimate but the sum of all Zestimates in the region. The total market appreciation, At, is the sum of the weighted appreciation of each home.
The total market appreciation is then used to find the previous typical home value in every period by dividing the mean Zestimate of the property universe at time t (It) by 1 plus the total market appreciation at time t.
There has been articles talking about the quality of the Zestimate, due to Zillow losing approx. 500 million from their house flipping business. Although critics say Zillow depended too much on its Zestimate, other experts are saying it has more to do with holding on to too many houses for too long and the expenses that come along with that.

## Methods

The data I sourced was seperated by RegionID and produced 26000 different regions. I decided to immediately change my focus to counties as there are only 3000. I started by taking the 27 values for the counties. I used this group to see which model and combination of orders would work best.

## Results


## Next Steps

## For More Information

For a more detailed look into my project see my full report:

* [Report](./Report.ipynb)

For additional infomation see:

* [](./MaidenVoyage.ipynb)

For a short presentation see:

* [](./Presentation.pdf)

## Repository Structure