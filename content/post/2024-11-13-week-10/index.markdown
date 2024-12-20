---
title: 'Week 10: Model Evaluation'
author: ShuXin Ho
date: '2024-11-17'
slug: week-10
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



# Election Blog

## Week 10: Model Evaluation

### Recap of My Model and Predictions

Prior to the 2024 presidential election, I developed a weighted ensemble model using super learning. The weights for this ensemble were determined from the out-of-sample performance of multiple OLS models incorporating various predictor variables, including lagged vote share, economic indicators, polling data, demographic variables, incumbency consideration, and their combinations.

My final forecast predicted Kamala Harris would win the national two-party popular vote with 56.76%, but lose the Electoral College vote, securing only 226 votes. The model accurately predicted the results of the battleground states, including Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin, all of which voted for Donald Trump.

### Electoral College Vote Share Evaluation

Below is the electoral college map showing the election outcome, which matched my model's predictions.



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The following bubble map illustrates county-level results by total number of votes casted in each county, to better visualize the vote distribution. Democratic vote share is concentrated in highly populated urban areas, while Republican vote share cover a broader geographic area, as shown by the widespread red bubbles.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

My prediction error for each state is demonstrated in the graph below. All values still result in the correct prediction for the party winner of each state's two-party popular vote.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

### National Two-Party Popular Vote Share Evaluation


```
## Bias: -7.638292
```

