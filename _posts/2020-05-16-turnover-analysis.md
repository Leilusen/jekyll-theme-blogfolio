---
layout: post
title: "HR data analysis: turnover"
date: 2020-05-16 05:00:00 +0200
---
![Yearly turnover rates](/assets/HR_main.jpg)

*In this blog-post I will be looking at one of the most important HR metrics in any company - employee turnover. According to The Society for Human Resource Management (SHRM) research, direct replacement costs can reach as high as 50%-60% of an employee’s annual salary.*

I used dataset prepared by New England College of Business of graduate MSHRM courses called HR Metrics and Analytics. It simulates an IT company and covers period from 2006 to 2017. Information includes data on all employees, their job statuses, pay rates, marital statuses and other data usually avaialable for HR analytics. Using available information I will try to find answers to the following questions:

1. What are the overall and department-wise turnover rates in the company? What managers have the highest turnover rates? What are the main reasons for resignation?
2. Could simple regression model be used to identify correlation between different factors and probability of resignation?

<h2>Turnover rates and main reasons for resignation</h2>

According to Linkedin, technology sector's average turnover rate in 2017 was approximately 13.2%. I will use a more conservative threshold of 15% for my analysis. Looking at a yearly turnover rates department-wise (figure below), we see that Production, Admin Offices and IT/IS departments had turnovers above 15% at some points. However, if we look at these departments' contribution into yearly turnover rates, it seems that only Production is troublesome. Overall yearly turnover does not exceed our threshold of 15% during last four years.

![Yearly turnover rates](/assets/Yearly_turnover.PNG)

Next, let's look into different departments' turnover rates broken down by managers. At the figure below we can see graphs for those managers whose turnover values were above the respecitve department levels for three and more years. We see that only six of Software Engineering and Production departments' managers fall under this category. 

![Yearly turnover rates of managers](/assets/Yearly_turnover_manager.PNG)

Let's dig deeper and identify main termination reasons given by their ex-subordinates.

![Yearly turnover rates of managers reasons](/assets/High_rates_managers_reasons.PNG)

The left part of the plot above depicts breakdown of number of employees who had worked under subject managers' command and terminated for different reasons as shares of total number of staff members terminated for corresponding reasons. Some of the particularly notable numbers include:

- Around 71% of all people who left the company and listed "Unhappy" as their reasons for termination.
- 44% of all overworked employees.
- 50% of all involuntarily terminated employees (dismissed due to either non-adherence to company policies or performance issues).

As we can see on the two righmost plots, these six managers (out of 21 managers in total) had 54% of all ever terminated people as their subordinates and jointly managed around 37% of all people ever employed in the company. For some of the managers the share of terminations is somewhat consistent with the share of totally managed people, whereas for others these values vary significantly.

Next, let's look into termination reasons at the department level (figure below).It is interesting to note, that higher remuneration has been the incentive for termination only for employees of Production department. Also, only Production staff indicated "Unhappy" as their main reason for leaving the company.

![Termination reasons](/assets/Term_reasons_department.PNG)

<h2>Logistic regression</h2>

In order to identify factors that correlate with termination, we used simple logistic regression.

Since our data has many explanatory variables, we applied "general-to-specific" approach, namely, we included as many variables as possible in the first iteration of the modeling and excluded variables with the lowest z-score at every subsequent iteration. Our final model includes only those variables whose Z-scores exceed threshold of 1.96 which is a critical value for statistical significance when using 95% confidence level. The p-value of the likelihood ratio chi-square for our model is 3.4107e-55 which tells us that the model fits the data significantly better than a hypothetical "empty" model that includes only intercept.

![Linear regression](/assets/LR_model.PNG)

The easiest way to interpret obtained coefficient estimators is to express them in terms of odd-ratios. By exponentiating coefficient estimators we yield following results:

1. The odds of termination are 7 times higher in case an employee was hired through a diversity job fair. This result is quite interesting. The data might indicate that company's inclusion initiatives do not work as effectively in the long run.
2. For a one unit increase in the number of special project that an employee performed, the odds of them leaving the company decrease by 68% (1 / 0.594).
3. With each additional year that an employee stays with the company, the odds of them leaving decreases by more than 5 times (1 / 0.196).
4. In order to interpret coefficient estimators of the combination of the termination age variable and its logarithmic transformation,  we need to take a first order derivative of the odds-ratio with respect to the AgeWhenTerminated variable and equate it to zero. I found the answer to be 42.2 years. This is the age for which the odds of termination are the highest.

<h2>Conclusion</h2>

In this post I made an attempt at analyzing turnover of an IT company and identify some factors that might affect termination rates. The subject of turnover, of course, could be analyzed from many other aspects that were not covered here. Some of the more interesting observations identified in the course of the analisys are the following:

- Some of the managers have consistently high turnover rates while a great deal of their subordinates had left the company for reasons other than changes in their personal circumstances or career transitions.
- Remuneration rates in the Production department might not be consistent with market levels.
- Employees brought in through company's diversity efforts seem to leave the company several times more often than those who were hired through other channels.

P.S. Here is a link to the corresponding Github project: [http://github.com/Leilusen/HR_data_analysis/] (http://github.com/Leilusen/HR_data_analysis/)
