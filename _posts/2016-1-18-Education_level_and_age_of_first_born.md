---
title: Education level and age when first child is born
layout: article
comments: true
abstract: Project report as part of the Coursera course Data Analysis and Statistical Inference.
image:
  teaser: education_figures/unnamed-chunk-3-1.png
  #feature: featured/cropped-Ocean-Sunrise-1024x256.jpg
---

2 November 2015  

<!-- For more info on RMarkdown see http://rmarkdown.rstudio.com/ -->

<!-- Enter the code required to load your data in the space below. The data will be loaded but the line of code won't show up in your write up (echo=FALSE) in order to save space-->

<!-- In the remainder of the document, add R code chunks as needed -->

## Introduction:

In this project report the aim is to investigate the following research question:

**Is there a relationship between the highest education degree and age when first child is born for US residents?** 

It is a common belief that people who complete higher education get children when they're older than people who "only" complete High School. But, is it in fact so? It might be a belief that is primarily due to people's own experience or perhaps even prejudice. In this project report we will use data from the US General Social Survey (GSS)  to investigate whether there actually exists a significant difference or if it is just a common misconception.

## Data:

The data used is from GSS data set. The data in the GSS is collected via in-person interviews with respondents of approximately 90 minutes [[1]](http://thearda.com/archive/files/descriptions/gss12pan.asp). The dataset used in this study is the Coursera abstract of the GSS, available [here](http://bit.ly/dasi_anes_data), which consists of survey data from 1972 until 2012. It has 50761 rows, which correspond to  respondents (i.e. the cases), and 114 columns, which correspond to the answers given by the respondents to the survey questions.

The variables used in this study are called 'degree' (categorical variable, 5 levels) and 'agekdbrn' (numerical variable). In addition to these two variables, the variable 'childs' (numerical variable) to determine if NA's in agekdbrn might be due to having 0 children (to include the category 0 children might create a broader and more interesting scope than just age of those who have children). Only data from 2012 will be used in this study.

The population of interest is the overall US population. The GSS is designed to be able to answer questions for the US population based on the samples, whether it is for comparing trends over time or intrayear comparisons. There might be biases related to, e.g.: participation in the survey (being volunteer, having access to telephone etc.), geography (are the responders well distributed throughout the US?), sociology (are people from all social backgrounds and classes included in proportions similar to the US population?). Hopefully the GSS is created by professional statisticians that deliberately aim to reduce the chance for such biases occuring, so that the results from this study will have little bias.

This is an observational study, as the data is collected without interfering with how the data has arised, the data is retrospective, and there is no randomly assigning of subjects to treatments. 

Since this is will be an observational study, it is in itself limited to establishing association between variables and not causality. If a significant relationship between degree and age of first child is found, one could start speculating on causal relationship, but it should be clearly stated that it is speculation (unless potential further studies are conducted). For instance, one might argue that "being able to combine higher studies and providing for a child is difficult", but not determine whether it was because someone got a child at a young age that they didn't complete higher education or, the other way around, didn't get a child because he/she were taking higher education.

## Exploratory data analysis:

First, we want to subset the variables of interest and for the appropriate year. We then take a look at it with `head`, and discover that `agkdbrn` contain NA's - the data needs some cleaning before it can be used for analysis. To investigate what that might be we check if the number of NA's in `agkdbrn` corresponds to the number of respondents in `childs` that say they have no children (`childs`=0). We find that the number is almost similar (544 vs. 536), which justifies removing all NA's  from the data that will be used in the study.


~~~ r
df <- subset(gss, year == 2012, select = c(degree, agekdbrn, childs)) # Create subset o
head(df)
~~~

~~~
##            degree agekdbrn childs
## 55088    Bachelor       NA      0
## 55089 High School       NA      0
## 55090 High School       32      2
## 55091 High School       24      2
## 55092    Bachelor       24      3
## 55093    Bachelor       25      2
~~~

~~~ r
sum(is.na(df$agekdbrn))
~~~

~~~
## [1] 544
~~~

~~~ r
table(df$childs)
~~~

~~~
## 
##   0   1   2   3   4   5   6   7   8 
## 536 274 569 301 167  56  33  12  23
~~~

~~~ r
df_tidy <- na.omit(df[ , c('degree', 'agekdbrn')])
str(df_tidy)
~~~

~~~
## 'data.frame':	1423 obs. of  2 variables:
##  $ degree  : Factor w/ 5 levels "Lt High School",..: 2 2 4 4 3 1 1 1 4 2 ...
##  $ agekdbrn: int  32 24 24 25 23 17 18 22 26 20 ...
##  - attr(*, "na.action")=Class 'omit'  Named int [1:551] 1 2 10 20 27 31 33 35 37 38 ...
##   .. ..- attr(*, "names")= chr [1:551] "55088" "55089" "55097" "55107" ...
~~~

The tidy data frame has 1423 cases of the variables `degree` and `agekdbrn`. Now we would like to calculate some summary statistics for it:


~~~r
library(dplyr); library(knitr)
by_degree <- group_by(df_tidy, degree)
stats <- data.frame(summarize(by_degree, mean(agekdbrn), median(agekdbrn), sd(agekdbrn), length(agekdbrn)))
stats$degree <- NULL # Removing degree column
stats <- t(stats)
colnames(stats) = levels(by_degree$degree); rownames(stats) = c('Mean', 'Median', 'SD', 'Sample size')
kable(stats, digits = 2)
~~~
|             | Lt High School | High School | Junior College | Bachelor | Graduate |
|-------------|----------------|-------------|----------------|----------|----------|
| Mean        | 21.10          | 23.22       | 24.43          | 27.07    | 28.74    |
| Median      | 20.00          | 22.00       | 23.50          | 27.00    | 29.00    |
| SD          | 4.74           | 5.22        | 5.31           | 4.89     | 5.48     |
| Sample size | 242.00         | 709.00      | 110.00         | 226.00   | 136.00   |

From the table it seems like there is a clear trend of increasing mean age for first child born with highest educational degree completed. A boxplot of the data also indicate this:

~~~r
library(ggplot2)
~~~

~~~
## Warning: package 'ggplot2' was built under R version 3.2.3
~~~

~~~r
p <- ggplot(df_tidy, aes(degree, agekdbrn))
p + geom_boxplot((aes(fill = degree))) + labs(x="Respondent's highest completed degree", y="Respondent's age when 1st child born")
~~~

![](/images/education_figures/unnamed-chunk-3-1.png) 

From the table and the boxplot it seems like there is a quite strong correlation between age when first child is born and highest educational degree completed. But, we need to perform some statistical analysis of the data before we be conclude that this is the case.

## Inference:

Considering the variables we have in this study - a categorical with 5 levels and one numerical - it seems that analysis of variation (ANOVA) and, potentially, pairwise tests are the most appropriate statistical techniques to use.

In order to use ANOVA we need to check that the following criteria are met:

1. Independence
    a. within groups: Assumed to be met by the survey design of the GSS. The survey is designed to be "big enough" that one can for data for each year perform inference. The survey should be made up of random samples of the population, both within across each educational group, and number of respondents make up less than 10% of the US population.
    b. between groups: Assumed to be met by the survey design of the GSS (reasoning as above).
2. Equal variance: Each group should have approximately equal variance. Considering the standard deviation calculated in the table of summary statistics above, and the shape of the boxplots, we can assume that the variance is equal "enough" to pass this criteria.
3. Approximately normal: The distributions within in each group should be nearly normal. This is probably the toughest criterion to meet, as explained more in detail below.

To easiest way to check for normality is probably to draw the histograms of the distributions (within each group) and their corresponding normal probability plots:


![](/images/education_figures/normality_figs-1.png) ![](/images/education_figures/normality_figs-2.png) 

From the plots it seems like there is a trend towards normality from left to right (Lt High School to Graduate). To my judgment, all distributions look sufficently normal when considering the large (>100) sample sizes except for Lt High School, which is quite heavily right skewed and the normality plot is not very straight. On the other side, the sample size is pretty large (242), which can make up for some of the skewness. I am not completely certain that this group actually meets the normality criteria, but for the sake of this study we assume it does and can hence continue with the analysis of variation.

It should be noted that there are some outliers in the High School group, but they don't seem to "distort" the distribution, or affect summary statistics, significantly. 

We continue with the analysis of variation, where the following hypthesis test is used:

\\[H_0: \mu_{LHS}=\mu_{HS}=\mu_{JC}=\mu_{Bachelor}=\mu_{Graduate}\\]

\\(H_a:\\) At least one pair of means are different from each other 

(For mathjax notation in Jekyll, see: http://www.christopherpoole.net/using-mathjax-on-githubpages.html)

~~~r
fit <- aov(agekdbrn ~ degree, data=df_tidy)
summary(fit)
~~~

~~~
##               Df Sum Sq Mean Sq F value Pr(>F)    
## degree         4   7656  1914.1   73.01 <2e-16 ***
## Residuals   1418  37175    26.2                   
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
~~~

We can see that the resulting p-value from the F distribution is close to zero (<2e-16), which indicates that there is very likely a relationship between age when first child is born and highest educational degree.

We can furthere check if there is significance between all educational levels, with two sample t-tests. We choose to investigate the following two two sample t-tests:

- Max mean vs min mean: Graduate vs. Lt High School
- Smallest difference in mean: High school vs. Junior College

We need to calculate new significance level, by using the Bonferroni correction. This is make sure that/reduce the chance for a significant finding is not due to randomne patterns in the overall data. Significance level used in the ANOVA analysis: 0.05.


~~~r
k = length(levels(df_tidy$degree))
comparison_count = k * (k - 1) / 2
sig_level_adj = 0.05 / comparison_count
gd <- df_tidy[df_tidy$degree == "Graduate", ]
lhs <- df_tidy[df_tidy$degree == "Lt High School", ]
hs <- df_tidy[df_tidy$degree == "High School", ]
jc <- df_tidy[df_tidy$degree == "Junior College", ]

sig_level_adj # New significance level
~~~

~~~
## [1] 0.005
~~~

~~~r
t.test(gd$agekdbrn, lhs$agekdbrn)
~~~

~~~
## 
## 	Welch Two Sample t-test
## 
## data:  gd$agekdbrn and lhs$agekdbrn
## t = 13.648, df = 247.7, p-value < 2.2e-16
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  6.540383 8.746564
## sample estimates:
## mean of x mean of y 
##  28.74265  21.09917
~~~

~~~r
t.test(jc$agekdbrn, hs$agekdbrn)
~~~

~~~
## 
## 	Welch Two Sample t-test
## 
## data:  jc$agekdbrn and hs$agekdbrn
## t = 2.2188, df = 143.58, p-value = 0.02807
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  0.1314746 2.2773727
## sample estimates:
## mean of x mean of y 
##  24.42727  23.22285
~~~

From the results we can see that there is a significant difference between the max and min means (p-value = <2.2e-16, which is much smaller than 0.005) and that there is *no* significant difference between High School and Junior College (p-value = 0.028, which is higher than 0.005).


## Conclusion:

The results of the ANOVA analysis suggest a strong relationship between age when first child is born and highest completed educational degree. The age seem to increase with educational degree, and significantly so. The resulting p-value is so low that even the most stringent significance criteria is met.

On the other hand, however, the multiple comparison tests performed indicate that it is not necessarily a significant difference between all levels of highest completed educational degree.

## References:

http://thearda.com/archive/files/descriptions/gss12pan.asp

Smith, Tom W., Michael Hout, and Peter V. Marsden. General Social Survey, 1972-2012 [Cumulative File]. ICPSR34802-v1. Storrs, CT: Roper Center for Public Opinion Research, University of Connecticut /Ann Arbor, MI: Inter-university Consortium for Political and Social Research [distributors], 2013-09-11. doi:10.3886/ICPSR34802.v1

The codebook below lists all variables, the values they take, and the survey questions associated with them. It is available here: https://d396qusza40orc.cloudfront.net/statistics%2Fproject%2Fgss1.html

Link to the data set: http://bit.ly/dasi_anes_data

# Appendix:


~~~r
head(df_tidy, 50)
~~~

~~~
##               degree agekdbrn
## 55090    High School       32
## 55091    High School       24
## 55092       Bachelor       24
## 55093       Bachelor       25
## 55094 Junior College       23
## 55095 Lt High School       17
## 55096 Lt High School       18
## 55098 Lt High School       22
## 55099       Bachelor       26
## 55100    High School       20
## 55101    High School       16
## 55102 Lt High School       18
## 55103    High School       25
## 55104    High School       28
## 55105    High School       21
## 55106    High School       34
## 55108 Lt High School       18
## 55109 Lt High School       25
## 55110 Junior College       23
## 55111 Junior College       28
## 55112    High School       37
## 55113       Bachelor       27
## 55115 Lt High School       33
## 55116       Bachelor       27
## 55117    High School       22
## 55119 Junior College       28
## 55121       Bachelor       34
## 55123       Graduate       33
## 55127    High School       17
## 55129    High School       27
## 55131       Bachelor       27
## 55132       Bachelor       34
## 55133       Bachelor       22
## 55134       Bachelor       22
## 55135       Graduate       35
## 55136       Bachelor       23
## 55137       Graduate       26
## 55138       Bachelor       29
## 55139       Bachelor       29
## 55140       Graduate       37
## 55141 Junior College       33
## 55142       Graduate       33
## 55143       Graduate       30
## 55144    High School       23
## 55145    High School       21
## 55146 Lt High School       18
## 55147 Lt High School       18
## 55148       Graduate       19
## 55149       Graduate       23
## 55150 Lt High School       28
~~~
