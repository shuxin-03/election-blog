---
title: 'Week 5: Who Votes, and How Do They Vote? An Overview of Demographics'
author: ShuXin Ho
date: '2024-10-06'
slug: week-5
categories: []
tags: []
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

# Election Blog

## Week 5: Demographics: Who Votes, and How Do They Vote?

In an increasingly polarized nation, or as Lynn Vavreck coined it, "**calcified**," demographics have become more predictive in understanding voting patterns.

### Who Votes?

Not every single citizen is registered vote, and not every registered voter will turnout. Individuals with higher education levels are more likely to vote because education provides information about the democratic process and instills a sense of civic virtue ([Wolfinger & Rosenstone, 1980](http://www.jstor.org/stable/j.ctt32bffz); [Shaw & Petrocik, 2020](https://doi-org.ezp-prod1.hul.harvard.edu/10.1093/oso/9780190089450.001.0001)). Older voters, especially retirees, are also more likely to participate due to their interest in preserving government programs like Social Security (Shaw & Petrocik, 2020). [Rosenstone & Hansen (1993)](https://doi.org/10.2307/2944841) also suggest that white and wealthier demographics are more likely to engage in politics and voting generally.



### How Do They Vote?

Political scientists widely agree that **party affiliation is the most significant predictor of voting behavior**, though this piece of information is not always available due to different states' data collection policies and voters' choice to disclose themselves as independent. While demographic factors like education level, age, gender, race, and income also play a role, they are generally seen as secondary to party identification.

To **explore how well demographic factors predict voting behavior**, I built **both logistic regression and random forest models** using the American National Election Studies (ANES) dataset from 1948 to 2020. My analysis focuses on core demographics like age, gender, race, education, and income to predict whether someone is likely to vote for the Democratic or Republican candidate in the U.S. presidential election. By comparing the performance of these two models, I aim to identify which method better captures the relationship between voter demographics and vote choice. The logistic regression model offers a more interpretable framework, while the random forest model capture non-linear interactions between explanatory variables to achieve greater predictive accuracy.

<table class="table" style="width: auto !important; margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;"> Predictor </th>
   <th style="text-align:right;"> Estimate </th>
   <th style="text-align:right;"> Std. Error </th>
   <th style="text-align:right;"> Z value </th>
   <th style="text-align:right;"> P-value </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> (Intercept) </td>
   <td style="text-align:right;"> 2.6891370 </td>
   <td style="text-align:right;"> 0.9954641 </td>
   <td style="text-align:right;"> 2.7013903 </td>
   <td style="text-align:right;"> 0.0069050 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age30-29 </td>
   <td style="text-align:right;"> -0.4079804 </td>
   <td style="text-align:right;"> 0.2368396 </td>
   <td style="text-align:right;"> -1.7226021 </td>
   <td style="text-align:right;"> 0.0849605 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age40-49 </td>
   <td style="text-align:right;"> -0.1196543 </td>
   <td style="text-align:right;"> 0.2438731 </td>
   <td style="text-align:right;"> -0.4906417 </td>
   <td style="text-align:right;"> 0.6236799 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age50-64 </td>
   <td style="text-align:right;"> -0.2749506 </td>
   <td style="text-align:right;"> 0.2287476 </td>
   <td style="text-align:right;"> -1.2019823 </td>
   <td style="text-align:right;"> 0.2293704 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age65-74 </td>
   <td style="text-align:right;"> -0.4033849 </td>
   <td style="text-align:right;"> 0.2718640 </td>
   <td style="text-align:right;"> -1.4837748 </td>
   <td style="text-align:right;"> 0.1378687 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age75+ </td>
   <td style="text-align:right;"> -0.1753498 </td>
   <td style="text-align:right;"> 0.3229942 </td>
   <td style="text-align:right;"> -0.5428882 </td>
   <td style="text-align:right;"> 0.5872068 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ageBelow 18 </td>
   <td style="text-align:right;"> 0.1135214 </td>
   <td style="text-align:right;"> 0.4158388 </td>
   <td style="text-align:right;"> 0.2729938 </td>
   <td style="text-align:right;"> 0.7848580 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> gender1 </td>
   <td style="text-align:right;"> 1.0893423 </td>
   <td style="text-align:right;"> 0.5834292 </td>
   <td style="text-align:right;"> 1.8671371 </td>
   <td style="text-align:right;"> 0.0618824 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> gender2 </td>
   <td style="text-align:right;"> 0.5614865 </td>
   <td style="text-align:right;"> 0.5831921 </td>
   <td style="text-align:right;"> 0.9627813 </td>
   <td style="text-align:right;"> 0.3356573 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> gender3 </td>
   <td style="text-align:right;"> -13.5126030 </td>
   <td style="text-align:right;"> 421.9008870 </td>
   <td style="text-align:right;"> -0.0320279 </td>
   <td style="text-align:right;"> 0.9744498 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> race2 </td>
   <td style="text-align:right;"> -4.8489919 </td>
   <td style="text-align:right;"> 0.4775212 </td>
   <td style="text-align:right;"> -10.1545068 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> race3 </td>
   <td style="text-align:right;"> -1.6048023 </td>
   <td style="text-align:right;"> 0.2078021 </td>
   <td style="text-align:right;"> -7.7227435 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> race4 </td>
   <td style="text-align:right;"> -1.0132994 </td>
   <td style="text-align:right;"> 0.2205616 </td>
   <td style="text-align:right;"> -4.5941794 </td>
   <td style="text-align:right;"> 0.0000043 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> race9 </td>
   <td style="text-align:right;"> -0.9279312 </td>
   <td style="text-align:right;"> 0.8325286 </td>
   <td style="text-align:right;"> -1.1145938 </td>
   <td style="text-align:right;"> 0.2650245 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> education1 </td>
   <td style="text-align:right;"> -1.2882956 </td>
   <td style="text-align:right;"> 0.9608317 </td>
   <td style="text-align:right;"> -1.3408130 </td>
   <td style="text-align:right;"> 0.1799812 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> education2 </td>
   <td style="text-align:right;"> -0.1582565 </td>
   <td style="text-align:right;"> 0.6678715 </td>
   <td style="text-align:right;"> -0.2369565 </td>
   <td style="text-align:right;"> 0.8126906 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> education3 </td>
   <td style="text-align:right;"> -0.0177212 </td>
   <td style="text-align:right;"> 0.6638642 </td>
   <td style="text-align:right;"> -0.0266940 </td>
   <td style="text-align:right;"> 0.9787038 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> education4 </td>
   <td style="text-align:right;"> -0.9217600 </td>
   <td style="text-align:right;"> 0.6628356 </td>
   <td style="text-align:right;"> -1.3906315 </td>
   <td style="text-align:right;"> 0.1643372 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income1 </td>
   <td style="text-align:right;"> -0.1009842 </td>
   <td style="text-align:right;"> 0.4245429 </td>
   <td style="text-align:right;"> -0.2378656 </td>
   <td style="text-align:right;"> 0.8119853 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income2 </td>
   <td style="text-align:right;"> -0.5612972 </td>
   <td style="text-align:right;"> 0.4246575 </td>
   <td style="text-align:right;"> -1.3217644 </td>
   <td style="text-align:right;"> 0.1862466 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income3 </td>
   <td style="text-align:right;"> -0.3959097 </td>
   <td style="text-align:right;"> 0.4075005 </td>
   <td style="text-align:right;"> -0.9715564 </td>
   <td style="text-align:right;"> 0.3312713 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income4 </td>
   <td style="text-align:right;"> -0.4037631 </td>
   <td style="text-align:right;"> 0.4057865 </td>
   <td style="text-align:right;"> -0.9950137 </td>
   <td style="text-align:right;"> 0.3197296 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income5 </td>
   <td style="text-align:right;"> -0.3135130 </td>
   <td style="text-align:right;"> 0.4815836 </td>
   <td style="text-align:right;"> -0.6510042 </td>
   <td style="text-align:right;"> 0.5150438 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> religion2 </td>
   <td style="text-align:right;"> -0.4560362 </td>
   <td style="text-align:right;"> 0.1346004 </td>
   <td style="text-align:right;"> -3.3880747 </td>
   <td style="text-align:right;"> 0.0007039 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> religion3 </td>
   <td style="text-align:right;"> -1.4741723 </td>
   <td style="text-align:right;"> 0.3904436 </td>
   <td style="text-align:right;"> -3.7756343 </td>
   <td style="text-align:right;"> 0.0001596 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> religion4 </td>
   <td style="text-align:right;"> -0.9018918 </td>
   <td style="text-align:right;"> 0.1456971 </td>
   <td style="text-align:right;"> -6.1901828 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_church2 </td>
   <td style="text-align:right;"> -0.8422143 </td>
   <td style="text-align:right;"> 0.1940227 </td>
   <td style="text-align:right;"> -4.3408032 </td>
   <td style="text-align:right;"> 0.0000142 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_church3 </td>
   <td style="text-align:right;"> -0.8324106 </td>
   <td style="text-align:right;"> 0.2050656 </td>
   <td style="text-align:right;"> -4.0592405 </td>
   <td style="text-align:right;"> 0.0000492 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_church4 </td>
   <td style="text-align:right;"> -1.1614787 </td>
   <td style="text-align:right;"> 0.1862265 </td>
   <td style="text-align:right;"> -6.2369154 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_church5 </td>
   <td style="text-align:right;"> -1.2976510 </td>
   <td style="text-align:right;"> 0.1660395 </td>
   <td style="text-align:right;"> -7.8153131 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_church8 </td>
   <td style="text-align:right;"> -15.3043407 </td>
   <td style="text-align:right;"> 882.7434567 </td>
   <td style="text-align:right;"> -0.0173372 </td>
   <td style="text-align:right;"> 0.9861676 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_church9 </td>
   <td style="text-align:right;"> -0.6938713 </td>
   <td style="text-align:right;"> 1.0450614 </td>
   <td style="text-align:right;"> -0.6639526 </td>
   <td style="text-align:right;"> 0.5067206 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> southern2 </td>
   <td style="text-align:right;"> -0.7372077 </td>
   <td style="text-align:right;"> 0.1210659 </td>
   <td style="text-align:right;"> -6.0893082 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_status2 </td>
   <td style="text-align:right;"> -0.1652648 </td>
   <td style="text-align:right;"> 0.2185222 </td>
   <td style="text-align:right;"> -0.7562840 </td>
   <td style="text-align:right;"> 0.4494790 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_status3 </td>
   <td style="text-align:right;"> -0.2301118 </td>
   <td style="text-align:right;"> 0.1802634 </td>
   <td style="text-align:right;"> -1.2765310 </td>
   <td style="text-align:right;"> 0.2017679 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_status4 </td>
   <td style="text-align:right;"> 0.8353494 </td>
   <td style="text-align:right;"> 0.2840779 </td>
   <td style="text-align:right;"> 2.9405646 </td>
   <td style="text-align:right;"> 0.0032761 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_status5 </td>
   <td style="text-align:right;"> -0.9420816 </td>
   <td style="text-align:right;"> 0.4381695 </td>
   <td style="text-align:right;"> -2.1500392 </td>
   <td style="text-align:right;"> 0.0315521 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_status9 </td>
   <td style="text-align:right;"> -0.6932322 </td>
   <td style="text-align:right;"> 1.2958353 </td>
   <td style="text-align:right;"> -0.5349694 </td>
   <td style="text-align:right;"> 0.5926710 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> homeowner2 </td>
   <td style="text-align:right;"> -0.2719238 </td>
   <td style="text-align:right;"> 0.1343368 </td>
   <td style="text-align:right;"> -2.0241940 </td>
   <td style="text-align:right;"> 0.0429502 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> homeowner8 </td>
   <td style="text-align:right;"> -12.7693069 </td>
   <td style="text-align:right;"> 882.7438283 </td>
   <td style="text-align:right;"> -0.0144655 </td>
   <td style="text-align:right;"> 0.9884586 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> homeowner9 </td>
   <td style="text-align:right;"> 0.6235183 </td>
   <td style="text-align:right;"> 0.8698008 </td>
   <td style="text-align:right;"> 0.7168519 </td>
   <td style="text-align:right;"> 0.4734655 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> married2 </td>
   <td style="text-align:right;"> -0.4623326 </td>
   <td style="text-align:right;"> 0.1825694 </td>
   <td style="text-align:right;"> -2.5323660 </td>
   <td style="text-align:right;"> 0.0113296 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> married3 </td>
   <td style="text-align:right;"> 0.0923388 </td>
   <td style="text-align:right;"> 0.1702063 </td>
   <td style="text-align:right;"> 0.5425109 </td>
   <td style="text-align:right;"> 0.5874666 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> married4 </td>
   <td style="text-align:right;"> 0.4498600 </td>
   <td style="text-align:right;"> 0.4822434 </td>
   <td style="text-align:right;"> 0.9328485 </td>
   <td style="text-align:right;"> 0.3508982 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> married5 </td>
   <td style="text-align:right;"> -0.2179678 </td>
   <td style="text-align:right;"> 0.2388866 </td>
   <td style="text-align:right;"> -0.9124322 </td>
   <td style="text-align:right;"> 0.3615412 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> married7 </td>
   <td style="text-align:right;"> -0.2584872 </td>
   <td style="text-align:right;"> 0.2252863 </td>
   <td style="text-align:right;"> -1.1473719 </td>
   <td style="text-align:right;"> 0.2512279 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> married9 </td>
   <td style="text-align:right;"> 0.4993386 </td>
   <td style="text-align:right;"> 0.8570243 </td>
   <td style="text-align:right;"> 0.5826423 </td>
   <td style="text-align:right;"> 0.5601341 </td>
  </tr>
</tbody>
</table>

In the logistic regression model, several demographic predictors show statistically significant relationships with vote choice. For instance, Black non-Hispanic voters are 99.22% less likely to vote Republican than White non-Hispanic voters, while Jewish are 77.1% less likely to vote Republican than Protestants, holding other variables constant. Interestingly, variables like age, gender, education level, and income do not have any meaningful impact on vote choice in this model.

The overall accuracy of the logistic model for in-sample predictions is 73.66%, while its out-of-sample accuracy is 71.59%, showing moderate accuracy.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The random forest model is consistent with the logistic regression model in showing that race and church attendance are important predictors for an individual's vote choice. However, the model rated age and income as fairly important, which differs from the results of the logistic regression model.

For the random forest model, the in-sample accuracy is 68.82% whereas the out-of-sample accuracy stood at 69.29%—both slightly lower than the logistic regression model, suggesting that the random forest method may have a poorer predictive performance when considering complex interactions between demographic factors with low model interpretability.

### Narrowing down states of interest using expert predictions

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

As seen in the map above containing expert predictions by [Sabato's Crystal Ball](https://centerforpolitics.org/crystalball/), most states are already categorized as likely or safe for one party. For simplicity, I'll assume that all electoral votes from these states will go to their predicted party. Although Maine and Nebraska have a different system (allocating electoral votes by congressional district), I will assume their overall votes cancel each other out, as Maine leans Democratic and Nebraska is solidly Republican.

Therefore, I will **focus my state-level demographic analysis on the seven battleground states**: Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin.

#### Using Pennsylvania as an example

The following plots display the demographic distribution in the state of Pennsylvania as an example.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

#### Comparison of demographic data in all battleground states

The following plots compares the demographic distribution in all seven battleground states: Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-2.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-3.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-4.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-5.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-6.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-7.png" width="672" />

In my next blog, I will use the random forest model above, due to its higher accuracy, to predict the winning party in each of the seven states based on state-level demographic data. Some data wrangling has to be done in order to ensure the data from voter files are compatible with the ANES data, which was used to train the random forest model. I will then translate these predictions into electoral college seats gained by each party and combine them with seats from safe and likely states, as projected by Sabato’s Crystal Ball.