Despite predicting the the electoral college vote share correctly, my prediction for the national two-party popular vote share went terribly wrong as of [November 18th](https://www.cookpolitical.com/vote-tracker/2024/electoral-college), where I overestimated The Democratic Party's popular vote by 7.64 percentage points.

Therefore, I will focus on evaluating the reason for inaccuracy in my national two-party popular vote share model. I hypothesize a few reasons for my model's inaccuracy and propose corresponding changes.

**1. Unique circumstance of incumbency**

The Harris-Trump matchup presented a unique incumbency scenario: Harris was the sitting vice president, while Trump was a former president. My initial model did not fully account for this dynamic.

Change: Replace the `\(IncumbentPresident\)` variable with `\(PrevAdmin\)` to better capture the influence of prior administrations in such scenarios.

**2. Polling model shortcomings**

My polling model's equation is `$$D\_pv2p = D\_NetLatest538PollAverage + D\_NetMean538PollAverage(30 weeks) + NetLatestJobApproval + NetMeanJobApproval(June-Oct)$$` for Democratic vote share, which I then repeat for Republican vote share separately, then rescaling them to a 100%. Predictors like net job approval and polling averages are meaningful only when used to model the incumbent party's vote share, which is not the case in my model that uses Democratic Party and Republican Party vote share as response variables.

Change: Re-run the polling model with the inclusion of dummy variables for `\(PrevAdmin\)` and `\(IncumbentParty\)`.

**3. Poor predictability of demographics**

The demographic model exhibited high variability in out-of-sample MSE, leading to a low weight in the ensemble model.

Change: Remove demographics as a predictor variable to simplify the model and reduce variability.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-7"></span>Table 1: In-Sample and Out-of-Sample MSEs with Ensemble Weights by Year (National)</caption>
 <thead>
  <tr>
   <th style="text-align:right;"> Year </th>
   <th style="text-align:right;"> In-Sample Economy MSE </th>
   <th style="text-align:right;"> In-Sample Polling MSE </th>
   <th style="text-align:right;"> In-Sample Combined MSE </th>
   <th style="text-align:right;"> In-Sample Ensemble MSE </th>
   <th style="text-align:right;"> Out-of-Sample Economy MSE </th>
   <th style="text-align:right;"> Out-of-Sample Polling MSE </th>
   <th style="text-align:right;"> Out-of-Sample Combined MSE </th>
   <th style="text-align:right;"> Out-of-Sample Ensemble MSE </th>
   <th style="text-align:right;"> Economy Weight </th>
   <th style="text-align:right;"> Polling Weight </th>
   <th style="text-align:right;"> Combined Weight </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 2020 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.837059 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.9122978 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.5612281 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.317541e+04 </td>
   <td style="text-align:right;background-color: violet !important;"> 13.6184627 </td>
   <td style="text-align:right;background-color: violet !important;"> 65477.451298 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1391090 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.7895167 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0713743 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2016 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.296768 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.3444192 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.5292405 </td>
   <td style="text-align:right;background-color: violet !important;"> 8.347200e-03 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.7241477 </td>
   <td style="text-align:right;background-color: violet !important;"> 378.947779 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4697574 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4789688 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0512738 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.148008 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.5810492 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.4386519 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.862322e+00 </td>
   <td style="text-align:right;background-color: violet !important;"> 39.7400609 </td>
   <td style="text-align:right;background-color: violet !important;"> 23.692840 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3319988 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2255234 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4424777 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2008 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.710408 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.4376414 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.4612257 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.049025e+03 </td>
   <td style="text-align:right;background-color: violet !important;"> 33.7935739 </td>
   <td style="text-align:right;background-color: violet !important;"> 393.869633 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.2239442 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3751625 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4008934 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2004 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.268307 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.0717113 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 8.1153974 </td>
   <td style="text-align:right;background-color: violet !important;"> 3.388892e-01 </td>
   <td style="text-align:right;background-color: violet !important;"> 5.9350622 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.560224 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.8102364 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1754739 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0142897 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 12.188676 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.4406611 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 3.7118069 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.979935e+00 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.0577291 </td>
   <td style="text-align:right;background-color: violet !important;"> 378.793680 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.5017074 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4563862 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0419064 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1996 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 8.265306 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.4359492 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.1421979 </td>
   <td style="text-align:right;background-color: violet !important;"> 4.938677e+01 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.2216226 </td>
   <td style="text-align:right;background-color: violet !important;"> 27.600333 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0410015 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.9304671 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0285315 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1992 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 7.884249 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.4281347 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.2868915 </td>
   <td style="text-align:right;background-color: violet !important;"> 6.602771e+01 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.4192285 </td>
   <td style="text-align:right;background-color: violet !important;"> 511.775086 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0045835 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.9693198 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0260966 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1988 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 11.576491 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.1061987 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.0000000 </td>
   <td style="text-align:right;background-color: violet !important;"> 9.176773e+00 </td>
   <td style="text-align:right;background-color: violet !important;"> 5.2244662 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.737042 </td>
   <td style="text-align:right;background-color: violet !important;"> 2.737042 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.0000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 1.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1984 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 4.109527 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 2.4359492 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.4110531 </td>
   <td style="text-align:right;background-color: violet !important;"> 1.407379e+02 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.2216226 </td>
   <td style="text-align:right;background-color: violet !important;"> 27.600333 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1941586 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3371914 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4686500 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1980 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 8.974900 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0.1700332 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 0 </td>
   <td style="text-align:right;background-color: lightgreen !important;"> 1.2043133 </td>
   <td style="text-align:right;background-color: violet !important;"> 5.151202e+02 </td>
   <td style="text-align:right;background-color: violet !important;"> 87.3821839 </td>
   <td style="text-align:right;background-color: violet !important;"> 4381.192756 </td>
   <td style="text-align:right;background-color: violet !important;"> 0.000000 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.3489344 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.4656557 </td>
   <td style="text-align:right;background-color: yellow !important;"> 0.1854098 </td>
  </tr>
</tbody>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" /><table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
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
   <td style="text-align:right;background-color: lightblue !important;"> 49.0203 </td>
   <td style="text-align:left;background-color: lightblue !important;"> FALSE </td>
  </tr>
  <tr>
   <td style="text-align:right;background-color: lightpink !important;"> 2024 </td>
   <td style="text-align:left;background-color: lightpink !important;"> Republican </td>
   <td style="text-align:right;background-color: lightpink !important;"> 50.9797 </td>
   <td style="text-align:left;background-color: lightpink !important;"> TRUE </td>
  </tr>
</tbody>
</table>

```
## Bias: 0.1039336
```

Incorporating the changes above, my revised model predicted the national two-party popular vote share with 0.1 percentage points error.

Other than the changes I have done above, I propose future modifications for election prediction models.

**1. Accounting for voter turnout**

Hypothesis: Lower turnout among traditionally Democratic voters, possibly due to dissatisfaction with the administration’s handling of difficult issues such as the [Gaza conflict](https://www.reuters.com/world/us/inside-democratic-rebellion-against-biden-over-gaza-war-2024-02-27/), reduced Harris's vote share.

Test: Compare turnout rates by demographic groups in 2024 to previous elections using voter file data and assess whether historically Democratic demographics (such as younger voters and minority ethnic groups) had a decline in turnout.

**2. Economic reality versus perception**

I will incorporate economic variables that more accurately measures voters' perception of the economy, as [people might still be recovering from the impact of COVID-19 economic downturn](https://www.cnn.com/2024/02/02/politics/cnn-poll-economy/index.html), so unemployment, GDP and RDPI figures may not reflect the full extent of how voters perceive the economy.

Hypothesis: My economic predictors (such as unemployment, GDP, S&P 500 volume, and real disposable personal income) failed to capture voters' subjective perceptions of the economy. For example, while unemployment rates were low, the impact of food price inflation or the lingering effects of the COVID-19 pandemic might have weighed more heavily on voters' decisions, given that [April 2022 food prices inflation rate rose up to 10.8%](https://www.bls.gov/opub/ted/2022/food-prices-up-10-8-percent-for-year-ended-april-2022-largest-12-month-increase-since-november-1980.htm#:~:text=FONT%20SIZE:%20PRINT:-,Food%20prices%20up%2010.8%20percent%20for%20year%20ended%20April%202022,month%20increase%20since%20November%201980&text=For%20the%20year%20ended%20April,percent%20increase%20in%20November%201981.), for instance.

Test: Analyze survey data on voters’ perception of economic conditions and correlate these perceptions with vote choices.

I will also expand economic variables:
- Use additional economic predictors, such as food price inflation and median wage growth, to capture the direct impact of economic stressors on voters.
- Extend the time frame for economic data to include the entire incumbent party’s term, not just the election year, as significantly poor economic conditions in 2022 and 2023 may have caused voter dissatistaction which carried on to 2024.

**3. Adjusting for airwar according to latest trends**

Hypothesis: While traditional airwar analysis focuses on campaign spending on television advertisements, modern media platforms such as podcasts, social media, and celebrity endorsements may play a significant role in shaping public opinion, especially among younger voters who are tech-savvy or older voters who have a lot of time to spend on their devices. For example, [Trump's appearance on Joe Rogan's podcast](https://www.thetimes.com/life-style/celebrity/article/donald-trump-joe-rogan-8grmztcjn), [Harris's endorsement by Taylor Swift](https://www.nbcnews.com/politics/2024-election/taylor-swift-endorses-kamala-harris-rcna170547), or interactions on platforms like FaceBook, Instagram and TikTok may influence voter sentiment in ways that are not captured by traditional ad spending metrics.

Test: Collect data on the following metrics and compare them to the candidates' vote share in specific demographic groups (such as younger voters) to evaluate their predictive power.

Metrics include:
- Audience size for each candidate's media appearances on platforms such as podcasts, late-night shows, and endorsements by public figures
- Engagement metrics such as the number of likes, shares, and comments for content related to each candidate
- Sentiment analysis of audience comments using natural language processing to assess voter sentiment
