---
title: 'Week 9: Final Election Prediction'
author: ShuXin Ho
date: '2024-11-03'
slug: week-9
categories: []
tags: []
output: 
  blogdown::html_page:
    mathjax: true
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />



# Election Blog

## Week 9: Final Election Prediction

### Part 1: National Two-Party Popular Vote Share

Model formula: `$$pv2p_t = \beta_0 + \beta_1\cdot{Economy_t} + \beta_2\cdot{Polling_t} + \beta_3\cdot{Demographics_t} + \beta_4\cdot{Incumbency_t}$$`

`\(Economy_t\)`: As [Sides & Vavreck (2013)](https://muse.jhu.edu/book/64467) emphasized, fundamentals, such as the state of the economy, play a stronger role than campaign dynamics in determining election outcomes. This is supported by [Achen & Bartels (2017)](https://muse.jhu.edu/book/64646), who argued that voters often vote retrospectively based on the economy.

I ran a random forest model to identify the most important economic indicators influencing vote share. To account for historical trends effectively, I incorporated data from 1980 onward, the beginning of the Reagan era, when election factors in significant realignments in American politics, so my model can reflect current ideological divides.

For my super learning model, I selected the five most predictive economic indicators: unemployment rate, GDP growth rate, S&P 500 volume, consumer sentiment index, and RDP growth in the second quarter of the election year.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

`\(Polling_t\)`: [Gelman & King (1993)](http://www.jstor.org/stable/194212) highlighted that polling closer to the election tends to be more accurate, as it reflects voters' settled and informed preferences. [Tien & Lewis-Beck (2017)](https://blog.oup.com/2017/01/forecasting-models-2016-election/) also similarly argued that long-view (historical and theoretical) models align closer with the actual popular vote result.

In my model, I used the mean [FiveThirtyEight poll averages](https://projects.fivethirtyeight.com/polls/) from three months before the election day and the final poll average immediately before the election. I also obtained [Gallup presidential job approval ratings](https://news.gallup.com/interactives/507569/presidential-job-approval-center.aspx) to calculate mean net approval since June and latest net approval ratings in the same manner, informed by [Abramowitz's Time-for-Change Model](https://www.emory.edu/central/NEWS/Releases/time-for-change2.html).

`\(Demographics_t\)`: According to [Kim & Zilinsky (2024)](https://rdcu.be/dYXVH)'s partisan identification is the strongest and most stable predictor of vote choice. Consistent with this finding, my random forest model reveals that party identification outperform other demographic variables in predictive power.

Therefore, I include [partisan affiliation among registered voters](https://ballotpedia.org/Partisan_affiliations_of_registered_voters#2000) as a demographic predictor in my model.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

`\(Incumbency_t\)`: Incumbent presidents are typically at an advantage, be it through name recognition, public attention through media coverage, headstart in campaigning without the concern of primary elections, and power for pork-barrel spending. In my model, I do not consider Kamala Harris as an incumbent president (even though she is the current vice president), but I take into account that she is from the incumbent party.

`\(AirWar_t\)`, `\(GroundGame_t\)`, and `\(Shocks_t\)`: After analyzing these variables in my previous blog posts, I found no significant interactions between these dynamic, volatile campaign elements and the actual election outcome. Therefore, I exclude them from my final prediction model.

I use super learning to develop a weighted ensemble where weights are determined by out-of-sample performance of each OLS models with different combination of variables. The tables below show the in-sample and out-of-sample MSEs. The large out-of-sample MSE for the economy model in 2020 is likely due to the outliers in economic indicators as a result of COVID-19, whereas that in 2008 can be attributed to the global financial crisis.

The variation in weights demonstrates the model’s adaptability based on each election's specific economic and political context. For example, in 2020, the economic data was weighted less heavily, as COVID-19 impacted economic indicators without drastically affecting vote share. In 1992, Clinton's campaign famously emphasized, "It's the economy, stupid," and economic models might have underemphasized public sentiment about Bush's perceived lack of connection to economic hardship, something that polling picked up through indicators like approval ratings and direct questions about voter preferences.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-4"></span>Table 1: In-Sample and Out-of-Sample MSEs with Ensemble Weights by Year (National)</caption>
 <thead>
  <tr>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:right;"> In-Sample Economy MSE </th>
   <th style="text-align:right;"> In-Sample Polling MSE </th>
   <th style="text-align:right;"> In-Sample Demographics MSE </th>
   <th style="text-align:right;"> In-Sample Combined MSE </th>
   <th style="text-align:right;"> In-Sample Ensemble MSE </th>
   <th style="text-align:right;"> Out-of-Sample Economy MSE </th>
   <th style="text-align:right;"> Out-of-Sample Polling MSE </th>
   <th style="text-align:right;"> Out-of-Sample Demographics MSE </th>
   <th style="text-align:right;"> Out-of-Sample Combined MSE </th>
   <th style="text-align:right;"> Out-of-Sample Ensemble MSE </th>
   <th style="text-align:right;"> Economy Weight </th>
   <th style="text-align:right;"> Polling Weight </th>
   <th style="text-align:right;"> Demographics Weight </th>
   <th style="text-align:right;"> Combined Weight </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 2020 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.837 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.8758 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 21.28 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 5.0185 </td>
   <td style="text-align:right;background-color: violet !important;"> 23175.4122 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.7734 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.2110 </td>
   <td style="text-align:right;background-color: violet !important;"> 65497.975 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0617 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4349 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4644 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0390 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2016 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.297 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.8880 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 21.53 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.2968 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0083 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.4688 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.6188 </td>
   <td style="text-align:right;background-color: violet !important;"> 378.679 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0083 </td>
   <td style="text-align:right;background-color: yellow !important;"> 1.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.148 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.8683 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 20.99 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.5631 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.8623 </td>
   <td style="text-align:right;background-color: violet !important;"> 19.6347 </td>
   <td style="text-align:right;background-color: violet !important;"> 8.1441 </td>
   <td style="text-align:right;background-color: violet !important;"> 23.688 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2347 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1656 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2160 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3837 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2008 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.710 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.7232 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 19.31 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.7556 </td>
   <td style="text-align:right;background-color: violet !important;"> 2049.0252 </td>
   <td style="text-align:right;background-color: violet !important;"> 33.5689 </td>
   <td style="text-align:right;background-color: violet !important;"> 31.8964 </td>
   <td style="text-align:right;background-color: violet !important;"> 393.809 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1841 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2782 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2780 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2596 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.268 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.7405 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 21.20 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.6760 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.3389 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.5818 </td>
   <td style="text-align:right;background-color: violet !important;"> 5.6484 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.561 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2792 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2241 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3169 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1798 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.189 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.9138 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 21.57 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 5.7391 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.9799 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.3773 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0064 </td>
   <td style="text-align:right;background-color: violet !important;"> 378.679 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3395 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3189 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3057 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0359 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1996 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 8.265 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.7477 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 19.92 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.0482 </td>
   <td style="text-align:right;background-color: violet !important;"> 49.3868 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.6406 </td>
   <td style="text-align:right;background-color: violet !important;"> 24.4830 </td>
   <td style="text-align:right;background-color: violet !important;"> 27.598 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1520 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.7434 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0531 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0515 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1992 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 7.884 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.9239 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 20.56 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.9239 </td>
   <td style="text-align:right;background-color: violet !important;"> 66.0277 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0235 </td>
   <td style="text-align:right;background-color: violet !important;"> 14.7096 </td>
   <td style="text-align:right;background-color: violet !important;"> 511.620 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0235 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 1.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1988 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 11.576 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.5760 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 20.11 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.1768 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.8048 </td>
   <td style="text-align:right;background-color: violet !important;"> 21.2632 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.737 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.7368 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 1.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1984 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.109 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.8966 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 15.94 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.7683 </td>
   <td style="text-align:right;background-color: violet !important;"> 140.7379 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.8586 </td>
   <td style="text-align:right;background-color: violet !important;"> 78.8061 </td>
   <td style="text-align:right;background-color: violet !important;"> 27.595 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1113 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3089 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1424 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4374 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 8.975 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.9999 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 21.36 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.1401 </td>
   <td style="text-align:right;background-color: violet !important;"> 515.1202 </td>
   <td style="text-align:right;background-color: violet !important;"> 26.4980 </td>
   <td style="text-align:right;background-color: violet !important;"> 3.9181 </td>
   <td style="text-align:right;background-color: violet !important;"> 4381.167 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2166 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3219 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3518 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1098 </td>
  </tr>
</tbody>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

Because the current vote shares do not add up to 100%, I rescaled them to 100%. Overall, I predict that the Democratic Party will receive 56.57% of the national two-party popular vote share, with a 90% prediction interval between 63.45% and 55.03%. However, as the 50% mark falls within this interval, the election outcome remains highly uncertain.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:left;"> Party </th>
   <th style="text-align:right;"> Predicted Vote Share (%) </th>
   <th style="text-align:left;"> Winner </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 56.57 </td>
   <td style="text-align:left;background-color: lightblue !important;"> TRUE </td>
  </tr>
  <tr>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 43.43 </td>
   <td style="text-align:left;background-color: lightpink !important;"> FALSE </td>
  </tr>
</tbody>
</table>

### Part 2: Electoral College Vote Share

Model formula: `\(pv2p_t = \beta_0 + \beta_1\cdot{pv2p_{t-1}} + \beta_2\cdot{pv2p_{t-2}} + \beta_3\cdot{Economy_t} + \beta_4\cdot{Polling_t} + \beta_5\cdot{Incumbency_t}\)`

In my state-level model predicting the Democratic Party’s popular vote share, I use a similar set of variables as in my national-level model. This includes economic indicators, polling data, demographics, and incumbency status. However, I also incorporate the Democratic Party’s vote share from the previous two elections in each state to account for the specific political climate and voter sentiment at the state level.

`\(Economy_t\)`: Including the `\(Economy_t\)` variable at the state level is tricky as it's unclear whether voters prioritize sociotropic concerns (national economic indicators) or individual concerns (state economic indicators). To explore this, I compared the significance of these two types of indicators in predicting vote share using a mixed-effects model. Accounting for each state's baseline political preference, higher state unemployment rates are associated with a significance decrease in the incumbent party’s vote share. This supports the theory that voters are more responsive to local economic conditions over national trends. Therefore, I included state unemployment as the economic indicator in my model.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Variable </th>
   <th style="text-align:right;"> Estimate </th>
   <th style="text-align:right;"> Std. Error </th>
   <th style="text-align:right;"> DF </th>
   <th style="text-align:right;"> t-value </th>
   <th style="text-align:right;"> p-value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;background-color: rgba(153, 153, 153, 255) !important;"> (Intercept) </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 49.5386 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 5.1652 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 452 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 9.5909 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightgray !important;"> state_gdp </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.0336 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.2343 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 452 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.1432 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.8862 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: rgba(153, 153, 153, 255) !important;"> state_unemployment </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> -1.6802 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 0.5862 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 452 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> -2.8661 </td>
   <td style="text-align:right;background-color: rgba(153, 153, 153, 255) !important;"> 0.0043 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightgray !important;"> natl_gdp </td>
   <td style="text-align:right;background-color: lightgray !important;"> -0.2394 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.3273 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 452 </td>
   <td style="text-align:right;background-color: lightgray !important;"> -0.7313 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.4650 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightgray !important;"> natl_unemployment </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.2547 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.4671 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 452 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.5452 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.5859 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightgray !important;"> natl_consumer_sentiment </td>
   <td style="text-align:right;background-color: lightgray !important;"> -0.0357 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.0465 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 452 </td>
   <td style="text-align:right;background-color: lightgray !important;"> -0.7692 </td>
   <td style="text-align:right;background-color: lightgray !important;"> 0.4422 </td>
  </tr>
</tbody>
</table>

`\(Demographics_t\)`: Due to lack of a time series data of voter's party registration and identification at the state-level, I omit this variable from my state-level analysis.

I use super learning to develop a weighted ensemble where weights are determined by out-of-sample performance of each OLS models with different combination of variables.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-8"></span>Table 2: In-Sample and Out-of-Sample MSEs with Ensemble Weights by Year (State)</caption>
 <thead>
  <tr>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:right;"> In-Sample Lagged Vote MSE </th>
   <th style="text-align:right;"> In-Sample Economy MSE </th>
   <th style="text-align:right;"> In-Sample Polling MSE </th>
   <th style="text-align:right;"> In-Sample Combined MSE </th>
   <th style="text-align:right;"> In-Sample Ensemble MSE </th>
   <th style="text-align:right;"> In-Sample Lagged Vote MSE </th>
   <th style="text-align:right;"> Out-of-Sample Economy MSE </th>
   <th style="text-align:right;"> Out-of-Sample Polling MSE </th>
   <th style="text-align:right;"> Out-of-Sample Combined MSE </th>
   <th style="text-align:right;"> Out-of-Sample Ensemble MSE </th>
   <th style="text-align:right;"> Lagged Vote Weight </th>
   <th style="text-align:right;"> Economy Weight </th>
   <th style="text-align:right;"> Polling Weight </th>
   <th style="text-align:right;"> Combined Weight </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 2020 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 37.34 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 63.59 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.380 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.993 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.203 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.625 </td>
   <td style="text-align:right;background-color: violet !important;"> 59.63 </td>
   <td style="text-align:right;background-color: violet !important;"> 7.553 </td>
   <td style="text-align:right;background-color: violet !important;"> 3.116 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.5989 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3354 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.6646 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2016 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 36.62 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 60.46 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.352 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.533 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.533 </td>
   <td style="text-align:right;background-color: violet !important;"> 16.593 </td>
   <td style="text-align:right;background-color: violet !important;"> 69.32 </td>
   <td style="text-align:right;background-color: violet !important;"> 6.389 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.909 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.9091 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 1.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 36.63 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 59.86 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 5.894 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.082 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.292 </td>
   <td style="text-align:right;background-color: violet !important;"> 17.305 </td>
   <td style="text-align:right;background-color: violet !important;"> 72.45 </td>
   <td style="text-align:right;background-color: violet !important;"> 17.497 </td>
   <td style="text-align:right;background-color: violet !important;"> 6.064 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.4031 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2640 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.7360 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2008 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 35.13 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 63.62 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.490 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.889 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.323 </td>
   <td style="text-align:right;background-color: violet !important;"> 34.722 </td>
   <td style="text-align:right;background-color: violet !important;"> 54.44 </td>
   <td style="text-align:right;background-color: violet !important;"> 10.115 </td>
   <td style="text-align:right;background-color: violet !important;"> 1349.840 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.5817 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1367 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0022 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.7796 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0815 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 37.21 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 61.92 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.846 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.951 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.527 </td>
   <td style="text-align:right;background-color: violet !important;"> 10.919 </td>
   <td style="text-align:right;background-color: violet !important;"> 62.90 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.541 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.797 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.9492 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1958 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8036 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0006 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 35.08 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 60.91 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.562 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.795 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.068 </td>
   <td style="text-align:right;background-color: violet !important;"> 34.448 </td>
   <td style="text-align:right;background-color: violet !important;"> 66.80 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.673 </td>
   <td style="text-align:right;background-color: violet !important;"> 3.817 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.9641 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1413 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8587 </td>
  </tr>
</tbody>
</table>


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />

Similar to what I did for the national two-party popular vote share, I rescaled the predicted vote share to 100%. The columns in grey show the original values that do not add up to 100%.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> State </th>
   <th style="text-align:right;"> Rescaled Predicted Democratic Vote Share (%) </th>
   <th style="text-align:right;"> Rescaled Predicted Republican Vote Share (%) </th>
   <th style="text-align:left;"> Winner </th>
   <th style="text-align:right;"> Lower Bound (D) </th>
   <th style="text-align:right;"> Mean (D) </th>
   <th style="text-align:right;"> Upper Bound (D) </th>
   <th style="text-align:right;"> Lower Bound (R) </th>
   <th style="text-align:right;"> Mean (R) </th>
   <th style="text-align:right;"> Upper Bound (R) </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Arizona </td>
   <td style="text-align:right;background-color: lightpink !important;"> 47.13 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 52.87 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.42 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.02 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.60 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.17 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.99 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.80 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> California </td>
   <td style="text-align:right;background-color: lightblue !important;"> 61.17 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 38.83 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 62.98 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.66 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 64.37 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 37.49 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.41 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 43.29 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Colorado </td>
   <td style="text-align:right;background-color: lightblue !important;"> 54.28 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 45.72 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.73 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.36 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.96 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.59 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.46 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.12 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Florida </td>
   <td style="text-align:right;background-color: lightpink !important;"> 45.12 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 54.88 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.25 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.93 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.59 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.27 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.08 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.93 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 47.44 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 52.56 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.71 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.34 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.97 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.96 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.68 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.47 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Indiana </td>
   <td style="text-align:right;background-color: lightpink !important;"> 39.26 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 60.74 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.18 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.80 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.39 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.41 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.13 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 65.86 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightblue !important;"> 63.41 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 36.59 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 65.17 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 65.99 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 66.82 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 35.05 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 38.08 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.00 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Massachusetts </td>
   <td style="text-align:right;background-color: lightblue !important;"> 62.82 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 37.18 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 64.51 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 65.33 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 66.09 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 35.82 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 38.66 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.50 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.61 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.39 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.99 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.56 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.16 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.76 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.44 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.21 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightblue !important;"> 51.18 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 48.82 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.59 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.16 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.75 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.97 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.71 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.41 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightpink !important;"> 40.55 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 59.45 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.58 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 42.18 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 42.81 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.17 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.85 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 64.61 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Montana </td>
   <td style="text-align:right;background-color: lightpink !important;"> 38.64 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 61.36 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.54 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.17 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.83 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.98 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.80 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 66.62 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Nebraska </td>
   <td style="text-align:right;background-color: lightpink !important;"> 38.94 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 61.06 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.85 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.46 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.09 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.87 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.44 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 65.98 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.17 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.83 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.44 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.12 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.80 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.16 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.94 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.63 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.89 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.11 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.30 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.94 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.55 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.39 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.08 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.68 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightblue !important;"> 52.08 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 47.92 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.59 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.20 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.82 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.32 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.88 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.46 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> New York </td>
   <td style="text-align:right;background-color: lightblue !important;"> 57.51 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 42.49 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.01 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.83 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.52 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.60 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.20 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.01 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 47.33 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 52.67 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.63 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.24 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.81 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.01 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.81 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.53 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightpink !important;"> 43.60 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 56.40 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.76 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.31 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.92 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.97 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.60 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.07 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.03 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.97 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.40 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.00 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.59 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.49 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.11 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.88 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> South Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 41.75 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 58.25 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 42.76 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 43.44 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.09 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.03 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.62 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.31 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Texas </td>
   <td style="text-align:right;background-color: lightpink !important;"> 44.30 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 55.70 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.43 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.09 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.73 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.08 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.94 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.91 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Utah </td>
   <td style="text-align:right;background-color: lightpink !important;"> 36.54 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 63.46 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 37.28 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 38.01 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 38.71 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.16 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 66.01 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 68.63 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 51.84 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 48.16 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.26 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.91 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.57 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.35 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.09 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.80 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Washington </td>
   <td style="text-align:right;background-color: lightblue !important;"> 58.03 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 41.97 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.71 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.38 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.04 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.86 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 43.67 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.47 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.38 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.62 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.76 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.29 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.84 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.95 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.65 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.44 </td>
  </tr>
</tbody>
</table>

For the states with a lack of data and hence are not shown here in the prediction, I assume that all their votes will go to the party projected by expert predictions, [Sabato Crystall Ball](https://centerforpolitics.org/crystalball/2024-president/), as shown in the map below. It is worth noting that there are no discrepencies between my prediction and the expert prediction.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="672" />

Therefore, my final prediction for the electoral college map is shown in the map below:

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-12-1.png" width="672" /><table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-12"></span>Table 3: Total Number of Electors by Party (2024)</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Party </th>
   <th style="text-align:right;"> Total Electors </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 226 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 312 </td>
  </tr>
</tbody>
</table>

Therefore, overall, I predict the Democratic Party to win the national-level two-party popular vote share with 56.57% (compared to 43.43% by the Republican Party), but lose the electoral college vote share with 226 votes (compared to 312 votes by the Republican Party), resulting in the Republican party winning the President and Vice President positions.
