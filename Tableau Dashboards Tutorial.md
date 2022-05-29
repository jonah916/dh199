# Dashboards in Tableau: An Intermediate Guide

## 1) Introduction: Why dashboards?

[Tableau dashboards](https://www.tableau.com/) are a compact way of combining multiple visualizations into a single view, making the trends in your data easier to see from multiple perspectives. Interactivity is a key feature, enabling you to slice and dice your data in more ways. There are a [wide variety of applications](https://www.idashboards.com/blog/2016/09/26/what-is-the-purpose-of-a-dashboard-2/), from business intelligence to sports analytics to data quality assurance.

This tutorial assumes that you have already downloaded Tableau (available [here](https://www.tableau.com/products/desktop/download)) and have basic knowledge of how to construct visualizations using it. You already know how to upload data, navigate the workspace, make basic visualizations, and customize basic aesthetic details. If any of these topics is still unfamiliar to you, take some time to [brush up on the basics](https://www.tableau.com/learn/training/20221). In addition, the data we will use requires that you have university credentials.

By the end of this tutorial, we will have created three types of visualizations and integrated them into an interactive dashboard that looks like the following:

<img src="https://github.com/jonah916/dh199/blob/main/visuals/Final%20Product.png" width="800">

## 2) Data for this tutorial

In this tutorial, we will use Tableau to visualize trends in American presidential elections between 1976 and 2020. The data, provided by the MIT Election Data + Science Lab, is available for download with university credentials [here](https://dataverse.harvard.edu/file.xhtml?fileId=4299753&version=6.0). This is a good dataset for this tutorial because there aren’t too many variables, and the ones we do have are a good mix of numeric, categorical, and geographic data. 

Download the data as a CSV, upload it to Tableau, and take a moment to familiarize yourself with it in the Data Source tab. Each row contains the vote totals and shares for a presidential candidate in a given state in a given election year.

## 3) Constructing your worksheets

<img align = "right" src = "https://github.com/jonah916/dh199/blob/main/visuals/Change%20Year%20Data%20Type.png" width = "300">

Start by reading the CSV file into Tableau. There is only one step of data cleaning required: Tableau thinks that **Year** is a number, when in reality we should treat it as a categorical variable. (There is also a “date” data type, but this changes all the date values to 1/1/1976, 1/1/1980, and so on, which is more granular than we want). Change this on the Data Source page by clicking on the # sign and changing the data type to String on the dropdown menu that pops up. (See right.)  

The first visualization we’re going to make is an interactive map showing how each state voted in a given year’s election. We’ll use it to compare electoral maps across different election years.

### a) Election map

On a blank sheet, drag **State** onto the workspace. It should automatically populate with a map of the US, like so:

<img src ="https://github.com/jonah916/dh199/blob/main/visuals/Map%20at%20First.png" width = "800">

We want to color each state by how it voted in a given year – that is, by the percentage of the vote that the Democrat or Republican got. The data only has the raw numbers of votes – **Candidatevotes**, or the number of votes a candidate got in a state, and **Totalvotes**, or the total votes cast in a state. We can easily generate a new variable, **Percent of Vote**, using the calculated field feature:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Percent%20of%20Vote%20Calculated%20Field.gif" width = "1000">

Drag **Percent of Vote** to the Color mark. It should look like this:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Map%20with%20Percent%20of%20Vote.png" width = "800">

Obviously, this isn’t right. Every state has the same percent of the vote, and the vote share should be a proportion, not a whole number. This is because we need to filter by Party and put the vote share in terms of one political party’s share.

Drag **Party Simplified** to Filters and select DEMOCRAT. This step makes the map show only the democratic candidate’s share of the vote. We’ll want to show this filter for later, so right-click on **Party Simplified** in the Filters tray and click Show Filter. You can also click on the downward-pointing arrow on the right side of the filter:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Adding%20Party%20Filter%20to%20Map.gif" width = "1000">

This looks better, but each state’s vote share is still over 1. This is because Tableau is summing the vote share won in each state by the Democratic candidate in every election from 1976-2020. We need to add **Years** to the Rows shelf and also include **Years** as a filter, like we did for party in the step before. The worksheet view should now look like this:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Map%20by%20Year%20before%20Coloring.png" width = "800">

To make the party breakdown easier to see, let’s change the color scale to Red-Blue Diverging. Make sure that lower values correspond to red and higher values to blue, and that the min and max values are 0 and 1, respectively. (Go into the Color mark, select Red-Blue Diverging from the dropdown menu, go to Advanced > check Start and End > set those values to 0 and 1.) You can also rename the color scale at the right side of the screen if you please.

The map is finished! Rename it **“Map”** for future reference. Make sure it looks like this before we move on to the next visualization:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Map%20Finished.png" width = "800">
