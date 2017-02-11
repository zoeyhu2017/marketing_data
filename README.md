# marketing_data
Udacity A/B Testing Project

choices of metrics:
● Number of cookies: That is, number of unique cookies to view the course overview page. (dmin=3000)
● Number of user-ids: That is, number of users who enroll in the free trial. (dmin=50)
● Number of clicks: That is, number of unique cookies to click the "Start free trial" button (which happens before the free trial screener is trigger). (dmin=240)
● Click-through-probability: That is, number of unique cookies to click the "Start free trial" button divided by number of unique cookies to view the course overview page. (dmin=0.01)
● Gross conversion: That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the "Start free trial" button. (dmin= 0.01)
● Retention: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin=0.01)
● Net conversion: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the "Start free trial" button. (dmin= 0.0075)

My choice of invariant metrics:

number of cookies
number of clicks
Click-through-probability

Reasoning: With the design of the experiment, no changes will happen before viewers see the prompted message about course dedication. Activities monitored by the three metrics above all happen before the designed change by the experiment.

My choice of evalution metrics:

Gross conversion
Net conversion
retention

Reasoning: With the designed change, it is expected that changes apply to the number of users who enroll the free trial because they are firstly questioned about whether they are ready to enroll or not, and the number of users who stay past 14-day free trial and make a payment because the experiment anticipates that with the extra free trail screener, users who pay and stay through the course are the ones with dedication to completion. these factors are involved in the metrics of gross conversion, net conversion and retention. Therefore, it is expected these are the metrics we will expect changes and use to evaluate the experiment. 


Measure variability of the evaluation metrics

Since the evaluation metrics follow a binomial distribution, the formula to calculate their standard deviation is as follow:
SD=SQRT(p*(1-p)/N (N stands for the sample size of the metric)

With a total sample size of 5,000 for the experiment, a CTP of 0.08, a enroll/click=0.53
we can calculate N for number of clicks=0.08*5000=400
                 N for number of enrollment=400*0.53=82.5
Therefore, standard deviation for the evaluation metrics are as follow:


Click-through-probability on "Start free trial":	0.08		
Probability of enrolling, given click:	0.20625	gross conversion	0.020230604
Probability of payment, given enroll:	0.53	retention	0.054949012
Probability of payment, given click	0.1093125	net conversion	0.015601545



