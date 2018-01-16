---
title: Learning to Share in the Sharing Economy
---

## Predicting the expected rental income of a new Airbnb listing using a combination of regression techniques.


__The "Side Hustle" Economy__

A recent poll found that 24% of American adults have a _side hustle_. That is they supplement their regular income by selling things online or offering a service such as driving for a ride-sharing company.

Whilst there is potential to turn these gigs into a full-time occupation it can take a lot of time and commitment, and the results aren't guaranteed.

As someone who has dabbled on some of these platforms with mixed success, the one that I've always been curious about is Airbnb.

__Earn Money as an Airbnb Host__

Airbnb is the poster child of the sharing economy, where hundreds of thousands of hosts around the world earn money by renting out their spare room or even their entire home.

On their website Airbnb provides an estimate of the potential earnings for a given location, but if you read the find print their calculations are based on a 50% occupancy rate, which I suspect isn't accurate in all cases.

As a data scientist I set out to see if I could come up with a better prediction.

__The Data__

To tackle this problem I used data from 40,000 Airbnb listings in New York City, covering 12 months of guest reservations. This data was sourced from [Inside Airbnb](http://insideairbnb.com/get-the-data.html) in November 2017.

I also pulled information from the latest [US Census Survey](https://factfinder.census.gov/faces/nav/jsf/pages/guided_search.xhtml) in order to help characterize the neighborhoods of the city.

__The Airbnb Equation__

Rental income is a product of two things:
1. The price charged per night, and
2. The occupancy rate.

So I built a supervised machine learning model to address each of these and evaluated their performance using actual data.

__The Pricing Model__

The pricing model was built using a scikit-learn gradient boosted regressor where the key features were location and property details. I achieved an R2 of 0.6 for this model, which equates to a mean absolute error of approximately $40.

__The Occupancy Model__

Occupancy was modeled using a generalized linear model with a binomial probability distribution, which predicts the number of nights booked in a 30-day month. For this model I achieved a mean absolute error of seven days.

__Application__

To bring these models to life I developed an interactive web application where potential Airbnb hosts can input the details of their home and obtain the following:
- Suggested nightly rate ($)
- Expected occupancy (%), broken down for each month of the year
- Resultant rental income ($)
- Calculation of 3% service fee automatically charged by Airbnb

The app also features control buttons which can be used to evaluate the effect of a higher or lower price on occupancy.

__Let's Put it to the Test__

So how did my model perform? Say you lived in Greenwich Village and you wanted to rent out your spare room which was fit for two adults. [Airbnb](https://www.airbnb.com/host/homes) will tell you that you could earn just under $1500 in a month.

My model would suggest that you could rent this room out for $127 per night and expect an occupancy rate of 58%, yielding a monthly income of $2201.

If you look at the actual data from October 2017 and all of the listings in Greenwich Village which fit this description, the mean rental income was $2080.

So whilst this particular example demonstrates where my combination pricing-occupancy model performs quite well, it did not yield the greatest predictive power for all cases.

This suggests that rental income depends on other features, for instance the quality of the listing photos and the sentiment of past guest reviews, which obviously aren't available for a new or unlisted Airbnb property.

__Closing Remarks__

While there is certainly room to improve the model, the aim of my tool is to provide potential Airbnb hosts with a more transparent look into the expected value of their home so that they can realistically set their expectations as to how profitable a _side hustle_ it may be.

__Links__

Thanks for reading! If you'd like to read more please refer to my [GitHub](https://github.com/stellamoretti/airbnb_income_prediction).
