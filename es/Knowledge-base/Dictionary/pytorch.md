---
title: PyTorch
description: 
published: true
date: 2023-02-17T05:18:26.412Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:18:21.715Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [PyTorch***English** document is available*](/en/Knowledge-base/Dictionary/pytorch)
{.links-list}


# Descripción general
PyTorch es un marco de aprendizaje profundo desarrollado por el laboratorio de investigación de IA de Facebook. Se utiliza para crear y entrenar modelos de aprendizaje profundo y está diseñado para ser rápido, flexible y fácil de usar.

# Descripción
PyTorch es una biblioteca de aprendizaje automático de código abierto para Python, basada en Torch, un marco de computación científica. Proporciona una amplia gama de algoritmos para el aprendizaje profundo, incluidas las redes neuronales convolucionales, las redes neuronales recurrentes y el aprendizaje por refuerzo. La biblioteca está diseñada para ser fácil de usar, con un enfoque en la velocidad, la flexibilidad y la facilidad de uso.

PyTorch se basa en un gráfico computacional dinámico, que permite una fácil depuración y un entrenamiento rápido. También es compatible con el entrenamiento distribuido, lo que permite que los modelos se entrenen en varias GPU y máquinas. PyTorch proporciona una variedad de conjuntos de datos y modelos preentrenados, así como una biblioteca de herramientas para el preprocesamiento y la visualización de datos.

PyTorch se usa ampliamente en la investigación y la industria, y es popular entre los desarrolladores debido a su facilidad de uso y flexibilidad. También se utiliza en aplicaciones como el procesamiento del lenguaje natural, la visión artificial y la robótica.

# Historia
PyTorch fue desarrollado inicialmente por el laboratorio de investigación de inteligencia artificial de Facebook en 2016. Se lanzó como una biblioteca de código abierto en 2017. Desde su lanzamiento, se ha convertido en uno de los marcos de aprendizaje profundo más populares y es utilizado por investigadores, desarrolladores y empresas de todo el mundo. el mundo.

# Características
PyTorch presenta una amplia gama de herramientas para construir y entrenar modelos de aprendizaje profundo. Proporciona soporte para redes neuronales convolucionales, redes neuronales recurrentes y aprendizaje por refuerzo. También cuenta con una gama de modelos y conjuntos de datos pre-entrenados para su uso en investigación y desarrollo.

PyTorch está diseñado para ser rápido, flexible y fácil de usar. Se basa en un gráfico computacional dinámico, que permite una fácil depuración y un entrenamiento rápido. También es compatible con el entrenamiento distribuido, lo que permite que los modelos se entrenen en varias GPU y máquinas.

# Ejemplo
En este ejemplo, usaremos PyTorch para construir una red neuronal convolucional (CNN) simple para la clasificación de imágenes. Usaremos el conjunto de datos CIFAR-10, que consta de 60 000 imágenes en color de 32x32 en 10 clases.

Primero, importaremos las bibliotecas necesarias.

```python
import torch
import torchvision
import torch.nn as nn
import torch.optim as optim
```

A continuación, definiremos nuestro modelo CNN.

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

Finalmente, entrenaremos nuestro modelo.

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

# Pros y contras
PyTorch tiene muchas ventajas, incluida su facilidad de uso, flexibilidad y velocidad. También es muy fácil de usar, con una gama de modelos y conjuntos de datos previamente entrenados, y una biblioteca de herramientas para el preprocesamiento y la visualización de datos.

Sin embargo, PyTorch tiene algunos inconvenientes. No se usa tanto como otros marcos de aprendizaje profundo, como TensorFlow, y no tiene tantas funciones y herramientas. Además, no es tan adecuado para aplicaciones a gran escala como otros marcos.

# Tecnología relacionada
PyTorch está estrechamente relacionado con Torch, un marco informático científico desarrollado por el laboratorio de investigación de IA de Facebook. Torch se utiliza para una amplia gama de aplicaciones, incluida la visión artificial, el procesamiento del lenguaje natural y la robótica. También se utiliza en el desarrollo de PyTorch.

PyTorch también está relacionado con otros marcos de aprendizaje profundo, como TensorFlow, Caffe y Theano. Todos estos marcos se utilizan para crear y entrenar modelos de aprendizaje profundo y están diseñados para ser rápidos, flexibles y fáciles de usar.

# Otros
PyTorch se usa ampliamente en la investigación y la industria, y es popular entre los desarrolladores debido a su facilidad de uso y flexibilidad. Se utiliza en aplicaciones como el procesamiento del lenguaje natural, la visión artificial y la robótica. También lo utilizan empresas como Google, Microsoft y Amazon para sus proyectos de aprendizaje profundo.