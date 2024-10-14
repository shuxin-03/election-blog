---
title: 'Week 6: The Air War'
author: ShuXin Ho
date: '2024-10-13'
slug: week-6
categories: []
tags: []
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

# Election Blog

## Week 6: The Air War

### The Costly Campaigns

From television commercials in the 20th century to Facebook ads and TikTok videos today, the **air war—campaign advertising through mass media—has become a vital element of elections**.

According to [opensecrets.org](https://www.opensecrets.org/news/2021/02/2020-cycle-cost-14p4-billion-doubling-16/), federal spending for the 2020 U.S. election reached an unprecedented 14.4 billion USD, with 5.7 billion USD spent on the presidential race alone. This made U.S. elections the most expensive in the world.

In previous blogs, I explored the predictive power of fundamentals like the economy, incumbency, and demographics in shaping election outcomes. But how do dynamic factors (that can be a result of choices of candidates), such as campaign efforts, influence elections when "voters are predictably partisan" and "the economy strongly shapes election results?"

[Sides & Vavreck (2013)](https://doi.org/10.2307/j.ctt7ztpn1) argue that while campaigns can shift votes through air wars (advertising) and ground games (field organizations), it is difficult for one candidate to gain enough support to change the polls dramatically or eventually win decisively. Think of a presidential election as a **tug-of-war**: if the polls remain steady, it doesn’t mean a campaign is weak, but rather that **both sides are running effective campaigns**. In the 2012 presidential elections, for instance, Obama and Romney, along with their supporters, spent nearly equal amounts of money, making it unlikely that one side had a significant advantage, as seen in the graph below.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

Interestingly, in all recent elections except for the 2012 cycle, the Democratic Party often outspend its opponents. So does Sides and Vavreck's theory hold when a party, particularly the Democrats, spends more? Let's explore this by comparing campaign spending to vote share.

Applying a log transformation to the contribution receipt amount provides a clearer picture. This graph highlights that **increased spending by the Democratic Party correlates with a higher vote share**, although the impact may not be dramatic, as the increase in vote share is more gradual when contributions are exceptionally large. In fact, the **effect is much smaller in swing states, and even reversed** in the 2012, 2016, and 2020 election cycles, showing that larger contribution amount does not necessarily translate to higher vote share, and other factors might play a larger role in influencing voters' decisions.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

The effect of campaign contributions is even less clear for the Republican Party, as illustrated by the graph below. In non-swing states, the Republican vote share seems to exhibit a negative correlation with increased contribution amounts, especially in the 2008, 2016, and 2020 elections. In swing states, there is little to no relationship between increased Republican contributions and their vote share, revealing that the **relationship between the Republican Party's spending and vote share is inconsistent across election cycles and state competitiveness**.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

### What Does the Air War Entail?

The topics that both parties advertise on, tracked by the [Wesleyan Media Project](https://mediaproject.wesleyan.edu/), offer some insights regarding their values and campaign messaging. Over the years, the Democratic Party consistently emphasized social welfare and healthcare issues, with an increasing focus on economic matters during times of financial crises (2008 and 2012). The Republican Party consistently highlighted national security, defense, and economic issues like taxes and government spending, adjusting their messaging based on the economic or political environment, such as post-9/11 security concerns in 2004.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-2.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-3.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-4.png" width="672" />

### Refining Final Election Prediction

Due to the unclear relationship between campaign spending and election outcome, I will not include the "air war" as a consideration factor in my final election prediction.

#### National Polls Prediction

Instead, I updated my prediction from polling by re-scaling the total percentage to 100% and including polling results up to four weeks before the election.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Candidate </th>
   <th style="text-align:right;"> Predicted Two-Party Vote Share (%) </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Kamala Harris </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.57937 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Donald Trump </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.42063 </td>
  </tr>
</tbody>
</table>

#### State Polls Prediction

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Party </th>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:left;"> State </th>
   <th style="text-align:right;"> Predicted Two-Party Vote Share (%) </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Arizona </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.42367 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Arizona </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.57633 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> California </td>
   <td style="text-align:right;background-color: lightblue !important;"> 56.54071 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> California </td>
   <td style="text-align:right;background-color: lightpink !important;"> 43.45929 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Florida </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.11468 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Florida </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.88532 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.39923 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.60077 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightblue !important;"> 51.62087 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.37913 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.14231 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.85769 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.53299 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.46701 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.34097 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.65903 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Montana </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.00000 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Montana </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.00000 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Nebraska Cd 2 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.00000 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Nebraska Cd 2 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.00000 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.49604 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.50396 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.55309 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.44691 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.49723 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.50277 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New York </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.83989 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New York </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.16011 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.45450 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.54550 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.05459 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.94541 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.49970 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.50030 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Texas </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.28975 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Texas </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.71025 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.30027 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.69973 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.40903 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.59097 </td>
  </tr>
</tbody>
</table>

My prediction of Harris receiving 50.6% of the popular vote and Trump 49.4% has a margin of error, as reflected in the MSE of 3.57, which means the average difference between my prediction and true vote share in this case would be around 1.9 percentage points. At the state-level prediction, an MSE of 70.26 indicates that, on average, the model’s predictions deviate from the actual vote share by about 8.4 percentage points. This error in predicting vote share could mean missing whether a state swings to a particular party, especially in battleground states where races are often decided by margins of 1-2%.

#### Comparing OLS, regularized regression, and random forest models for economic variables

#### Using demographic variables for prediction

*Code developed with the assistance of ChatGPT.*

