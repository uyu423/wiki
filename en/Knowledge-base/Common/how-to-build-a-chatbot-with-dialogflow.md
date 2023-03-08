---
title: How to Build a Chatbot with Dialogflow
description: 
published: true
date: 2023-03-04T03:32:46.497Z
tags: 
editor: markdown
dateCreated: 2023-03-04T03:32:39.203Z
---

- [Dialogflow로 챗봇을 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-chatbot-with-dialogflow)
{.links-list}
How to Build a Chatbot with Dialogflow

In today's age of digital communication, chatbots have become a popular tool for businesses to automate their customer service and support. Dialogflow, formerly known as API.ai, is a natural language processing (NLP) platform that enables developers to build robust chatbots for various platforms.

In this tutorial, we will walk you through the process of building a chatbot with Dialogflow. We will cover the following topics:

- Creating a Dialogflow agent
- Adding intents to the agent
- Adding entities to the agent
- Implementing fulfillment
- Integrating the chatbot with a web application

## Creating a Dialogflow Agent

A Dialogflow agent is the core component of a chatbot. It contains all the intents, entities, and fulfillment logic required to build a conversational interface. To create a Dialogflow agent, follow these steps:

1. Sign in to the Dialogflow console.
2. Click on the Create Agent button.
3. Enter a name for the agent and select the default language and time zone.
4. Click on the Create button.

![Creating a Dialogflow Agent](https://i.imgur.com/vy8uSed.png)

## Adding Intents to the Agent

Intents are the building blocks of a chatbot. They represent the user's intention or goal behind the conversation. To add an intent to the agent, follow these steps:

1. Click on the Intents tab in the left-hand menu.
2. Click on the Create Intent button.
3. Enter a name for the intent and provide some sample phrases that the user might say to trigger the intent.
4. Add training phrases to the intent by clicking on the Add Training Phrases button and entering the phrases.
5. Specify the actions that should be taken when the intent is triggered by adding a response or a fulfillment webhook.

![Adding Intents to the Agent](https://i.imgur.com/fyFhLwB.png)

## Adding Entities to the Agent

Entities are used to extract specific pieces of information from the user's input. For example, if the user asks for a weather update, the entity would extract the location for which the weather is being requested. To add an entity to the agent, follow these steps:

1. Click on the Entities tab in the left-hand menu.
2. Click on the Create Entity button.
3. Enter a name for the entity and add synonyms and examples for the entity values.
4. Save the entity.

![Adding Entities to the Agent](https://i.imgur.com/m5y5W5y.png)

## Implementing Fulfillment

Fulfillment is the logic that executes when an intent is triggered. It can be used to provide a response to the user, call an external API, or perform any other custom logic. Dialogflow supports two types of fulfillment:

- Inline Editor: Allows you to write fulfillment logic in Node.js directly within the Dialogflow console.
- Webhook: Allows you to use an external service to handle fulfillment.

To implement fulfillment using the Inline Editor, follow these steps:

1. Click on the Fulfillment tab in the left-hand menu.
2. Enable the Inline Editor by toggling the switch.
3. Write the fulfillment logic in the index.js file within the editor.

```javascript
function weatherHandler(agent) {
  const city = agent.parameters.city;
  const apiKey = "YOUR_API_KEY";
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}`;
  return axios.get(url)
    .then((response) => {
      const weather = response.data.weather[0].description;
      const temperature = response.data.main.temp;
      agent.add(`The weather in ${city} is ${weather} with a temperature of ${temperature} degrees.`);
    })
    .catch((error) => {
      console.log(error);
      agent.add(`I'm sorry, I couldn't find the weather for ${city}.`);
    });
}

let intentMap = new Map();
intentMap.set('Get Weather', weatherHandler);
agent.handleRequest(intentMap);
```

To implement fulfillment using a webhook, follow these steps:

1. Click on the Fulfillment tab in the left-hand menu.
2. Enter the URL for the webhook service in the Webhook URL field.
3. Save the changes.

## Integrating the Chatbot with a Web Application

After creating the chatbot, it can be integrated with a web application using the Dialogflow Messenger integration or the Dialogflow API. The Dialogflow Messenger integration provides an easy way to add a chatbot to a website without requiring any code changes. To integrate the chatbot using the Dialogflow Messenger integration, follow these steps:

1. Click on the Integrations tab in the left-hand menu.
2. Click on the Dialogflow Messenger tile.
3. Configure the appearance and behavior of the chatbot.
4. Copy the integration code and paste it into the web application.

Alternatively, the chatbot can be integrated with a web application using the Dialogflow API. This requires making HTTP requests to the API using a client library or HTTP client such as Axios. To integrate the chatbot using the Dialogflow API, follow these steps:

1. Create a new service account in the Google Cloud Console.
2. Download the service account key and save it as a JSON file.
3. Install the Dialogflow client library using npm.

```bash
npm install dialogflow
```

4. Use the client library to make requests to the Dialogflow API.

```javascript
const dialogflow = require('dialogflow');
const uuid = require('uuid');

const sessionId = uuid.v4();
const sessionClient = new dialogflow.SessionsClient({
  keyFilename: 'path/to/service-account-key.json'
});
const sessionPath = sessionClient.sessionPath('PROJECT_ID', sessionId);

async function sendMessageToDialogFlow(message) {
  const request = {
    session: sessionPath,
    queryInput: {
      text: {
        text: message,
        languageCode: 'en-US'
      }
    }
  };

  const responses = await sessionClient.detectIntent(request);
  const result = responses[0].queryResult;
  return result.fulfillmentText;
}
```

## Conclusion

In this tutorial, we have learned how to build a chatbot with Dialogflow. We covered the process of creating a Dialogflow agent, adding intents and entities to the agent, implementing fulfillment logic, and integrating the chatbot with a web application. With the knowledge gained from this tutorial, you can now build your own chatbot with Dialogflow and provide a seamless conversational experience for your users.

## External Resources

- [Dialogflow Documentation](https://cloud.google.com/dialogflow/docs/)
- [Dialogflow Essentials YouTube Series](https://www.youtube.com/playlist?list=PLIivdWyY5sqJxnwJhe3etaK7utrBiPBQ2)
- [Dialogflow Node.js Client Library](https://www.npmjs.com/package/dialogflow)