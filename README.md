# jp-blog_analysis

## Description 
Our client needs a daily report on traffic to their blog site( https://dev.classmethod.jp/ )
The access logs are stored in the S3 bucket s3://replica.log.developers.io/alb/devio-nginx-al2-20180823/AWSLogs/554474346280/elasticloadbalancing/ap-northeast-1/ on a daily basis.

The report should include the items below on the previous day(JST).

total page view

hourly page view

top 10 articles

sample
----------------------
### 1. Daily Page View 
[2019/03/09]
PV: 1220439


### 2. Hourly Page View :

> 00: 35242

> 01: 645

> 02: 632

> ...

> 23: 5215
### 3. Top 10 articles : 

>1. xxxxx

>2. yyyyy

>...

>10. zzzz

----------------------

The reports should be stored in a S3 bucket.

s3://{bucket-name}/traffic_reports/20190301.txt

s3://{bucket-name}/traffic_reports/20190302.txt

s3://{bucket-name}/traffic_reports/20190303.txt

## Lambda functions 
Create tables trigger lambda function everyday at 12AM JST 

CloudWatch Events: cron(15 15 * * ? *)

- jp-blog_analysis.py
- jp-blog_analysis_JST.py


Generate Reports and save to S3 bucket: 

- jp-blog_analysis_PV.py ---PV
- jp-blog_analysis_hourlyPV.py --hourly page view
- jp-blog_analysis_topten.py --top 10 articles

### Regions:
ca-cental-1
- Athena
- S3 bucket 

us-west-2
- Lambda functions 

## Infrastructure 
![alt text](https://github.com/astrobetacancri/Blog_analysis/blob/master/jp-blog_analysis-Page-2.png)


## Lambda code reference
https://thedataguy.in/automatically-create-aws-athena-partitions-for-cloudtrail-between-two-dates/
https://thedataguy.in/automate-aws-athena-create-partition-on-daily-basis/
