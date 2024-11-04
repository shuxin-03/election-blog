---
title: 'Week 8: Shocks: Game Changer or Status Quo?'
author: ShuXin Ho
date: '2024-10-27'
slug: week-8
categories: []
tags: []
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />



# Election Blog

## Week 8: Shocks: Game Changer or Status Quo?

As Florida residents woke up to the devastation left by the recent [hurricanes](https://apnews.com/article/harris-trump-biden-helene-milton-hurricane-fema-f1bf69434656bd693daf316db3842fac#), Democratic presidential candidate Kamala Harris, who is also the current vice president, stepped in to provide support and demonstrate leadership. Meanwhile, her challenger, Republican candidate Donald Trump, criticized the government’s poor management of the crisis and pledged his support to those affected.

This brings up an important question: **Do shocks and unexpected events, such as hurricanes, scandals, and protests, truly influence election outcomes?** Or are they just temporary disruptions that do not change the political landscape? [Sides and Vavreck (2013)](https://hollis.harvard.edu/permalink/f/1mdq5o5/TN_cdi_jstor_books_j_ctt7ztpn1) hypothesized that such **game changers** may shape short-term narratives, but ultimately it is the fundamentals determining the election outcome and reinforcing the **status quo**.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

In states where the Democratic Party won in the previous election (shown in blue), the two-party vote share has decreased slightly but remains above 50%. In contrast, states that did not vote Democratic in the last election (shown in red) show a slight increase in Democratic vote share, but with more variability.

However, removing 1996 data points from the graph tells a completely different story, states with more hurricanes tend to have higher Democratic vote shares, regardless of prior voting history. The relationship between hurricanes and vote share seems less dramatic, supporting the idea that **shocks like hurricanes tend to maintain the status quo rather than being true game changers in the electoral landscape**.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

Therefore, while unexpected shocks present candidates with an opportunity to appeal to voters, they may not have a lasting impact on election outcomes. For this reason, I’ve decided not to include these variables in my final prediction model.

## Building the Final Election Prediction Model

### Consideration: Economic Variables

Building on my findings from Week 2, where I found that GDP growth and the unemployment rate in the second quarter of the election year are the best predictors of election outcomes, I’ve now expanded my analysis to include additional economic variables that better capture consumers’ perceptions of the economy. While GDP growth and unemployment are important, they don’t always translate into immediate effects that voters feel. There can be a time lag or disconnect between macroeconomic indicators and individual experiences.

To address this, I am **incorporating the Index of Consumer Sentiment** measured by the [University of Michigan](http://www.sca.isr.umich.edu/) into my **national two-party popular vote share and electoral college share prediction**. These indices gauge consumer sentiment by asking questions like, "Would you say that you (and your family living there) are better off or worse off financially than you were a year ago?" and "Looking ahead, which would you say is more likely—that in the country as a whole we’ll have continuous good times during the next five years, or that we will have periods of widespread unemployment or depression?" These additional variables offer a more direct reflection of how voters perceive the economy and may provide a more accurate prediction of election outcomes.

Random forest

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" /><table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Candidate </th>
   <th style="text-align:right;"> Predicted Two-Party Vote Share (%) </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> Kamala Harris </td>
   <td style="text-align:right;background-color: lightblue !important;"> 47.73014 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Donald Trump </td>
   <td style="text-align:right;background-color: lightpink !important;"> 52.26986 </td>
  </tr>
</tbody>
</table>

The random forest model shows that indeed, the Index of Consumer Sentiment is one of the most important predictors of the national two-party popular vote share. Based on economic fundamentals alone, I predict that Harris will receive 47.73% of the popular vote, with a test error of approximately 6.76 percentage points, suggesting the model may be overfitting, as indicated by a training error of 0 percentage points.

### Consideration: Demographic Variables

As noted in Week 5, demographic variables are fairly important predictors of voting behavior, hence I will use the 1% voter file data from October 2024 to capture **demographic distributions in my final state-level electoral college share prediction**.

### Consideration: Polling Averages

To account for historical trends in polling data, I will incorporate polling data from 1992 onward, a period when polling methodologies became more sophisticated. Starting from this election cycle also factors in significant realignments in American politics, so my model can reflect current ideological divides.

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
   <td style="text-align:right;background-color: lightblue !important;"> 50.71448 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Donald Trump </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.28552 </td>
  </tr>
</tbody>
</table>

My prediction of Harris receiving 50.7% of the popular vote and Trump 49.3% has a margin of error, as reflected in the MSE of 0.984, which means the average difference between my prediction and true vote share in this case would be around 0.992 percentage point. This **margin of error explains why the economic variables and polling data show different prediction outcome, which I will reconcile in my final prediction model.**

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
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Arizona </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.36323 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Arizona </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.63677 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> California </td>
   <td style="text-align:right;background-color: lightblue !important;"> 57.64164 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> California </td>
   <td style="text-align:right;background-color: lightpink !important;"> 42.35836 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Florida </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.27411 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Florida </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.72589 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.45827 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.54173 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightblue !important;"> 51.08386 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.91614 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.10148 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.89852 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.47868 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.52132 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.54522 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.45478 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Montana </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.58290 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Montana </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.41710 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Nebraska </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.71781 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Nebraska </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.28219 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Nebraska Cd 2 </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.08388 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Nebraska Cd 2 </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.91612 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.56689 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.43311 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.45168 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.54832 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.31918 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.68082 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New York </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.81280 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New York </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.18720 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.39013 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.60987 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.20338 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.79662 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.50616 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.49384 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Texas </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.00246 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Texas </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.99754 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.04569 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.95431 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> democrat </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.44591 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.55409 </td>
  </tr>
</tbody>
</table>

At the state-level prediction, an MSE of 69.3 indicates that, on average, the model’s predictions deviate from the actual vote share by about 8.3 percentage points. This error in predicting vote share could mean missing whether a state swings to a particular party, especially in battleground states where races are often decided by margins of 1-2%.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />

To find out the cause of the high state-level MSE, I plotted residuals using a heat map. Certain years, like 2008 and 2020, show consistently high residuals across states, indicating that my model may miss critical time-specific factors. State overestimations and underestimations suggest that unique state-level dynamics are not fully captured by polling data, leading me to **limit polling data to national predictions only**.

### Prediction: National Two-Party Popular Vote Share and Electoral College Seats

I will predict the national two-party popular vote share and electoral college seats by evaluating the predictive accuracy of these three models: (1) super learning using a weighted ensemble of OLS models, (2) random forest, and (3) regularized regression. To enhance the robustness of these predictions, I will also conduct 1,000 simulations to provide not only point estimates but also prediction intervals.







*Code developed with the assistance of ChatGPT.*
