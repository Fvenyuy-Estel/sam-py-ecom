
const cars = ["BMW", "Volvo", "Mini"];

let text = "";
for (let x of cars) {
  text += x;
}

const cars = ["BMW", "Volvo", "Mini"];

let text = "";
for (let x of cars) {
  text += x;
}

### Modern Serverless application development with AWS SAM, Vuejs, Flutter, AWS API gateway, EventBridge pipes, SNS, SQS and Python

# ** Description: **

In this course you will be able to build an e-commerce application using:

* AWS SAM
* Python
  
With the following AWS services:

* AWS API gateway
* Lambda functions
* EventBridge
* SNS
* SQS
* AWS DynamoDB

# **Objectives**

* By the end of this course, you should be able to have a mastry of the following: 

   * CloudFormation, AWS SAM, SQS, SNS, EventBridge and EventBridge pipes and in each of this cases you should be able to  explain:
    * What it is
    * What it's not
    * Why it is used 
    * When to use it and  
* You should be able to build an AWS SAM applications with ease
  
---

Hey wassup guys!

In this course we are going to be building a modern Serverless application development with AWS SAM, Vuejs, Flutter, AWS API gateway, EventBridge, SNS, SQS and Python. The building process is going to be devided in to two phases which are:

   * Phase one: 
      
      * A brief description of the various AWS services and resources that are going to be used in the development process
      * A description of the architecture of the project
   
   * Phase two: 
      * The actual developement of the application.

# **Phase one**

In this phase we are going to be focusing on:

  * SQS
  * SNS
  * EventBridge
  * Project architecture

If you are already familiar with the above terms you might want to consider moving to phase two.

## **SQS**

**Pattern**
   - Queues
   - Messages
   - Polling

**What is SQS**
    
  - Amazon Simple Queue Service (SQS) lets you send, store, and receive messages between software components at any volume, without losing messages or requiring other services to be available.
  - It allows application owners to publish messages in to a queue and in doing so decoupling the applications from one another
  - An SQS queue belongs to the application or service that is pooling the queue and not necessarily owned by the person publishing messages to the queue
  - By default, queue's are not FIFO, so if you want yours to act in a FIFO manner you would have to configure it that way
  - It offers async message base communication as opposed to API calls
  - Scalable, highly available, fully managed, and cost effective.
  
**why SQS**

   - You want to create loosely coupled architecture.
  
   - All operations don’t need to be completed in a single transaction, and some operations can be asynchronous.
  
   - The downstream system cannot handle the incoming transactions per second (TPS) rate. 
   
   - The messages can be written to the queue and processed based on the availability of resources.

**When to use SQS**
   
   This service is usefull in a variety of contex and across many different domains. Its very effective for:

  - Data processing workloads or maybe when you have a group of producers which could be IoT devices or mobile phone devices that are all producing events and you want to process those events, you can set it so that those event's are being delivered to a queue and have a system on the other side that is going to be processing all those event's.
     
   - Real time events processing maybe if you have like an e-commerce application that is producing event's and you have something on the other side maybe something like an analytic dashboard that needs to agregate all of this information and kind of store it on it's own dashboard.
  
   - Or for example in the e-commerce application we are going to be building, we are going to be using an **SQS** to handle orders created by users. This is so because we will be having a lot of users creating orders and we don't want some messages missing. So we place all the messages in a queue and have some other service which we are going to be talking about in a not shell poll and process them one after the other 
   Asynchronous processing workflows.

   - Processing messages in parallel (by using multiple SQS queues).

   - Decoupling and scaling microservices, distributed systems, and serverless applications.

   - Sending, storing, and receiving events with reliable messaging guarantees (ordering & exactly-once processing).
  
**Advantages of SQS**
   - **Backpressure control:** Consumers can choose the rate of processing
   - **Fire and forget:** Publishers have no insight in to client processing
   - **Eventually guaranteed processing:** Great for async or non realtime apps
   - **Application decoupling:** Decouple service dependencies
  
* Disadvantage of SQS

   - A disadvantage of this pattern is that business transaction actions are synchronous. Even though the calling system receives a response, some part of the transaction might still continue to be processed by downstream systems.

## **SNS**

