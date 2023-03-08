---
title: Docker Image Management: Tagging and Pushing to a Registry
description: 
published: true
date: 2023-02-01T21:43:20.030Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:43:18.428Z
---

- [Administración de imágenes de Docker: etiquetado y envío a un registro***Spanish** document is available*](/es/Knowledge-base/Docker/docker-image-management-tagging-and-pushing-to-a-registry)
{.links-list}
- [Docker 镜像管理：标记和推送到注册表***Chinese Simplified** document is available*](/zh/Knowledge-base/Docker/docker-image-management-tagging-and-pushing-to-a-registry)
{.links-list}
- [Docker 이미지 관리: 레지스트리에 태깅 및 푸시***Korean** document is available*](/ko/Knowledge-base/Docker/docker-image-management-tagging-and-pushing-to-a-registry)
{.links-list}



# Docker Image Management: Tagging and Pushing to a Registry

Docker images are the basis for creating containers. By default, images are pulled from the Docker Hub, which is a public registry managed by Docker, Inc. However, you can also run your own registry, and push images to it.

This article covers two methods for managing Docker images: tagging and pushing to a registry.

## Tagging Images

You can tag images with `docker tag`. This is useful for labeling images with version numbers, for example. To tag an image, use the following syntax:

```
docker tag <image> <tag>
```

For example, to tag the image `nginx` with the tag `1.7.9`, you would run the following command:

```
docker tag nginx 1.7.9
```

Tagging is important for managing images because it allows you to specify a specific version of an image when you run a container. By default, the `latest` tag is used, which corresponds to the most recent version of the image.

## Pushing Images to a Registry

Once you have tagged an image, you can push it to a registry. You can use the `docker push` command to push an image to a registry. The syntax for this command is as follows:

```
docker push <registry>/<repository>/<image>
```

For example, to push the image `nginx` to the Docker Hub, you would use the following command:

```
docker push nginx
```

Pushing images to a registry is a way of sharing images with others. By pushing an image to a registry, you make it available for others to pull and use.

## Summary

In this article, you learned about two methods for managing Docker images: tagging and pushing to a registry. Tagging images is a way of labeling them with version numbers or other information. Pushing images to a registry is a way of sharing them with others.