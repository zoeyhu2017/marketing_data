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
SD(gross conversion)=0.0202
SD(retention)=0.0549
SD(net conversion)=0.0156

Decide how many pageviews you will need to power all your evaluation metrics?

α=0.05 β=0.2
calculator used http://www.evanmiller.org/ab-testing/sample-size.html

For P(gross conversion)=0.20625, dmin= 0.01, the sample size of clicks per group is 25835, so the sample size of pageview needed for both groups is 25835/0.08*2=645875
For P(retention)=0.53, dmin=0.01, the sample size of enrollments per group is 39087, so the sample size of pageview needed for both groups is 39115/0.08/0.20625*2=4741212
For P(net conversion)=0.1093125, dmin=0.0075, the sample size of clicks per group is 27413, so the sample size of pageview needed for both groups is 27413/0.08*2=685325

So, we will need 4,741,212 pageviews to power all three metrics.


Duration and Exposure
Unique cookies to view page per day:	40000

We intend to expose 50% of the traffic to the experiment, which is pretty risky. However, since the experiment required a large number of pageviews compare to its daily pageview, we have to compromise to make sure the duration is not too long.
With half of the traffic exposed to the experiment, the duration will be 4741212/20000=237 days. The duration is too long to be realistic. Therefore, we had to drop the retention as the evaulation metric. 

Based on the rest metrics, we will need 685325 pageviews for the experiment. With 50% traffic exposed to the experiment, the duration will be  685325/(40000/2)=34.3 days. 


Sanity Check on the invariant metrics: check whether the invariant metrics are randomly distributed in two groups.

number of cookies--summary of the experiment data:
 
 num_of_pageview(cont)=345543
 num_of_pageview(exp)=344660
 CI=95%
 with a binomial distribution, SE=SQRT(0.5*0.5/(345543+344660)=0.0006
                               M=1.96*0.0006=0.0012
                               Lower bound=0.4988
                               Upper bound=0.5012
                               Pcont=0.5006
Since Pcont is within the confidence interval, the metric number of cookies past the sanity check.

number of clicks--summary of the experiment data:
num_of_clicks(cont)=28378
num_of_clicks(exp)=28325
CI=95%
with a binomial distribution, SE=SQRT(0.5*0.5/(28325+28378)=0.0021
                               M=1.96*0.0021=0.0041
                               Lower bound=0.4959
                               Upper bound=0.5041
                               Pcont=0.5005
Since Pcont is within the confidence interval, the metric number of clicks past the sanity check as well.
              

Bonferroni correction: 

For the evaluation metrics we have now: gross conversion and net conversion, using bonferroni correction is too conservative since they are highly coorelated and will change together. 

Effect Size

Starting from Nov.3, there is no more record of enrollment or payment, therefore, we will not sum the sample clicks or enrollments before Nov.3.

For metric gross conversion, Ppool=(Xexp+Xcont)/(Ncont+Nexp)=(3785+3423)/(17293+17260)=0.208607067
                             M=1.96*SQRT((1-0.208607067)*0.208607067)*(1/17293+1/17260))=0.0086
                             d=Pexp-Pcont=-0.0206
                             lower bound=-0.0291
                             upper bound=-0.0120
                             dmin=0.01
So gross conversion is both statistically significant and practically significant,  but the effect is that the change decreases the gross conversion. 

For metric net conversion, Ppool=(Xexp+Xcont)/(Ncont+Nexp)=(2033+1945)/(17293+17260)=0.1151
                             M=1.96*SQRT((1-0.1151)*0.1151)*(1/17293+1/17260))=0.0067
                             d=Pexp-Pcont=-0.0049
                             lower bound=-0.0116
                             upper bound=0.0019
                             dmin=0.0075
So net conversion is neither statistically significant nor practically significant. that's to say the experiment won't have impact on the net conversion.


Sign test: to further test the result, we will look closer at the day-by-day data of the evaluation metrics.
num of the total experiment date: 23 days(exclude days when there is no record for payment or enrollment)

num of the positive change date for gross conversion: 4 days
num of the positive change date for net conversion: 10 days

with the calculator http://graphpad.com/quickcalcs/binomial1.cfm, we will calculate how likely the change happens randomly or by chance?

for gross conversion, p value= 0.0026, so the change is statistically significant 
for net conversion, p value=  0.6776, so the change is not statistically significant


In conclusion, making the design change is not recommended for the goal of improving students' expectaion and course completion. It is likely to decrease the gross conversion and net conversion. 




 