**Pattern** 

  - Topics
  - Messages
  - Publisher/Subscriber(Pubsub)

**What is SNS**

   - Amazon Simple Notification Service (Amazon SNS) is a managed service that provides message delivery from publishers to subscribers (also known as producers and consumers).
   
   - It's a cloud service offered by AWS, It fully managed distributed publish-subscribe system that operates on a Fan-out model. It offers a push notification functionality that lets us send individual messages or bulk messages to a large set of subscribing clients or applications.
  
   - Publishers communicate asynchronously with subscribers by sending messages to a topic, which is a logical access point and communication channel. 
   
   - Clients can subscribe to the SNS topic and receive published messages using a supported endpoint type, such as Amazon Kinesis Data Firehose, Amazon SQS, AWS Lambda, HTTP, email, mobile push notifications, and mobile text messages (SMS).
  
**Why use SNS**
   - SNS is typically used for applications that need realtime notifications and when we want to broadcast messages to many subscribers at once
  
**When to use SNS**
   - Sending email, SMS, and push notifications to end-users in realtime. Note that you can send push notifications to Apple, Google, Fire OS, and Windows devices.

   - Broadcasting messages to multiple subscribers (for example, fanning out the same push notifications to all users of your app).

   - Workflow systems. For example, you can use SNS to pass events between distributed apps, or to update records in various business systems (e.g., inventory changes).

   - Realtime alerts and monitoring applications.

## **Differences between SQS and SNS**

**Entity Type**

SQS : Queue (similar to JMS, MSMQ).

SNS : Topic-Subscriber (Pub/Sub system).

**Message consumption**

SQS : Pull Mechanism — Consumers poll messages from SQS.

SNS : Push Mechanism — SNS pushes messages to consumers.

**Persistence**

SQS : Messages are persisted for some duration is no consumer available. The retention period value is from 1 minute to 14 days. The default is 4 days.

SNS : No persistence. Whichever consumer is present at the time of message arrival, get the message and the message is deleted. If no consumers available then the message is lost.

In SQS the message delivery is guaranteed but in SNS it is not.

**Consumer Type**

SQS : All the consumers are supposed to be identical and hence process the messages in exact same way.

SNS : All the consumers are (supposed to be) processing the messages in different ways.

## **EventBridge**

**Pattern**
  - Message bus
  - Events
  - Rules
  - Targets

**What is an EventBridge**

EventBridge is a serverless service that uses events to connect application components together, making it easier for you to build scalable event-driven applications. Use it to route events from sources such as home-grown applications, AWS services, and third- party software to consumer applications across your organization. EventBridge provides a simple and consistent way to ingest, filter, transform, and deliver events so you can build new applications quickly.

EventBridge event buses are well suited for many-to-many routing of events between event-driven services. EventBridge Pipes is intended for point-to-point integrations between these sources and targets, with support for advanced transformations and enrichment.

- in general, AWS eventbridge is similar to AWS SNS with specific rule sets.

**Summary**

   * In summary, AWS EventBridge is a powerful event bus that allows you to easily integrate different systems and services, while AWS SNS is a messaging service that enables you to send messages to a wide range of endpoints and SQS is messaging service that enables you to send, store, and receive messages between different applications and services and decouple and scale them. 
   * Both services are highly scalable and reliable, and can be used to build highly responsive and resilient applications. However, depending on the use case, one service may be more appropriate than the other.

## **Project architecture**

...

# **Phase two**

This phase consist of the actual development of the application and we are going to go through the following:
   
   * Initialize, deploy and run an AWS SAM hello world project 
   
      *  Initialize the sample Hello World application
      *  Build your application
      *  Deploy your application to the AWS Cloud
      *  Run your application
  
   * A brief explanation of:
  
      * AWS SAM template.yaml file
      * Functions,
      * API gatways and how they all function
  
   * Implement authentication with Cognito
  
   ...

   ## **AWS SAM prerequisites**
   
   Before we begin you have to make sure you have the following things checked.

   1. Sign up for an AWS account
   2. Create an IAM user account
   3. Create an access key ID and secret access key
   4. Install the AWS CLI
   5. Use the AWS CLI to configure AWS credentials
   


# **1. Initialize, deploy and run an AWS SAM hello world project**

## **Step one: Initialize the sample Hello World application**

