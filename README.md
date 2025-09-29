# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** Łukasz Brodziak  
**Email:** lukasz.brodziak@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

In this project we will create development environment consisting of local installation of VSCode with Remote SSH plugin and EC2 instance that will host Java and Maven along with app code. Also I will set up security group with SSH inbound rules to be able to connect from local VSCode to EC2. The project also involves crating IAM user but since I already have one I will skip this step.

### Key tools and concepts

Services I used were EC2 and SSH. Key concepts I learnt include creating EC2 instance, configuring SSH and connecting to EC2 instance using key pair.

### Project reflection

One thing I didn't expect in this project was the amount of problems with establishing reliable SSH connection. It appears that instance type used (t3. micro) had too little RAM to handle the VSCode remote connection. The solution was to create a swapfile with 1 GiB size to act as "additional" RAM.

This project took me approximately 2 hours to finish. The most challenging part was establishing SSH connection to EC2 from VSCode. It was most rewarding to relove all the problems based on my own research.

This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project in the upcoming days.

---

## Launching an EC2 instance

The "development" EC2 instance is created so that whole workflow from creating the app, build process and hosting it will reside entirely in the cloud. Thanks to this EC2 instance I can develop the app directly on AWS.

### I also enabled SSH

Secure Shell is a protocol used to make sure only authorized users can access a remote server. When you connect to your EC2 instance later in this project, SSH verifies you have the correct private key that matches the public key on the server.

### Key pairs

A key pair in EC2 is like the keys to our virtual computer. Just like you need a key to unlock and start your car, a key pair lets you securely access your EC2 instance.

Once I set up my key pair, AWS automatically downloaded a pem file with the key. The file can then be used to authenticate user while conecting to EC2 instance using SSH.

---

## Set up VS Code

VS Code is a free IDE from Microsoft. It is used to develop application in many different languages e.g. Python, C#, Java and many others.

I installed VS Code to connect to EC2 instance and develop the app code directly in the cloud using SSH.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is where you send instructions to your computer using text instead of clicks. The first command I ran for this project is cd which helps to navigate to folder specified in the commands argument.

I also updated my private key's permissions by running a chmod with 400 parameter which gives read permissions only to the owner of the file. We can set following permissions: 
Execute (denoted by 1 or x)
Write (denoted by 2 or w)
Read (denoted by 4 or r)
If we want to set multiple permissions to a file we simplu sum the digits e.g. 3 will give Execute and Write permissions. If we want to give full access to the file we set permission to 7 (4+2+1). Also the position of the number determines who gets permission. The order is as follows: Owner - Group - Others. So in our pem file the number 400 indcatest that the Owner gets Read rights and Group and Oter users don't get any rights for the file. 

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

To connect to my EC2 instance, I ran the command ssh -i <path to .pem file> ec2-user@<ec2 public dns server url>

### This command required an IPv4 address

A Public IPv4 DNS (which stands for Domain Name System) is the public address for your EC2 server that the internet uses to find and connect to it.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

Apache Maven is a tool that helps developers build and organize Java software projects. It's also a package manager, which means it automatically download any external pieces of code your project depends on to work.

Maven is required in this project because it can help us with creating the app by using something called archetypes, which are like templates, to lay out the foundations for different types of projects e.g. web apps.

Java is a popular programming language used to build different types of applications, from mobile apps to large enterprise systems.

Java is required in this project because it will be used to develop the app for this project.

---

## Create the Application

I generated a Java web app using the command 
mvn archetype:generate \
   -DgroupId=com.nextwork.app \
   -DartifactId=nextwork-web-project \
   -DarchetypeArtifactId=maven-archetype-webapp \
   -DinteractiveMode=false


I installed Remote - SSH extension in VS Code lets you connect directly via SSH to another computer securely over the internet. This lets you use VS Code to work on files or run programs on that server as if you were doing it on your own computer

Configuration details required to set up a remote connection include:
 HostName
 IdentityFile - path to pem file
 User 


![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

Using VS Code's file explorer, I could see a tree of folders of the web app project

Two of the project folders created by Maven are src and webapp. The src (source) folder contains all the source code files that define how your web app looks and works. src is further divided into webapp, which are the web app's files.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

The index.jsp is a file used in Java web apps. It's similar to an HTML file because it contains markup to display web pages.

I edited index.jsp by modifying the body of web page by adding: <h2>Hello enter user</h2>
    <p>This is my NextWork web application working!</p>

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

An alternative to using IDEs is using terminal. To edit index.jsp, I ran the command nano index.jsp. This opened a terminal-based editor called nano in which I could edit the file

Compared to using an IDE, editing index.jsp in the terminal felt limiting due to lack of atocomplete and code formatting.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-vscode_a3324ad41)

