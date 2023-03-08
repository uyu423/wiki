---
title: Kubernetes on AWS: Deploying Clusters on Amazon Web Services
description: 
published: true
date: 2023-02-01T00:06:07.773Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:06:03.872Z
---

- [AWS의 Kubernetes: Amazon Web Services에 클러스터 배포***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-on-aws-deploying-clusters-on-amazon-web-services)
{.links-list}
- [AWS での Kubernetes: アマゾン ウェブ サービスでのクラスターのデプロイ***Japanese** version of this document is available*](/ja/Knowledge-base/Kubernetes/kubernetes-on-aws-deploying-clusters-on-amazon-web-services)
{.links-list}
- [AWS 上的 Kubernetes：在 Amazon Web Services 上部署集群***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-on-aws-deploying-clusters-on-amazon-web-services)
{.links-list}



# Kubernetes on AWS: Deploying Clusters on Amazon Web Services

Kubernetes is an open-source container-orchestration system for automating application deployment, scaling, and management. It groups containers that make up an application into logical units for easy management and discovery.

AWS is a comprehensive, evolving cloud computing platform provided by Amazon. It offers a mix of infrastructure as a service (IaaS), platform as a service (PaaS) and packaged software as a service (SaaS) offerings.

You can use Kubernetes on AWS to deploy, manage, and scale containerized applications on AWS. In this article, we will show you how to deploy a Kubernetes cluster on AWS.

## Prerequisites

To follow this guide, you will need the following:

- An AWS account. If you don't have one, you can create one [here](https://aws.amazon.com/).

