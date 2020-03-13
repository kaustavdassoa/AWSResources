# CI CD using AWS Code Pipeline 

**Objective** : To demostrate the CI/CD capabilities of AWS Code Pipeline, leveraging AWS Code Commit , AWS Code Build , AWS Code deploy, AWS Cloud Watch , AWS X-Ray, and AWS Cloud Formation.

**Task 1: Create a cloudFormation template for Prod and Staging Ec2-Instance - with CloudDeploy agent Installed.**

Note: To install code-deploy agent on the EC2 instance refer <a href="https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-linux.html" target="_blank">this</a> link.

Code snippet for installing Asia Pacific (Mumbai) region the install URL is 
```
cd /home/ec2-user
wget https://aws-codedeploy-ap-south-1.ap-south-1.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto
```

**Task 2: Create InstanceProfile and add it to EC2 instaces.** 
Instance profile(s) are required for attaching IAM policies/roles to EC2 instances for accessing other AWS resources like S3,codeDeploy etc. 

Note : When CloudFormation template contains a IAM Resource creation steps, one need to provide additional concent while creating the Stack.
![](https://user-images.githubusercontent.com/5097017/76581936-fac46d00-64fa-11ea-8786-f1b5da0846d1.png)

**Task 3: Create a new repository CodeCommit > Repositories.** 
![image](https://user-images.githubusercontent.com/5097017/76603369-d1273800-6532-11ea-99fb-ff3ec7ce63cd.png)

1. Create CodeCommit repository 
2. Generate HTTPS Git credentials for AWS CodeCommit for the IAM user. 
![image](https://user-images.githubusercontent.com/5097017/76604331-91615000-6534-11ea-959c-8dfb59096421.png)
Note : Its always advisable to use IAM user instead of root user. 
3. Push the code using the downloaded credentials 
```
git init
git add ccdemo
git remote add origin https://git-codecommit.<region>.amazonaws.com/v1/repos/<repo-name>
# The below command to verify ONLY
git remote -v 
git push -u origin master 
# when promoted provide the downloaded credentials 
```
4. verify the code by login into codeDeploy 
![image](https://user-images.githubusercontent.com/5097017/76606772-dedfbc00-6538-11ea-9323-c4c2180dc4c0.png)
