---
title: Xamarin を使用したクロスプラットフォーム モバイル アプリの開発
description: 
published: true
date: 2023-01-31T11:57:41.163Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:57:39.511Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Developing Cross-Platform Mobile Apps with Xamarin***English** version of this document is available*](/en/Knowledge-base/Common/developing-cross-platform-mobile-apps-with-xamarin)
{.links-list}



#Xamarinによるクロスプラットフォームモバイルアプリの開発

Xamarinは、開発者がC#を使用してAndroidおよびiOS用のネイティブアプリケーションを作成できるクロスプラットフォームの開発ツールです。この記事では、クロスプラットフォームのモバイル開発にXamarinを使用する利点について説明し始めるための実用的なガイドを提供します。

## Xamarinを使用する理由

次のモバイル開発プロジェクトでXamarinの使用を検討する理由はいくつかあります。

- **Xamarinは無料でオープンソースです** - Xamarinは商用プロジェクトでも無料で利用できます。さらに、Xamarinプラットフォームはオープンソースなので、必要に応じて開発に貢献できます。

- **Xamarinは優れた言語サポートを提供します** - Xamarinはよく設計され、強力で現代的な言語であるC#プログラミング言語を使用しています。 C#はオブジェクト指向プログラミングをうまくサポートし、LINQなどの関数型プログラミング機能も提供します。

- **Xamarinには素晴らしいツールがあります** - Xamarin開発環境には、アプリケーションの開発、テスト、デプロイに必要なすべてが含まれています。 Xamarin Studio IDEはVisual Studioに似ており、優れた開発環境を提供します。

- **Xamarinは強力なコミュニティサポートを提供します** - サポートとサポートを提供できる大規模でアクティブなXamarinコミュニティがあります。

## Xamarinを始めよう

このセクションでは、Xamarin開発環境を設定し、簡単な「Hello、World」アプリケーションを作成するプロセスについて説明します。

### 前提条件

始める前に必要ないくつかのことがあります。

- WindowsまたはmacOSを実行しているコンピュータ
- 有効なMicrosoftアカウント（Visual Studioにログインするために必要）

### Xamarinプラットフォームのインストール

最初にすべきことは、Xamarinプラットフォームをインストールすることです。最も簡単な方法は、MicrosoftのVisual Studio IDEをダウンロードしてインストールすることです。

Visual Studioがインストールされたら、起動してMicrosoftアカウントでログインします。ログインすると、Visual Studioのようこそ画面が表示されます。インストールプロセスを開始するには、「インストール」ボタンをクリックしてください。

![Visual Studio スタート画面](https://i.imgur.com/p0sU6Tv.png)

インストールプロセスが完了すると、コンピュータを再起動するように求められます。コンピュータが再起動したら、Visual Studioを再起動して[新しいプロジェクトを作成]ボタンをクリックします。

![Visual Studio で新しいプロジェクトを作成](https://i.imgur.com/7bTzC4I.png)

「New Project」ダイアログボックスで「Cross-Platform」タブを選択し、「Blank App（Android、iOS、Windows）」テンプレートを選択します。プロジェクト名を指定して[作成]ボタンをクリックします。

![Visual Studioで新しいXamarinプロジェクトを作成する]（https://i.imgur.com/eLFgU6O.png）

この時点で、ターゲットプラットフォームを尋ねるダイアログボックスが表示されます。この例では、AndroidとiOSのみを選択します。そのプラットフォームもターゲットとして指定する場合は、Windowsを選択することもできます。

![Xamarinプロジェクトの対象プラットフォームを選択](https://i.imgur.com/KzZ7bVx.png)

ターゲットプラットフォームを選択して[作成]ボタンをクリックすると、Visual Studioで新しいプロジェクトを作成します。

### コードを書く

これでプロジェクトが設定されているので、いくつかのコードを書くことができます。 「ソリューションエクスプローラ」ウィンドウで「MainPage.xaml」ファイルを展開し、「MainPage.xaml.cs」ファイルをダブルクリックしてエディタで開きます。

「MainPage.xaml.cs」ファイルの内容を次のコードに置き換えます。

```csharp
using System;

using Xamarin.Forms;

namespace HelloWorld
{
    public class MainPage: ContentPage
    {
        public MainPage()
        {
            Content = new Label
            {
                Text="Hello, World!",
                HorizontalOptions = LayoutOptions.Center,
                VerticalOptions = LayoutOptions.Center
            };
        }
    }
}
```

このコードは、画面の中央に表示される単純な「Hello、World」ラベルを定義します。

###アプリテスト

ここでいくつかのコードを書いたので、アプリが期待どおりに機能するかどうかをテストしましょう。 Visual Studioで[デバッグ]メニューを選択し、[デバッグせずに開始]メニュー項目を選択します。

![Visual StudioでデバッグせずにXamarinアプリを起動](https://i.imgur.com/W2nJNcu.png)

これで、Visual Studioが選択したシミュレータまたはエミュレータでアプリを起動します。 「Hello、World！」メッセージが表示されます。画面中央のラベル。

!["Hello, World!" iOSシミュレータで実行されているアプリ]（https://i.imgur.com/5MWK0bY.png）

おめでとうございます！ Xamarinを使用して、最初のクロスプラットフォームのモバイルアプリを作成しました。

##結論

この記事では、クロスプラットフォームのモバイル開発にXamarinを使用する利点について議論し始めるための実用的なガイドを提供しました。 Xamarinは、単一のコードベースを使用して複数のプラットフォーム用のネイティブアプリケーションを作成するための優れたツールです。