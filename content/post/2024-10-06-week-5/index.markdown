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

## Week 5: Who Votes, and How Do They Vote? An Overview of Demographics

In an increasingly polarized nation, or as Lynn Vavreck coined it, "**calcified**," demographics have become more predictive in understanding voting patterns.

### Who Votes?

Not every single citizen is registered to vote, and not every registered voter will turnout. The graph below shows the voter turnout in different states in the presidential elections from 1980 to 2020.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

Individuals with higher education levels are more likely to vote because education provides information about the democratic process and instills a sense of civic virtue ([Wolfinger & Rosenstone, 1980](http://www.jstor.org/stable/j.ctt32bffz); [Shaw & Petrocik, 2020](https://doi-org.ezp-prod1.hul.harvard.edu/10.1093/oso/9780190089450.001.0001)). Older voters, especially retirees, are also more likely to participate due to their interest in preserving government programs like Social Security (Shaw & Petrocik, 2020). [Rosenstone & Hansen (1993)](https://doi.org/10.2307/2944841) also suggest that white and wealthier demographics are more likely to engage in politics and voting generally.



### How Do They Vote?

Political scientists widely agree that **party affiliation is the most significant predictor of voting behavior**, though this piece of information is not always available due to different states' data collection policies and voters' choice to disclose themselves as independent. While demographic factors like education level, age, gender, race, and income also play a role, they are generally seen as secondary to party identification.

To **explore how well demographic factors predict voting behavior**, I built **both logistic regression and random forest models** using the American National Election Studies (ANES) dataset in 2020. My analysis focuses on core demographics like age, gender, race, education, and income to predict whether someone is likely to vote for the Democratic or Republican candidate in the U.S. presidential election. By comparing the performance of these two models, I aim to identify which method better captures the relationship between voter demographics and vote choice. The logistic regression model offers a more interpretable framework, while the random forest model capture non-linear interactions between explanatory variables to achieve greater predictive accuracy.

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
   <td style="text-align:right;"> 3.0466894 </td>
   <td style="text-align:right;"> 0.3879300 </td>
   <td style="text-align:right;"> 7.8537100 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age30-29 </td>
   <td style="text-align:right;"> 0.2605495 </td>
   <td style="text-align:right;"> 0.1932560 </td>
   <td style="text-align:right;"> 1.3482090 </td>
   <td style="text-align:right;"> 0.1775912 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age40-49 </td>
   <td style="text-align:right;"> 0.2814913 </td>
   <td style="text-align:right;"> 0.1971868 </td>
   <td style="text-align:right;"> 1.4275362 </td>
   <td style="text-align:right;"> 0.1534254 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age50-64 </td>
   <td style="text-align:right;"> 0.4790822 </td>
   <td style="text-align:right;"> 0.1804352 </td>
   <td style="text-align:right;"> 2.6551486 </td>
   <td style="text-align:right;"> 0.0079273 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age65-74 </td>
   <td style="text-align:right;"> 0.2513214 </td>
   <td style="text-align:right;"> 0.2100600 </td>
   <td style="text-align:right;"> 1.1964266 </td>
   <td style="text-align:right;"> 0.2315301 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> age75+ </td>
   <td style="text-align:right;"> 0.2873645 </td>
   <td style="text-align:right;"> 0.2503041 </td>
   <td style="text-align:right;"> 1.1480614 </td>
   <td style="text-align:right;"> 0.2509432 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ageBelow 18 </td>
   <td style="text-align:right;"> 0.4689021 </td>
   <td style="text-align:right;"> 0.3298902 </td>
   <td style="text-align:right;"> 1.4213885 </td>
   <td style="text-align:right;"> 0.1552038 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> genderFemale </td>
   <td style="text-align:right;"> -0.0232485 </td>
   <td style="text-align:right;"> 0.0968415 </td>
   <td style="text-align:right;"> -0.2400670 </td>
   <td style="text-align:right;"> 0.8102783 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> raceBlack non-Hispanic </td>
   <td style="text-align:right;"> -1.8433006 </td>
   <td style="text-align:right;"> 0.2820778 </td>
   <td style="text-align:right;"> -6.5347237 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> raceHispanic </td>
   <td style="text-align:right;"> -0.6179115 </td>
   <td style="text-align:right;"> 0.1828442 </td>
   <td style="text-align:right;"> -3.3794424 </td>
   <td style="text-align:right;"> 0.0007263 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> raceOther or multiple races, non-Hispanic </td>
   <td style="text-align:right;"> 0.0305557 </td>
   <td style="text-align:right;"> 0.1661450 </td>
   <td style="text-align:right;"> 0.1839099 </td>
   <td style="text-align:right;"> 0.8540842 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> educationHigh school </td>
   <td style="text-align:right;"> -0.0752261 </td>
   <td style="text-align:right;"> 0.3247652 </td>
   <td style="text-align:right;"> -0.2316321 </td>
   <td style="text-align:right;"> 0.8168238 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> educationSome college </td>
   <td style="text-align:right;"> -0.0811367 </td>
   <td style="text-align:right;"> 0.3121902 </td>
   <td style="text-align:right;"> -0.2598953 </td>
   <td style="text-align:right;"> 0.7949446 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> educationCollege+ </td>
   <td style="text-align:right;"> -0.8579110 </td>
   <td style="text-align:right;"> 0.3130217 </td>
   <td style="text-align:right;"> -2.7407398 </td>
   <td style="text-align:right;"> 0.0061301 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income7-33 percentile </td>
   <td style="text-align:right;"> -0.1264412 </td>
   <td style="text-align:right;"> 0.1715965 </td>
   <td style="text-align:right;"> -0.7368519 </td>
   <td style="text-align:right;"> 0.4612124 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income34-67 percentile </td>
   <td style="text-align:right;"> 0.1473429 </td>
   <td style="text-align:right;"> 0.1428070 </td>
   <td style="text-align:right;"> 1.0317624 </td>
   <td style="text-align:right;"> 0.3021834 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income68 to 95 percentile </td>
   <td style="text-align:right;"> 0.1106322 </td>
   <td style="text-align:right;"> 0.1520675 </td>
   <td style="text-align:right;"> 0.7275207 </td>
   <td style="text-align:right;"> 0.4669070 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> income96 to 100 percentile </td>
   <td style="text-align:right;"> -0.2014069 </td>
   <td style="text-align:right;"> 0.2263415 </td>
   <td style="text-align:right;"> -0.8898366 </td>
   <td style="text-align:right;"> 0.3735536 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> religionCatholic </td>
   <td style="text-align:right;"> -0.2136832 </td>
   <td style="text-align:right;"> 0.1241851 </td>
   <td style="text-align:right;"> -1.7206827 </td>
   <td style="text-align:right;"> 0.0853084 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> religionJewish </td>
   <td style="text-align:right;"> -0.4982795 </td>
   <td style="text-align:right;"> 0.3542658 </td>
   <td style="text-align:right;"> -1.4065132 </td>
   <td style="text-align:right;"> 0.1595718 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> religionOther </td>
   <td style="text-align:right;"> -0.5680956 </td>
   <td style="text-align:right;"> 0.1153176 </td>
   <td style="text-align:right;"> -4.9263556 </td>
   <td style="text-align:right;"> 0.0000008 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_churchAlmost every week - often </td>
   <td style="text-align:right;"> -0.2095727 </td>
   <td style="text-align:right;"> 0.1842234 </td>
   <td style="text-align:right;"> -1.1376013 </td>
   <td style="text-align:right;"> 0.2552870 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_churchOnce or twice a month </td>
   <td style="text-align:right;"> -0.2023907 </td>
   <td style="text-align:right;"> 0.2035687 </td>
   <td style="text-align:right;"> -0.9942130 </td>
   <td style="text-align:right;"> 0.3201192 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_churchA few times a year - seldom </td>
   <td style="text-align:right;"> -0.2808382 </td>
   <td style="text-align:right;"> 0.1827159 </td>
   <td style="text-align:right;"> -1.5370211 </td>
   <td style="text-align:right;"> 0.1242881 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> attend_churchNever </td>
   <td style="text-align:right;"> -0.7653464 </td>
   <td style="text-align:right;"> 0.1438191 </td>
   <td style="text-align:right;"> -5.3215916 </td>
   <td style="text-align:right;"> 0.0000001 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_statusNot employed </td>
   <td style="text-align:right;"> -0.1516865 </td>
   <td style="text-align:right;"> 0.1792080 </td>
   <td style="text-align:right;"> -0.8464268 </td>
   <td style="text-align:right;"> 0.3973147 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_statusRetired </td>
   <td style="text-align:right;"> 0.1027262 </td>
   <td style="text-align:right;"> 0.1553820 </td>
   <td style="text-align:right;"> 0.6611201 </td>
   <td style="text-align:right;"> 0.5085353 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_statusHomemaker </td>
   <td style="text-align:right;"> 0.1850355 </td>
   <td style="text-align:right;"> 0.2223238 </td>
   <td style="text-align:right;"> 0.8322796 </td>
   <td style="text-align:right;"> 0.4052511 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> work_statusStudent </td>
   <td style="text-align:right;"> -1.4388741 </td>
   <td style="text-align:right;"> 0.5425110 </td>
   <td style="text-align:right;"> -2.6522484 </td>
   <td style="text-align:right;"> 0.0079958 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> party_identificationIndependent </td>
   <td style="text-align:right;"> -2.4964501 </td>
   <td style="text-align:right;"> 0.1111003 </td>
   <td style="text-align:right;"> -22.4702338 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> party_identificationNo preference; none; neither </td>
   <td style="text-align:right;"> -2.3768968 </td>
   <td style="text-align:right;"> 1.4335381 </td>
   <td style="text-align:right;"> -1.6580632 </td>
   <td style="text-align:right;"> 0.0973047 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> party_identificationOther </td>
   <td style="text-align:right;"> -2.2416718 </td>
   <td style="text-align:right;"> 0.2383706 </td>
   <td style="text-align:right;"> -9.4041439 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> party_identificationDemocrat </td>
   <td style="text-align:right;"> -5.2693001 </td>
   <td style="text-align:right;"> 0.1612323 </td>
   <td style="text-align:right;"> -32.6814216 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
</tbody>
</table>

In the logistic regression model, several demographic predictors show statistically significant relationships with vote choice. For instance, **Black non-Hispanic voters** are 84.17% less likely to vote Republican than White non-Hispanic voters, holding other variables constant. Consistent with the literature, **people who think of themselves as Democrats** are 99.49% less likely to vote Republican than those who identify as Republicans. **Students** are 76.28% less likely to vote Republican, whereas **homemakers** are 20.33% more likely to vote Republican, compared to employed individuals. Those who **attend church less frequently** are significantly less likely to vote Republican compared to those who attend every week regularly. Interestingly, variables like age, gender, education level, and income do not have any meaningful impact on vote choice in this model, as their p-values are above the typical 5% significance level.

The overall accuracy of the logistic model for in-sample predictions is 85.79%, while its out-of-sample accuracy is 86.23%, showing fairly high accuracy.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

The random forest model is consistent with the logistic regression model in showing that **party identification, race,  and church attendance** are important predictors for an individual's vote choice. However, the model rated age as fairly important and work status as less important, which differs from the results of the logistic regression model.

For the random forest model, the in-sample accuracy is 84.52% whereas the out-of-sample accuracy stood at 84.77%—slightly lower than the logistic regression model, suggesting that the random forest method may have a poorer predictive performance when considering complex interactions between demographic factors with low model interpretability.

### Narrowing down states of interest using expert predictions

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

As seen in the map above containing expert predictions by [Sabato's Crystal Ball](https://centerforpolitics.org/crystalball/), most states are already categorized as likely or safe for one party. For simplicity, I'll assume that all electoral votes from these states will go to their predicted party. Although Maine and Nebraska have a different system (allocating electoral votes by congressional district), I will assume their overall votes cancel each other out, as Maine leans Democratic and Nebraska is solidly Republican.

Therefore, I will **focus my state-level demographic analysis on the seven battleground states**: Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin.

#### Using Pennsylvania as an example

The following plots display the demographic distribution in the state of Pennsylvania as an example, using its 1% voterfile data.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

#### Comparison of demographic data in all battleground states

The following plots compares the demographic distribution in all seven battleground states: Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-2.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-3.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-4.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-5.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-6.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-7.png" width="672" />

*Code developed with the assistance of ChatGPT.*
