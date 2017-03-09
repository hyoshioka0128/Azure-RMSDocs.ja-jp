---
title: "権限保護対応アプリケーションをデバッグする方法 | Azure RMS"
description: "このトピックでは、アプリケーションをデバッグし、Windows イベント ログを使用する方法について説明します。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 6F6C7651-6A6E-45DD-A0C5-F036F803249B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: da5a9fa1a2c2eaccb6768914a0c425983b14fdbe


---

# <a name="how-to-debug-a-rights-enabled-application"></a>方法: 権限保護対応アプリケーションのデバッグ

このトピックでは、アプリケーションをデバッグし、Windows イベント ログを使用する方法について説明します。

## <a name="debugging-your-application"></a>アプリケーションのデバッグ

Rights Management サービス SDK 2.1 では、ランタイムの開発者バージョンでのアンチデバッグ機能のチェックは無効になっています。

デバッグ トレースは、次のレジストリ キーを使用して有効にすることができます (デバッグ トレースを無効にするには、値を 0 に変更します)。このリリースでは、デバッグを実行するのに何も必要ありません。


```
HKEY_LOCAL_MACHINE
   SOFTWARE
      Microsoft
         MSIPC
            "Trace" = 00000001
            Data type
            dword
```

### <a name="application-logging-by-using-the-windows-event-log"></a>Windows イベント ログを使用したアプリケーションのログ記録

イベント ログの名前は "Microsoft-RMS-MSIPC/Debug" です。 これは、Windows イベント ビューアーでログが表示される場所が "アプリケーションとサービス ログ\\Microsoft\\RMS\\MSIPC\\Debug" であることを意味します。

**注**: ログは既定で有効に設定され、詳細レベル 3 に設定されます。

 

ログ機能の設定を変更するには、Windows イベント ビューアーの UI か、Windows の組み込みコマンド ライン ツールである Wevtutil を使用できます。

Wevtutil インターフェイスを使うと、ログの詳細レベルを制御できます。

現時点では、3 つのログ記録レベルがサポートされています。

-   レベル 2 - エラー
-   レベル 3 - 警告
-   レベル 4 - 情報

たとえば、次のコマンドは、MSIPC イベント ログを有効にし、詳細レベルを "情報" に設定します。

**wevtutil sl Microsoft-RMS-MSIPC/Debug /e:true /l:4**

**注**: Windows イベント ビューアーで、**[表示]** メニューの **[分析およびデバッグ ログの表示]** を選択すると、MSIPC デバッグ ログが表示されます。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


