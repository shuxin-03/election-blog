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

**Model formula:** `$$pv2p_t = \beta_0 + \beta_1\cdot{Economy_t} + \beta_2\cdot{Polling_t} + \beta_3\cdot{Demographics_t} + \beta_4\cdot{Incumbency_t}$$`

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

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

Because the current vote shares do not add up to 100%, I rescaled them to 100%. Overall, I predict that the Democratic Party will receive 56.76% of the national two-party popular vote share, with a 90% prediction interval between 56.5% and 54.55%.

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
   <td style="text-align:right;background-color: lightblue !important;"> 56.76 </td>
   <td style="text-align:left;background-color: lightblue !important;"> TRUE </td>
  </tr>
  <tr>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 43.24 </td>
   <td style="text-align:left;background-color: lightpink !important;"> FALSE </td>
  </tr>
</tbody>
</table>

### Part 2: Electoral College Vote Share

**Model formula:** `$$pv2p_t = \beta_0 + \beta_1\cdot{pv2p_{t-1}} + \beta_2\cdot{pv2p_{t-2}} + \beta_3\cdot{Economy_t} + \beta_4\cdot{Polling_t} + \beta_5\cdot{Incumbency_t}$$`

In my state-level model predicting the Democratic Party’s popular vote share, I use a similar set of variables as in my national-level model. This includes economic indicators, polling data, demographics, and incumbency status.

`\(pv2p_{t-1} + {pv2p_{t-2}}\)`: I incorporate the Democratic Party’s vote share from the previous two elections in each state to account for the specific political climate and voter sentiment at the state level.

`\(Economy_t\)`: Including the `\(Economy_t\)` variable at the state level is tricky as it's unclear whether voters prioritize sociotropic concerns (national economic indicators) or individual concerns (state economic indicators). To explore this, I compared the significance of these two types of indicators in predicting vote share using a mixed-effects model. Accounting for each state's baseline political preference, higher state unemployment rates are associated with a significant decrease in the incumbent party’s vote share. This supports the theory that voters are responsive to local economic conditions. Therefore, I included state unemployment as an economic indicator in my model.

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
   <td style="text-align:left;background-color: lightgreen !important;"> (Intercept) </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 49.5386 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 5.1652 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 452 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 9.5909 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: rgba(102, 205, 0, 255) !important;"> state_gdp </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.0336 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.2343 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 452 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.1432 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.8862 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightgreen !important;"> state_unemployment </td>
   <td style="text-align:right;background-color: lightgreen !important;"> -1.6802 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.5862 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 452 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> -2.8661 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.0043 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: rgba(102, 205, 0, 255) !important;"> natl_gdp </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> -0.2394 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.3273 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 452 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> -0.7313 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.4650 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: rgba(102, 205, 0, 255) !important;"> natl_unemployment </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.2547 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.4671 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 452 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.5452 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.5859 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: rgba(102, 205, 0, 255) !important;"> natl_consumer_sentiment </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> -0.0357 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.0465 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 452 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> -0.7692 </td>
   <td style="text-align:right;background-color: rgba(102, 205, 0, 255) !important;"> 0.4422 </td>
  </tr>
</tbody>
</table>

`\(Demographics_t\)`: Due to lack of a time series data of voter's party registration and identification at the state-level, I omit this variable from my state-level analysis.

I use super learning to develop a weighted ensemble where weights are determined by out-of-sample performance of each OLS models with different combination of variables.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-7"></span>Table 2: In-Sample and Out-of-Sample MSEs with Ensemble Weights by Year (State)</caption>
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
   <td style="text-align:right;background-color: lightgreen !important;"> 62.01 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.380 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.993 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.409 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.625 </td>
   <td style="text-align:right;background-color: violet !important;"> 132.64 </td>
   <td style="text-align:right;background-color: violet !important;"> 7.553 </td>
   <td style="text-align:right;background-color: violet !important;"> 734.79 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.0564 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0773 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8536 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0691 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2016 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 36.62 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 57.40 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.352 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.533 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.487 </td>
   <td style="text-align:right;background-color: violet !important;"> 16.593 </td>
   <td style="text-align:right;background-color: violet !important;"> 70.62 </td>
   <td style="text-align:right;background-color: violet !important;"> 6.389 </td>
   <td style="text-align:right;background-color: violet !important;"> 27.37 </td>
   <td style="text-align:right;background-color: violet !important;"> 6.1389 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1341 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8659 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 36.63 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 57.28 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 5.894 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.074 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.864 </td>
   <td style="text-align:right;background-color: violet !important;"> 17.305 </td>
   <td style="text-align:right;background-color: violet !important;"> 190.04 </td>
   <td style="text-align:right;background-color: violet !important;"> 17.497 </td>
   <td style="text-align:right;background-color: violet !important;"> 5589.23 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.2054 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.9503 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0497 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2008 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 35.13 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 61.54 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.490 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.889 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.790 </td>
   <td style="text-align:right;background-color: violet !important;"> 34.722 </td>
   <td style="text-align:right;background-color: violet !important;"> 52.33 </td>
   <td style="text-align:right;background-color: violet !important;"> 10.115 </td>
   <td style="text-align:right;background-color: violet !important;"> 21.48 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.7409 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0857 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.9143 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 37.21 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 59.71 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.846 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.951 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.529 </td>
   <td style="text-align:right;background-color: violet !important;"> 10.919 </td>
   <td style="text-align:right;background-color: violet !important;"> 58.25 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.541 </td>
   <td style="text-align:right;background-color: violet !important;"> 14.39 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.9492 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1959 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8041 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 35.08 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 57.67 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 6.562 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.795 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.912 </td>
   <td style="text-align:right;background-color: violet !important;"> 34.448 </td>
   <td style="text-align:right;background-color: violet !important;"> 68.55 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.673 </td>
   <td style="text-align:right;background-color: violet !important;"> 26.02 </td>
   <td style="text-align:right;background-color: violet !important;"> 3.6306 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1554 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8446 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000 </td>
  </tr>
