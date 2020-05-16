---
layout: post
title: "Analysis of a yearly turnover"
date: 2020-05-16 05:00:00 +0200
---

*In this blog-post I will be looking at one of the most important HR metrics in any company - employee turnover. According to The Society for Human Resource Management (SHRM) research, direct replacement costs can reach as high as 50%-60% of an employee’s annual salary.

I used dataset prepared by New England College of Business of graduate MSHRM courses called HR Metrics and Analytics. It simulates an IT company and covers period from 2006 to 2017. Information includes data on all employees, their job statuses, pay rates, marital statuses and other data usually avaialable for HR analytics. Using available information I will try to find answers to the following questions:

1. What are the overall and department-wise turnover rates in the company? What managers have the highest turnover rates? What are the main reasons for resignation?
2. Could simple regression model be used to identify correlation between different factors and probability of resignation?

<h2>Turnover rates and main reasons for resignation</h2>

According to Linkedin, technology sector's average turnover rate in 2017 was approximately 13.2%. I will use a more conservative thrshold of 15% for my analysis. Looking at a yearly turnover rates department-wise (figure below), we see that Production, Admin Offices and IT/IS departments had turnovers above 15% at some points. However, if we look at these departments' contribution into yearly turnover rates, it seems that only Production looks troublesome. Overall yearly turnover does not exceed our threshold of 15% during last four years.

![Yearly turnover rates](/assets/Yearly_turnover.PNG)
