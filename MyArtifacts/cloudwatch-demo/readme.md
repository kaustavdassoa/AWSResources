# CloudWatch - Demo 

# DEMO 1 : Create a simple CloudWatch Alarms and Notification 
## Objective
* Showcase cloudWatch Alarm & notification features
* Document detailed step-by-step guide to create cloudWatch Alarm & notification 

#### Create a new Alarm for EC2 CPUUtilization 
![](https://user-images.githubusercontent.com/5097017/77521117-328ec580-6ea8-11ea-8d51-31bdcf9671ee.png)

NOTE : Verify the instance ID , ensure that it correctly represents the desired EC2 instance 

#### Define conditions
![](https://user-images.githubusercontent.com/5097017/77521977-80f09400-6ea9-11ea-9ccf-084ebec3cd8c.png)

#### Create a new Notification action 
![](https://user-images.githubusercontent.com/5097017/77522318-155af680-6eaa-11ea-9295-9f9e1c2b46a1.png)

#### Add name and description for the alarm  
![](https://user-images.githubusercontent.com/5097017/77522927-0759a580-6eab-11ea-936b-f29c52f3c1aa.png)

#### Create a EC2 instance 
Create a simple free tier EC2 instance using Amazon Lunix AMI

#### Install Stress load utility  

Install stress utility 
```unix
sudo amazon-linux-extras install epel -y
sudo yum install stress -y
```

Run stress utility to simulate stress load
```unix
sudo stress --cpu 8 -v --timeout 30s
```
### View Alerts on CloudWach Alarm 
![](https://user-images.githubusercontent.com/5097017/77526186-2e66a600-6eb0-11ea-9559-080fd11ec518.png)

Verify the load by login into EC2 instance cloudWatch metrics tab
![](https://user-images.githubusercontent.com/5097017/77526293-5b1abd80-6eb0-11ea-8186-356334ed6adc.png)

Alarm status can also viewed from the EC2 instance dashboard 
![](https://user-images.githubusercontent.com/5097017/77526032-f3647280-6eaf-11ea-8634-ba15a0b77283.png)

### Reference 
<a href="https://www.loggly.com/blog/performance-monitoring-aws-cloudwatch-metrics/" target="_blank">www.loggly.com - performance monitoring aws cloudwatch metrics/</a>

<a href="https://www.metricly.com/subtleties-ec2-cpu-utilization/" target="_blank">www.metricly.com - EC2 cpu utilization</a>


----
# DEMO 2 : Process VPC logs to CloudWatch Logs 
## Objective
* Showcase how to process VPC log in CloudWatch Logs
* Showcase CloudWatch filter capability 


### Reference 
https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-cwl.html

----
# DEMO 2 :  CloudWatch Event
## Objective
* Showcase CloudWatch Events Capability

#### Create two EC2 instnace - one primary instance and another secondary instance
![image](https://user-images.githubusercontent.com/5097017/77709313-a20fcc80-6ff0-11ea-8c7d-f4a660b50408.png)

#### Create a simple CloudWatch Event rule - When Secondary comes-up Primary should be stop.
![image](https://user-images.githubusercontent.com/5097017/77709881-7392f100-6ff2-11ea-8830-fa481c479481.png)

#### Validate the same by bringing up the secondary instance when primary instance is still running 
![image](https://user-images.githubusercontent.com/5097017/77709959-b6ed5f80-6ff2-11ea-9582-12ffbd1ca95f.png)

Same can also be validated from the CloudWatch metrics dashboad 
![image](https://user-images.githubusercontent.com/5097017/77710100-24998b80-6ff3-11ea-9065-8e162446e086.png)

