---
title: Case Study: Developing and Launching a Simple Chat Application on Azure
description: 
published: true
date: 2023-02-19T07:06:28.138Z
tags: 
editor: markdown
dateCreated: 2023-02-19T07:06:26.671Z
---

- [사례 연구: Azure에서 간단한 채팅 애플리케이션 개발 및 실행***Korean** document is available*](/ko/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-chat-application-on-azure)
{.links-list}


# Case Study: Developing and Launching a Simple Chat Application on Azure

In this article, we'll walk through the process of developing and launching a simple chat application on Azure. We'll cover the following topics:

*Creating a chat application using the Azure portal
*Configuring the chat application
*Deploying the chat application to Azure

## Creating a chat application using the Azure portal

To create a chat application using the Azure portal, follow these steps:

1. Sign in to the Azure portal.

2. In the left-hand navigation pane, click **Create a resource**.

3. In the **Search the Marketplace** field, enter "chatbot" and press Enter.

4. In the search results, click **Chatbot Service (preview)**.

5. On the **Chatbot Service (preview)** page, click **Create**.

6. On the **Create** page, enter the following information:

* **Bot name**: Enter a name for your chatbot.

* **Subscription**: Select your Azure subscription.

* **Location**: Select the location for your chatbot.

* **Pricing tier**: Select the pricing tier for your chatbot.

* **Resource group**: Select an existing resource group or create a new one.

* **Application Insights**: Select whether to create a new Application Insights resource or use an existing one.

* **Storage account**: Select whether to create a new storage account or use an existing one.

* **App service plan**: Select whether to create a new App service plan or use an existing one.

7. Click **Create**.

Your chatbot will be created and deployed to Azure.

## Configuring the chat application

Once the chatbot has been created, you can configure it by clicking on the **Configure** tab in the Azure portal. From here, you can do the following:

* **Basic settings**: Configure the chatbot's name, description, avatar, and time zone.

* **Channels**: Configure the chatbot's channels, such as Facebook, Slack, Microsoft Teams, etc.

* **Features**: Configure the chatbot's features, such as language understanding, QnA Maker, and web app integration.

* **Connections**: Configure the chatbot's connections, such as Azure Active Directory, Bot Framework, and LUIS.

* **Test in Web Chat**: Test the chatbot in the Web Chat channel.

* **Publish**: Publish the chatbot to Azure.

## Deploying the chat application to Azure

Deploying the chatbot to Azure is a two-step process. First, you need to create a web app in Azure and then deploy the chatbot to that web app.

To create a web app in Azure, follow these steps:

1. Sign in to the Azure portal.

2. In the left-hand navigation pane, click **Create a resource**.

3. In the **Search the Marketplace** field, enter "web app" and press Enter.

4. In the search results, click **Web App**.

5. On the **Web App** page, click **Create**.

6. On the **Create** page, enter the following information:

* **Name**: Enter a name for your web app.

* **Subscription**: Select your Azure subscription.

* **Resource group**: Select an existing resource group or create a new one.

* **OS**: Select the operating system for your web app.

* **Runtime stack**: Select the runtime stack for your web app.

* **Region**: Select the region for your web app.

* **Application insights**: Select whether to create a new Application Insights resource or use an existing one.

7. Click **Create**.

Your web app will be created in Azure.

To deploy the chatbot to the web app, follow these steps:

1. Sign in to the Azure portal.

2. In the left-hand navigation pane, click on the chatbot that you want to deploy.

3. In the chatbot's overview page, click on the **Deploy** button.

4. In the **Deploy to web app** blade, select the web app that you want to deploy the chatbot to and click **Deploy**.

5. In the **Summary** blade, verify the deployment settings and click **Deploy**.

The chatbot will be deployed to the web app.