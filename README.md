#### From Codecademy's Data Science Learning Path

# Project Assignment: User Churn
###

Codeflix, a streaming video startup, is interested in measuring their user churn rate. In this project, you’ll be helping them answer these questions about their churn:
- How many months has the company been operating? Which months do you have enough information to calculate a churn rate? What segments of users exist?
- What is the overall churn trend since the company started?
- Compare the churn rates between user segments. Which segment of users should the company focus on expanding?

The dataset contains one SQL table, `subscriptions`. Within the table, there are 4 columns:
- `id` - the subscription id
- `subscription_start` - the start date of the subscription
- `subscription_end` - the end date of the subscription
- `segment` - this identifies which segment the subscription owner belongs to

Codeflix requires a minimum subscription length of 31 days, so a user can never start and end their subscription in the same month.

The first 20 rows in `subscriptions` look like this:

id | subscription_start | subscription_end | segment
--- | --- | --- | ---
1 |	2016-12-01 | 2017-02-01 | 87
2 |	2016-12-01 | 2017-01-24 | 87
3 |	2016-12-01 | 2017-03-07 | 87
4 |	2016-12-01 | 2017-02-12 | 87
5 |	2016-12-01 | 2017-03-09 | 87
6 |	2016-12-01 | 2017-01-19 | 87
7 |	2016-12-01 | 2017-02-03 | 87
8 |	2016-12-01 | 2017-03-02 | 87
9 |	2016-12-01 | 2017-02-17 | 87
10 | 2016-12-01 | 2017-01-01 | 87
11 | 2016-12-01 | 2017-01-17 | 87
12 | 2016-12-01 | 2017-02-07 | 87
13 | 2016-12-01	| |	30
14 | 2016-12-01 | 2017-03-07 | 30
15 | 2016-12-01 | 2017-02-22 | 30
16 | 2016-12-01	| | 30
17 | 2016-12-01	| | 30
18 | 2016-12-02 | 2017-01-29 | 87
19 | 2016-12-02 | 2017-01-13 | 87
20 | 2016-12-02 | 2017-01-15 | 87
