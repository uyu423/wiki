---
title: AWS ECS: Deploying and Managing Docker Containers in the Cloud
description: 
published: true
date: 2023-02-16T00:18:00.173Z
tags: 
editor: markdown
dateCreated: 2023-02-16T00:17:51.798Z
---

- [AWS ECS: implementación y administración de contenedores Docker en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-ecs-deploying-and-managing-docker-containers-in-the-cloud)
{.links-list}
- [AWS ECS：在云中部署和管理 Docker 容器***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-ecs-deploying-and-managing-docker-containers-in-the-cloud)
{.links-list}
- [AWS ECS: 클라우드에서 Docker 컨테이너 배포 및 관리***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-ecs-deploying-and-managing-docker-containers-in-the-cloud)
{.links-list}


# AWS ECS: Deploying and Managing Docker Containers in the Cloud

Docker containers have become the standard for packaging and deploying applications in recent years. They offer a number of benefits over traditional virtual machines, including portability, reduced resource overhead, and easy integration with Continuous Integration/Continuous Delivery (CI/CD) pipelines.

AWS Elastic Container Service (ECS) is a managed container orchestration service that makes it easy to run and manage Docker containers in the cloud. In this article, we'll take a look at how to deploy and manage Docker containers on AWS ECS.

## Creating an ECS Cluster

The first step in using AWS ECS is to create an ECS cluster. An ECS cluster is a logical grouping of EC2 instances that are used to host your Docker containers. You can create an ECS cluster using the AWS Management Console, AWS Command Line Interface (CLI), or AWS SDK.

### Creating an ECS Cluster Using the AWS Management Console

To create an ECS cluster using the AWS Management Console, first open the Amazon ECS console and select the "Clusters" link in the left-hand navigation. Then, click the "Create Cluster" button.

On the "Create Cluster" page, select the "Networking only" template and give your cluster a name. Then, click the "Create" button.

Your cluster will now be created and you can view it in the "Clusters" list.

### Creating an ECS Cluster Using the AWS CLI

To create an ECS cluster using the AWS CLI, first create a file named "ecs-cli-cluster.json" with the following contents:

```json
{
    "clusterName": "my-ecs-cluster",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

Replace the values in the "clusterName", "subnets", and "securityGroups" fields with the appropriate values for your environment. Then, run the following command to create the cluster:

```
aws ecs create-cluster --cli-input-json file://ecs-cli-cluster.json
```

## Creating an ECS Task Definition

Now that you have an ECS cluster, you can deploy applications to it. An application in ECS is defined by a task definition, which specifies the Docker images and other resources that are needed to run the application.

You can create a task definition using the AWS Management Console, AWS CLI, or AWS SDK.

### Creating a Task Definition Using the AWS Management Console

To create a task definition using the AWS Management Console, first open the Amazon ECS console and select the "Task Definitions" link in the left-hand navigation. Then, click the "Create new Task Definition" button.

On the "Select launch type" page, select the "EC2" launch type and click the "Next Step" button.

On the "Configure task and container definitions" page, give your task a name and description. Then, scroll down to the "Container Definitions" section and click the "Add container" button.

In the "Add container" modal, enter the following values:

- **Container name:** my-container
- **Image:** nginx:latest
- **Memory limit (MiB):** 512
- **Port mappings:** 80:80

Then, click the "Add" button.

Your container will now be added to the task definition. Scroll down to the "Task Role" section and select the "None" option. Then, scroll down to the "Network Mode" section and select the "bridge" option. Finally, click the "Next Step" button.

On the "Review" page, review your task definition and click the "Create" button.

Your task definition will now be created and you can view it in the "Task Definitions" list.

### Creating a Task Definition Using the AWS CLI

To create a task definition using the AWS CLI, first create a file named "ecs-cli-task-definition.json" with the following contents:

```json
{
    "family": "my-task-definition",
    "networkMode": "bridge",
    "containerDefinitions": [
        {
            "name": "my-container",
            "image": "nginx:latest",
            "memory": 512,
            "portMappings": [
                {
                    "containerPort": 80,
                    "hostPort": 80
                }
            ]
        }
    ]
}
```

Replace the values in the "family" and "containerDefinitions" fields with the appropriate values for your environment. Then, run the following command to create the task definition:

```
aws ecs register-task-definition --cli-input-json file://ecs-cli-task-definition.json
```

## Deploying an Application to an ECS Cluster

Now that you have an ECS cluster and a task definition, you can deploy your application to the cluster. You can deploy an application to an ECS cluster using the AWS Management Console, AWS CLI, or AWS SDK.

### Deploying an Application Using the AWS Management Console

To deploy an application using the AWS Management Console, first open the Amazon ECS console and select the "Clusters" link in the left-hand navigation. Then, select the cluster that you want to deploy to and click the "Tasks" tab.

On the "Tasks" tab, click the "Run new task" button.

On the "Configure task and container settings" page, select the "my-task-definition" task definition and click the "Next Step" button.

On the " Configure network" page, select the "bridge" network mode and click the "Next Step" button.

On the "Review" page, review your task settings and click the "Run Task" button.

Your task will now be deployed to the cluster and you can view its status in the "Tasks" tab.

### Deploying an Application Using the AWS CLI

To deploy an application using the AWS CLI, first create a file named "ecs-cli-run-task.json" with the following contents:

```json
{
    "taskDefinition": "my-task-definition",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

Replace the values in the "taskDefinition", "subnets", and "securityGroups" fields with the appropriate values for your environment. Then, run the following command to deploy the task:

```
aws ecs run-task --cli-input-json file://ecs-cli-run-task.json
```

## Monitoring an ECS Cluster

AWS ECS offers a number of tools for monitoring your cluster and the tasks that are running on it.

The first tool is CloudWatch. CloudWatch is a AWS service that collects and processes monitoring data for AWS resources, including ECS clusters. You can use CloudWatch to view metrics for your ECS cluster, set alarms, and view logs.

The second tool is Amazon CloudWatch Logs. CloudWatch Logs is a service that you can use to monitor, store, and access log files from AWS resources, including ECS clusters. You can use CloudWatch Logs to view logs for your ECS cluster and the tasks that are running on it.

The third tool is Amazon CloudWatch Events. CloudWatch Events is a service that you can use to monitor events from AWS resources, including ECS clusters. You can use CloudWatch Events to view events for your ECS cluster and the tasks that are running on it.

## Deleting an ECS Cluster

If you no longer need an ECS cluster, you can delete it using the AWS Management Console, AWS CLI, or AWS SDK.

### Deleting an ECS Cluster Using the AWS Management Console

To delete an ECS cluster using the AWS Management Console, first open the Amazon ECS console and select the "Clusters" link in the left-hand navigation. Then, select the cluster that you want to delete and click the "Delete" button.

On the "Delete Cluster" page, review the information about the cluster and click the "Delete" button.

Your cluster will now be deleted.

### Deleting an ECS Cluster Using the AWS CLI

To delete an ECS cluster using the AWS CLI, run the following command:

```
aws ecs delete-cluster --cluster my-ecs-cluster
```

## Conclusion

In this article, we've looked at how to deploy and manage Docker containers on AWS ECS. We've seen how to create an ECS cluster, create a task definition, and deploy an application to the cluster. We've also seen how to monitor an ECS cluster using CloudWatch. Finally, we've seen how to delete an ECS cluster.