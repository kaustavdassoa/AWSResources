# Deep Dive on AWS CloudFormation Helper Scripts

Helper function can be use to install software and start services on an Amazon EC2 instance that you create as part of your stack.

**AWS::CloudFormation::Init** : Use the AWS::CloudFormation::Init type to include metadata on an Amazon EC2 instance for the cfn-init helper script. cfn-init supports all metadata types for Linux systems, but does not supports all metadata types for windows system.

The following is the template for the AWS::CloudFormation::Init
```
Resources: 
  MyInstance: 
    Type: AWS::EC2::Instance
    Metadata: 
      AWS::CloudFormation::Init: 
        config: 
          packages: 
            :
          groups: 
            :
          users: 
            :
          sources: 
            :
          files: 
            :
          commands: 
            :
          services: 
            :
  ### EC2 instance fields 
    Properties:
      ImageId: ami-0d9462a653c34dab7
      InstanceType: t2.micro
      KeyName: !Ref KeyName
````

#### Command : 
This is use for execution of the commnads on EC2 instance.Commands are process in alphabetical order by name.
###### Command Supporting Keys  
* command
* env (set/override system enviroment variables)
* cwd (current working directory)
* test 
* ignoreError







##### Steps to create a Tomcat WAR file for testing Packages 

1. Create WEB-INF folder 
2. Create web.xml file inside WEB-INF
3. Create a HTML page 
4. jar cmF HelloWorld.war * 