---

# Connect a GitHub Repo with AWS

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-github)

---

## Connect a GitHub Repo with AWS

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_dd9d254e)

---

## Introducing Today's Project!

In this project, I will demonstrate how to create a GitHub repo and push code changes to it. This repository will be then used in next steps of CI/CD pipeline.

### Key tools and concepts

Services I used were git and GitHub. Key concepts I learnt include creating new repository on GitHub, initializing local git repo on EC2, pushing code to remote.

### Project reflection

This project took me approximately 30 minutes 

I did this project because I needed the code on github repository to use it in CI/CD pipeline that will be created in later steps.

This project is part two of a series of DevOps projects where I'm building a CI/CD pipeline! 

---

## Git and GitHub

Git is often called a version control system since it tracks changes by taking snapshots of what files look like at specific moments, and each snapshot is considered a 'version'. I installed Git using the command sudo dnf install git -y


GitHub is a place for engineers to store and share their code and projects online. It's called GitHub because it uses Git to manage your projects' version history. I'm using GitHub in this project to store app files to be used in next projects.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_efaadbf7)

---

## My local repository

A Git repository is a folder that contain all project files and their entire version history.

Git init is a command that sets up the directory as a local Git repository which means changes are now tracked for version control. After running git init, the response from the terminal was "Initialized empty Git repository in /home/ec2-user/nextwork-web-project/.git/"

A branch in Git is an "alternate" version of the code in the same repository. This allows developers to add changes and new features without affecting the main branch and thus possibly breaking the working production code.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_7bf21bae)

---

## To push local changes to GitHub, I ran three commands

### git add

The first command I ran was "git add". This command is used to add new and changed files to staging area. In the command I ran I use . (dot) as an argument which added all files to staging are. Another usage is by passing particular filename to be added. A staging area is a place where all changed files are stashed by git for review before pushing them to remote.

### git commit

The second command I ran was git commit -m "Message". Using '-m' means te we are adding a comment about what was changed in this commit.

### git push

The third command I ran was git push -u origin master Using '-u' means that we are setting an upstream for local branch, which makes Git push to this branch by default.

---

## Authentication

Git needs to double check that you have the right to push any changes to the remote origin your local repo is connected with. To do this, Git is now authenticating your identity by asking for your GitHub credentials.

### Local Git identity

Git needs author information for commits to track who made what change. If you don't set it manually, Git uses the system's default username, which might not accurately represent your identity in your project's version history.

Running git log showed me that jsp file has been updated with new content

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_9a27ee3b)

---

## GitHub tokens

GitHub authentication failed when I entered my password because GitHub phased out password authentication to connect with repositories over HTTPS - there are too many security risks and passwords can get intercepted over the internet 

A GitHub token is a unique string of characters that looks like a random password.  I'm using one in this project because it is a better practice than using password.

I could set up a GitHub token by going into Profile -> Settings->Developer settings -> Personal Access Tokens -> Tokens (classic). 

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_fa11169d)

---

## Making changes again

I wanted to see Git working in action, so I updated the index.jsp file. I couldn't see the changes in my GitHub repo initially because changes were only done locally.

I finally saw the changes in my GitHub repo after I commited them and pushed them form local repo to remote.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_6becb2bc)

---

## Setting up a READMe file

As a finishing touch to my GitHub repository, I added a README file, which is a file containing projects documentation. I added a README file by runing touch command to create it in local repo and then pushed the file to github.

My README is written in Markdown because this is the language used for formatting md files. Special characters can help you format text in Markdown, such as ** for making text bold, or # which creates a large header (H1 in HTML).

My README file has 6 sections that outline general information about the code, technologies used in the project, instructions on how to install and setup the project, contact information

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-github_c94976902)

---

# Secure Packages with CodeArtifact

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codeartifact-updated)


---

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Introducing Today's Project!

In this project, I will demonstrate how to create CodeArtifact repository for my CI/CD pipeline. I'm doing this project to learn basic concepts of CodeArtifact.

### Key tools and concepts

Services I used CodeArtifact. Key concepts I learnt include creting CodeArtifact repository, using it to store Maven packages needed to build my project. Also I learnt how to create and publish my own packages.

### Project reflection

This project took me approximately... The most challenging part was... It was most rewarding to...

This project is part three of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project...

---

