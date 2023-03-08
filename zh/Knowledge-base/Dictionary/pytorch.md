---
title: PyTorch
description: 
published: true
date: 2023-02-17T05:18:26.265Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:18:21.712Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [PyTorch***English** document is available*](/en/Knowledge-base/Dictionary/pytorch)
{.links-list}


# 概述
PyTorch 是 Facebook 人工智能研究实验室开发的深度学习框架。它用于构建和训练深度学习模型，旨在快速、灵活且用户友好。

# 描述
PyTorch 是 Python 的开源机器学习库，基于科学计算框架 Torch。它为深度学习提供了广泛的算法，包括卷积神经网络、递归神经网络和强化学习。该库旨在易于使用，重点是速度、灵活性和用户友好性。

PyTorch 建立在动态计算图之上，可以轻松调试和快速训练。它还支持分布式训练，允许模型在多个 GPU 和机器上进行训练。 PyTorch 提供一系列预训练模型和数据集，以及用于数据预处理和可视化的工具库。

PyTorch 广泛应用于研究和工业领域，并且由于其易用性和灵活性而受到开发人员的欢迎。它还用于自然语言处理、计算机视觉和机器人技术等应用。

# 历史
PyTorch 最初由 Facebook 的 AI Research 实验室于 2016 年开发，于 2017 年作为开源库发布。自发布以来，它已成为最流行的深度学习框架之一，被各地的研究人员、开发人员和公司使用世界。

# 特征
PyTorch 具有用于构建和训练深度学习模型的广泛工具。它为卷积神经网络、递归神经网络和强化学习提供支持。它还具有一系列用于研究和开发的预训练模型和数据集。

PyTorch 旨在快速、灵活且用户友好。它建立在动态计算图上，可以轻松调试和快速训练。它还支持分布式训练，允许模型在多个 GPU 和机器上进行训练。

# 例子
在此示例中，我们将使用 PyTorch 构建一个用于图像分类的简单卷积神经网络 (CNN)。我们将使用 CIFAR-10 数据集，它包含 10 个类别的 60,000 张 32x32 彩色图像。

首先，我们将导入必要的库。

```python
import torch
import torchvision
import torch.nn as nn
import torch.optim as optim
```

接下来，我们将定义我们的 CNN 模型。

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

最后，我们将训练我们的模型。

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

# 优点和缺点
PyTorch 有很多优点，包括易用性、灵活性和速度。它还具有高度的用户友好性，具有一系列预训练模型和数据集，以及用于数据预处理和可视化的工具库。

然而，PyTorch 确实有一些缺点。它不像其他深度学习框架（例如 TensorFlow）那样广泛使用，并且没有那么多的功能和工具。此外，它不像其他一些框架那样适合大型应用程序。

# 相关技术
PyTorch 与 Torch 密切相关，Torch 是 Facebook 人工智能研究实验室开发的科学计算框架。 Torch 用于广泛的应用，包括计算机视觉、自然语言处理和机器人技术。它还用于 PyTorch 的开发。

PyTorch 还与其他深度学习框架相关，例如 TensorFlow、Caffe 和 Theano。所有这些框架都用于构建和训练深度学习模型，并且旨在快速、灵活且用户友好。

# 其他的
PyTorch 广泛应用于研究和工业领域，并且由于其易用性和灵活性而受到开发人员的欢迎。它用于自然语言处理、计算机视觉和机器人技术等应用程序。它也被谷歌、微软和亚马逊等公司用于他们的深度学习项目。