In this step, you will use the AWS SAM CLI to create a sample Hello World application project on your local machine.

**To initialize the sample Hello World application**

1. Open up the folder directory in which you would want your SAM application to be created in the editor of your choice be it sublime text, VS code etc. But in my case am using VS code.
2. In your command line, run the following:
      
```
   sam init
```
      
3. The AWS SAM CLI will guide you through initializing a new application. Configure the following:

   * Select AWS Quick Start Templates to choose a starting template.

   * Choose the Hello World Example template and download it.

   * Use the Python runtime and zip package type.

   * For this tutorial, opt out of AWS X-Ray tracing.

   * For this tutorial, opt out of monitoring with Amazon CloudWatch Application Insights. 

   * Name your application as python-sam-ecom.

   * To use the AWS SAM CLI interactive flow:

      * Brackets ([ ]) indicate default values. Leave your answer blank to select the default value.

      * Enter y for yes, and n for no.

   * The following is an example of the sam init interactive flow:

         
   ```
      sam init
      ...
      Which template source would you like to use?
         1 - AWS Quick Start Templates
         2 - Custom Template Location
      Choice: 1

      Choose an AWS Quick Start application template
         1 - Hello World Example
         2 - Multi-step workflow
         3 - Serverless API
         4 - Scheduled task
         5 - Standalone function
         6 - Data processing
         7 - Hello World Example With Powertools
         8 - Infrastructure event management
         9 - Serverless Connector Hello World Example
         10 - Multi-step workflow with Connectors
         11 - Lambda EFS example
         12 - DynamoDB Example
         13 - Machine Learning
      Template: 1

      Use the most popular runtime and package type? (Python and zip) [y/N]: y

      Would you like to enable X-Ray tracing on the function(s) in your application?  [y/N]: 

      Would you like to enable monitoring using CloudWatch Application Insights? [y/N]: 

      Project name [python-sam-ecom]: 

   ```

4. The AWS SAM CLI downloads your starting template and creates the application project directory structure on your local machine. The following is an example of the AWS SAM CLI output:

   ```
      Cloning from https://github.com/aws/aws-sam-cli-app-templates (process may take a moment)

      -----------------------
      Generating application:
      -----------------------
      Name: python-sam-ecom
      Runtime: python3.9
      Architectures: x86_64
      Dependency Manager: pip
      Application Template: hello-world
      Output Directory: .
      Configuration file: python-sam-ecom/samconfig.toml

      Next steps can be found in the README file at python-sam-ecom/README.md

      Commands you can use next
      =========================
      [*] Create pipeline: cd python-sam-ecom && sam pipeline init --bootstrap
      [*] Validate SAM template: cd python-sam-ecom && sam validate
      [*] Test Function in the Cloud: cd python-sam-ecom && sam sync --stack-name {stack-name} --watch

   ```

5. From your command line, move to the newly created python-sam-ecom directory. The following is an example of what the AWS SAM CLI has created:
      
   ```
      cd python-sam-ecom

      tree

      ├── README.md
      ├── __init__.py
      ├── events
      │   └── event.json
      ├── hello_world
      │   ├── __init__.py
      │   ├── app.py
      │   └── requirements.txt
      ├── samconfig.toml
      ├── template.yaml
      └── tests
         ├── __init__.py
         ├── integration
         │   ├── __init__.py
         │   └── test_api_gateway.py
         ├── requirements.txt
         └── unit
            ├── __init__.py
            └── test_handler.py
            
      6 directories, 14 files
   ```

   Some important files to highlight:

      * hello_world/app.py – Contains your Lambda function code.

      * hello_world/requirements.txt – Contains any Python dependencies that your Lambda function requires.

      * samconfig.toml – Configuration file for your application that stores default parameters used by the AWS SAM CLI.

      * template.yaml – The AWS SAM template that contains your application infrastructure code.

   You now have a completely authored serverless application on your local machine!

## **Step two: Build your application**

In this step, you use the AWS SAM CLI to build your application and prepare for deployment. When you build, the AWS SAM CLI creates a .aws-sam directory and organizes your function dependencies, project code, and project files there.

**To build your application**
      
* In your command line, from the python-sam-ecom project directory, run the following:
      
