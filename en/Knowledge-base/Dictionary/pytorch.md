---
title: PyTorch
description: 
published: true
date: 2023-02-17T05:18:33.316Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:18:21.718Z
---

- [PyTorch***Japanese** document is available*](/ja/Knowledge-base/Dictionary/pytorch)
{.links-list}
- [PyTorch***Spanish** document is available*](/es/Knowledge-base/Dictionary/pytorch)
{.links-list}
- [PyTorch***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/pytorch)
{.links-list}
- [PyTorch***Korean** document is available*](/ko/Knowledge-base/Dictionary/pytorch)
{.links-list}


# Overview
PyTorch is a deep learning framework developed by Facebook's AI Research lab. It is used to build and train deep learning models, and is designed to be fast, flexible, and user-friendly.

# Description
PyTorch is an open source machine learning library for Python, based on Torch, a scientific computing framework. It provides a wide range of algorithms for deep learning, including convolutional neural networks, recurrent neural networks, and reinforcement learning. The library is designed to be easy to use, with a focus on speed, flexibility, and user-friendliness.

PyTorch is built on a dynamic computational graph, which allows for easy debugging and fast training. It also supports distributed training, allowing models to be trained on multiple GPUs and machines. PyTorch provides a range of pre-trained models and datasets, as well as a library of tools for data pre-processing and visualization.

PyTorch is widely used in research and industry, and is popular among developers due to its ease of use and flexibility. It is also used in applications such as natural language processing, computer vision, and robotics.

# History
PyTorch was initially developed by Facebook's AI Research lab in 2016. It was released as an open source library in 2017. Since its release, it has become one of the most popular deep learning frameworks, and is used by researchers, developers, and companies around the world.

# Features
PyTorch features a wide range of tools for building and training deep learning models. It provides support for convolutional neural networks, recurrent neural networks, and reinforcement learning. It also features a range of pre-trained models and datasets for use in research and development.

PyTorch is designed to be fast, flexible, and user-friendly. It is built on a dynamic computational graph, which allows for easy debugging and fast training. It also supports distributed training, allowing models to be trained on multiple GPUs and machines.

# Example
In this example, we will use PyTorch to build a simple convolutional neural network (CNN) for image classification. We will use the CIFAR-10 dataset, which consists of 60,000 32x32 color images in 10 classes.

First, we will import the necessary libraries.

```python
import torch
import torchvision
import torch.nn as nn
import torch.optim as optim
```

Next, we will define our CNN model.

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

Finally, we will train our model.

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

# Pros and Cons
PyTorch has many advantages, including its ease of use, flexibility, and speed. It is also highly user-friendly, with a range of pre-trained models and datasets, and a library of tools for data pre-processing and visualization.

However, PyTorch does have some drawbacks. It is not as widely used as other deep learning frameworks, such as TensorFlow, and it does not have as many features and tools. Additionally, it is not as well-suited for large-scale applications as some other frameworks.

# Related Technology
PyTorch is closely related to Torch, a scientific computing framework developed by Facebook's AI Research lab. Torch is used for a wide range of applications, including computer vision, natural language processing, and robotics. It is also used in the development of PyTorch.

PyTorch is also related to other deep learning frameworks, such as TensorFlow, Caffe, and Theano. All of these frameworks are used for building and training deep learning models, and are designed to be fast, flexible, and user-friendly.

# Others
PyTorch is widely used in research and industry, and is popular among developers due to its ease of use and flexibility. It is used in applications such as natural language processing, computer vision, and robotics. It is also used by companies such as Google, Microsoft, and Amazon for their deep learning projects.