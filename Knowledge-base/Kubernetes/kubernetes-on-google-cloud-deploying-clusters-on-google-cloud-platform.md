---
title: Google Cloud의 Kubernetes: Google Cloud Platform에 클러스터 배포
description: 
published: true
date: 2023-02-14T05:33:12.838Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:33:05.637Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes on Google Cloud: Deploying Clusters on Google Cloud Platform***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-google-cloud-deploying-clusters-on-google-cloud-platform)
{.links-list}


# Google Cloud의 Kubernetes: Google Cloud Platform에 클러스터 배포

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 시스템입니다. 애플리케이션을 구성하는 컨테이너를 논리 단위로 그룹화하여 쉽게 관리하고 검색할 수 있습니다. Kubernetes는 Google Cloud Platform(GCP)에서 호스팅되며 GCP에 배포된 컨테이너를 조정하고 관리하는 데 사용됩니다.

GCP의 Kubernetes는 컨테이너화된 애플리케이션을 배포하는 확장 가능하고 안정적이며 비용 효율적인 방법입니다. GCP는 종량제 가격 책정, 분당 청구, 선결제 비용 없음 등 다른 클라우드 제공업체에 비해 많은 이점을 제공합니다. GCP에서 Kubernetes를 사용하여 온프레미스 워크로드를 관리할 수도 있습니다.

이 기사에서는 GCP에 Kubernetes 클러스터를 배포하는 방법을 보여줍니다. 또한 Kubernetes 클러스터에 간단한 애플리케이션을 배포하는 방법도 보여줍니다.

## 전제 조건

- Google 클라우드 계정
- Google Cloud Console에서 생성된 프로젝트
- 로컬 머신에 설치된 gcloud 명령줄 도구
- Kubernetes에 대한 기본 지식

## 쿠버네티스 클러스터 만들기

Kubernetes 클러스터는 노드 집합으로 구성되며 각 노드는 Kubernetes 구성 요소를 실행하는 물리적 또는 가상 머신입니다. Kubernetes 클러스터에는 두 가지 유형의 노드가 있습니다.

- **마스터 노드**: 이 노드는 Kubernetes 클러스터 관리를 담당합니다. API 서버, 스케줄러 및 컨트롤러 관리자 구성 요소를 제공합니다.
- **작업자 노드**: 이 노드는 Kubernetes 클러스터에 배포된 애플리케이션을 실행합니다.

이 섹션에서는 3개의 노드(하나의 마스터 노드와 2개의 작업자 노드)가 있는 Kubernetes 클러스터를 생성하는 방법을 보여줍니다.

### 마스터 노드 생성

1. Google Cloud Console에 로그인하고 **Compute Engine** > **VM 인스턴스** 페이지로 이동합니다.
2. **인스턴스 만들기** 버튼을 클릭합니다.
3. **이름** 필드에 **kubernetes-master**를 입력합니다.
4. **Zone** 필드에서 현재 위치와 가까운 구역을 선택합니다.
5. **머신 유형** 필드에서 **n1-standard-1**을 선택합니다.
6. **부팅 디스크** 섹션에서 **변경**을 클릭합니다.
7. **부팅 디스크** 섹션의 **운영 체제** 드롭다운 목록에서 **Ubuntu 16.04 LTS**를 선택합니다.
8. **부팅 디스크 유형** 드롭다운 목록에서 **SSD(영구 디스크)**를 선택합니다.
9. **부팅 디스크 크기** 필드에 **10GB**를 입력합니다.
10. **선택** 버튼을 클릭합니다.
11. **방화벽** 섹션에서 **HTTP 트래픽 허용** 확인란을 선택합니다.
12. **만들기** 버튼을 클릭합니다.

이제 마스터 노드가 생성되어야 합니다.

### 작업자 노드 생성

