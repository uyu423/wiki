---
title: Hypervisor
description: 
published: true
date: 2023-02-17T18:15:50.595Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:57:41.068Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Hypervisor***English** version of this document is available*](/en/Knowledge-base/Dictionary/hypervisor)
{.links-list}


#Overview
**ハイパーバイザー**は、物理サーバー上で仮想マシン（VM）を作成して実行するソフトウェアベースの仮想化技術です。複数のオペレーティングシステムとアプリケーションを同じハードウェアで実行できるため、仮想化コンピューティング環境を作成できます。

#History
仮想化の概念は、1960年代と1970年代の**時分割**システムの開発とともに導入されました。これらのシステムにより、複数のユーザーが同じコンピューティングリソースにアクセスでき、リソースを効率的に使用できます。最初の商用ハイパーバイザーであるIBMのDIS / VMSは1978年にリリースされました。

#description
ハイパーバイザーは、物理ハードウェアとオペレーティングシステムの間にあるソフトウェア層です。複数のゲストオペレーティングシステムを同じ物理サーバー上で実行できるため、仮想化コンピューティング環境を作成できます。ハイパーバイザーは物理サーバーに**仮想マシン**（VM）を作成します。各VMには独自のオペレーティングシステム、アプリケーション、およびデータがあり、同じサーバー上の他のVMとは独立して管理できます。

ハイパーバイザーは、CPU、メモリ、ストレージなどの物理サーバーのリソースを管理し、VMに割り当てます。ゲストオペレーティングシステムが互いに分離され、物理ハードウェアに直接アクセスできるようにする**仮想化レイヤ**も提供します。

最も一般的なタイプのハイパーバイザーは、既存のオペレーティングシステムで実行されている**ホスト型ハイパーバイザー**です。 VMware ESXi と Microsoft Hyper-V の例があります。他のタイプは、物理ハードウェアで直接実行される**ベアメタルハイパーバイザー**です。 VMware ESX および Microsoft Hyper-V サーバーの例があります。

#関連リンク
- [ハイパーバイザーとは* VMware*](https://www.vmware.com/resources/compatibility/what-is-a-hypervisor.html)
- [Hypervisor*Microsoft*](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/hypervisor-overview)
- [ハイパーバイザータイプ：総合ガイド*Ravello Systems*](https://ravellosystems.com/hypervisor-types-guide/)
{.links-list}