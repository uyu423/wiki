---
title: PyTorch
description: 
published: true
date: 2023-02-17T05:18:25.166Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:18:21.711Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [PyTorch***English** document is available*](/en/Knowledge-base/Dictionary/pytorch)
{.links-list}


# 개요
PyTorch는 Facebook의 AI 연구소에서 개발한 딥 러닝 프레임워크입니다. 딥 러닝 모델을 구축하고 교육하는 데 사용되며 빠르고 유연하며 사용자 친화적으로 설계되었습니다.

# 설명
PyTorch는 과학 컴퓨팅 프레임워크인 Torch를 기반으로 하는 Python용 오픈 소스 기계 학습 라이브러리입니다. Convolutional Neural Network, Recurrent Neural Network, Reinforcement Learning 등 딥 러닝을 위한 다양한 알고리즘을 제공합니다. 라이브러리는 속도, 유연성 및 사용자 친화성에 중점을 두고 사용하기 쉽게 설계되었습니다.

PyTorch는 동적 계산 그래프를 기반으로 구축되어 쉽게 디버깅하고 빠르게 교육할 수 있습니다. 또한 분산 교육을 지원하여 여러 GPU 및 머신에서 모델을 교육할 수 있습니다. PyTorch는 데이터 전처리 및 시각화를 위한 도구 라이브러리뿐만 아니라 다양한 사전 훈련된 모델 및 데이터 세트를 제공합니다.

PyTorch는 연구 및 산업 분야에서 널리 사용되며 사용 편의성과 유연성으로 인해 개발자들 사이에서 인기가 있습니다. 또한 자연어 처리, 컴퓨터 비전 및 로봇 공학과 같은 응용 프로그램에도 사용됩니다.

# 역사
PyTorch는 2016년 페이스북의 AI 연구소에서 처음 개발되었습니다. 2017년 오픈 소스 라이브러리로 공개되었습니다. 공개 이후 가장 인기 있는 딥 러닝 프레임워크 중 하나가 되었으며, 전 세계 연구원, 개발자 및 기업에서 사용하고 있습니다. 세계.

# 특징
PyTorch는 딥 러닝 모델을 구축하고 교육하기 위한 다양한 도구를 제공합니다. 컨볼루션 신경망, 순환 신경망 및 강화 학습을 지원합니다. 또한 연구 및 개발에 사용하기 위해 사전 학습된 다양한 모델과 데이터 세트를 제공합니다.

PyTorch는 빠르고 유연하며 사용자 친화적으로 설계되었습니다. 동적 계산 그래프를 기반으로 구축되어 쉽게 디버깅하고 빠르게 교육할 수 있습니다. 또한 분산 교육을 지원하여 여러 GPU 및 머신에서 모델을 교육할 수 있습니다.

# 예
이 예에서는 PyTorch를 사용하여 이미지 분류를 위한 간단한 CNN(컨볼루션 신경망)을 구축합니다. 우리는 10개의 클래스에 60,000개의 32x32 컬러 이미지로 구성된 CIFAR-10 데이터 세트를 사용할 것입니다.

먼저 필요한 라이브러리를 가져옵니다.

```python
import torch
import torchvision
import torch.nn as nn
import torch.optim as optim
```

다음으로 CNN 모델을 정의합니다.

```python
class CNN(nn.Module):
    def __init__(self):
        super(CNN, self).__init__()
        self.conv1 = nn.Conv2d(3, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(16 * 5 * 5, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = x.view(-1, 16 * 5 * 5)
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x
```

마지막으로 모델을 학습시킵니다.

```python
# Load the data
transform = transforms.Compose([transforms.ToTensor(),
                              transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))])

trainset = torchvision.datasets.CIFAR10(root='./data', train=True, download=True, transform=transform)
trainloader = torch.utils.data.DataLoader(trainset, batch_size=4, shuffle=True, num_workers=2)

testset = torchvision.datasets.CIFAR10(root='./data', train=False, download=True, transform=transform)
testloader = torch.utils.data.DataLoader(testset, batch_size=4, shuffle=False, num_workers=2)

# Initialize the model
model = CNN()

# Define the loss function and optimizer
criterion = nn.CrossEntropyLoss()
optimizer = optim.SGD(model.parameters(), lr=0.001, momentum=0.9)

# Train the model
for epoch in range(2):  # loop over the dataset multiple times

    running_loss = 0.0
    for i, data in enumerate(trainloader, 0):
        # get the inputs; data is a list of [inputs, labels]
        inputs, labels = data

        # zero the parameter gradients
        optimizer.zero_grad()

        # forward + backward + optimize
        outputs = model(inputs)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()

        # print statistics
        running_loss += loss.item()
        if i % 2000 == 1999:    # print every 2000 mini-batches
            print('[%d, %5d] loss: %.3f' %
                  (epoch + 1, i + 1, running_loss / 2000))
            running_loss = 0.0

print('Finished Training')
```

# 장점과 단점
PyTorch는 사용 용이성, 유연성 및 속도를 포함하여 많은 장점을 가지고 있습니다. 또한 다양한 사전 훈련된 모델 및 데이터 세트와 데이터 사전 처리 및 시각화를 위한 도구 라이브러리를 통해 매우 사용자 친화적입니다.

그러나 PyTorch에는 몇 가지 단점이 있습니다. TensorFlow와 같은 다른 딥 러닝 프레임워크만큼 널리 사용되지 않으며 많은 기능과 도구가 없습니다. 또한 일부 다른 프레임워크만큼 대규모 애플리케이션에 적합하지 않습니다.

# 관련 기술
PyTorch는 Facebook의 AI 연구소에서 개발한 과학 컴퓨팅 프레임워크인 Torch와 밀접한 관련이 있습니다. Torch는 컴퓨터 비전, 자연어 처리 및 로봇 공학을 포함한 광범위한 응용 분야에 사용됩니다. PyTorch 개발에도 사용됩니다.

PyTorch는 TensorFlow, Caffe 및 Theano와 같은 다른 딥 러닝 프레임워크와도 관련이 있습니다. 이러한 모든 프레임워크는 딥 러닝 모델을 구축하고 교육하는 데 사용되며 빠르고 유연하며 사용자 친화적으로 설계되었습니다.

# 기타
PyTorch는 연구 및 산업 분야에서 널리 사용되며 사용 편의성과 유연성으로 인해 개발자들 사이에서 인기가 있습니다. 자연어 처리, 컴퓨터 비전 및 로봇 공학과 같은 응용 프로그램에 사용됩니다. 또한 Google, Microsoft 및 Amazon과 같은 회사에서 딥 러닝 프로젝트에 사용합니다.