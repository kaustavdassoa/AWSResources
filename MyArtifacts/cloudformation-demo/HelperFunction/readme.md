# Deep Dive on AWS CloudFormation Helper Scripts

Helper function can be used to install software and start services on an Amazon EC2 instance that you create as part of your stack.

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
#### Package :
Installed packages that needs to be installed.

#### Groups :
The Lunix/Unix groups & assign IDs, this section irrelevant for windows system. 

#### Sources :

#### Files :

#### Command : 
This is use for execution of the commnads on EC2 instance.Commands are process in alphabetical order by name.
###### Supporting Keys  
* command
* env (set/override system enviroment variables)
* cwd (current working directory)
* test 
* ignoreError (true or false)
* waitAfterCompletion

#### Services : 
This is use to enable /disable services when a new EC2 instance is launched. This is accomplinished by sysvinit for Lunix and Window Service Manager for Windows system.
###### Supporting Keys 
* ensureRunning
* enabled
* files
* source
* package
* commands

<u>**cfn-init helper script**</u> read the metadata from the AWS::CloudFormation::Init key and act accordingly 
* Fetch & Parse metadata from AWS cloudFormation template 
* Install packages
* Write files to the disk 
* Enable/disable services

Note : cfn-init does not requried credentials, however if no creadentials are defined, AWS CloudFormation checks stack membership and limit the scope of the call to the stack and the instance belong to. 

Syntax 
```
cfn-init --stack|-s stack.name.or.id \
         --resource|-r logical.resource.id \
         --region region
         --access-key access.key \
         --secret-key secret.key \
         --role rolename\
         --credential-file|-f credential.file \
         --configsets|-c config.sets \
         --url|-u service.url \
         --http-proxy HTTP.proxy \
         --https-proxy HTTPS.proxy \
         --verbose|-v
```
<u>**cfn-signal helper script**</u> signals AWS cloudFormation weather Amazon EC2 instance have been successfully created / updated. cfn-helper script can be use in conjunction with the creation policy.

Syntax 
```
cfn-signal --success|-s signal.to.send \
        --access-key access.key \
        --credential-file|-f credential.file \
        --exit-code|-e exit.code \
        --http-proxy HTTP.proxy \
        --https-proxy HTTPS.proxy \
        --id|-i unique.id \
        --region AWS.region \
        --resource resource.logical.ID \
        --role IAM.role.name \
        --secret-key secret.key \
        --stack stack.name.or.stack.ID \
        --url AWS CloudFormation.endpoint
```







##### Steps to create a Tomcat WAR file for testing Packages 

1. Create WEB-INF folder 
2. Create web.xml file inside WEB-INF
3. Create a HTML page 
4. Run the following command to create the war file ```JAVA_HOME\bin\jar cmF HelloWorld.war * ``` 