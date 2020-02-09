# CLOUD FORMATION HANDS-ON GUIDE 

### Prerequisite
1. Create a new default VPC in the targeted region ap-south-1 (Asia Pacific - Mumbai ). AWS console > VPC > Your VPC > Create Default VPC
2. Create a Keypair (pem base) to access EC2 instance - cfn-key-1 and cfn-key-2 




### Stack Overview 
##### Create New Stack : Create-ec2-instance-stack.yml
1. Go to CloudFormation 
2. Create New Stack 
3. Select "Template is ready" & "Upload a template file"
4. Provide the Create-ec2-instance.yml location 
5. Click on create Stack.

##### Update Existing Stack : Update-ec2-instance.yml
1. Click on the stack name 
2. Replace current template
3. Provide the name of the S3 bucket name where Update-ec2-instance.yml exists.
4. View the change set
![](https://user-images.githubusercontent.com/5097017/74091039-1fcb5780-4ad9-11ea-9c02-8e61c5c31e42.png)
5. Click on update Stack
6. View the events tab to validate - old resource been replaced by new resource 
![](https://user-images.githubusercontent.com/5097017/74091076-805a9480-4ad9-11ea-893e-dfe72329e56f.png)

##### Delete Stack
1. On deleting a stack all associated resources will be automatically deleted, there is no need to delete each resource individually. 
![](https://user-images.githubusercontent.com/5097017/74091122-18f11480-4ada-11ea-8a28-211ae7f947b0.png)

##### Creating Change Set 
1. Click on the existing stack 
2. Select "Template is ready" & "Upload a template file"
3. Create Change Stack
4. If the change can be applied without replacing the existing resource then Replacement will be set to 'False' as shown below. 
Note the change is just adding a new inbound rule to the existing security group thus no resource replacement needed. 
![](https://user-images.githubusercontent.com/5097017/74097922-03aad300-4b38-11ea-91c3-e71ec00c7f4b.png)
5. Once the change set is created - it can be executed to apply the changes OR can be deleted on dis-approving the changes. 
![](https://user-images.githubusercontent.com/5097017/74097983-ad8a5f80-4b38-11ea-8a67-17e865536300.png)

##### Parameters 
* Parameters enable users to enter customer values (input values) to the cloudFormation stack. 
* There can be upto 60 parameters within a single stack.
* Parameter names can be alphanumeric, and should be unique within the stack. 
* Parameter names are applied at the runtime - one can also define default value for each defined parameters. 

1. Add a Paramter to the Stack and refer the new Parameter instead of hardcoded value. 
2. Select "Template is ready" & "Upload a template file"
3. Provide StackName and Select Parameter value
![](https://user-images.githubusercontent.com/5097017/74098238-d7915100-4b3b-11ea-8ea7-c32b75a9679b.png)