---
title: Docker Hub: Building and Sharing Your Docker Images
description: 
published: true
date: 2023-02-14T01:17:18.854Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:17:17.202Z
---

- [Docker Hub: crear y compartir sus imágenes de Docker***Spanish** document is available*](/es/Knowledge-base/Docker/docker-hub-building-and-sharing-your-docker-images)
{.links-list}
- [Docker Hub：构建和共享您的 Docker 镜像***Chinese Simplified** document is available*](/zh/Knowledge-base/Docker/docker-hub-building-and-sharing-your-docker-images)
{.links-list}
- [Docker 허브: Docker 이미지 빌드 및 공유***Korean** document is available*](/ko/Knowledge-base/Docker/docker-hub-building-and-sharing-your-docker-images)
{.links-list}


# Docker Hub: Building and Sharing Your Docker Images

Docker Hub is a cloud-based registry service for building and sharing Docker images. With Docker Hub, you can build, test, and deploy your applications with ease.

Docker Hub offers a Free plan and a paid Pro plan. With the Free plan, you can create unlimited public repositories, but you are limited to one private repository. With the Pro plan, you can create an unlimited number of both public and private repositories.

There are two ways to push images to Docker Hub:

1. The **docker push** command

2. The **Docker Hub web interface**

## The docker push command

The **docker push** command pushes images to a Docker registry. A Docker registry is a host that stores and serves images.

The **docker push** command requires that you specify the name of the image and the tag. For example, to push an image with the tag "latest" to Docker Hub, you would use the following command:

```
docker push <username>/<image>:<tag>
```

Replace <username> with your Docker Hub username, <image> with the name of the image, and <tag> with the tag.

## The Docker Hub web interface

The Docker Hub web interface is a web-based application that you can use to push, pull, and manage your Docker images.

To push an image to Docker Hub using the web interface, first log in to your Docker Hub account. Then, click the **Create Repository** button.

Enter the name of the repository and a description, then click the **Create** button.

Next, click the **Upload File** button.

Select the image you want to upload, then click the **Upload** button.

Finally, click the **Publish** button.

Your image is now pushed to your repository on Docker Hub.

## Conclusion

Docker Hub is a great way to share your Docker images with the world. With Docker Hub, you can build, test, and deploy your applications with ease.