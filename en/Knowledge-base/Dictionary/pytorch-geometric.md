---
title: Pytorch Geometric
description: 
published: true
date: 2023-02-25T05:32:59.217Z
tags: 
editor: markdown
dateCreated: 2023-02-25T05:32:52.281Z
---

- [Pytorch Geometric***Korean** document is available*](/ko/Knowledge-base/Dictionary/pytorch-geometric)
{.links-list}


# Overview
PyTorch Geometric is a library for deep learning on graph-structured data, designed to enable fast prototyping and research. It provides efficient implementations of graph neural networks, along with other useful tools for working with graph-structured data.

# Description
PyTorch Geometric is a library for deep learning on graph-structured data, designed to enable fast prototyping and research. It provides efficient implementations of graph neural networks, along with other useful tools for working with graph-structured data. Graph neural networks are a type of neural network designed to process data that has a graph structure, such as social networks, molecular structures, and road networks. PyTorch Geometric makes it easy to build graph neural networks and other models for graph-structured data.

The library implements a variety of graph neural network architectures, including Graph Convolutional Networks (GCNs), Graph Attention Networks (GATs), and GraphSAGE. It also provides tools for working with graph-structured data, such as graph generation, graph sampling, graph filtering, and graph visualization.

PyTorch Geometric is built on top of PyTorch, a popular deep learning framework. This makes it easy to integrate PyTorch Geometric into existing PyTorch workflows, and to use PyTorch’s existing tools, such as its automatic differentiation library, for graph-structured data.

# Features
PyTorch Geometric provides a variety of features for working with graph-structured data:

- Graph neural network architectures: PyTorch Geometric provides efficient implementations of a range of graph neural network architectures, such as Graph Convolutional Networks, Graph Attention Networks, and GraphSAGE.

- Graph generation: PyTorch Geometric provides tools for generating graphs with various properties, such as Erdos-Renyi graphs, Watts-Strogatz small-world graphs, and Barabasi-Albert scale-free graphs.

- Graph sampling: PyTorch Geometric provides tools for sampling from graphs, such as random walk sampling and uniform node sampling.

- Graph filtering: PyTorch Geometric provides tools for filtering graphs, such as edge filtering and node filtering.

- Graph visualization: PyTorch Geometric provides tools for visualizing graphs, such as edge weights, node colors, and node labels.

# Example
Let’s look at an example of using PyTorch Geometric to build a graph neural network. We’ll use a graph convolutional network to classify the nodes in a graph.

First, we’ll generate a graph with the Erdos-Renyi graph generator from PyTorch Geometric.

```python
import torch
from torch_geometric.datasets import Planetoid
from torch_geometric.utils import erdos_renyi_graph

dataset = Planetoid(root='/tmp/Cora', name='Cora')
graph = erdos_renyi_graph(dataset.num_nodes, 0.1)
```

Next, we’ll create a graph convolutional network.

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

Finally, we’ll train the network on the graph.

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

# Pros and Cons

Pros: 

- PyTorch Geometric makes it easy to build graph neural networks and other models for graph-structured data.
- It provides efficient implementations of graph neural network architectures, such as Graph Convolutional Networks, Graph Attention Networks, and GraphSAGE.
- It provides tools for working with graph-structured data, such as graph generation, graph sampling, graph filtering, and graph visualization.
- It is built on top of PyTorch, making it easy to integrate into existing PyTorch workflows.

Cons:

- PyTorch Geometric is relatively new and may not be as well-tested as some other libraries.
- It may not have the same level of support as other libraries.