---
title: PyOpenGL
description: 
published: true
date: 2023-02-11T13:56:01.359Z
tags: 
editor: markdown
dateCreated: 2023-02-11T13:55:59.532Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}



- [PyOpenGL***English** document is available*](/en/Knowledge-base/Dictionary/pyopengl)
{.links-list}


# 概要
PyOpenGL は、OpenGL (Open Graphics Library) API へのバインディングを提供する Python プログラミング言語用のオープン ソース ライブラリです。 PyOpenGL は、Python アプリケーションで 3D グラフィックスと視覚効果を作成するために使用されます。

# 説明
PyOpenGL は、OpenGL (Open Graphics Library) API へのバインディングを提供する Python プログラミング言語用のオープン ソース ライブラリです。 OpenGL は、アプリケーションで 3D グラフィックスと視覚効果を作成するために使用されるアプリケーション プログラミング インターフェイス (API) です。コンピュータ ゲーム、科学的視覚化、バーチャル リアリティ アプリケーションで広く使用されています。

PyOpenGL は OpenGL API へのオブジェクト指向インターフェースを提供し、Python プログラマーが OpenGL API の詳細を学ばなくても OpenGL プログラムを作成できるようにします。また、3D オブジェクトとテクスチャを操作するための多数のユーティリティ関数も含まれています。

PyOpenGL は、Windows、Mac OS X、および Linux で使用でき、Python Package Index (PyPI) を使用してインストールできます。

# 歴史
PyOpenGL は、1998 年に Mike Fletcher によって最初にリリースされました。当初は、Python アプリケーションで 3D グラフィックスと視覚効果を作成するためのツールとして開発されました。最初のリリース以来、PyOpenGL は Python で 3D グラフィックスを作成するための最も人気のあるライブラリの 1 つに成長しました。

# 特徴
PyOpenGL は、Python アプリケーションで 3D グラフィックスと視覚効果を作成するための次のような多くの機能を提供します。

- OpenGL API へのオブジェクト指向インターフェース
- 3D オブジェクトとテクスチャを操作するためのユーティリティ関数
- Windows、Mac OS X、および Linux のサポート
- カスタム シェーダーを作成する機能
- ハードウェア アクセラレーション レンダリングのサポート

# 例
次の例は、PyOpenGL を使用して単純な 3D キューブを作成する方法を示しています。

パイソン
OpenGL.GL を gl としてインポート

# キューブを作成する
頂点 = (
    (1, -1, -1),
    (1, 1, -1),
    (-1、1、-1)、
    (-1、-1、-1)、
    (1, -1, 1),
    (1, 1, 1),
    (-1、-1、1)、
    (-1、1、1)
)

エッジ = (
    (0, 1),
    (0, 3),
    (0, 4),
    (2, 1),
    (2, 3),
    (2, 7),
    (6, 3),
    (6, 4),
    (6, 7),
    (5, 1),
    (5, 4),
    (5,7)
)

デフ draw_cube():
    gl.glBegin(gl.GL_LINES)
    エッジ イン エッジの場合:
        エッジの頂点:
            gl.glVertex3fv(頂点[頂点])
    gl.glEnd()

draw_cube()
```

# 長所と短所
PyOpenGL は、Python アプリケーションで 3D グラフィックスと視覚効果を作成するための強力なライブラリです。 OpenGL API へのオブジェクト指向インターフェイスを提供し、3D オブジェクトとテクスチャを操作するための多数のユーティリティ関数が含まれています。ただし、PyOpenGL は、OpenGL API を十分に理解している必要があるため、習得が難しい場合があります。

# 関連技術
PyGame は、Python でゲームを作成するための一般的なライブラリです。イベント システム、オーディオとビデオの再生、ジョイスティックやゲームパッドなどの入力デバイスのサポートなど、ゲームを作成するための多くの機能を提供します。 PyGame は OpenGL API へのバインディングも提供するため、開発者はゲームで 3D グラフィックスと視覚効果を作成できます。