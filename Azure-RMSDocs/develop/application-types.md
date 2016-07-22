---
title: "アプリケーションの種類 | Azure RMS"
description: "このトピックでは、権限保護対応として作成できるアプリケーションの種類について説明します。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 872bb0c20db2ef8d661d321598a2b1fe61d69316
ms.openlocfilehash: a27d1921336a795df5a3c91b36b97846e74cca34


---

# アプリケーションの種類


このトピックでは、権限保護対応として作成できるアプリケーションの種類について説明します。

Rights Management サービス SDK 2.1 では、次のアプリケーションの種類が現在サポートされています。

## 単純なアプリケーション

単純なアプリケーションには、指定されたファイルを暗号化するために作成されたコマンド ライン ツールなどがあります。 権限保護に対応する単純なアプリケーションの例については「[IPCHelloWorld - サンプル アプリケーション](how-to-build-your-first-application.md)」を参照してください。

### サーバー モード アプリケーション

*サーバー モード*は、RMS で保護されたコンテンツの使用、保護、処理を行う非対話型アプリケーションのためのモードです。 例として、ファイル サーバー上のサービスとして動作し、機密性の高いドキュメントを自動的に保護する、*データ損失防止*アプリケーションが挙げられます。 このアプリケーションの種類の例については、[IpcDlp サンプルのページ](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)を参照してください。

アプリケーションで*サーバー モード*を使用する場合は、RMS サーバーをサイレント認証する必要があります。 *クライアント モード*とは異なり、サイレント認証に失敗した場合にも、RMS SDK 2.1 は資格情報プロンプトを開きません。 また、*サーバー モード*で実行しているときは、アプリケーション マニフェストも必要ありません。

API のセキュリティ モード設定の詳細については、「[Setting the API security mode (API のセキュリティ モードの設定)](setting-the-api-security-mode-api-mode.md)」を参照してください。

### リッチ クライアント アプリケーション

リッチ クライアント アプリケーションでは、ユーザーはグラフィカル ユーザー インターフェイス (GUI) を介してデータを表示および操作できます。 多くの場合、この GUI に表示されるデータは価値が高く、盗難されたり、誤って開示されたりすると問題になるデータです。 通常、情報の保護により既存のシナリオの強化がサポートされますが、情報の保護はこのアプリケーションを開発する主な目的ではありません。

リッチ クライアント アプリケーションで RMS SDK 2.1 を使用すると、次のことがサポートされます。

-   データを常に確実に暗号化する

-   保護されていない形式にユーザーがデータを抽出する (クリップボードを使用してコピーして貼り付けるなど) のを防ぐ

Microsoft のメモ帳は、単純なリッチ クライアント アプリケーションです。 Microsoft Office は、より複雑なリッチ クライアント アプリケーションです。

アプリケーションの保護の詳細については、「[Understanding usage restrictions (使用制限について)](understanding-usage-restrictions.md)」を参照してください。

## 関連項目

* [IpcDlp サンプルのページ](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
* [IPCHelloWorld - サンプル アプリケーション](how-to-build-your-first-application.md)
* [Setting the API security mode (API のセキュリティ モードの設定)](setting-the-api-security-mode-api-mode.md)
* [Understanding usage restrictions (使用制限について)](understanding-usage-restrictions.md)



<!--HONumber=Jun16_HO4-->


