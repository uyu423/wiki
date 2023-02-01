---
title: Node.js 애플리케이션 도커화
description: 
published: true
date: 2023-02-01T19:38:41.116Z
tags: 
editor: markdown
dateCreated: 2023-02-01T19:38:41.116Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Dockerizing Your Node.js Applications***English** document is available*](/en/Knowledge-base/Backend/dockerizing-your-node-js-applications)
{.links-list}


  느낌표 구문을 사용하여 이미지를 인라인으로 추가할 수 있습니다. ```![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")```.

#Dockerizing Your Node.js Applications

Docker is an open platform for developers and sysadmins to build, ship, and run distributed applications. Consisting of Docker Engine, a portable, runtime-independent application environment, and Docker Hub, a cloud service for sharing applications and automating workflows, Docker enables apps to be quickly assembled from components and eliminates the friction between development, QA, and production environments.  As a result, IT can ship faster and run the same app, unchanged, on laptops, data center VMs, and any cloud.

Dockerizing your Node.js applications provides a number of benefits:

- **Isolation**: Containers isolate your application from other applications running on the same host. This makes it easier to run multiple applications on the same host and to ensure that your application has the required libraries and configuration.

- **Reproducibility**: A Docker image contains all the information that is required to run an application. This makes it easy to share applications with other developers and to deploy them in different environments.

- **Efficiency**: By packaging all the dependencies required to run an application in a container, you can avoid installing these dependencies on every host where the application is deployed.

- **Flexibility**: A Docker image can be run on any host that has a Docker runtime. This makes it easy to deploy applications in hybrid environments, such as on-premises data centers and cloud-based platforms.

In this article, we will show you how to dockerize a Node.js application. We will use the Express web framework to build a simple web application and will package it in a Docker image.

## Prerequisites

Before you begin, you will need the following:

- A text editor. We recommend using [Visual Studio Code](https://code.visualstudio.com/).

- [Node.js](https://nodejs.org/en/) installed on your development machine.

- [Docker](https://www.docker.com/) installed on your development machine.

## Creating a Node.js Application

We will start by creating a simple Node.js application using the Express web framework. Create a new directory for your project and initialize a Node.js project in it:

```
mkdir nodejs-도커
cd nodejs-도커
npm 초기화
```

You will be prompted to enter information about your project, such as the name, version, description, etc. You can accept the default values by pressing Enter.

Next, install the Express web framework and other dependencies:

```
npm 설치 익스프레스 --저장
```

Create a file named `app.js` in your project directory and add the following code to it:

```자바스크립트
const 익스프레스 = 요구('익스프레스');
const 앱 = 익스프레스();

app.get('/', (요청, 응답) => {
  res.send('안녕, 세상!');
});

app.listen(3000, () => {
  console.log('포트 3000에서 수신하는 예제 앱!');
});
```

This code creates a simple web server that listens on port 3000 and returns the string "Hello, world!" when you make a request to the root URL of the server.

You can start the web server by running the following command:

```
노드 app.js
```

You can then access the web server at http://localhost:3000.

## Creating a Dockerfile

A Dockerfile is a text file that contains the instructions for building a Docker image. Create a file named `Dockerfile` in your project directory and add the following content to it:

```
FROM 노드:알파인

WORKDIR / 앱

패키지 복사*.json ./

실행 npm 설치

복사 . .

노출 3000

CMD ["노드", "app.js"]
```

This Dockerfile uses the [Node.js](https://hub.docker.com/_/node/) [Alpine](https://hub.docker.com/_/alpine/) image as the base image for our Docker image. The Alpine image is a small Linux distribution that contains the bare minimum required to run a Node.js application.

The `WORKDIR` instruction sets the working directory for the subsequent instructions. The `COPY` instruction copies the `package.json` and `package-lock.json` files from the project directory to the working directory. The `RUN` instruction runs the `npm install` command to install the dependencies for the application. The `COPY` instruction then copies the rest of the files from the project directory to the working directory. The `EXPOSE` instruction exposes port 3000. The `CMD` instruction specifies the command to run when the container is started.

## Building the Docker Image

Now that we have created the Dockerfile, we can build the Docker image. Run the following command in your project directory:

```
도커 빌드 -t nodejs-docker .
```

This command will create a Docker image with the name `nodejs-docker`.

## Running the Docker Container

We can now run the Docker image as a container. Run the following command to start the container:

```
도커 실행 -d -p 3000:3000 nodejs-docker
```

이 명령은 컨테이너를 시작하고 호스트의 포트 3000을 컨테이너의 포트 3000에 바인딩합니다. `-d` 옵션은 컨테이너를 분리 모드로 실행하도록 Docker에 지시합니다. 즉, 컨테이너는 백그라운드에서 실행되고 콘솔은 명령 프롬프트로 돌아갑니다.

이제 http://localhost:3000에서 웹 서버에 액세스할 수 있습니다.