## CodeArtifact Repository

CodeArtifact is a secure, central place to store all your software packages. An artifact repository gives a consistent, reliable place to store and retrieve these components. 

A CodeArtifact domain is like a folder that holds multiple repositories belonging to the same project or organization. Domains give you a single place to manage permissions and security settings that apply to all repositori

Upstream repositories are like backup libraries that the primary repository can access when it doesn't have what you need. 

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codeartifact-updated_n4o5p6q7)

---

## CodeArtifact Security

### Issue

To access CodeArtifact, we need an authorisation token. I ran into an error when retrieving a token because by default, the EC2 instance doesn't have permission to access other AWS services (including CodeArtifact). This is intentional - AWS follows the "principle of least privilege," meaning resources only get the minimum permissions they need to function.

### Resolution

To resolve the error with my security token, I created an IAM role with attached policy. This resolved the error because the policy attached to the role allows the role to get the security token.

It's security best practice to use IAM roles because it allows for granular control of oermissions by attaching one or more security policies following the rule of least privilege.

---

## The JSON policy attached to my role

The JSON policy I set up grants permission to get authentication tokens, find repository locations, and read packages from repositories and allows temporarily elevated access specifically for CodeArtifact operations.
This follows the "principle of least privilege" - granting only the minimum permissions needed to perform the required tasks, enhancing security posture.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codeartifact-updated_23rp7q8r9)

---

## Maven and CodeArtifact

### To test the connection between Maven and CodeArtifact, I compiled my web app using settings.xml

By configuring settings.xml properly, we're creating a seamless connection between Maven and CodeArtifact. Builds will automatically authenticate and pull dependencies from the right place without having to think about it again. It's one of those "set it up once, benefit forever" kinds of configurations that make a developer's life much easier.

Compiling means turning application code into executable files.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codeartifact-updated_c17eace8)

---

## Verify Connection

After compiling, I checked the CodeArtifact repository. I noticed that it contains a list of Maven packges used to compile the project.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codeartifact-updated_1d79e699)

---

## Uploading My Own Packages

In a project extension, I also decided to create my own custom package. This is useful in situations where we create proprietary, custom, in-house code to be shared internally but keep private from the outside world. Companies use this to distribute everything from shared UI components to specialized data processing libraries without exposing their intellectual property.

To create my own package, I created a file containing my code and then created a tar.gz archive. I also generated a security hash that will be verified after someone downloads my code.

To publish the package, I used a cloud console command: 
aws codeartifact publish-package-version \
  --domain nextwork \
  --repository nextwork-devops-cicd \
  --format generic \
  --namespace secret-mission \
  --package secret-mission \
  --package-version 1.0.0 \
  --asset-content secret-mission.tar.gz \
  --asset-name secret-mission.tar.gz \
  --asset-sha256 $ASSET_SHA256
When I look at the package details in CodeArtifact, I can see
informaton about package like version, name, package status etc.

To validate my packages, I downloaded and unpacked the tar archive and opened the file.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codeartifact-updated_sm12-upload)

---

# Continuous Integration with CodeBuild

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codebuild-updated)

---

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codebuild-updated_35588a47)

---

## Introducing Today's Project!

In this project, I will create and configure CodeBuild project as part of a CI/CD pipeline.

### Key tools and concepts

Services I used were S3, CodeBuild. Key concepts I learnt include creating CodeBuild project and connecting it to GitHub repository, creating a build artifact and storing it in dedicated S3 bucket.

### Project reflection

This project took me approximately 1 hour to finish. 

This project is part four of a series of DevOps projects where I'm building a CI/CD pipeline!

---

## Setting up a CodeBuild Project

CodeBuild is a continuous integration service, which means after every new commit it builds and runs tests on a project. 

My CodeBuild project's source configuration holds the place where code is going to be fetched from and I selected GitHub.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codebuild-updated_fewgrhte)

---

## Connecting CodeBuild with GitHub

There are multiple credential types for GitHub, like GitHub App, Personal Access Token and OAuth. I used GitHub App because of it's ease of use and enhanced security.

.AWS CodeConnections is like a secure bridge between AWS and your external code repositories. Instead of dealing with the headache of managing API keys, tokens (like GitHub's Personal Access Tokens!), or SSH cre

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codebuild-updated_a7c98e2d)

---

## CodeBuild Configurations

### Environment

My CodeBuild project's Environment configuration is like a template for the build environment (just like how AMI's are templates for your EC2 instances).

### Artifacts

