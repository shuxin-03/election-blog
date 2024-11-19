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

My prediction error for each state is demonstrated in the graph below.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />

### National Two-Party Popular Vote Share Evaluation


```
## Bias: -7.638292
```

Despite predicting the the electoral college vote share correctly, my prediction for the national two-party popular vote share went terribly wrong as of [November 18th](https://www.cookpolitical.com/vote-tracker/2024/electoral-college), where I overestimated The Democratic Party's popular vote by 7.64 percentage points.

Therefore, I will focus on evaluating the reason for inaccuracy in my national two-party popular vote share model. I hypothesize a few reasons for my model's inaccuracy and propose corresponding changes:

**1. Polling model shortcomings**

My polling model's equation is `$$D\_pv2p = D\_NetLatest538PollAverage + D\_NetMean538PollAverage(30 weeks) + NetLatestJobApproval + NetMeanJobApproval(June-Oct)$$` for Democratic vote share, which I then repeat for Republican vote share separately, then rescaling them to a 100%.

Hypothesis: My polling model did not account for incumbency effects. Specifically, variables such as net job approval and polling averages were not adjusted for the impact of incumbency, which can influence voter perception differently for challengers versus incumbents.

Test: Re-run the polling model with the inclusion of dummy variables for `\(IncumbentParty\)` and `\(IncumbentPresident\)` and test the adjusted model's performance on past elections where the incumbent party or president faced challenges such as poor global economic conditions or ran against a strong challenger.

**2. Economic reality versus perception**

I will incorporate economic variables that more accurately measures voters' perception of the economy, as [people might still be recovering from the impact of COVID-19 economic downturn](https://www.cnn.com/2024/02/02/politics/cnn-poll-economy/index.html), so unemployment, GDP and RDPI figures may not reflect the full extent of how voters perceive the economy.

Hypothesis: My economic predictors (such as unemployment, GDP, S&P 500 volume, and real disposable personal income) failed to capture voters' subjective perceptions of the economy. For example, while unemployment rates were low, the impact of food price inflation or the lingering effects of the COVID-19 pandemic might have weighed more heavily on voters' decisions, given that [April 2022 food prices inflation rate rose up to 10.8%](https://www.bls.gov/opub/ted/2022/food-prices-up-10-8-percent-for-year-ended-april-2022-largest-12-month-increase-since-november-1980.htm#:~:text=FONT%20SIZE:%20PRINT:-,Food%20prices%20up%2010.8%20percent%20for%20year%20ended%20April%202022,month%20increase%20since%20November%201980&text=For%20the%20year%20ended%20April,percent%20increase%20in%20November%201981.), for instance.

Test: Analyze survey data on voters’ perception of economic conditions and correlate these perceptions with vote choices.

I will also expand economic variables:
- Use additional economic predictors, such as food price inflation and median wage growth, to capture the direct impact of economic stressors on voters.
- Extend the time frame for economic data to include the entire incumbent party’s term, not just the election year, as significantly poor economic conditions in 2022 and 2023 may have caused voter dissatistaction which carried on to 2024.

**3. Accounting for voter turnout**

Hypothesis: Lower turnout among traditionally Democratic voters, possibly due to dissatisfaction with the administration’s handling of difficult issues such as the [Gaza conflict](https://www.reuters.com/world/us/inside-democratic-rebellion-against-biden-over-gaza-war-2024-02-27/), reduced Harris's vote share.

Test: Compare turnout rates by demographic groups in 2024 to previous elections using voter file data and assess whether historically Democratic demographics (such as younger voters and minority ethnic groups) had a decline in turnout.

**4. Adjusting for airwar**

Hypothesis: While traditional airwar analysis focuses on campaign spending on television advertisements, modern media platforms such as podcasts, social media, and celebrity endorsements may play a significant role in shaping public opinion, especially among younger voters who are tech-savvy or older voters who have a lot of time to spend on their devices. For example, [Trump's appearance on Joe Rogan's podcast](https://www.thetimes.com/life-style/celebrity/article/donald-trump-joe-rogan-8grmztcjn), [Harris's endorsement by Taylor Swift](https://www.nbcnews.com/politics/2024-election/taylor-swift-endorses-kamala-harris-rcna170547), or interactions on platforms like FaceBook, Instagram and TikTok may influence voter sentiment in ways that are not captured by traditional ad spending metrics.

Test: Collect data on the following metrics and compare them to the candidates' vote share in specific demographic groups (such as younger voters) to evaluate their predictive power.

Metrics include:
- Audience size for each candidate's media appearances on platforms such as podcasts, late-night shows, and endorsements by public figures
- Engagement metrics such as the number of likes, shares, and comments for content related to each candidate
- Sentiment analysis of audience comments using natural language processing to assess voter sentiment


