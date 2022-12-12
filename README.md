# Omri's DevOps Project

The following project is to create and deploy an architicture for an image gallery website that will support two objectives:
1. Support high traffic by horizontally scaling the website over 3 instances.
2. Support continious deployment by synchronizing the github "main" to the instances.

## Architecture  
![AWS diagram](https://github.com/omrikat/WebSite-Project/blob/main/Aws-diagram1.jpg)

### Scalability support
The scalability is managed by deploying the application into 3 EC2 instances that share the traffic. The external internet traffic is managed and routed by an elastic load balancer. The web application is shared among the instances through an elastic file system (EFS) that is connected to the EC2 instances.

### CI/CD support
The continious deployment is managed by a simple lambda function that is triggered to every push to the main branch.
The push will first trigger a simple test that will check if the gallery website still includes the header and only then it will copy it to the EFS and publish the new version of the website application.

## Installation

### 1. Deployment through cloud formation
#### 1.a Deploying using command line:
1. Download the deployment.yaml file locally
2. run the following command from the terminal ``` aws cloudformation deploy --template-file deployment.yaml --stack-name "my-new-stack"```

#### 1.b Deploying through the AWS console:
1. Go to the [AWS console](https://aws.amazon.com/console/)
2. Log into your account and go to the cloud formation section.
3. Choose "Upload a template file",then upload the "deployment.yaml" file and press "Next".
![image](https://github.com/omrikat/WebSiteProject/blob/main/Aws1.png)
4.Type a name under "Stack Name" and then press "Next".
![image](https://github.com/omrikat/WebSiteProject/blob/main/Aws2.png)
5.Scroll down and then Click on the checkbook then press "Submit"
![image](https://github.com/omrikat/WebSiteProject/blob/main/Aws3.png)
6.Should waiting for the status to be "CREATE_COMPLETE"
![image](https://github.com/omrikat/WebSiteProject/blob/main/Aws4.png)

### 2. Configuring the github repository
After the CloudFormation run done. go to lambda function in AWS account.
1.) Go to API "Getaway"
![image](https://github.com/omrikat/WebSiteProject/blob/main/API-Gateway.png)
2.) Copy the API endpoint
![image](https://github.com/omrikat/WebSiteProject/blob/main/ApiGatewayLink.png)
3.) Go to GitHub account and select your repo
4.) in the repo click on settings in the top left
![image](https://github.com/omrikat/WebSiteProject/blob/main/s1.png)
5.) Click on Webhooks in the right table then click on "Add webhook" in the top right
![image](https://github.com/omrikat/WebSiteProject/blob/main/s3.png)
6.)Past the endPoint for the API Gateway under "payload URL", then choose which event would you like to trigger , then Click on "Add Webhooks" button .
![image](https://github.com/omrikat/WebSiteProject/blob/main/s4.png)
## Maintainers
This repository is maintained by Omri Katesh.