# SETTING UP A MERN STACK AND DEPLOYING A TODO APPLICATION ON AWS CLOUD

A MERN web stack consist of the following components: MongoDB, ExpressJS, ReactJS, and NodeJS. The following are the steps taken to setting up a MERN stack in AWS cloud:

## STEP 1: Setting up a virtual server in the cloud

To setup a virtual server, I Created a new EC2 Instance of t2.nano family with Ubuntu Server 20.04 LTS (HVM) image from aws account which is the free tier(limited) offered by aws. After a successful launch of the EC2 instance(ubuntu server), I connected to the EC2 instance from MobaXterm(as a window user) terminal with my private key(.pem file).

## STEP 2: Server Configuration

The following commands are used to configure the ubuntu server:

 - Update ubuntu : `$ sudo apt update`
  
 - Upgrade ubuntu: `$ sudo apt upgrade`
