# CLOUD FORMATION DEMO 

### Prerequisite
1. Create a new default VPC in the targeted region ap-south-1 (Asia Pacific - Mumbai ). AWS console > VPC > Your VPC > Create Default VPC
2. Create a Keypair (pem base) to access EC2 instance - cfn-key-1 and cfn-key-2 




### Stack Overview 
Create New Stack : Create-ec2-instance-stack.yml
1. Go to CloudFormation 
2. Create New Stack 
3. Select "Template is ready" & "Upload a template file"
4. Provide the Create-ec2-instance.yml location 
5. Click on create Stack.

Update Existing Stack : Update-ec2-instance.yml
1. Click on the stack name 
2. Replace current template
3. Provide the name of the S3 bucket name where Update-ec2-instance.yml exists.
4. View the change set
![](https://user-images.githubusercontent.com/5097017/74091039-1fcb5780-4ad9-11ea-9c02-8e61c5c31e42.png)
5. Click on update Stack
6. View the events tab to validate - old resource been replaced by new resource 
![](https://user-images.githubusercontent.com/5097017/74091076-805a9480-4ad9-11ea-893e-dfe72329e56f.png)

Delete Stack 
1. Delete Stack 
2. Delete all the associated resources too, in this case EC2 instance ![](https://user-images.githubusercontent.com/5097017/74091122-18f11480-4ada-11ea-8a28-211ae7f947b0.png)


