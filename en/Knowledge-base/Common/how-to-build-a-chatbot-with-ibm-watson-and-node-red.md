---
title: How to Build a Chatbot with IBM Watson and Node-RED
description: 
published: true
date: 2023-02-24T07:33:23.737Z
tags: 
editor: markdown
dateCreated: 2023-02-24T07:33:16.732Z
---

- [IBM Watson 및 Node-RED로 챗봇을 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-chatbot-with-ibm-watson-and-node-red)
{.links-list}


# How to Build a Chatbot with IBM Watson and Node-RED

Nowadays, chatbots are widely used to communicate with customers or perform simple tasks, and their popularity is only increasing. Businesses are finding chatbots to be valuable because they can handle a high volume of requests 24/7 without getting tired, they don’t require breaks, and they can be deployed quickly and cheaply.

While there are many different ways to build a chatbot, in this article we will focus on how to build one using IBM Watson and Node-RED. Node-RED is a visual programming tool that runs on Node.js, and it makes it easy to wire together flows using the wide range of nodes in the palette. It also has a built-in library for interacting with IBM cloud services, including Watson.

## Setting up Node-RED

The first thing you need to do is set up Node-RED. If you don’t already have Node.js installed, you can download it from the [Node.js website](https://nodejs.org/en/).

Once you have Node.js installed, you can install Node-RED using the following command:

```
npm install -g node-red
```

Once Node-RED is installed, you can launch it by running the following command:

```
node-red
```

This will start the Node-RED server and open up the Node-RED web interface in your browser.

## Setting up Watson

Now that you have Node-RED up and running, you need to set up your IBM Watson services. You can do this by going to the [IBM Cloud catalog](https://catalog.cloud.ibm.com/) and creating a new instance of the following services:

- Watson Assistant
- Speech to Text
- Text to Speech

Once you have created your Watson services, you need to go to the **Service Credentials** tab for each service and create a new set of credentials. Be sure to copy these credentials somewhere safe, as you will need them later.

## Creating the Flow

Now that you have Node-RED and Watson set up, you can start creating your chatbot flow. To do this, go to the Node-RED web interface and click on the **Create new flow** button.

![Create new flow button](https://i.imgur.com/lU4kbjN.png)

This will open up the Node-RED flow editor. The first thing you need to do is drag a **http in** node from the palette and drop it onto the canvas.

![http in node](https://i.imgur.com/mUJygcT.png)

Next, double-click on the http in node to open up the node configuration. In the **URL** field, enter `/chatbot`. This will be the URL that your chatbot will be accessible at. In the **Method** field, select `POST`. Leave the **Name** field blank and click on the **Done** button.

![http in node configuration](https://i.imgur.com/pzMgASN.png)

Now, drag an **IBM Watson** node from the palette and drop it onto the canvas. Connect the **http in** node to the **IBM Watson** node.

![IBM Watson node](https://i.imgur.com/JjlbTGi.png)

Double-click on the **IBM Watson** node to open up the node configuration. In the **Service** field, select the **Assistant** service that you created earlier. In the **Assistant ID** field, enter the **Assistant ID** of your service. This can be found in the **Service Credentials** tab of your service. In the **API Key** field, enter the **API Key** of your service. This can also be found in the **Service Credentials** tab of your service.

![IBM Watson node configuration](https://i.imgur.com/vALDKJs.png)

Next, drag a **http response** node from the palette and drop it onto the canvas. Connect the **IBM Watson** node to the **http response** node.

![http response node](https://i.imgur.com/Wql4v1B.png)

Now, you need to configure the **IBM Watson** node to send the user input to Watson Assistant. To do this, double-click on the **IBM Watson** node to open up the node configuration. In the **Input** field, enter `{ "text": "$input.body" }`. This will send the user input to Watson Assistant as JSON in the format `{ "text": "user input" }`. In the **Output** field, leave the default value of `$output.intents[0].intent`. This will cause the node to output the first intent that Watson Assistant detects.

![IBM Watson node configuration](https://i.imgur.com/FtWfZoG.png)

Now, you need to configure the **http response** node to send the output of the **IBM Watson** node back to the user. To do this, double-click on the **http response** node to open up the node configuration. In the **Status code** field, enter `200`. This will send a successful HTTP response back to the user. In the **Message** field, enter `$output.text`. This will send the output text of the **IBM Watson** node back to the user.

![http response node configuration](https://i.imgur.com/eLKcnpz.png)

Now, you need to deploy your chatbot flow. To do this, click on the **Deploy** button in the top right corner of the screen.

![Deploy button](https://i.imgur.com/pzMgASN.png)

This will deploy your chatbot flow and make it accessible at the URL that you specified earlier.

## Testing the Chatbot

To test your chatbot, you can send a POST request to the URL that you specified earlier with a JSON body in the format `{ "text": "user input" }`.

For example, if you send the following JSON body to the chatbot URL:

```
{
  "text": "Hello"
}
```

The chatbot will respond with the following JSON body:

```
{
  "text": "Hello, how are you?"
}
```

You can also test your chatbot using the [cURL](https://curl.haxx.se/) command line tool. To do this, you can use the following command:

```
curl -X POST -H "Content-Type: application/json" -d '{"text": "Hello"}' <chatbot URL>
```

Replace `<chatbot URL>` with the URL of your chatbot.

## Conclusion

In this article, we have shown you how to build a chatbot using IBM Watson and Node-RED. We have also shown you how to test your chatbot using the cURL command line tool.

If you want to learn more about building chatbots, we recommend the following resources:

- [Building chatbots with Watson Assistant](https://www.ibm.com/cloud/garage/content/course/building-chatbots-with-watson-assistant/)
- [Build a chatbot with Watson Assistant](https://developer.ibm.com/patterns/build-a-chatbot-with-watson-assistant/)
- [How to build a chatbot](https://chatbotsmagazine.com/how-to-build-a-chatbot-4bca7aa8e4d0)