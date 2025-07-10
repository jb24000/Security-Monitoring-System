<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Security Monitoring System

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-monitoring)

**Author:** Melvin J Bonner  
**Email:** melvinj.bonner@gmail.com

---

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_reghtjy)

---

## Introducing Today's Project!

In this project, I will be building my own powerful monitoring system using AWS. I'm doing this project to learn how to use Secrets Manager and configure an alarm using CloudWatch. I will be using SNS to send me an email when my secret has been accessed.  

### Tools and concepts

The services I used were CloudTrail, S3, CloudWatch, Secrets Manager, and SNS. Key concepts I learned include,  log delivery, metric filter, and alarm configuration. 

### Project reflection

This project took me approximately 3 hours to complete.  

---

## Create a Secret

Secrets Manager helps you protect secrets, which are passwords, API keys, credentials and sensitive information.  You could use Secrets Manager to keep database passwords, API keys, and other sensitive information

To set up for my project, I created a secret called TopSecretInfo that contains a key and a value.  

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_o5p6q7r8)

---

## Set Up CloudTrail

CloudTrail is monitoring service that records activity throughout my account.

CloudTrail events include types like management events, data events, insight events, and network activity events.

### Read vs Write Activity

Read API activity involves when someone views but doesn't change anything. Write API activity involves when changes happen - creating, deleting, modifying resources, or even retrieving the value of a secret.  For this project, we need both Read API and Write API.  

---

## Verifying CloudTrail

I retreived the secret in two ways: first through AWS console, and second using the AWS CLI.  

To analyze my CloudTrail events, I visited event history. I found GetSecretValue.  This tells me that my secret's value was retreived or used.  

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_s8t9u0v1)

---

## CloudWatch Metrics

CloudWatch Logs is a service that helps you bring together your logs from different AWS services, including CloudTrail, for visibility, troubleshooting, and analysis. It's important for monitoring because its a service that helps you bring together your logs from different AWS services, including CloudTrail, for visibility, troubleshooting, and analysis.

CloudTrail's Event History is useful for storing events for only 90 days; with CloudWatch Logs you are able to store events for as long as you like.  

A CloudWatch metric is what gets recorded when our filter spots a match in the logs. When setting up a metric, the metric value represents the number of times someone acceses our secret. Default value is used when our filter doesn't find any matches during a given time period.

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_a9b0c1d2)

---

## CloudWatch Alarm

A CloudWatch alarm is based on the SecretIsAccessed metric. I set my CoudWatch alarm threshold to greater than or equal to 1 in a 5-minute period, so the alarm will trigger when the SecretIsAccessed metric is greater than or equal to 1 in a 5-minute period.

I created an SNS topic along the way. An SNS topic is like a broadcast channel for your notifications. My SNS topic is set up to email.

AWS requires email confirmation because they want to make sure it's really you asking for these alerts. This helps prevents sending unsolicited emails.  

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_fsdghstt)

---

## Troubleshooting Notification Errors

To test my monitoring system, I retrieved my secret value. The results were not what I expected.  I didn't receive an email.  

When troubleshooting the notification issues I exposed my secret value, checked my email, I checked CloudWatch and checked CloudTrail event history. 

I initially didn't receive an email before because the CloudWatch alarm statistic was set to average. The solution was changing the CloudWatch alarm statistic to sum. Sum adds up all occurrences of secret access in the period (what I want).

---

## Success!

To validate the alarm, I checked the alarm configuration using a CLI command for manually triggering the alarm.

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_ageraergearge)

---

## Comparing CloudWatch with CloudTrail Notifications

In a project extension, I enabled SNS notification delivery in CloudTrail, because it will send a notification to my SNS topic every time a new log file is delivered to my S3 bucket. 

Aftrer enabling CloudTrail SNS notifications, my inbox was flooded with alerts.  In terms of the usefulness of these emails, I thought they were unnecessary and useless notifications. 

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-security-monitoring_d7e8f9g0)

---

---
