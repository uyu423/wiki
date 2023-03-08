---
title: 029: Deploying Nest.js applications to production
description: 
published: true
date: 2023-02-09T18:17:40.154Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:17:33.938Z
---

- [029: Implementación de aplicaciones Nest.js en producción***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/029-deploying-nest-js-applications-to-production)
{.links-list}
- [029：将 Nest.js 应用程序部署到生产环境***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/029-deploying-nest-js-applications-to-production)
{.links-list}
- [029: Nest.js 애플리케이션을 프로덕션에 배포***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/029-deploying-nest-js-applications-to-production)
{.links-list}


# Deploying Nest.js Applications to Production

## Introduction

Nest.js is a Node.js framework for building server-side applications. It is a relatively new framework and is gaining popularity due to its ease of use and scalability.

The Nest.js framework is based on the Express.js framework and uses TypeScript, a superset of JavaScript, for development.

Nest.js applications can be deployed to a variety of production environments, such as on-premises servers, cloud-based servers, or even to serverless environments.

In this post, we will focus on how to deploy a Nest.js application to a production environment.

## Prerequisites

Before we get started, there are a few things that you will need:

- A Nest.js application. If you don't have one, you can create a simple one using the Nest.js CLI.
- A production environment. This can be an on-premises server, a cloud-based server, or a serverless environment.
- A domain name. This is optional, but it is recommended if you want to make your application accessible to the world.

## Deploying to a Production Environment

There are two main ways to deploy a Nest.js application to a production environment:

- Deploying using a Nest.js-specific tool, such as the Nest.js CLI or the Nest.js Deployer.
- Deploying manually.

### Deploying Using a Nest.js-Specific Tool

The easiest way to deploy a Nest.js application to a production environment is to use a Nest.js-specific tool.

There are two main tools that can be used for this: the Nest.js CLI and the Nest.js Deployer.

The Nest.js CLI is a command-line interface that can be used to deploy Nest.js applications. It is installed as a global Node.js module and can be used to deploy applications to a variety of production environments, such as on-premises servers, cloud-based servers, or even to serverless environments.

To use the Nest.js CLI, you first need to install it using npm:

```
npm install -g @nestjs/cli
```

Once the Nest.js CLI is installed, you can use it to deploy your Nest.js application.

For example, to deploy your Nest.js application to an on-premises server, you would use the following command:

```
nest deploy --server=on-premises
```

This would deploy your Nest.js application to an on-premises server.

The Nest.js Deployer is a tool that can be used to deploy Nest.js applications to a variety of production environments, such as on-premises servers, cloud-based servers, or even to serverless environments.

To use the Nest.js Deployer, you first need to install it using npm:

```
npm install -g @nestjs/deployer
```

Once the Nest.js Deployer is installed, you can use it to deploy your Nest.js application.

For example, to deploy your Nest.js application to an on-premises server, you would use the following command:

```
deployer deploy --server=on-premises
```

This would deploy your Nest.js application to an on-premises server.

### Deploying Manually

If you don't want to use a Nest.js-specific tool to deploy your Nest.js application, you can deploy it manually.

To deploy your Nest.js application manually, you will need to:

- Build your Nest.js application.
- Deploy your application to your production environment.

#### Building Your Nest.js Application

The first step is to build your Nest.js application.

To do this, you will need to use the Nest.js CLI.

The Nest.js CLI is a command-line interface that can be used to build Nest.js applications. It is installed as a global Node.js module and can be used to build applications for a variety of production environments, such as on-premises servers, cloud-based servers, or even to serverless environments.

To use the Nest.js CLI, you first need to install it using npm:

```
npm install -g @nestjs/cli
```

Once the Nest.js CLI is installed, you can use it to build your Nest.js application.

For example, to build your Nest.js application for an on-premises server, you would use the following command:

```
nest build --server=on-premises
```

This would build your Nest.js application for an on-premises server.

#### Deploying Your Application to Your Production Environment

The next step is to deploy your application to your production environment.

How you deploy your application will depend on your production environment.

For example, if you are deploying to an on-premises server, you will need to use a tool like scp to copy your application files to the server.

If you are deploying to a cloud-based server, you will need to use a tool like AWS Elastic Beanstalk to deploy your application.

If you are deploying to a serverless environment, you will need to use a tool like AWS Lambda to deploy your application.

## Conclusion

In this post, we have covered how to deploy a Nest.js application to a production environment.

We have looked at two main ways to do this:

- Deploying using a Nest.js-specific tool, such as the Nest.js CLI or the Nest.js Deployer.
- Deploying manually.

Whichever method you choose, ensure that you test your application thoroughly in your production environment before making it available to your users.