---
title: 'Week 3: Polling and Public Opinion'
author: ShuXin Ho
date: '2024-09-22'
slug: week-3
categories: []
tags: []
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />



# Election Blog

## Week 3: Polling and Public Opinion

Leading up to the 2020 presidential elections, then-President Donald Trump [famously claimed](https://x.com/realDonaldTrump/status/1315638896550576131) on X (formerly Twitter) that he was "winning BIG in all of the polls that matter," dismissing the rest as "fake." This raises an important question: can we trust polls to reflect the real state of public opinion?

### Polling, explained

Polls are designed to **reveal the public’s preferences ahead of an election**. They help politicians gauge voter sentiment and allow the public to monitor general trends, which can lend credibility to the election process by reducing the chances of surprise results.

The goal of a poll is to offer an **unbiased** estimate of the population's opinion by surveying a **large, representative sample**. In theory, while some individuals may be at different ends of the extreme when answering polls, these biases should cancel out, and the aggregate result will provide a median estimate that closely reflects the true public opinion.

To further refine this, platforms like [FiveThirtyEight](https://projects.fivethirtyeight.com/polls/president-general/2024/national/) aggregate multiple polls. Individual polls can sometimes be biased towards certain populations or parties, for instance, one might overestimate support for a candidate, while another underestimates it. Therefore, **aggregating polls helps average out these errors** and gives us a clearer picture of the overall voter landscape.

### What can we learn from the polling averages over 2020 election cycle?

Though the media often describes certain events as "**gamechangers**," such as a candidate giving a notable speech or performing poorly for the presidential debate, political scientists argue that many **dynamic campaign elements may not matter as much as the underlying fundamentals**.

Looking at the graph below of polling averages during the 2020 election cycle, we can see this in action. While there were **some expected shifts after key events** like the Democratic National Convention (DNC) and the Republican National Convention (RNC), other moments showed surprising results. For example, despite expectations that Trump's COVID-19 diagnosis might significantly alter support for the Republican party, there was only a modest and short-lived bump in the polling numbers. On the Democratic side, approval fluctuated after events such as Ruth Bader Ginsburg's passing and the presidential debates, but there wasn't a dramatic shift that persisted. These trends suggest that even though certain events are billed as "gamechangers," their actual impact on polling is often limited or unpredictable, leaving many **fluctuations unexplained by these moments alone**.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

### Predicting 2024 election outcome using national polling data

To predict the 2024 election outcome, I will use the **regularized regression methods**, namely Ridge, Lasso, and Elastic Net. The regression plots below demonstrates how the coefficients for each variable (polling data from various weeks leading up to the election) change as I adjust the regularization strength (lambda) in each method. Ridge shows that all variables are kept in the model, though their influence decreases as lambda increases. Lasso reveals that some coefficients are driven to zero as lambda increases, indicating that certain weeks' polling data may not be as relevant. Elastic Net Regression offers a middle ground, where some coefficients are reduced to zero, but others are merely shrunk.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The graph below compares the estimated coefficients across different methods. This gives an overview of which predictors (polling weeks) are most consistently influential in predicting the election outcome across various methods. Based on my analysis, I have predicted:

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
   <td style="text-align:right;background-color: lightblue !important;"> 50.56093 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> Donald Trump </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.43907 </td>
  </tr>
</tbody>
</table>

These predictions are derived from polling data up to 30 weeks before the election trained on historical data from the election in 1968 to the most recent one in 2020, using Elastic Net regression for its balance between feature selection and regularization. However, my prediction of Harris receiving 50.6% of the popular vote and Trump 49.4% has a margin of error, as reflected in the MSE of 2.33, which means the average difference between my prediction and true vote share in this case would be around 1.5 percentage points.

### How do state-level polls differ from national level polls?

While national level polls may not perfectly explain election results, **can state-level polls can provide more granular insights** into voter preferences and behavior? Each state is a unique battleground in U.S. elections due to the electoral college system. Therefore, state-level polls offer a closer approximation to how individual states may swing, allowing for a finer understanding of electoral outcomes.

To demonstrate this, I used state-level polling data to build a **predictive model for the 2024 presidential election** using regularized regression methods. The regression plots visualizes the coefficients estimated for each of the weeks leading up to the election across different regression methods: OLS, Ridge, Lasso, and Elastic Net, using polling data from 1972 to 2020.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

I decided to use Elastic Net regression for prediction, as it yielded the most consistent coefficient estimates, accounting for the complexity in the data without overfitting.

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
   <td style="text-align:right;background-color: lightblue !important;"> 50.47361 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Arizona </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.52639 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> California </td>
   <td style="text-align:right;background-color: lightblue !important;"> 58.58440 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> California </td>
   <td style="text-align:right;background-color: lightpink !important;"> 41.41560 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Florida </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.09147 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Florida </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.90853 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.49647 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Georgia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.50353 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightblue !important;"> 51.68104 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Maryland </td>
   <td style="text-align:right;background-color: lightpink !important;"> 48.31896 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.19327 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Michigan </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.80673 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.47664 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Minnesota </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.52336 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.31651 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Missouri </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.68349 </td>
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
   <td style="text-align:right;background-color: lightblue !important;"> 50.63533 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Nevada </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.36467 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.42339 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New Hampshire </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.57661 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.51622 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New Mexico </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.48378 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> New York </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.45037 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> New York </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.54963 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.51302 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> North Carolina </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.48698 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightblue !important;"> 49.18747 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Ohio </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.81253 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.62929 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Pennsylvania </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.37071 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Texas </td>
   <td style="text-align:right;background-color: lightblue !important;"> 48.91102 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Texas </td>
   <td style="text-align:right;background-color: lightpink !important;"> 51.08898 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.06479 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Virginia </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.93521 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightblue !important;"> DEM </td>
   <td style="text-align:right;background-color: lightblue !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightblue !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightblue !important;"> 50.55380 </td>
  </tr>
  <tr>
   <td style="text-align:left;background-color: lightpink !important;"> REP </td>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Wisconsin </td>
   <td style="text-align:right;background-color: lightpink !important;"> 49.44620 </td>
  </tr>
</tbody>
</table>

An MSE of 70.04 indicates that, on average, the model’s predictions deviate from the actual vote share by about 8.4 percentage points. This error in predicting vote share could mean missing whether a state swings to a particular party, especially in battleground states where races are often decided by margins of 1-2%.

### Insights from Silver and Morris

Nate Silver was a key figure behind FiveThirtyEight, one of the largest election forecasting platforms in recent election cycles, which is now led by Elliot Morris. Their contrasting perspectives on the roles of fundamentals (economic forces and demographic information) versus poll-based forecasts provide valuable insights into election prediction.

[Nate Silver (2024)](https://www.natesilver.net/p/model-methodology-2024) takes a more **case-by-case approach** to election prediction. He emphasizes the importance of accounting for specific events and conditions that may impact an election. For instance, he considered the unique influence of COVID-19 during the 2020 presidential elections and has since decided to remove those considerations as we transition from a pandemic to an endemic state. He also highlights the potential effects of independent candidates, like Robert F. Kennedy Jr., who recently suspended his presidential campaign. Additionally, Silver points out that with Biden (who has dropped out and been replaced by Harris) and Trump potentially facing off again, examining historical data from past presidential rematches becomes essential. This granularity in analysis ensures that all factors specific to the election year, particularly those affecting the candidates and significant societal changes, are adequately considered.

[Elliot Morris (2024)](https://abcnews.go.com/538/538s-2024-presidential-election-forecast-works/story?id=110867585), on the other hand, adopts a **big-picture perspective** in his forecasting model. He integrates polling averages—assigning different weights and scores to various pollsters—with fundamental data that captures the economic landscape, such as employment rates, consumer spending, inflation, and political metrics like presidential approval ratings. This combination allows Morris to provide a more holistic view of the electoral landscape.

Silver's focus on depth and Moris's comprehensive coverage of breadth brings me to a novel idea: **what if we approached election predictions from an individual or micro-level perspective?** Imagine a perfect world where we could obtain any information from voters, except for who they will actually vote for on election day. In such a scenario, we could segment voters based on their behaviors and motivations:
* Partisan Voters: These individuals would support their party regardless of candidate or any “game-changing” moments.
* Candidate-Centric Voters: A smaller group, who decide based on the individual candidate rather than party affiliation.
* Challenger Voters: Voters who lean towards challengers when dissatisfied with current economic and social conditions, driven by a desire for change.
* Swing Voters: Those who fluctuate between parties based on specific issues or candidate qualities.
* Situational Voters: Their likelihood to show up could depend on various circumstances, such as pressing issues or the overall campaign dynamics.

If we could quantify these segments, we might be able to predict election outcomes accurately. **However, this perfect world with perfect information lives only in our imagination, much like the ideal of a perfect democracy**. In reality, voters' motivations are complex, often influenced by emotions, misinformation, and social dynamics that are difficult to quantify. While we may never achieve that perfect clarity, this attempt to understand voters' decision-making process can offer insights to how democracy works in practice.

*Code developed with the assistance of ChatGPT.*