are the tangible outputs of your build process. They're what you'll actually deploy to your servers or distribute to users.  My build process will create WAR files containing everything needed to run the app. To store them, I created an S3 bucket.

### Packaging

When setting up CodeBuild, I also chose to package artifacts in a ZIP file because it is easier to manage, it has smaller size and it is simpler to deploy or share.

### Monitoring

For monitoring, I enabled CloudWatch Logs, which is monitoring service that collects and tracks logs from AWS services. CloudWatch will record everything that happens during the build process, including the commands that are run.

---

## buildspec.yml

My first build failed because there was no buildspec.yml file in code repository. A buildspec.yml file is needed because it contains instructions of step by step build of the project.

The first two phases in my buildspec.yml file prepare all necessary prerequisites. The third phase in my buildspec.yml file is the actual build of the project. The fourth phase in my buildspec.yml file is creating a WAR file.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codebuild-updated_35588a47)

---

## Success!

My second build also failed, but with a different error that was a command execution error due to insufficient permissions. To fix this I attached proper IAM policy to the CodeBuild role.

To resolve the second error, I attached a proper codeartifact IAM policy to codebuild role. When I built my project again, I saw a successful build.

To verify the build, I checked a dedicated S3 bucket. Seeing the artifact tells me that the build was successful.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codebuild-updated_d9cc6191)

---

## Automating Testing

In a project extension, I'm going to automate tests. I added a test script that checks the structure of the project and verifies if proper files nad folders are present.

To add the test script to the build process, I modified buildspec.yml file to include the test step.

After pushing my code to GitHub, I ran the build in CodeBuild. I could see test results in the build logs.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codebuild-updated_sm-test-script-upload)

---
# Deploy a Web App with CodeDeploy

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-codedeploy-updated)


---

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codedeploy-updated_val-27)

---

## Introducing Today's Project!

In this project I will create the deployment part of the CI/CD pipeline. To achieve this I will use AWS CodeDeploy. Also I will create an EC2 instance that will be used to host the web app. To create the EC2 instance I will use CloudFormation which is AWS Infrastructure as Code (IaC) service.

### Key tools and concepts

I used AWS CodeDeploy, EC2, S3, IAM, and CodePipeline. I learned how to automate
deployments, manage revision locations, configure appspec.yml, and verify web apps
through public IPs.

### Project reflection

This project took me approximately 2 hours.

This project is part five of a series of DevOps projects where I'm building a CI/CD pipeline!

---

## Deployment Environment

To set up for CodeDeploy, I launched an EC2 instance and VPC to create a live production environment with secure, isolated network settings needed for app deployment.

Instead of launching resources manually, I used AWS CloudFormation to deploy my EC2 instance and VPC. This allows version-controlled, repeatable infrastructure
creation and easy cleanup.

Other resources created in this template are a VPC, subnet, route table, internet
gateway, security group, and EC2 instance to build a complete and secure network for
the web app deployment.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codedeploy-updated_val-5)

---

## Deployment Scripts

Scripts are shell files used to automate tasks such as installing dependencies (Tomcat,
Apache), starting/stopping services, and setting up configurations. To set up
CodeDeploy, I also wrote scripts to help deploy the application correctly.

The install_dependencies.sh script installs Tomcat and Apache, sets up reverse proxy
configuration so Apache forwards traffic to Tomcat, and prepares the EC2 instance to
host the web application. It ensures the server is ready for deployment.

The start_server.sh will start both Tomcat (our Java application server) & Apache (our
web server), and make sure they are set to automatically restart if EC2 instance
reboots. This ensures our web application remains available even after restart.

The stop_server.sh will stop both the Tomcat (Java app.server) & Apache (web server)
services. This is useful for shutting down the application safely before
deployments/maintenance, ensuring that no requests are being served during those
operations.

---

## appspec.yml

The appspec.yml is a configuration file used by AWS CodeDeploy to tell it exactly how
to deploy an application. It defines: Which files to copy and where to place them on
the EC2 instance. Which scripts to run during each deployment phase.

I updated buildspec.yml because AWS CodeBuild needs to know which files to include
in the final deployment package. I added the appspec.yml and scripts/ directory under
the artifacts section, so CodeDeploy will know how to run the deployment & manage

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codedeploy-updated_val-12)

---

## Setting Up CodeDeploy

A CodeDeploy application defines what to deploy (the app and its files). A deployment
group defines how and where to deploy it, including target instances, settings, and
triggers for that application.

To set up a deployment group, you also need to create an IAM role to so it has the
necessary permissions to interact with other AWS services during the deployment
process.This role ensures CodeDeploy can perform only the actions it needs.

