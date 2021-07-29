## Rolling Update In AWS ECS

**Overview**

  1. What is AWS ECS?

      - Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that offers simplfied deploy, manage, and scale containerized applications. It deeply integrates with the rest of the AWS platform to provide a secure and easy-to-use solution for running container workloads in the cloud.

      - Amazon ECS are a particularly attractive delivery vehicle for CI/CD for the following reasons

        - Speed in terms of deployment

        - Revision control through image tagging

        - Single artifact from local to production

      - Below are the keys of ECS

        - **Task definition**: The task definition is a text file, in JSON format that allow to specify details like launch type, CPU and memory requirements, ports to be opened, and data volumes should be used with the containers in the task.

        - **Task**: A task is the instantiation of a task definition within a cluster

        - **Service**: An Amazon ECS service allows to run and maintain a specified number of instances of a task definition 

  2. What is CI/CD?

      - Continuous Integration: The practice of automating the integration of code changes from multiple contributors into a single software project 

      - Continuous Delivery: A methodology in which teams ensure that the application can be reliably released at any time, but which still relies on human intervention to determine what gets pushed into production.

      - Continuous Deployment: This process takes continuous delivery a step further by automatically deploying all releases into production

  3. How does AWS enable CI/CD?

      - AWS offers different services which simplify to configure CI/CD pipelines, and further templatize these pipelines to promote the reusability for multiple services. Relevant AWS services include:

        - AWS CodeCommit as source code repositories

        - AWS CodeBuild for building service artifacts

        - AWS CodeDeploy for deploying artifacts into environments

        - AWS CodePipline to manage the end-to-end control flow of a change from source through to deployment.

        - AWS CloudFormation to deploy and update infrastructure resources.

  4. What is rolling update in AWS ECS?

      - In rolling update, Amazon ECS service scheduler swap the currently running tasks with new tasks. The number of tasks that Amazon ECS adds or removes from the service during a rolling update is managed by the deployment configuration. The deployment configuration consists of the minimumHealthyPercent and maximumPercent, both of these values are very important to ensure ECS task is up & running during updates.

      - The minimumHealthyPercent represents the lower limit on the number of tasks that should be running for a service during a deployment or when a container instance is draining, as a percent of the desired number of tasks for the service

      - The maximumPercent represents the upper limit on the number of tasks that should be running for a service during a deployment or when a container instance is draining, as a percent of the desired number of tasks for a service. 

**Tutorial**

  - In this section we will perform rolling updates on AWS ECS services, by:
  
      - Prerequisite 

          - Launch a bare AWS ECS cluster 

          - Configure AWS ECS repo and AWS CodeCommit 

      - Deploy a HelloWorld ECS task on the bare cluster

      - Configure AWS CodePipeline

      - Perform Rolling Update

  -  Prerequisite
      
      - Launch a bare AWS ECS cluster 

          - In this demo, we will use ECS cluster running in a VPC

          - The cluster is deployed over 2AZs, with the container instances sitting in private subnets. We then use a public ALB to enable container services to be exposed to the public Internet, and a NAT Gateway to enable services to access the public Internet
          
          - Download the <a href="https://github.com/sanchitdilipjain/rolling-update-in-ecs/blob/main/ecs-cft.json">cloudformation template</a> from this link and Deploy it 
            
          - The setup for each cluster is shown below
  
             <img src="images/image1.png" class="inline" width="700" height="700"/> 
          
          - Once the Cloudformation stack is deployed successfully please capture all the output values
             
             <img src="images/image2.png" class="inline" width="700" height="400"/> 

      - Configure AWS ECS repo and AWS CodeCommit 
  
          - Download the <a href="https://github.com/sanchitdilipjain/rolling-update-in-ecs/blob/main/cloudformation.json">cloudformation template</a> from this link and Deploy it

          - Once the Cloudformation stack is deployed successfully please capture all the output values like AWS ECR, AWS CodeCommit, CloudWatch LogGroup name etc
          
            <img src="images/image3.png" class="inline" width="700" height="200"/> 
          
          - Prepare the source code to deliver into the code commit repo we deployed recently
          
              - Download & Unzip the <a href="https://github.com/sanchitdilipjain/aws-glue-databrew/blob/main/cloudformation.json">code base</a> that we will store into code commit 
              
              - Run below commands to clone & initialise the empty code commit repository and upload the code 
                  
                    mkdir docker-app
                    cd ~/docker-app
                    git clone SRC_REPO_URL docker-app
              

    

  

