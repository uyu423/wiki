---
title: PyTorch
description: 
published: true
date: 2023-02-17T05:18:24.959Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:18:21.714Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}



- [PyTorch***English** document is available*](/en/Knowledge-base/Dictionary/pytorch)
{.links-list}


# 概要
PyTorch は、Facebook の AI Research lab によって開発されたディープ ラーニング フレームワークです。ディープ ラーニング モデルの構築とトレーニングに使用され、高速で柔軟、かつユーザー フレンドリーになるように設計されています。

# 説明
PyTorch は、科学計算フレームワークである Torch に基づく、Python 用のオープンソースの機械学習ライブラリです。畳み込みニューラル ネットワーク、再帰型ニューラル ネットワーク、強化学習など、深層学習用の幅広いアルゴリズムを提供します。このライブラリは、速度、柔軟性、および使いやすさに重点を置いて、使いやすいように設計されています。

PyTorch は動的な計算グラフ上に構築されているため、簡単なデバッグと高速なトレーニングが可能です。また、分散トレーニングもサポートしているため、複数の GPU とマシンでモデルをトレーニングできます。 PyTorch は、さまざまな事前トレーニング済みのモデルとデータセット、およびデータの前処理と視覚化のためのツールのライブラリを提供します。

PyTorch は研究や産業で広く使用されており、その使いやすさと柔軟性から開発者の間で人気があります。また、自然言語処理、コンピューター ビジョン、ロボット工学などのアプリケーションでも使用されています。

# 歴史
PyTorch は、2016 年に Facebook の AI 研究所によって最初に開発されました。2017 年にオープン ソース ライブラリとしてリリースされました。リリース以来、最も人気のあるディープ ラーニング フレームワークの 1 つになり、研究者、開発者、および企業によって使用されています。世界。

# 特徴
PyTorch は、ディープ ラーニング モデルを構築およびトレーニングするための幅広いツールを備えています。畳み込みニューラル ネットワーク、再帰型ニューラル ネットワーク、および強化学習のサポートを提供します。また、研究開発で使用するためのさまざまな事前トレーニング済みのモデルとデータセットも備えています。

PyTorch は、高速で柔軟性があり、使いやすいように設計されています。これは、動的な計算グラフに基づいて構築されているため、簡単なデバッグと迅速なトレーニングが可能です。また、分散トレーニングもサポートしているため、複数の GPU とマシンでモデルをトレーニングできます。

# 例
この例では、PyTorch を使用して、画像分類用の単純な畳み込みニューラル ネットワーク (CNN) を構築します。 10 クラスの 60,000 個の 32x32 カラー画像で構成される CIFAR-10 データセットを使用します。

まず、必要なライブラリをインポートします。

パイソン
輸入トーチ
トーチビジョンの輸入
torch.nn を nn としてインポート
torch.optim を optim としてインポート
```python
import torch
import torchvision
import torch.nn as nn
import torch.optim as optim
```

最後に、モデルをトレーニングします。

パイソン
# データを読み込む
transform = transforms.Compose([transforms.ToTensor(),
                              transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))])

trainset = torchvision.datasets.CIFAR10(root='./data', train=True, download=True, transform=transform)
trainloader = torch.utils.data.DataLoader(trainset、batch_size=4、shuffle=True、num_workers=2)

testset = torchvision.datasets.CIFAR10(root='./data', train=False, download=True, transform=transform)
testloader = torch.utils.data.DataLoader(テストセット、batch_size=4、shuffle=False、num_workers=2)

# モデルを初期化する
モデル = CNN()

# 損失関数とオプティマイザーを定義する
基準 = nn.CrossEntropyLoss()
オプティマイザ = optim.SGD(モデル.パラメータ(), lr=0.001, モメンタム=0.9)

# モデルをトレーニングする
for epoch in range(2): # データセットを複数回ループします

    running_loss = 0.0
    for i, enumerate(trainloader, 0) のデータ:
        # 入力を取得します。データは[入力、ラベル]のリストです
        入力、ラベル = データ

        # パラメータ勾配をゼロにする
        optimizer.zero_grad()

        # 前方 + 後方 + 最適化
        出力 = モデル (入力)
        損失 = 基準 (出力、ラベル)
        loss.backward()
        オプティマイザ.ステップ()

        # 統計を出力する
        running_loss += loss.item()
        if i % 2000 == 1999: # 2000 ミニバッチごとに出力
            print('[%d, %5d] 損失: %.3f' %
                  (エポック + 1, i + 1, running_loss / 2000))
            running_loss = 0.0

print('トレーニング終了')
```

# 長所と短所
PyTorch には、使いやすさ、柔軟性、速度など、多くの利点があります。また、さまざまな事前トレーニング済みのモデルとデータセット、およびデータの前処理と視覚化のためのツールのライブラリを備えた、非常にユーザーフレンドリーです。

ただし、PyTorch にはいくつかの欠点があります。 TensorFlow などの他の深層学習フレームワークほど広く使用されておらず、機能やツールもそれほど多くありません。さらに、他のフレームワークほど大規模なアプリケーションには適していません。

# 関連技術
PyTorch は、Facebook の AI Research lab によって開発された科学計算フレームワークである Torch と密接に関連しています。 Torch は、コンピューター ビジョン、自然言語処理、ロボット工学など、幅広いアプリケーションに使用されています。 PyTorch の開発にも使用されます。

PyTorch は、TensorFlow、Caffe、Theano などの他の深層学習フレームワークにも関連しています。これらのフレームワークはすべて、ディープ ラーニング モデルの構築とトレーニングに使用され、高速、柔軟、かつユーザー フレンドリーになるように設計されています。

# その他
PyTorch は研究や産業で広く使用されており、その使いやすさと柔軟性から開発者の間で人気があります。自然言語処理、コンピューター ビジョン、ロボット工学などのアプリケーションで使用されます。また、Google、Microsoft、Amazon などの企業でもディープ ラーニング プロジェクトに使用されています。