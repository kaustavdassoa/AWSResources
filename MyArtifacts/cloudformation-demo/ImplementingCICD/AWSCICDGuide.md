# CI CD using AWS Services 
## Objective
* To demonstrate the CI/CD capabilities of AWS CodePipeline leveraging AWS CodeCommit , AWS CodeBuild , AWS CodeDeploy. 
* Monitor Deployment using AWS CloudWatch , AWS SNS (SimpleNotificationService), builds Logs etc.
* Develop AWS CloudFormation templates for CI/CD pipeline.

## Prerequisite
1. AWS free tire account 
2. A Sample Spingboot java project 
3. Lots of Patience.

## Implementing CI/CD pipeline using AWS console
### Task 1: Create a new repository CodeCommit Repositories.

#### Task 1.1 Create CodeCommit repository 

#### Task 1.2 Generate HTTPS Git credentials for AWS CodeCommit for the IAM user. 
![image](https://user-images.githubusercontent.com/5097017/76604331-91615000-6534-11ea-959c-8dfb59096421.png)
Note : Its always advisable to use IAM user instead of root user. 

#### Task 1.3 Push the code using the downloaded credentials 
```git
git init
git add <project-folder-name>
git remote add origin https://git-codecommit.<region>.amazonaws.com/v1/repos/<codeCommit-repo-name>
# The below command to verify git remote
git remote -v 
git push -u origin master 
# when prompted provide the downloaded credentials 
```
**Note:** Anyone with an AWS account can get started with AWS CodeCommit for free. Your account gets 5 active users per month for free (within limits), after which you pay $1.00 per additional active user per month. There are no upfront fees or commitments.
![image](https://user-images.githubusercontent.com/5097017/76618526-c24e7e80-654e-11ea-96fe-e605ffc5712f.png)

**Task 1.4** Verify the code by login into codeCommit management console 
![image](https://user-images.githubusercontent.com/5097017/76675792-536f3500-65e3-11ea-8c71-2cbe67cbe554.png)

### Task 2: Add buildspec.yml for the Porject.
Sample buildspec.yml for installting springboot project using maven build tool ```mvn install```

```yml
version: 0.2
phases:
  install: 
    commands:
     - echo Nothing to do in the install phase..
  pre_build:
    commands:
      - echo Nothing to do in the pre build phase...
  build:
    commands:
      - echo Build started on `date`
      - mvn install  # THIS IS THE MAIN BUILD COMMAND 
  post_build:
    commands:
      - echo Build completed on `date`
artifacts:
  files:
    - 'target/ccdemo.war'
```
Note : buildspec.yml file should be placed directly under the repository location, thus its advisable to have separate repository for separate project. 

### Task 3: Create a new CodeBuild Porject.
Code build project can be use to build the checked-in code. 


### Task 4: Add Notification for CodeBuild Phase Change & State change events.
CloudWatch can be cofigure to send Notification for CodeBuild Phase Change & State change events.<a href="https://docs.aws.amazon.com/codebuild/latest/userguide/sample-build-notifications.html" target="_blank">Refer Link for more details</a>


### Task 5: Create AWS CodeDeploy project.
**Note:** CodeDeploy pricing For CodeDeploy on EC2/Lambda there is no additional charge for code deployments to Amazon EC2 or AWS Lambda through AWS CodeDeploy.For CodeDeploy On-Premises, one may have to pay $0.02 per on-premises instance update using AWS CodeDeploy. There are no minimum fees and no upfront commitments. For example, a deployment to three instances equals three instance updates. One will only be charged if CodeDeploy performs an update to an instance and will not be charged for any instances skipped during the deployment.

**AWS CodeDeploy can deploy artifacts to**
1. EC2 instance 
2. EC2 autoscaling 
3. AWS Lambda 
4. AWS ECS (Elastic Container Services)

**AWS CodeDeploy can deploy of types**
1. Code 
2. Serverless AWS Lambda Function
3. Web & Configuration files 
4. Executable 
5. Packages
6. Scripts 
7. Media Files 

#### Task 5.1 Before starting to create codeDeploy project create two IAM service roles for codeDeploy service to access EC2 instance and S3 bucket on your behalf.

#### Task 5.2 Create a new EC2 instance, add the following userdata & a security group with ingress PORT 8080/22 open. TAG the EC2 instance with "Environment-Name = DEV"
```shell
  #!/bin/bash -xe
  sudo yum update -y
  sudo yum install -y ruby > /tmp/ruby.install.log
  sudo yum install -y wget > /tmp/wget.install.log
  sudo yum erase -y  java-1.7.0-openjdk.x86_64 > /tmp/jdk.unstall.log
  sudo yum install -y  java-1.8.0-openjdk.x86_64 > /tmp/jre.install.log
  sudo yum install -y  java-1.8.0-openjdk-devel > /tmp/jdk.install.log
  sudo yum install -y  tomcat > /tmp/tomcat.install.log
  cd /home/ec2-user
  wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
  chmod +x ./install
  sudo sudo ./install auto
```

#### Task 5.3 Create a AppSpec.yml and checkin with the code along with its associated scripts
NOTE: buildspecs.yml file need to be altered to ensure that AppSpec.yml & script folder is also included in the artifact section. 

#### Task 5.4 Create new application in AWSCloudDeploy console

#### Task 5.5 Create a new deployment plan







## Implementing CI/CD using CloudFoundation template 

### Task 1: Create a cloudFormation template for Prod and Staging Ec2-Instance - with CloudDeploy agent Installed.

Note: To install code-deploy agent on the EC2 instance refer <a href="https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-linux.html" target="_blank">this</a> link.

Code snippet for installing Asia Pacific (Mumbai) region the install URL is 
```unix
cd /home/ec2-user
wget https://aws-codedeploy-ap-south-1.ap-south-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
```

### Task 2: Create InstanceProfile and add it to EC2 instaces.#### 
Instance profile(s) are required for attaching IAM policies/roles to EC2 instances for accessing other AWS resources like S3,codeDeploy etc. 

Note : When CloudFormation template contains a IAM Resource creation steps, one need to provide additional concent while creating the Stack.
![](https://user-images.githubusercontent.com/5097017/76581936-fac46d00-64fa-11ea-8786-f1b5da0846d1.png)