Tags help CodeDeploy identify the right EC2 instances for deployment. I used the tag
role=webserver to automatically target the correct instance, making the deployment
process easier, automated, and more accurate.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codedeploy-updated_val-18)

---

## Deployment configurations

Another key setting is the deployment configuration, which affects how updates are
rolled out. I used CodeDeployDefault.AllAtOnce, so all instances are updated at the
same time. Other options include OneAtATime and HalfAtATime for safer rollouts.

In order to connect and deploy apps to EC2, a CodeDeploy Agent is also set up on the
instance. It listens for deployment instructions from CodeDeploy and runs the scripts
defined in appspec.yml to install, start, or stop the application.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codedeploy-updated_val-20)

---

## Success!

A CodeDeploy deployment is a single update to an app with a unique ID. It defines
what to deploy (revision), where (deployment group), and how (settings). It differs
from a group, which defines the target instances and config for deployment.

I had to configure a revision location, which means CodeDeploy knows where to find
the app files. My revision location was an S3 bucket with a .zip file containing the build
artifact to deploy to EC2 instances.

To check that the deployment was a success, I visited the EC2 instance's public IP
using HTTP in my browser. I saw the "Hello enter user!" message, which confirmed that
my web application deployed and ran correctly.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-codedeploy-updated_val-27)

---

## Disaster Recovery

In a project extension, I decided to add an error to the app. The intentional error I created was an incorrect call in stop_server.sh script. This will cause the deployment to fail because it will result in command not found error.

I also enabled rollbacks with this deployment, which means that if deployment of new version fails the previous version is restored. This minimises the downtime of the application.

---
# Infrastructure as Code with CloudFormation

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-cloudformation-updated)

---

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_bd8b836b)

---

## Introducing Today's Project!

In this project, I will work on moving the CI/CD pipeline into CloudFormation. I'm doing this project to learn Infrastructure as Code (IaC).

### Key tools and concepts

Services I used were CloudFormation and IaC generator. Key concepts I learnt include creating CloudFormation templates, using templates to create stack and deploy resources. Also I have explored manual creation of code for resources that IaC generator was not able to scan for.

### Project reflection

This project took me approximately 2 hours to complete. The most challenging part was dealing with errors that were not included in the project like the problem with deploying connections. It was most rewarding to have this error handled.

This project is part six of a series of DevOps projects where I'm building a CI/CD pipeline!

---

## Generating a CloudFormation Template

The IaC Generator is a tool in AWS CloudFormation that scans all AWS resources which then can be placed in a template. It works in a three-step process:
1. A scan of resources is performed
2. A template file is created
3. Template is imported into CloudFormation and can be later deployed.

A CloudFormation template contains code definitions for all the resources we want to create. The resources that I could add to my template include IAM roles and policies, EC2 instance profiles, CodeArtifact repos and more.

The resources I couldn’t add to my template were CodeBuild and CodeDeploy because they require specific configuration details and and security permissions that our generator isn't able to handle automatically.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_0495b046)

---

## Template Testing

Before testing my template, I deleted existing resources from my account because they will be now recreated by the CloudFormation template. If they were not removed it would cause conflicts and the template deployment failure.

I tested my template by creating a new stack and submitting it. The result of my first test was a failure due to the policies being created before the role they depend on.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_f56730fd)

---

## DependsOn

To resolve the error, I by adding the DependsOn attribute to failing policies. The DependsOn attribute means that the resource it was defined in will not be created until the resource mentioned in DependsOn attribute is created.

The DependsOn line was added to for different parts of my template which are four CodeBuild policies, which allow access to CodeArtifact, CodeConnection, CloudWatch and EC2 instances which is underCodeBuild base policy.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_f0df8018)

---

## Circular Dependencies

I gave my CloudFormation template another test! But this time I encountered a circular dependency error. This means that two(or more) resources defined in the template refer to each other.

To fix this error, I the references to the IAM policies from the IAM role definition.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_e6fd85ed)

---

## Manual Additions

In a project extension, I manually defined two more resources:
1. CodeBuild
2. CodeDeploy

I also had to make sure the references were consistent in this template, so I edited CodeBuild role id, S3 Bucket id, codedeploy role id and codedeploy application id.

I also introduced Parameters, which are a way of making code more flexible. 

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_1cee0428)

---

## Success!

I could verify all the deployed resources by visiting Resources tab that contains the list of created resources.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-devops-cloudformation-updated_bd8b836b)

---




---


---