</tbody>
</table>


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />

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
   <td style="text-align:right;background-color: lightpink !important;"> 47.73 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 52.27 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.20 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.58 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.94 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.75 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.11 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.48 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> California </td>
   <td style="text-align:right;background-color: lightblue !important;"> 62.42 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 37.58 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.46 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.97 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 62.52 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 36.85 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 37.32 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 37.80 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Colorado </td>
   <td style="text-align:right;background-color: lightblue !important;"> 55.13 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 44.87 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.46 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.86 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.27 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.17 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.65 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.14 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Florida </td>
   <td style="text-align:right;background-color: lightpink !important;"> 45.57 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 54.43 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.00 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.39 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.78 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 53.89 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.22 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.57 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.23 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.77 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.83 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.19 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.53 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.31 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.72 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.09 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Indiana </td>
   <td style="text-align:right;background-color: lightpink !important;"> 39.78 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 60.22 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.40 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.86 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.34 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.88 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.33 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.76 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightblue !important;"> 64.66 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 35.34 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.34 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.99 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 64.64 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 34.27 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 34.97 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 35.56 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Massachusetts </td>
   <td style="text-align:right;background-color: lightblue !important;"> 63.93 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 36.07 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 62.70 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.29 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.91 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 35.11 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 35.71 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 36.25 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.44 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.56 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.01 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.35 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.70 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.12 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.48 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.82 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightblue !important;"> 52.08 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 47.92 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.60 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.96 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.32 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.38 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.81 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.22 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightpink !important;"> 41.25 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 58.75 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.89 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.34 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.79 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.43 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.86 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.29 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Montana </td>
   <td style="text-align:right;background-color: lightpink !important;"> 39.01 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 60.99 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 38.54 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.04 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.57 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.59 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.03 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.49 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Nebraska </td>
   <td style="text-align:right;background-color: lightpink !important;"> 39.67 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 60.33 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.32 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.83 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.32 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.07 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 60.57 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 61.02 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.85 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.15 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.32 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.66 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.01 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.60 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.95 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.29 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightblue !important;"> 51.66 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 48.34 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.01 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.44 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.86 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.69 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.14 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.56 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightblue !important;"> 52.84 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 47.16 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.09 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.51 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.93 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.44 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.87 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.27 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> New York </td>
   <td style="text-align:right;background-color: lightblue !important;"> 58.44 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 41.56 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.56 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.00 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.44 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.84 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.24 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.65 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.26 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.74 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.88 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.25 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.64 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.36 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.73 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.09 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightpink !important;"> 44.29 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 55.71 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 43.93 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.32 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.70 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.37 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.74 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 56.08 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.88 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.12 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.46 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.80 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.15 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.70 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.04 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.39 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> South Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 42.35 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 57.65 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 41.92 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 42.35 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 42.78 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.22 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 57.65 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.04 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Texas </td>
   <td style="text-align:right;background-color: lightpink !important;"> 44.85 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 55.15 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.39 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 44.75 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 45.14 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 54.64 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.03 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 55.40 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Utah </td>
   <td style="text-align:right;background-color: lightpink !important;"> 36.90 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 63.10 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 36.40 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 36.96 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 37.52 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 62.75 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.21 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 63.66 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 52.59 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 47.41 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.95 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.33 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 52.69 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 46.77 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.17 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 47.61 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Washington </td>
   <td style="text-align:right;background-color: lightblue !important;"> 59.31 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 40.69 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Democrat </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 58.51 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.00 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 59.48 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 39.98 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.48 </td>
   <td style="text-align:right;background-color: lightblue !important;background-color: rgba(204, 204, 204, 255) !important;"> 40.97 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.32 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.68 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 48.95 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.31 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 49.67 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.30 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 50.67 </td>
   <td style="text-align:right;background-color: lightpink !important;background-color: rgba(204, 204, 204, 255) !important;"> 51.00 </td>
  </tr>
</tbody>
</table>

For states with insufficient data, and therefore not included in this prediction, I assume their electoral votes will go to the party projected by expert predictions from [Sabato Crystall Ball](https://centerforpolitics.org/crystalball/2024-president/), as shown in the map below. there are no discrepancies between my predictions and those from Sabato’s Crystal Ball, and I predict that all swing states will vote Republican.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

Therefore, my final prediction for the electoral college vote distribution by party is shown in the map below:

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="672" /><table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-11"></span>Table 3: Total Number of Electors by Party (2024)</caption>
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


I predict that the Democratic Party will win the national two-party popular vote with a share of 56.76% compared to 43.24% for the Republican Party. However, despite this popular vote advantage, I anticipate the Democratic Party will lose the electoral college vote, receiving 226 votes compared to the Republican Party’s 312 votes. This would result in the Republican Party winning the Presidency and Vice Presidency.
