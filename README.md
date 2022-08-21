# UdacityStarbucksFinalProject

## Travis Helm
## August 2022

## Introduction to the Project (taken directly from the Udacity Introduction)

This data set contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). Some users might not receive any offer during certain weeks.

Not all users receive the same offer, and that is the challenge to solve with this data set.

Your task is to combine transaction, demographic and offer data to determine which demographic groups respond best to which offer type. This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products.

Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. You'll see in the data set that informational offers have a validity period even though these ads are merely providing information about a product; for example, if an informational offer has 7 days of validity, you can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

## Datasets (also directly from the Udacity Introduction)

Data Sets
The data is contained in three files:

- portfolio.json - containing offer ids and meta data about each offer (duration, type, etc.)
- profile.json - demographic data for each customer
- transcript.json - records for transactions, offers received, offers viewed, and offers completed

Here is the schema and explanation of each variable in the files:

portfolio.json

id (string) - offer id
offer_type (string) - type of offer ie BOGO, discount, informational
difficulty (int) - minimum required spend to complete an offer
reward (int) - reward given for completing an offer
duration (int) - time for offer to be open, in days
channels (list of strings)
profile.json

age (int) - age of the customer
became_member_on (int) - date when customer created an app account
gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
id (str) - customer id
income (float) - customer's income
transcript.json

event (str) - record description (ie transaction, offer received, offer viewed, etc.)
person (str) - customer id
time (int) - time in hours since start of test. The data begins at time t=0
value - (dict of strings) - either an offer id or transaction amount depending on the record

## Additional Files
Starbucks Capstone Notebook - This file details the work I put in to finding which offers drive the most net revenue
for Starbucks.  

## Methodology
I used a bootstrapping method on customer data from offer period 0 and offer period 168 to determine 
confidence intervals around the net revenue per person per hour that was received for the test group (one with an offer)
and the control group (one without the offer).  

I chose net revenue per person per hour because it allowed me to compare all offers against eachother.  Since impression times varied across the offers, I needed to divide by the duration of the offers to get them all on a per hour basis.  

## Key Findings:

- All offers, discounts and informationals showed a statistically significant (p=0.05) difference from their respective controls
- discount_dif010_dur240_rew002 had the highest increase in net revenue per hour (average of 0.156 dollars per hour additional revenue over the control).  Since the offer lasted for 240 hours, that meant that compared to the control group, customers with this offer spent (on average) and additional $37 during the time period.  This net revenue is about 50% higher than the next highest which was discount_dif007_dur168_rew003 (0.09 dollars per hour additional over control).
- As expected, informational offers yielded the lowest increase in hourly revenue since they didn't offer any reward and were informatiional in nature only.


## Suggestions for Future Studies

It would be suggested that the tests are run again at a later date to ensure that part of the reason for the increase in net revenue isn't tied to a novelty factor.  We weren't told whether this was the first time Starbucks offered the rewards or not.  If it is the first time, then some of the net revenue may be coming from the novelty of the new offers (vs the offers driving the values themselves).  Testing again at a later date would help to confirm if this is the case.

In the event that it's found that two offers perform similarly, the offer with the longest duration should be used.  This will lower marketing costs/efforts internally as fewer offers will have to be prepared/audited/launched on an annual basis.
