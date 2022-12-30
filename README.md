# Udagram

## Description
Here, we are creating an Instagram clone called Udagram. We build the the AWS infrastructure
for that app with CloudFormation.
We provision the required infrastructure and deploy a dummy application, along with 
the necessary supporting software. 
This needs to be automated so that the infrastructure can be discarded as soon as 
the testing team finishes their tests and gathers their results.

The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.

A sample website files located in a public S3 Bucket to the Apache Web Server running on an EC2 instance. 

To connect to the private servers with SSH for troubleshooting, a jumpbox(bastion host) is created in the public subnet.

Here is a diagram representing the architecture to build:

![alt text](https://github.com/awadiagne/Udagram/blob/3b5a194112a6ea2c71d0dddf2cbbf7c85dec8300/Udagram%20Diagram.png)

## Considerations

### Launch Configuration 
Application servers are deployed four servers, two located in each of the private subnets. 
The launch configuration will be used by an auto-scaling group.

### Servers specs
Each server needs 2 vCPUs and at least 4GB of RAM. The Operating System is Ubuntu 18.
At least 10GB of disk space for each server.

### App archive in S3
The application archive from an S3 Bucket, we'll need to create an IAM Role that allows the instances to use the S3 Service.

### Security Groups and Roles
Servers inbound port : HTTP Port: 80 for the Load Balancer and the Load Balancer Health Check. 
Servers outbound ports: Unrestricted internet access for downloads and update their software.
Load balancer security group: Public traffic (0.0.0.0/0) on port 80 inbound. 
Load balancer Outbound: Port 80 to reach the internal servers.

Output exports of the CloudFormation script should be the public URL of the LoadBalancer.

## Project Structure
The code is splitted into 3 parts representing the networking that should be deployed first, then the servers and finally the storage. 
Each of them has a json file parameter.

## Load Balancer URL
http://udagr-Udagr-K582NCOATLZ8-1983179249.us-east-1.elb.amazonaws.com
