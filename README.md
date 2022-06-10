# Statistical Models

- [Regression Models](#regression-models)
- [Time Series](#time-series)
- [Experimental Design](#experimental-design)
- [Survey Statistics](#survey-statistics)
- [Generalized Regression Models](#)
- [Mixed Models](#)
- [Computational and Graphical Methods](#) 
- [Methods in Simulation and Computation](#)
- [Nonparametric Methods](#)
- [Multivariate Analysis](#)
- [Bayesian Statistics](#)
- [Statistical Learning and Data Mining](#)

I will discuss topics listed above according to my understanding. If you have any questions, feel free to leave a comment. I would like learn about your ideas. :smiley:

## Regression Models

Probabilities and mathematical statistics are the foundation of Statistics, clearly. Stand behind these two basical courses are regression analysis. The importance of a good understanding of these two courses can never be overestimated, not only for statistics but machine learning. 

### Overview

So, what is the start point of it? Or in orther words, what issues does regression analysis intend to solve?

A short answer is **the relationship between covariates (X) and response(Y)**. 

In terms of classical statistics, regression means relationship, seriously. You can check a sad <a href="http://blog.minitab.com/blog/statistics-and-quality-data-analysis/so-why-is-it-called-regression-anyway">story</a> behind the naming of regression.

I guess this is one of the cores of all studies -- the **relationship**. For statistics, we intend to analyze the relationship reflected by data. Furthermore, I would like to give you a big picture of how it is organized.

|         |           |Covariates|||
|---------|-----------|---|---|---|
| | |Continuous | Catigorical | Mixed |
|Response |Continuous |Normal Regression | ANOVA | Multiple Linear Regression|
|Response |Catigorical|Logistic Regression; Generalized Linear Model | Contigency Table | Generalized Linear Regression|

In the perspective of machine learning (statistcal learning, data mining), all above are **supervised learning**, for given response and predictors. In addition, similar problems have different names between classical statistics and machine learning: **regression and classification**. There are more efficient tools in statistical learning, in terms of ablity of prediction. However, they may lose the convenience of interpretation. 

As mentioned above, there is a **trade-off** between **predictability and interpretability**. This is one of the big difference between the original intention fo classical statistics and machine learing. The former one is created to explain the relationships, while the latter one is designed for prediction. 

### Linear Regression Models

Come back to regression models, leaving aside models like **Analysis of Variance (ANOVA) and contigency table of counts**, what is the insight of the **linear regression models**? As we known, there are plenty of linear regression models - simple linear regression, multiple regression, logistic regression, Poisson regression, you name it. But what are they in common, or can we put all of them in a nutshell?

Yes, we can. 

That's the idea fo **General Linear Regression (GLR): the mean (or transformed mean) of a random variable follows a linear model**. This sentence includes the three components of a GLR: 

|Link Function |Random Component |Systematic Component |
|---|---|---|
|mean (or transformed mean)|a random variable|a linear model|

The source of this idea comes from the **distributions** of response. As mentioned, probabilities and mathematical statistics are the foundation of Statistics. 

|Distribution |Random Component | Link Function | Systematic Component |
|---|---|---|---|
|Normal      | y ~ Normal      | $link(u) = u$        | BX |
|Binomial    | y ~ Binomial    | $link(u) = logit(u)$ | BX |
|Multinomial | y ~ Multinomial | $link(u) = logit(u)$ | BX |
|Poisson     | y ~ Poisson     | $link(u) = log(u)$   | BX |

<a href="https://en.wikipedia.org/wiki/Generalized_linear_model#Link_function">Wikipedia</a> provides more link functions of different distributions.

The above is the big picture of generalized lieanr regression models. I did not go into details in them, but it does not mean no details there. Actually, there are much more, including model checking (can we simplify our model? or is our mdoel fit adequatly?), model diagnostics (outliers, systematic structure, or overdispersion), and one model in different scenario being different. We restric our discussion to a big picture of regression model, and wont cover these staff here.

### Other Regressiom Models

**Analysis of variance (ANOVA)** is a collection of statistical models used to analyze the **differences among group means and their associated procedures** (<a href="https://en.wikipedia.org/wiki/Analysis_of_variance">Wikipedia</a>). This part is frequently used in **experimental design**, for whom covariates are usually categorical (factor with levels). 

A **contingency table** is a type of table in a matrix format that displays the (multivariate) **frequency distribution** of the variables. People usually use it to test **homogenity and independence**. A classical example is <a href="https://en.wikipedia.org/wiki/Lady_tasting_tea">Lady Tasting Tea</a>. We use <a href="https://en.wikipedia.org/wiki/Fisher%27s_exact_test">Fisher's Exact Test</a> to analyze its independence.

||Lady: Milk First |Lady: Tea First|
|---|---|---|
|Truth: Milk First| 3 | 1 |
|Truth: Tea Firts | 1 | 3 |

The analysis of contingency tables depends on the probability distribution of count data, which, however, depends on the study design. We provide several types of study, but will not go into details. 

Suppose X's are covariates and Y is response. 

|Control on? |Study Name |Study Type |Data Avaliable? |Probability Distribution |
|---|---|---|---|---|
|None or n |Cross-Sectional |Observational |Cross-Sectional |Poisson; Multinomial |
|X total |Cohort Study if X is self-selected |Observational |Prospective |Indep. Multinomial across rows |
|X total |Clinical Study if X is randomly assigned |Experimental |Prospective |Indep. Multinomial across rows |
|Y total |Case Control |Observational |Retrospective |Non-indep. Multinomial across columns |
|All fixed |Case Control |Observational |Retrospective |Hypergeometric |

Some common tools used to test independence are Chi-Square Test, Pearson's Chi-Square test, and Likelihood Ratio Test. In addition, we can develop the two-way contingency tables to three-way one, but will not discuss it here. 

May 29, 2016

June 3, 2016 Revised

Fort Collins

--- 

## Time Series

The definition of time series is clear and intuitive, but less insight: a sequence of measurements of the same variable collected over time. Yes, we know a time series is a sequence of measurements indexed by discrete time, but can you use some statistical language tell us what does it concern about? As we underlined before, probabilities and mathematical statistics locate at important position of the whole statistics. We could and should think in a statistical way. 

### Overview

The core of analysis of time series is **dependence**. Being indexed by time is just a superficial attribute of time series, the very underlying feature of it is the dependence of that series. Instead of analyze the relationship of covariates and response, we care more about the behavior of one vairable over time. This is a take-home message of this article. 

### Autoregressive Models

Before I go into detials of specific time series models, please follow me to do a thinking exercise. I have explained that the difference between time series and regression models we discussed in last section is denpendence. So, my question is that where can the dependence come from? 

It is no difficult to find one possibility -- the dependence comes from a previous measurement or p previous measurements of that variable. Yes, you have already get started your journey of time series. This case is a very common one in nature and ecomonic, like quake data and Google stock data. We call them **Autoregressive Models (AR)**. In general, we express this dependence as following equation:

$$ x_t = \phi x_{t-1} + w_t $$

where $\{w_t\}$ are **uncorrelated** random variables with **mean 0 and finite variance**, and called **white noise**. If white noises are independent, they are called iid noise, which are not required here. More details about independence and uncorrelated will be discussed later. 

According to different values of $\phi$, the autoregressive models (AR) have specific names.

|$\phi$|AM Type |
|---|---|
|$\phi = 0$| White Noise|
|$\|\phi\| < 1$| Stationary AM|
|$\phi = 1$| Random Walk|
|$\phi > 1$| Explosion|

### Moving Average Models

Let's continue our thinking exercise. What if the latter measurement is uncorrelated to the former one? Where can the dependence come from? 

Inspired by the AR models, it is reasonable to guess that another possibility comes from a linear combination of q previous white noises. We call this kind of models as **Moving Average (MA)** models. Based on similar idea of classificatin as AR models, moving average (MA) can be grouped into several types. 

|Weights of q previous white noises |MA Type |
|---|---|
|Equally weighted|Simple Moving Average|
|Further data gets the less weight|Weighted Moving Average|
|Further data gets the less weight exponentially| Exponential Moving Average|

So far we have discussed two bisic time series models: AR and MA. It is naturaly to consider combining these two models as one, then we get ARMA models. We usually write an ARMA model as $ARMA(p, q)$, where p indicates p previous measurements and q stands for q previouse white noises. 

### ARIMA and SARIMA

Sometimes you will encounter with $ARIMA(p, d, q)$ or more complicated $SARIMA(p, d, q, P, D, Q)$. I indicates differencing d times, for a stationary model. S stands for seanonal model, just a bigger version of the original one. I would like to treat differencing as a kind of data preprocessing. Besides, seasonal models can be discovered in the stage of Exploratory Data Analysis (EDA), and be fulfilled by common software like R. More details will not be covered here.

### Autoregressive Conditional Heteroskedastic Models

We have find two source of dependence of time series, what else? The requirement of uncorrelated but not independent white noises foreshadows the third possibility of dependence. When variance of measurements are constant, but conditional variance are heteroskedastic, we refer it as Autoregressive Conditional Heteroskedastic Models (ARCH). More detials can be found in <a href="https://en.wikipedia.org/wiki/Autoregressive_conditional_heteroskedasticity">Wikipedia</a>.

May 30, 2016

Fort Collins

---

## Experimental Design

If we regard time series analysis as an observational study, we now will take a look at another type of study -- experiments. The difference between these two kinds of studies is pretty straightforward: people can control variables in an experiment, while only nature conditions can be used in an observational study. As a result, cause-and-effect relationship may be found through experiments, while you can only find association relationship by observational studies (**Principle of Experimantal Manipulation**). 

### Questions should be considered before designing

All experiments have thier objectives, which direct researchers hwo to design and analyze. According to objectives of designs, most common ones are **comparative design**, and **screening design**. More details can be found <a href="http://www.itl.nist.gov/div898/handbook/pri/section3/pri31.htm">here</a>. When you have an objective, to design an effective and efficient experiment, we should be clear of the following questions:

- 1. What population you intend to make inference to? 

**Fundamental Principle of Statistical Inference** concludes that you can only make inference to the population from which you sample.

- 2. How do you compare experiments in comparative design?

**Principle of Comparative Experimention** says that differences between responses to treatments will be less affected by uncontrolled influences than individual responses to treatments. As as consquence, you need a control treatment in you experiment.

- 3. How do you analyze effects of different factors in a screening design?

Screening designs are to identify which factors/effects are important. Comparing different treatments of different levels of on factor is conducted in a comparative design. While, factorization focuses on more than one factor and analyzes thier effects to the response variable. **Factorial Principle** indicates that efficiency can be gained by using factorial treatment structures. 

- 4. When you get multiple factors in a study, you need to consider how these factors are structured? 

You need to know whether the factors are crossed or nested. More details check <a href="http://support.minitab.com/en-us/minitab/17/topic-library/modeling-statistics/anova/anova-models/what-are-crossed-and-nested-factors/">here</a>. Besides, when time or period is considered in the model, you may think about repeated measures design, which is associated to **time series analysis**. If we take time series analysis as a study for dependence in one dimension, **spatial analysis** can be regarded as a dependence analysis in a two-dimension level. 

- 5. How do you avoid bias?

One well-known way is to randomize treatments to experimental units. This is **Principle of Randomization**. Randomization makes the estimate of treatment effect unbiased. 

Randomization makes sure that variability in different treatments are almost same (consider unbiasedness). More efficiently, we can control variability by blocking. To some degree, we can treat block as a factor in a screening design; the difference is the block factor is of no interest in our experimental studies. When block factors are considered in our model, comparison of treatment means will be more accurate. This is the **Principle of Blocking**.

### A quick reference of experimental designs

Only if you have clear answers to above questions, you could go forward to designing your experiments. A quick reference is shown as following:

|Factors |Blocks |Design |Notes|
|---|---|---|---|
|One |No |**Completely Randomized Design (CRD)** | |
|One |One |**Randomized Complete Block Design (RCBD)** |Mixed Model: RCBD with random blocks |
|One |Two |Latin Square Design (LSD) |# trts = # rows = # columns |
|One |One |Balanced Imcomplete Block Design (BIBD) |natural block size < number of treatments |
|More than one |No |**Balanced Factorial Design (BFD)** |Factor structures should be considered|
|Two |One |**Split-Plot Design** |An experiment within an experiment|
|Two |One |Split-Block Design |The two factors are interchangeable|
|Three |One |Split-Split-Plot Design |An experiment within an experiment, within an experiment|
|Two |One |**Repeated Measures Design** |whole plot factor = between subject factor; subplot factor = within subject factor|
| | |Random Coefficients Models |Linear regression models |
|Two |No |Spatial Correlation Models |Out of scope of this article |

I did not seperate fixed models and mixed models in this reference, because they are not independent to each other. The difference lies in ways hwo you analyze them, which will be explained below, and researchers' interests. For example, when a factor is fixed, you are probabaly interested in every specific levels of that factor; while a factor is random, you may be more interested in whether or not include that factor in the model than the levels or values of the factor.


### Analysis your models

- 1. Fixed Models:

We can compare two groups' means with a T-test, we can test whether several groups have the same means through an Analyis of Variance (ANOVA). Furthermore, we may want to do multiple comparisos. As I only intend to provide you a intuitive idea of experimental design, I will not go into more detials about it, but you can check it on <a href="https://en.wikipedia.org/wiki/Multiple_comparisons_problem">Wikipedia</a>.

- 2. Mixed Models:

In fixed models, we are interested in group means; while in mixed models, we care more about variance. Thus, the analysis of mixed models is around the estimation of variance. Based on the same reason as above, we will not cover this part in this article. 

June 2, 2016

Fort Collins

---

## Survey Statistics

A quick review:

- (1) **Experimental Studies:** deliberately perturb part of population and study the effect. 

- (2) **Purely Observational Studies:** observe part of population, but no control over which part. 

The topic of today is kind of different from the previous two studies -- **Surveys**. (1) In surveys, avoid disturbing the population or sampled part of population. (2) In surveys, carefully control which part of the population you will study to ensure that the part is representative of the whole.  

From where I stand, the best and fast way to learn survey statistics is to understand each argument in the function `svydesign` of a `R` package <a href="http://r-survey.r-forge.r-project.org/survey/html/svydesign.html">survey</a>. When it comes to survey statistics, **a complex survey design** is a common topic. However, what does `complex` really mean? We can find some inclues in the fuction `svydesgin`.

```
svydesing(ids = ~ cluster, strata = ~ strata, weights = ~ weights, data = data)

ids	Formula or data frame specifying cluster ids from largest level to smallest level, ~0 or ~1 is a formula for no clusters.

strata	Formula or vector specifying strata, use NULL for no strata

weights	Formula or vector specifying sampling weights as an alternative to prob
```
