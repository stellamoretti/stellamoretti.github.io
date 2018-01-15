---
layout: post
title: Analyzing NYC Subway Data using Pandas
---

## A data-driven approach to optimizing the placement of promotional street teams


__The Problem Statement__

WomenTechWomenYes (WTWY) will hold their annual gala in early summer 2018 and want to invite guests who are passionate about increasing the participation of women in technology, who will build awareness of their organization and contribute to the WTWY cause.

WTWY plan on sending street teams to various NYC subway stops to sign up for this event.  WTWY are seeking advice on how to optimize the placement of their street teams in order to maximize the number of individuals who sign up.

The proposed solution will utilize MTA turnstile data, and other relevant data sources, to identify a shortlist of NYC subway stations for which WTWY street teams can concentrate their efforts.  The recommendation will be based on a combination of foot traffic, geographic and demographic factors.

## The data

The New York Metropolitan Transit Authority (MTA) provides [turnstile data](http://web.mta.info/developers/turnstile.html) on their website. These datasets are available to download as plain text files, each file covering a period of seven days. Each row contains the number of entries and exits per turnstile at every subway station in the five boroughs.

Data is presented in the following comma-separated format:

`C/A,UNIT,SCP,STATION,LINENAME,DIVISION,DATE,TIME,DESC,ENTRIES,EXITS`

An example of the data:

![raw MTA data](/images/mta_images/turnstile_data_raw.png)

A description of these fields is provided by the MTA [here](http://web.mta.info/developers/resources/nyct/turnstile/ts_Field_Description.txt).

For the purpose of this project, 4 weeks of MTA data were downloaded and imported into a Pandas dataframe in a Jupyter Notebook.

## Wait, what do pandas have to do with the subway?

![panda GIF](https://media.giphy.com/media/EatwJZRUIv41G/giphy.gif)

Not _those_ pandas! _pandas_ is an open source library providing high-performance, easy-to-use data structures and data analysis tools for the Python programming language. [Learn how to use _pandas_ in 10 minutes](http://pandas.pydata.org/pandas-docs/stable/10min.html).

_pandas_ is a robust and useful tool that makes it easy to access, subset and filter data for statistical analysis.


## Preparing the data

At first glance, the MTA data appeared to be clean and ready for analysis.  However after running some simple sums it became apparent that something was off.  It is easy to think of Times Square as one of New York's busiest locations, however its highly unlikely that the 42nd Street subway station sees over 300 BILLION passengers in one week!

Upon closer inspection of the data it became clear that the entries and exits values were __cumulative__ over a period of time, with each turnstile maintaining a register of entries (or exits) before sporadically resetting to zero after a number of days.

Once this discovery was made it was a simple matter of transforming  the entry/exit values into actual counts per time, utilizing the sequential properties of the original cumulative values.

Additional data cleaning tasks included:
- Removing duplicate values.
- Dropping rows where the count was clearly erroneous (e.g. negative).
- Dropping rows where the count was impossibly high.


## Exploring the data

Looking at one month worth of MTA data provided a list of the top 10 busiest subway station control areas:

![Top 10](/images/mta_images/top_10_stations.png)

## Problem solved? Not quite...

With all of this information at hand, it was tempting to conclude the project with a recommendation for WTWY to place their street teams at these top 10 subway stations.

However at this point it was helpful to revisit the problem statement and spend time thinking more about how best to achieve WTWY's goal of maximizing attendance at their Summer gala.  Does quantity equal quality?

## A refined approach

A key next step was to define three three things which would help determine if we had the right data, and what to do with it.

### Define the target audience

WTWY want to invite guests who are passionate about increasing the participation of women in technology, and who will build awareness of their organization and contribute to the WTWY cause.  With this goal in mind, we were able to define our target audience as:
- Local residents (not tourists).
- Individuals inspired by the WTWY cause, who perhaps work in or alongside the tech industry.
- Philanthropic individuals who may wish to make a charitable donation to WTWY.


### Define the ideal location

The ideal subway station was defined as one which which was:
- High traffic (to maximize exposure).
- In close proximity to "tech hubs" where it would be more likely to find our target individual.

### Define the ideal time

The ideal time to send out WTWY street teams was defined as:
- Weekdays, to target individuals who work during the week.
- "Shoulder" hours just outside of rush hours, where foot traffic was high, but not so high as to prevent quality interactions.

## An additional data source

Focusing on the desire to target individuals in the tech industry, we set out looking for additional data which could be tied in with our original analysis of MTA data.

[Digital NYC](http://www.digital.nyc/) maintains a database of over 9000 tech startups, which is free to download from the [NYC Open Data](https://data.cityofnewyork.us/dataset/Mapped-In-NY-Companies/f4yq-wry5) website.

Using the GoogleMaps Geocoding API, we converted the street addresses of over 1000 tech startups into geographic coordinates (latitude and longitude), and then plot them on a Google map using [Bokeh](https://bokeh.pydata.org/en/latest/), a Python visualization library.

![Bokeh plot](/images/mta_images/bokeh.png)

This map allowed us to locate the high-density tech areas in relation to the busiest subways stations identified earlier.  Two decisions were made based on this visualization:
1. To focus street team efforts solely in Manhattan.
2. To include the 23rd RW subway station due to its proximity to a large number of tech companies.

## Right place, right time

Returning to the MTA data and drilling further down it was possible to identify which days of the week saw the most traffic (weekdays - no surprises there!) and also which hours of the day could be considered as our target "shoulder" hours outside of peak hour.

![Subway by the day](/images/mta_images/day.png)

![Subway by the hour](/images/mta_images/time.png)

## Final recommendation

Based on our analysis, the final recommendation given to WTWY was to place street teams at the following six locations during weekday "shoulder" hours:
- Grand Central station
- World Trade Center
- Penn Station
- Union Square
- Columbus Circle
- 23rd Street (RW)

More information on this project can be found on our team's [GitHub repository](https://github.com/stellamoretti/project_benson_1).