- The AWS Command Line Interface (CLI) installed and configured on your machine. You can find instructions on how to do that [here](https://docs.aws.amazon.com/cli/latest/userguide/installing.html).

- The kubectl command line tool installed on your machine. You can find instructions on how to do that [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

- A domain name. You can get one for free from a service like [Freenom](https://www.freenom.com/).

## Setting up an AWS Kubernetes Cluster

There are many ways to set up a Kubernetes cluster on AWS. In this article, we will use the AWS Management Console to set up our cluster.

First, log in to the AWS Management Console and navigate to the Amazon EKS service.

![](https://i.imgur.com/LDAd5u8.png)

Click the "Create Cluster" button.

![](https://i.imgur.com/p0bJUO4.png)

On the next page, enter a name for your cluster and choose the region you want to deploy it in. Then, choose the Kubernetes version you want to use. We will use the latest version, which at the time of writing is 1.17.

![](https://i.imgur.com/Ft7YIxu.png)

Next, we need to configure our worker nodes. Worker nodes are the machines in our cluster that will run our applications. We will use Amazon EC2 instances for our worker nodes.

Click the "Launch CloudFormation Stack" button.

![](https://i.imgur.com/O4E0b4I.png)

On the next page, select the "I acknowledge that AWS CloudFormation might create IAM resources" checkbox and click the "Create Stack" button.

![](https://i.imgur.com/VkzM0Ss.png)

On the next page, you will see a stack being created in CloudFormation. This will take a few minutes.

![](https://i.imgur.com/W0Qiu8D.png)

Once the stack has been created, you can click the "Outputs" tab to see the details of our worker node configuration.

![](https://i.imgur.com/tY0NVT3.png)

Make a note of the "NodeInstanceRole" and "WorkerNodeSecurityGroup" values, as we will need them later.

Now that our worker nodes are set up, we can go back to the Amazon EKS console and create our cluster.

Click the "Next Step" button.

![](https://i.imgur.com/Ft7YIxu.png)

On the next page, we need to configure our worker nodes. Choose the number of worker nodes you want to have and enter the "NodeInstanceRole" and "WorkerNodeSecurityGroup" values that we noted down earlier.

![](https://i.imgur.com/vALDKQi.png)

Next, we need to configure our networking. Choose the "VPC" option and select the VPC that was created by our CloudFormation stack. Then, choose the "Subnets" option and select the two subnets that were created by our CloudFormation stack.

![](https://i.imgur.com/7DpjTGi.png)

Now, we need to choose a Kubernetes cluster endpoint access type. Choose the "Public" option.

![](https://i.imgur.com/DY0b4oI.png)

Next, we need to configure our security groups. Choose the "Security groups" option and select the security group that was created by our CloudFormation stack.

![](https://i.imgur.com/4JcM0Ss.png)

Now, we need to choose a Kubernetes cluster logging type. Choose the "Amazon CloudWatch" option.

![](https://i.imgur.com/BkzM0Ss.png)

Next, we need to choose a Kubernetes cluster monitoring type. Choose the "Amazon CloudWatch" option.

![](https://i.imgur.com/nALDKQi.png)

Now, we need to choose a Kubernetes cluster encryption type. Choose the "AES-256" option.

![](https://i.imgur.com/p0bJUO4.png)

Now, we need to choose a Kubernetes cluster auto-scaling group type. Choose the "AsgBasedAutoScaling" option.

![](https://i.imgur.com/FkzM0Ss.png)

Now, we need to configure our worker node auto-scaling group. Choose the "WorkerNodesAsg" option and select the auto-scaling group that was created by our CloudFormation stack.

![](https://i.imgur.com/VkzM0Ss.png)

Now, we need to choose a Kubernetes cluster scaling configuration type. Choose the "Default" option.

![](https://i.imgur.com/p0bJUO4.png)

On the next page, review your cluster configuration and click the "Create Cluster" button.

![](https://i.imgur.com/LDAd5u8.png)

On the next page, you will see your cluster being created. This will take a few minutes.

![](https://i.imgur.com/W0Qiu8D.png)

Once the cluster has been created, you can click the "Configure kubectl" button to configure the kubectl command line tool to communicate with our cluster.

![](https://i.imgur.com/nALDKQi.png)

On the next page, click the "Download Config" button.

![](https://i.imgur.com/7DpjTGi.png)

This will download a kubeconfig file to your machine. Move this file to the ~/.kube directory and rename it to config.

Now, we can test that our cluster is working by running the following command:

```
kubectl get svc
```

If everything is working correctly, you should see a list of services in your cluster.

## Deploying an Application on our Kubernetes Cluster

Now that our Kubernetes cluster is up and running, we can deploy an application on it. For this example, we will deploy a simple "Hello World" application written in Go.

First, we need to create a Dockerfile for our application. Create a file called "Dockerfile" in the root of our project with the following contents:

```
FROM golang:1.13-alpine

RUN mkdir /app

ADD . /app/

WORKDIR /app

RUN go build -o main .

CMD ["/app/main"]
```

Next, we need to write our application code. Create a file called "main.go" in the root of our project with the following contents:

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

Now, we can build our Docker image and push it to a Docker registry. We will use Amazon ECR for our Docker registry.

First, we need to create a new repository in Amazon ECR. Log in to the Amazon ECR console and click the "Create repository" button.

![](https://i.imgur.com/tY0NVT3.png)

On the next page, enter a name for your repository and click the "Create repository" button.

![](https://i.imgur.com/nALDKQi.png)

Now, we can build our Docker image and push it to our new repository.

Run the following commands to build and push our Docker image:

```
$ docker build -t {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name} .

$ docker push {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
```

Replace {your_aws_account_id}, {your_region} and {your_repository_name} with the appropriate values for your account and repository.

Now that our Docker image is pushed to our repository, we can deploy it on our Kubernetes cluster.

First, we need to create a deployment file. Create a file called "deployment.yaml" in the root of our project with the following contents:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
        ports:
        - containerPort: 8080
```

Replace {your_aws_account_id}, {your_region} and {your_repository_name} with the appropriate values for your account and repository.

Now, we can deploy our application on our Kubernetes cluster by running the following command:

```
kubectl apply -f deployment.yaml
```

This will create a deployment called "hello-world" with three replicas.

To see our deployment in action, we need to expose it to the outside world. We can do this by creating a service.

First, we need to create a service file. Create a file called "service.yaml" in the root of our project with the following contents:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: hello-world
```

Now, we can deploy our service by running the following command:

```
kubectl apply -f service.yaml
```

This will create a service called "hello-world" of type "LoadBalancer". This type of service will create a load balancer in AWS and expose our deployment to the outside world.

To find out the URL of our load balancer, run the following command:

```
kubectl get svc hello-world
```

You should see an output similar to the following:

```
NAME           TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
hello-world    LoadBalancer   10.100.200.16   aaa.bbb.ccc.ddd   80:32000/TCP,443:31943/TCP   5m29s
```

The "EXTERNAL-IP" value is the URL of our load balancer.

## Deleting our Kubernetes Cluster

If you want to delete your Kubernetes cluster, you can do so from the Amazon EKS console.

First, log in to the Amazon EKS console and navigate to the "Clusters" page.

![](https://i.imgur.com/LDAd5u8.png)

On the next page, select the checkbox next to the cluster you want to delete and click the "Delete" button.

![](https://i.imgur.com/7DpjTGi.png)

On the next page, enter the name of your cluster in the "Cluster name" field and click the "Delete Cluster" button.

![](https://i.imgur.com/p0bJUO4.png)

## Conclusion

In this article, we have shown you how to deploy a Kubernetes cluster on AWS. We have also shown you how to deploy an application on your cluster.

If you want to learn more about Kubernetes, we recommend the following resources:

- The official Kubernetes documentation: https://kubernetes.io/docs/

- The official Amazon EKS documentation: https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html

- The official Amazon ECR documentation: https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html