```
   sam build
```

After running the **sam buld**, the following is a shortened example of the .aws-sam directory created by the AWS SAM CLI:

```.aws-sam
   ├── build
   │   ├── HelloWorldFunction
   │   │   ├── __init__.py
   │   │   ├── app.py
   │   │   └── requirements.txt
   │   └── template.yaml
   └── build.toml
```
      
Some important files to highlight:

   * build/HelloWorldFunction – Contains your Lambda function code and dependencies. The AWS SAM CLI creates a directory for each function in your application.

   * build/template.yaml – Contains a copy of your AWS SAM template that is referenced by AWS CloudFormation at deployment.

   * build.toml – Configuration file that stores default parameter values referenced by the AWS SAM CLI when building and deploying your application.

You are now ready to deploy your application to the AWS Cloud.

## **Step three: Deploy your application to the AWS Cloud**

In this step, you use the AWS SAM CLI to deploy your application to the AWS Cloud. The AWS SAM CLI will do the following:

* Guide you through configuring your application settings for deployment.

* Upload your application files to Amazon Simple Storage Service (Amazon S3).

* Transform your AWS SAM template into an AWS CloudFormation template. It then uploads your template to the AWS CloudFormation service to provision your AWS resources.

**To deploy your application**

1. In your command line, from the python-sam-ecom project directory, run the following:

  ```
     sam deploy --guided
  ```

2. Follow the AWS SAM CLI interactive flow to configure your application settings. Configure the following:

* The AWS CloudFormation stack name – A stack is a collection of AWS resources that you can manage as a single unit.

* The AWS Region to deploy your AWS CloudFormation stack to.

* For this tutorial, opt out of confirming changes before deploy.

* Allow IAM role creation – This lets AWS SAM create the IAM role necessary for your API Gateway resource and Lambda function resource to interact.

* For this tutorial, opt out of disabling rollback.

* Allow HelloWorldFunction without authorization defined – This message displays because your API Gateway endpoint is configured to be publicly accessible, without authorization. Since this is the intended configuration for your Hello World application, allow the AWS SAM CLI to continue.

* Save arguments to configuration file – This will update your application’s samconfig.toml file with your deployment preferences.

* Select the default configuration file name.

* Select the default configuration environment.

The following is an example output of the sam deploy --guided interactive flow:

```
   python-sam-ecom sam deploy --guided

   Configuring SAM deploy
   ======================

      Looking for config file [samconfig.toml] :  Found
      Reading default arguments  :  Success

      Setting default arguments for 'sam deploy'
      =========================================
      Stack Name [python-sam-ecom]:
      AWS Region [us-west-1]:
      #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
      Confirm changes before deploy [Y/n]: n
      #SAM needs permission to be able to create roles to connect to the resources in your template
      Allow SAM CLI IAM role creation [Y/n]: 
      #Preserves the state of previously provisioned resources when an operation fails
      Disable rollback [y/N]: 
      HelloWorldFunction may not have authorization defined, Is this okay? [y/N]: y
      Save arguments to configuration file [Y/n]: 
      SAM configuration file [samconfig.toml]:
      SAM configuration environment [default]:
```

1. The AWS SAM CLI deploys your application by doing the following:

* The AWS SAM CLI creates an Amazon S3 bucket and uploads your .aws-sam directory.

* The AWS SAM CLI transforms your AWS SAM template into AWS CloudFormation and uploads it to the AWS CloudFormation service.

* AWS CloudFormation provisions your resources.

With all that set, your application is now deployed and running in the AWS Cloud!

## **Step four: Run your application**

In this step, you will send a GET request to your API endpoint and see your Lambda function output.

**To get your API endpoint value**

4. From the information displayed by the AWS SAM CLI in the previous step, locate the Outputs section. In this section, locate your HelloWorldApi resource to find your HTTP endpoint value. The following is an example output:

```
   ----------------------------------------------------------------------------------------------------------------------------------------------
   Outputs
   ----------------------------------------------------------------------------------------------------------------------------------------------
   ...
   Key                 HelloWorldApi
   Description         API Gateway endpoint URL for Prod stage for Hello World function
   Value               https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod/hello/
   ...
   ----------------------------------------------------------------------------------------------------------------------------------------------
```

