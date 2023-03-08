---
title: Continuous Integration
description: 
published: true
date: 2023-02-17T18:15:08.409Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:36:27.366Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Continuous Integration***English** version of this document is available*](/en/Knowledge-base/Dictionary/continuous-integration)
{.links-list}


#Overview
CI（連続統合）は、複数の貢献者のコード変更を共有リポジトリに定期的にマージするソフトウェア開発方法です。このプロセスは、コードベースが動作していてエラーがないことを確認するのに役立ちます。 CIはまた、開発をスピードアップし、チームがバグを迅速に識別、検出、修正するのに役立ちます。

#description
継続的な統合は、共有リポジトリで複数の開発者や他の貢献者のコード変更を頻繁にマージするプロセスです。これは、すべての貢献者が同じバージョンのコードベースで作業し、コードが作業状態にあることを確認するのに役立ちます。 CIは一般的に機敏なソフトウェア開発に使用され、しばしば自動化されたテストおよびコードレビュープロセスと組み合わせられます。

継続的な統合プロセスは、開発者がコード変更を共有リポジトリにプッシュするときに開始されます。これにより、コードのエラーと既存のコードとの競合を確認する自動化されたビルドプロセスがトリガーされます。エラーが見つからない場合、ビルドプロセスは自動テストを実行してコードが正しく機能していることを確認します。テストに失敗すると、プロセスが停止し、開発者に警告が表示されます。テストに合格すると、プロセスは続行され、コードの変更は共有コードベースにマージされます。

CIは、ソフトウェア開発に必要な時間と労力を削減するのに役立ちます。コードの変更を定期的にマージしてテストすることで、チームはバグが問題になる前にすばやく識別、検出、および修正できます。これにより、チームは敏捷性を維持し、開発に必要な時間を短縮し、製品品質を向上させることができます。

#余談
継続的な統合は、チームと開発環境の要件に応じてさまざまな方法で実装できます。一般的な方法には、JenkinsやTravis CIなどの**継続的な統合ツール**を使用することが含まれます。これらのツールは、ビルドプロセスを自動化し、テストを実行し、複数の貢献者のコード変更をマージするように設計されています。

また、チームはGitやSubversionなどの**バージョン管理システム**を使用してコードの変更を追跡できます。バージョン管理システムは時間の経過とともに変更を追跡するため、チームは異なるバージョンのコードベースを簡単に確認して比較できます。これにより、バグを簡単に識別、検出、修正できます。

#関連リンク
- [持続的統合とは**DigitalOcean*](https://www.digitalocean.com/community/tutorials/what-is-continuous-integration)
- [継続的な統合ツール：Jenkins、Travis CI、CircleCI * Blogの比較 - CircleCI *]（https://circleci.com/blog/continuous-integration-tools-comparing-jenkins-travis-ci-and-circleci/）
- [バージョン管理システム：彼らは何ですか？*DigitalOcean*](https://www.digitalocean.com/community/tutorials/version-control-systems-what-are-they)
{.links-list}