1. Google Cloud Console에 로그인하고 **Compute Engine** > **VM 인스턴스** 페이지로 이동합니다.
2. **인스턴스 만들기** 버튼을 클릭합니다.
3. **이름** 필드에 **kubernetes-worker-1**을 입력합니다.
4. **Zone** 필드에서 마스터 노드에 대해 선택한 동일한 영역을 선택합니다.
5. **머신 유형** 필드에서 **n1-standard-1**을 선택합니다.
6. **부팅 디스크** 섹션에서 **변경**을 클릭합니다.
7. **부팅 디스크** 섹션의 **운영 체제** 드롭다운 목록에서 **Ubuntu 16.04 LTS**를 선택합니다.
8. **부팅 디스크 유형** 드롭다운 목록에서 **SSD(영구 디스크)**를 선택합니다.
9. **부팅 디스크 크기** 필드에 **10GB**를 입력합니다.
10. **선택** 버튼을 클릭합니다.
11. **방화벽** 섹션에서 **HTTP 트래픽 허용** 확인란을 선택합니다.
12. **만들기** 버튼을 클릭합니다.

위의 단계를 반복하여 두 번째 작업자 노드를 생성하되 **kubernetes-worker-2**를 두 번째 노드의 이름으로 사용합니다.

이제 작업자 노드가 생성되어야 합니다.

## 쿠버네티스 설치하기

이 섹션에서는 마스터 노드에 Kubernetes를 설치하는 방법을 보여줍니다.

1. SSH를 사용하여 마스터 노드에 로그인합니다.
2. 다음 명령을 실행하여 Kubernetes apt 리포지토리를 추가합니다.

```
$ sudo apt-get install -y apt-transport-https
3. Run the following command to add the Kubernetes GPG key:

```
$ 컬 -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key 추가-
4. 다음 명령을 실행하여 Kubernetes 리포지토리를 추가합니다.

```
$ sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
5. Update the package list:

```
$ sudo apt-get 업데이트
6. 쿠버네티스를 설치합니다.

```
$ sudo apt-get install -y kubelet kubeadm kubectl
7. Once the installation is complete, run the following command to start the Kubernetes master node:

```
$ sudo kubeadm 초기화
8. 다음 명령을 실행하여 kubectl을 구성합니다.

```
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
9. Your Kubernetes master node should now be up and running.

## Joining Worker Nodes to the Cluster

In this section, we will show you how to join your worker nodes to the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to get the join command:

```
$ sudo kubeadm 토큰 생성 --print-join-command
3. SSH를 사용하여 작업자 노드에 로그인합니다.
4. 각 작업자 노드에서 이전 단계에서 가져온 조인 명령을 실행합니다.
5. 이제 작업자 노드가 Kubernetes 클러스터에 결합되어야 합니다.

## 애플리케이션 배포

이 섹션에서는 Kubernetes 클러스터에 간단한 애플리케이션을 배포하는 방법을 보여줍니다.

1. SSH를 사용하여 마스터 노드에 로그인합니다.
2. 다음 내용으로 **nginx-deployment.yaml**이라는 파일을 생성합니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
3. Run the following command to deploy the application:

```
$ kubectl create -f nginx-deployment.yaml
4. 다음 명령을 실행하여 배포된 포드를 나열합니다.

```
$ kubectl get pods
5. Run the following command to expose the deployment:

```
$ kubectl 노출 배포 nginx-deployment --type=LoadBalancer --port=80 --target-port=80
6. 다음 명령을 실행하여 서비스 URL을 가져옵니다.

```
$ kubectl get service nginx-deployment
7. Access the application using the service URL. You should see the default Nginx page.

Your application is now deployed on your Kubernetes cluster.

## Deleting the Cluster

In this section, we will show you how to delete the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to delete the cluster:

```
$ sudo kubeadm 재설정
3. 마스터 노드를 삭제합니다.

```
$ gcloud compute instances delete kubernetes-master
4. Delete the worker nodes:

```
$ gcloud 컴퓨팅 인스턴스 삭제 kubernetes-worker-1
$ gcloud 컴퓨팅 인스턴스 삭제 kubernetes-worker-2
5. 이제 Kubernetes 클러스터가 삭제되어야 합니다.

## 결론

이 기사에서는 GCP에 Kubernetes 클러스터를 배포하는 방법을 설명했습니다. 또한 Kubernetes 클러스터에 간단한 애플리케이션을 배포하는 방법도 보여 주었습니다.