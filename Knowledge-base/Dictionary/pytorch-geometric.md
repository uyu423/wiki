---
title: Pytorch Geometric
description: 
published: true
date: 2023-02-25T05:32:53.619Z
tags: 
editor: markdown
dateCreated: 2023-02-25T05:32:52.279Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Pytorch Geometric***English** document is available*](/en/Knowledge-base/Dictionary/pytorch-geometric)
{.links-list}


# 개요
PyTorch Geometric은 빠른 프로토타이핑 및 연구를 가능하게 하기 위해 설계된 그래프 구조 데이터에 대한 딥 러닝용 라이브러리입니다. 그래프 구조 데이터로 작업하기 위한 다른 유용한 도구와 함께 그래프 신경망의 효율적인 구현을 제공합니다.

# 설명
PyTorch Geometric은 빠른 프로토타이핑 및 연구를 가능하게 하기 위해 설계된 그래프 구조 데이터에 대한 딥 러닝용 라이브러리입니다. 그래프 구조 데이터로 작업하기 위한 다른 유용한 도구와 함께 그래프 신경망의 효율적인 구현을 제공합니다. 그래프 신경망은 소셜 네트워크, 분자 구조, 도로 네트워크와 같은 그래프 구조를 갖는 데이터를 처리하도록 설계된 일종의 신경망입니다. PyTorch Geometric을 사용하면 그래프 구조 데이터에 대한 그래프 신경망 및 기타 모델을 쉽게 구축할 수 있습니다.

이 라이브러리는 GCN(Graph Convolutional Networks), GAT(Graph Attention Networks) 및 GraphSAGE를 비롯한 다양한 그래프 신경망 아키텍처를 구현합니다. 또한 그래프 생성, 그래프 샘플링, 그래프 필터링 및 그래프 시각화와 같은 그래프 구조 데이터 작업을 위한 도구를 제공합니다.

PyTorch Geometric은 널리 사용되는 딥 러닝 프레임워크인 PyTorch를 기반으로 구축되었습니다. 이를 통해 PyTorch Geometric을 기존 PyTorch 워크플로에 쉽게 통합하고 자동 미분 라이브러리와 같은 PyTorch의 기존 도구를 그래프 구조 데이터에 사용할 수 있습니다.

# 특징
PyTorch Geometric은 그래프 구조 데이터 작업을 위한 다양한 기능을 제공합니다.

- 그래프 신경망 아키텍처: PyTorch Geometric은 Graph Convolutional Networks, Graph Attention Networks 및 GraphSAGE와 같은 다양한 그래프 신경망 아키텍처의 효율적인 구현을 제공합니다.

- 그래프 생성: PyTorch Geometric은 Erdos-Renyi 그래프, Watts-Strogatz small-world 그래프, Barabasi-Albert scale-free 그래프와 같은 다양한 속성을 가진 그래프를 생성하는 도구를 제공합니다.

- 그래프 샘플링: PyTorch Geometric은 랜덤 워크 샘플링 및 균일한 노드 샘플링과 같은 그래프에서 샘플링하는 도구를 제공합니다.

- 그래프 필터링: PyTorch Geometric은 에지 필터링 및 노드 필터링과 같은 그래프 필터링을 위한 도구를 제공합니다.

- 그래프 시각화: PyTorch Geometric은 에지 가중치, 노드 색상 및 노드 레이블과 같은 그래프 시각화를 위한 도구를 제공합니다.

# 예
PyTorch Geometric을 사용하여 그래프 신경망을 구축하는 예를 살펴보겠습니다. 우리는 그래프의 노드를 분류하기 위해 그래프 컨벌루션 네트워크를 사용할 것입니다.

먼저 PyTorch Geometric의 Erdos-Renyi 그래프 생성기로 그래프를 생성합니다.

```python
import torch
from torch_geometric.datasets import Planetoid
from torch_geometric.utils import erdos_renyi_graph

dataset = Planetoid(root='/tmp/Cora', name='Cora')
graph = erdos_renyi_graph(dataset.num_nodes, 0.1)
```

다음으로 그래프 컨벌루션 네트워크를 만듭니다.

```python
from torch_geometric.nn import GCNConv

class Net(torch.nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        self.conv1 = GCNConv(dataset.num_features, 16)
        self.conv2 = GCNConv(16, dataset.num_classes)

    def forward(self, data):
        x, edge_index = data.x, data.edge_index

        x = self.conv1(x, edge_index)
        x = torch.relu(x)
        x = self.conv2(x, edge_index)

        return x
```

마지막으로 그래프에서 네트워크를 훈련합니다.

```python
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
model = Net().to(device)
data = dataset[0].to(device)
optimizer = torch.optim.Adam(model.parameters(), lr=0.01)

model.train()
for epoch in range(200):
    optimizer.zero_grad()
    out = model(data)
    loss = torch.nn.functional.cross_entropy(out[data.train_mask], data.y[data.train_mask])
    loss.backward()
    optimizer.step()
```

# 장점과 단점

장점:

- PyTorch Geometric을 사용하면 그래프 구조 데이터에 대한 그래프 신경망 및 기타 모델을 쉽게 구축할 수 있습니다.
- Graph Convolutional Networks, Graph Attention Networks 및 GraphSAGE와 같은 그래프 신경망 아키텍처의 효율적인 구현을 제공합니다.
- 그래프 생성, 그래프 샘플링, 그래프 필터링, 그래프 시각화 등 그래프 구조의 데이터 작업을 위한 도구를 제공합니다.
- PyTorch 위에 구축되어 기존 PyTorch 워크플로에 쉽게 통합할 수 있습니다.

단점:

- PyTorch Geometric은 상대적으로 새롭고 일부 다른 라이브러리만큼 잘 테스트되지 않았을 수 있습니다.
- 다른 라이브러리와 동일한 수준의 지원이 없을 수 있습니다.