1. Alternatively, you can use the sam list endpoints --output json command to get this information. The following is an example output:

   ```
      sam list endpoints --output json
      2023-03-15 12:39:19 Loading policies from IAM...
      2023-03-15 12:39:25 Finished loading policies from IAM.
      [
      {
         "LogicalResourceId": "HelloWorldFunction",
         "PhysicalResourceId": "python-sam-ecom-HelloWorldFunction-yQDNe17r9maD",
         "CloudEndpoint": "-",
         "Methods": "-"
      },
      {
         "LogicalResourceId": "ServerlessRestApi",
         "PhysicalResourceId": "ets1gv8lxi",
         "CloudEndpoint": [
            "https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod",
            "https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Stage"
         ],
         "Methods": [
            "/hello['get']"
         ]
      }
      ]
   ```

**To invoke your function**
   
* Using your browser or the command line, send a GET request to your API endpoint. The following is an example using the curl command:

```
   curl https://ets1gv8lxi.execute-api.us-west-2.amazonaws.com/Prod/hello/
   {"message": "hello world"}
```

# **2. A brief explanation of the AWS SAM template.yaml file, functions, API gatways and how they all function**

## **AWS SAM template.yaml file**
        
After initializing and deploying your application, you will have a template.yaml file as below:

```
   AWSTemplateFormatVersion: '2010-09-09'
   Transform: AWS::Serverless-2016-10-31
   Description: Sample SAM Template for python-sam-ecom

   # More info about Globals: https://github.com/awslabs/serverless-application-model/blob/master/docs/globals.rst
   Globals:
      Function:
         Timeout: 3
         MemorySize: 128
   
   Resources:

      HelloWorldFunction:
         Type: AWS::Serverless::Function # More info about Function Resource: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#awsserverlessfunction
         Properties:
            CodeUri: hello_world/
            Handler: app.lambda_handler
            Runtime: python3.9
            Architectures:
            - x86_64
            Events:
            HelloWorld:
               Type: Api # More info about API Event Source: https://github.com/awslabs/serverless-application-model/blob/master/versions/2016-10-31.md#api
               Properties:
                  Path: /hello
                  Method: get

   Outputs:
      # ServerlessRestApi is an implicit API created out of Events key under Serverless::Function
      # Find out more about other implicit resources you can reference within SAM
      # https://github.com/awslabs/serverless-application-model/blob/master/docs/internals/generated_resources.rst#api
      HelloWorldApi:
         Description: "API Gateway endpoint URL for Prod stage for Hello World function"
         Value: !Sub "https://${ServerlessRestApi}.execute-api.${AWS::Region}.amazonaws.com/Prod/hello/"
      HelloWorldFunction:
         Description: "Hello World Lambda Function ARN"
         Value: !GetAtt HelloWorldFunction.Arn
      HelloWorldFunctionIamRole:
         Description: "Implicit IAM Role created for Hello World function"
         Value: !GetAtt HelloWorldFunctionRole.Arn
```  

AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: Sample SAM Template for python-sam-ecom

* AWSTemplateFormatVersion just definds the version 
* Transform is needed to tell AWS Cloudformation that this is a serverless transformation 
* Description simply describes the project 
* Globals:
   
   * Sometimes resources that you declare in an AWS SAM template have common configurations. For example, you might have an application with multiple AWS::Serverless::Function resources that have identical Runtime, Memory, VPCConfig, Environment, and Cors configurations. Instead of duplicating this information in every resource, you can declare them once in the Globals section and let your resources inherit them. 
   
   * The Globals section is supported by the AWS::Serverless::Function, AWS::Serverless::Api, AWS::Serverless::HttpApi, and AWS::Serverless::SimpleTable resources.

* Resources: 

   * The stack resources and their properties, such as an Amazon Elastic Compute Cloud (Amazon EC2) instance or an Amazon Simple Storage Service (Amazon S3) bucket. You can refer to resources in the Resources and Outputs sections of the template.

   * This section is similar to the Resources section of AWS CloudFormation templates. In AWS SAM templates, this section can contain AWS SAM resources in addition to AWS CloudFormation resources. 
   
   * In general, all AWS resources that are to be used in your project are defined in this section.
   
   
      
   
