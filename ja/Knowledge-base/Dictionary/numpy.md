---
title: Numpy
description: 
published: true
date: 2023-01-31T06:36:41.974Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:36:40.420Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Numpy***English** version of this document is available*](/en/Knowledge-base/Dictionary/numpy)
{.links-list}

  
#Overview
Numpyは、Pythonの科学コンピューティングに使用されるオープンソースライブラリです。データ分析と操作のための強力なツールであり、高速実行速度、オブジェクト指向プログラミング、強力なデータ構造など、多くの便利な機能を提供します。 Numpyは、データ分析から機械学習、科学コンピューティングまで、さまざまな作業に使用できます。

#History
Numpyは2006年にTravis Oliphantによって作成されました。科学コンピューティングのためのオープンソースライブラリであるSciPyライブラリの一部として開発されました。 Numpyは生成以来人気が高まっており、現在世界中のデータ科学者、機械学習エンジニア、ソフトウェア開発者が日常的に使用しています。

#description
Numpyは、Pythonで数値データを迅速かつ効率的に操作できる強力なライブラリです。次のような多くの便利な機能を提供します。

* **配列オブジェクト**: Numpy は、同じタイプの複数の要素を保持できる配列オブジェクトを提供します。配列を使用すると、大量のデータをすばやく効率的に保存および操作できます。

* **数学関数**: Numpyは、配列で数学演算を実行するために使用できる多くの数学関数を提供します。これらの関数には、加算、減算、乗算、除算などの基本的な数学演算、行列乗算、フーリエ変換、線形代数演算などの高度な関数が含まれます。

* **オブジェクト指向プログラミング**: Numpyはデータ操作に対するオブジェクト指向のアプローチを提供し、使いやすく理解しやすいです。オブジェクト、クラス、および関数を使用してデータを操作および分析できます。

#yes
データポイントの2次元配列があるとしましょう。 Numpyを使用すると、次のコードを使用して配列の各行の平均を簡単に計算できます。

```python
import numpy as np

#Create a 2D array
data = np.array([[1,2,3],
                 [4,5,6],
                 [7,8,9]])

# Calculate the average of each row
row_means = np.mean(data, axis=1)

# Print the result
print(row_means)

#出力：[2。 5. 8.]
```

#長所と短所
Numpyは、効率的なデータ分析と操作を可能にする強力で柔軟なライブラリです。次のような多くの利点があります。

* **速度**: Numpyは高度に最適化されており、他のほとんどのライブラリよりも高速に実行できます。

* **オブジェクト指向プログラミング**: Numpyのオブジェクト指向アプローチを使用すると、使いやすく理解しやすくなります。

* **多様な機能**: Numpy は複雑な計算を簡単に行うための多様な数学関数を提供します。

しかし、Numpyには次のようないくつかの欠点もあります。

* **一部のデータ型のサポートの欠如**：Numpyは、オブジェクトや文字列などの一部のデータ型をサポートしていません。

* **制限された文書**：Numpyは良い文書を提供しますが、範囲が限られており、必ずしも明確または理解しにくい場合があります。

#関連リンク
- [Numpy (英語) *公式サイト*](https://numpy.org/)
- [Numpy チュートリアル (英語) *Real Python*](https://realpython.com/numpy-tutorial-python/)
- [NumPy チュートリアル (ドイツ語) *Python Academy*](https://www.python-academy.com/python_numpy_tutorial.html)
{.links-list}