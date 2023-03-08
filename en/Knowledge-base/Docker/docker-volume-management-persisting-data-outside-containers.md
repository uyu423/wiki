---
title: Docker Volume Management: Persisting Data Outside Containers
description: 
published: true
date: 2023-01-31T11:04:29.192Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:04:25.699Z
---

- [Docker 볼륨 관리: 컨테이너 외부에 데이터 유지***Korean** version of this document is available*](/ko/Knowledge-base/Docker/docker-volume-management-persisting-data-outside-containers)
{.links-list}
- [Docker ボリューム管理: コンテナー外のデータの永続化***Japanese** version of this document is available*](/ja/Knowledge-base/Docker/docker-volume-management-persisting-data-outside-containers)
{.links-list}
- [Docker 卷管理：在容器外持久化数据***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Docker/docker-volume-management-persisting-data-outside-containers)
{.links-list}



# Docker Volume Management: Persisting Data Outside Containers

When working with Docker containers, it is important to consider how data is stored and accessed. Data inside a container is ephemeral, which means that it is not persisted after the container is stopped or removed. This can be a problem if you need to store data outside of the container, for example in a database.

There are two main ways to store data outside of a container:

1. Use a volume manager like Flocker or Rex-Ray. This is a good option if you need to store data on a remote server or if you want to use a specific storage backend like Amazon S3.
2. Use bind mounts. This is a good option if you want to store data on the host file system or if you need to use a specific file system like NFS.

In this article, we will focus on bind mounts. We will cover the following topics:

- What are bind mounts?
- How to use bind mounts?
- What are the benefits of using bind mounts?
- What are the drawbacks of using bind mounts?

## What are bind mounts?

A bind mount is a type of mount where a file or directory from the host file system is mounted into a container. The file or directory is then accessible from inside the container.

Bind mounts are useful for a number of reasons:

- You can use bind mounts to persist data outside of the container. This is useful if you need to store data in a database or if you want to share data between containers.
- You can use bind mounts to access data on the host file system. This is useful if you need to use a specific file system or if you want to access data that is not stored in a container.

## How to use bind mounts?

Bind mounts can be used in two ways:

1. You can use the `docker run` command to mount a file or directory from the host file system into the container. For example, the following command will mount the `/data` directory from the host file system into the `/data` directory in the container:

```
docker run -v /data:/data my-image
```

2. You can use the `docker volume` command to create a named volume and then mount it into the container. Named volumes are useful if you want to share data between containers or if you want to persist data outside of the container. For example, the following command will create a named volume called `my-volume` and mount it into the `/data` directory in the container:

```
docker volume create my-volume
docker run -v my-volume:/data my-image
```

## What are the benefits of using bind mounts?

Bind mounts have a number of benefits:

- They are easy to use. You can use the `docker run` command to mount a file or directory from the host file system into the container.
- They are flexible. You can mount any file or directory from the host file system into the container.
- They are fast. Bind mounts do not have the overhead of a volume manager like Flocker or Rex-Ray.

## What are the drawbacks of using bind mounts?

Bind mounts have a few drawbacks:

- They are not portable. If you move the host file system, the bind mount will no longer work.
- They are not secure. If the host file system is compromised, the bind mount can be used to access data in the container.
- They are not scalable. If you need to mount many files or directories, bind mounts can be slow.