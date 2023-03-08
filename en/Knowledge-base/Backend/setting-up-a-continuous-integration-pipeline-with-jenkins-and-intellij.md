---
title: Setting up a Continuous Integration Pipeline with Jenkins and IntelliJ
description: 
published: true
date: 2023-02-13T13:18:10.011Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:18:08.217Z
---

- [Configuración de una canalización de integración continua con Jenkins e IntelliJ***Spanish** document is available*](/es/Knowledge-base/Backend/setting-up-a-continuous-integration-pipeline-with-jenkins-and-intellij)
{.links-list}
- [使用 Jenkins 和 IntelliJ 设置持续集成管道***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/setting-up-a-continuous-integration-pipeline-with-jenkins-and-intellij)
{.links-list}
- [Jenkins 및 IntelliJ로 지속적인 통합 파이프라인 설정***Korean** document is available*](/ko/Knowledge-base/Backend/setting-up-a-continuous-integration-pipeline-with-jenkins-and-intellij)
{.links-list}


# Setting up a Continuous Integration Pipeline with Jenkins and IntelliJ

## Introduction

Continuous integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early.

Setting up a CI pipeline can be a daunting task, but with the right tools it can be relatively simple. In this article, we will show you how to set up a CI pipeline using Jenkins and IntelliJ.

## What you will need

- A GitHub account
- A Jenkins server
- IntelliJ IDEA

## Step 1: Create a GitHub repository

The first step is to create a GitHub repository for your project. To do this, head over to GitHub and create a new repository.

![Create a new GitHub repository](https://i.imgur.com/EuU8GtO.png)

Name your repository and click "Create repository".

![Name your repository](https://i.imgur.com/VNcuCY5.png)

## Step 2: Create a Jenkins job

Next, we need to create a Jenkins job. A Jenkins job is a task that Jenkins can execute. In our case, the Jenkins job will checkout our code from GitHub, build it, and run our tests.

To create a Jenkins job, head over to your Jenkins server and click "New Job".

![Jenkins New Job](https://i.imgur.com/pLJnV1N.png)

Give your job a name and select "Freestyle project".

![ Jenkins Job Name](https://i.imgur.com/lGZm4z3.png)

Click "OK".

On the next page, scroll down to the "Source Code Management" section and select "Git".

![Jenkins Source Code Management](https://i.imgur.com/Lg4U4jf.png)

In the "Repository URL" field, enter the URL of your GitHub repository.

![Jenkins Repository URL](https://i.imgur.com/VkzM0cw.png)

Scroll down to the "Build" section and click "Add build step". Select "Execute shell".

![Jenkins Build Section](https://i.imgur.com/KJ3fZUO.png)

In the "Command" field, enter the following command:

```
mvn clean install
```

This command will clean our project, install any dependencies, and run our tests.

Scroll down to the "Post-build Actions" section and click "Add post-build action". Select "Publish JUnit test result report".

![Jenkins Post-Build Actions](https://i.imgur.com/NDYaTGi.png)

In the "Test report XMLs" field, enter the following:

```
**/target/surefire-reports/*.xml
```

This will tell Jenkins to publish the results of our tests.

Click "Save".

## Step 3: Set up IntelliJ

Now that we have our Jenkins job set up, we need to configure our IDE. In this section, we will show you how to set up IntelliJ to trigger a build on our Jenkins server when we make changes to our code.

Open IntelliJ and navigate to the "File" menu. Select "Settings".

![IntelliJ Settings](https://i.imgur.com/mEUDKjK.png)

In the "Settings" window, navigate to "Build, Execution, Deployment" > "Continuous Integration". Select "Jenkins".

![IntelliJ Jenkins](https://i.imgur.com/VkzM0cw.png)

In the "Jenkins URL" field, enter the URL of your Jenkins server.

![IntelliJ Jenkins URL](https://i.imgur.com/dc9gKbD.png)

In the "Project name" field, enter the name of your Jenkins job.

![IntelliJ Project Name](https://i.imgur.com/P0zM0cw.png)

Click "OK".

## Step 4: Trigger a build

Now that our Jenkins job is set up and our IDE is configured, we are ready to trigger a build. To do this, make a change to your code and push it to GitHub.

![IntelliJ Push to GitHub](https://i.imgur.com/VkzM0cw.png)

Once you push your code to GitHub, Jenkins will automatically detect the change, checkout the code, build it, and run the tests.

![Jenkins Build](https://i.imgur.com/u4JnV1N.png)

You can view the results of the build by clicking on the "build" link in the "Build History" section.

![Jenkins Build History](https://i.imgur.com/ VkzM0cw.png)

## Conclusion

In this article, we showed you how to set up a CI pipeline using Jenkins and IntelliJ. While this is a simple pipeline, it can be easily extended to include additional steps, such as deploying to a staging or production environment.