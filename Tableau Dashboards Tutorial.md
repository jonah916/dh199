# Dashboards in Tableau: An Intermediate Guide

1) [Introduction: Why dashboards?](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#1-introduction-why-dashboards)  
2) [Data for this tutorial](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#2-data-for-this-tutorial)
3) [Constructing your worksheets](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#3-constructing-your-worksheets)  
  a) [Election map](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#3-constructing-your-worksheets)  
  b) [Candidate Vote Totals by Year](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#b-candidate-vote-totals-by-year)  
  c) [Party Vote Share by Year](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#c-party-vote-share-by-year)  
4) [Constructing your dashboard](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#4-constructing-your-dashboard)  
  a) [Parts of the dashboard workspace](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#a-parts-of-the-dashboard-workspace)  
  b) [Adding sheets to your dashboard](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#b-adding-sheets-to-your-dashboard)  
  c) [Dynamic filters and interactivity](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#c-dynamic-filters-and-interactivity)  
  d) [Best practices](https://github.com/jonah916/dh199/blob/main/Tableau%20Dashboards%20Tutorial.md#d-best-practices)

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

### a) Election Map

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

### b) Candidate Vote Totals by Year

Next, we’re going to make a series of barplots showing the top candidates in each election and how many votes they received. Make a new worksheet and add **Year** and **Candidate** to the Rows shelf and **Candidatevotes** to the Columns shelf. (Make sure it aggregates with SUM of vote totals.) Click the Sort descending button above the workspace:

<p align = "center">
  <img src = "https://github.com/jonah916/dh199/blob/main/visuals/Sort%20descending%20button.png" width = 250>
</p>                  

With all of the candidates listed, it’s not very readable. Let’s add **Party Simplified** as a filter again, like we did above, and uncheck Other.

Let’s also color by party and reassign each party to its traditional color (democrats blue, republicans red, and libertarians purple). Note that there’s also a **Party Detailed** column – this is **not** the column we want to use:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Coloring%20by%20Political%20Party.gif" width = "1000">

Finally, we’ll add **Year** to the filters, like we did above. Try unchecking boxes to compare 3 or 4 elections at once. Last but not least, we’ll change the view from Standard View to Entire View so that we maximize our use of space:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Entire%20View.gif" width = "1000">

Rename sheet as **“Candidate Vote Totals by Year”** and we’re ready to move on.

### c) Party Vote Share by Year

<p align = "center">
<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Change%20Mark%20Type.png" height = 450>
</p>
  
The last visualization we’re going to make before our dashboard is a line graph of party vote share by year. Make a new sheet and drag **Year** to the Columns shelf and **Candidatevotes** to the Rows shelf. The default plot will be a barplot, but we can change this to a line graph by clicking on the dropdown menu under Marks and selecting “Line”. (See left)

Let’s break it up by party. Drag **Party Simplified** to the Colors mark. By now, the graph should look like this:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Line%20Graph%20Middle.png" width = "800">

We want it in terms of party vote percentage, which means we have to use a quick calculation on the **Candidatevotes** variable we put in the Rows shelf. Right click on that variable > Quick Table Calculation > Percent of Total. Right click on that variable again > Edit Quick Calculation > Compute Using: Table (down). Hovering over each data point should now show each party’s vote share in a given year’s election.

Like in previous steps, add **Year** and **Party Simplified** as filters and show them. Also, change the view to Entire View. The final product should look like this:

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Line%20Graph%20Finished.png" width = "800">

Rename this sheet to **“Party Vote Share by Year”** or something similar. Now that our visualizations are complete, we’re ready to build our dashboard!

## 4) Constructing your dashboard

Start by clicking New Dashboard at the bottom of the screen.

### a) Parts of the dashboard workspace

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Dashboard%20Workspace.png" width = "800">

`1)` is where you specify what **type of device** the dashboard is for. You might wish to make a dashboard that’s viewable on mobile devices, but for this tutorial we’ll just use the default option, which is a desktop.
`2)` is where you specify the **size of desktop** the dashboard will be compatible with. Change it to Generic Desktop.
`3)` is the **list of worksheets** that exist in your workbook. In our case, they are the three visualizations we just made.
`4)` is the bank of possible **objects** you can add to your dashboard. They let you customize the overall look, for instance by adding titles, third-party images, or blank space. For a complete explanation of each object, look [here](https://help.tableau.com/current/pro/desktop/en-us/dashboards_create.htm#add-dashboard-objects-and-set-their-options).
`5)` is where you specify whether your **dashboard layout** will be tiled or floating. In a tiled layout, all your sheets snap into a grid-like arrangement. In a floating layout, they are free to exist anywhere. For this tutorial, we’ll use a tiled layout.

### b) Adding sheets to your dashboard

Start to assemble your dashboard by dragging the **Map** sheet to the workspace. It should take up the entire workspace initially. Next, drag the **Candidate Vote Count by Year** barplot to the workspace. As you move it around, you’ll see gray rectangles appearing. These give you a preview of where the sheet will appear if you release it in a given spot.

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Adding%20Sheets%20to%20Dashboard.gif" width = "1000">

I dropped the barplot on the right half of the dashboard, but you’re welcome to put it anywhere. Do the same with the **Party Vote Share by Year** line graph. It might make sense to put it in the same column/row as the barplot to give the map extra space, since it can get cluttered if too many years are selected.

### c) Dynamic filters and interactivity

Play around with some of the filters on the right side of the screen and see how the visualizations change. You’ll notice that there are 3 sets of filters, one set that controls each part of the dashboard.

The aim of this section (and the aim of a good dashboard) is to edit the filters such that they link multiple visualizations and show how each changes for different combinations of variables. In this case, we want to be able to see trends in **Candidate Vote Totals by Year** and **Party Vote Share by Year** given specific years and political parties, so that we can ask questions like, How did the Republican candidate’s performance change between 1988 and 1996?

You’ll notice, however, that the electoral **Map** should only be filtered by year and not by political party. This is because the coloring scheme depends on the **Party Simplified** variable, which is filtered to just Democrats in order to display the Democratic vote share in all the years selected.

This means we want to apply **Year** as a filter to all worksheets, and **Party Simplified** as a filter to just the barplot and the line graph.

First, we’ll deal with **Year**. Locate any of the **Year** filters at right and select it. Click the downward pointing arrow, hover over **Apply to Worksheets**, and select **All Using This Data Source**.

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Apply%20Year%20Filter%20to%20All.gif" width = "1000">

Try selecting different year values on this filter. Now, this should change the years displayed on all three visualizations. We can get rid of the other two **Year** filters by clicking on each of them and selecting the **X** at the top right of the filter.

This is the basic formula for making dynamic filters that link together multiple worksheets on a dashboard. If you wish to apply a filter to some sheets but not others, the process is only a little more complicated.

To apply the **Party** filter to the barplot and line graph but not the map, first locate the **Party** filter associated with just the map. Check and uncheck different parties to make sure that doing so changes the colors of the map, but not the other two worksheets. (You can also make sure it’s only being applied to the map by clicking on the downward facing arrow associated with this filter, hovering over **Apply to Worksheets**, and making sure that **Only This Worksheet** is selected.)

Make sure that only Democrat is selected and then remove this filter from the dashboard.

Next, choose either of the other two **Party** filters and go back to **Apply to Worksheets** and choose **Selected Worksheets**. Check both **Candidate Vote Totals** by **Year** and **Party Vote Share by Year**. Make sure **Map** remains unchecked. Click OK. 

<img src = "https://github.com/jonah916/dh199/blob/main/visuals/Apply%20Party%20Filter%20to%20Selected.gif" width = "1000">

Make sure this did what we wanted by selecting different values of **Party**. Doing so should affect the barplot and line graph but not the map. If so, we can delete the other **Party** filter.

**Congrats!** You’ve made your first dashboard, complete with dynamic filtering and interactivity. From here on out, most of the changes you might make would be cosmetic. For example, you can change the order of the filters on the right side of the screen, or you might wish to move the color scale closer to the map it corresponds to. Feel free to check out the “Best Practices” section below to get a better idea of how to construct a dashboard that helps you and others get the most out of your data.

### d) Best Practices

- Less is more  
- Leverage the most-viewed spot (top left of the page)  
- Highlighting  
- Show filters as much as possible but not more than necessary  
- Size: ranges, automatic, different sizing for different device types
