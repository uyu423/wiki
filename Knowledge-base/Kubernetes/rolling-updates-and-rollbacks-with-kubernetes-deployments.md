---
title: Kubernetes 배포를 통한 롤링 업데이트 및 롤백
description: 
published: true
date: 2023-01-31T11:36:19.710Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:36:18.137Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Rolling Updates and Rollbacks with Kubernetes Deployments***English** version of this document is available*](/en/Knowledge-base/Kubernetes/rolling-updates-and-rollbacks-with-kubernetes-deployments)
{.links-list}



# Kubernetes 배포를 통한 롤링 업데이트 및 롤백

프로덕션 환경에서는 다운타임 없이 애플리케이션을 업데이트해야 하는 경우가 많습니다. 쿠버네티스는 이를 돕기 위해 '롤링 업데이트'라는 기능을 제공합니다. 이 가이드에서는 '롤링 업데이트'가 무엇이며 어떻게 사용하는지 설명합니다.

## 롤링 업데이트란?

롤링 업데이트는 다운타임을 최소화하거나 전혀 하지 않고 소프트웨어를 업데이트하는 방법입니다. 이 방법을 사용하면 새 버전의 소프트웨어가 점진적으로 서버에 배포됩니다. 이렇게 하면 일부 서버가 업데이트되는 경우에도 항상 작동하는 소프트웨어 버전을 사용할 수 있습니다.

## 롤링 업데이트는 어떻게 작동합니까?

롤링 업데이트는 배포에서 개별 포드를 업데이트하여 수행됩니다. Kubernetes는 한 번에 하나씩 포드를 업데이트합니다. 이렇게 하면 항상 작동하는 소프트웨어 버전을 사용할 수 있습니다.

## 롤링 업데이트는 어떻게 수행합니까?

롤링 업데이트를 수행하려면 배포의 '사양'을 새 이미지로 업데이트해야 합니다. 그런 다음 Kubernetes는 한 번에 하나씩 포드를 업데이트합니다.

## 업데이트에 문제가 있다면?

업데이트에 문제가 있는 경우 배포를 이전 버전으로 롤백할 수 있습니다. 이렇게 하려면 배포의 `사양`을 이전 이미지로 업데이트해야 합니다. 그런 다음 Kubernetes는 한 번에 하나씩 포드를 업데이트합니다.

## 결론

롤링 업데이트는 중단 시간을 최소화하거나 중단하지 않고 소프트웨어를 업데이트하는 좋은 방법입니다. 쿠버네티스는 '롤링 업데이트' 기능으로 롤링 업데이트를 쉽게 수행할 수 있습니다.