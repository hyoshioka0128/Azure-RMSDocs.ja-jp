---
# required metadata

title: 運用環境のアプリケーションへの署名 | Azure RMS
description: このトピックでは、運用モードのアプリケーションに署名するプロセスについて説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c73fde39-6e16-470c-800e-59ab04c78f5f

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 運用環境のアプリケーションへの署名

このトピックでは、運用モードのアプリケーションに署名するプロセスについて説明します。

## 権限保護対応アプリケーションへの署名

次の手順では、運用前階層向けにアプリケーションに既に署名していると仮定しています。 まだ署名していない場合は、「[Testing your rights-enabled application (権限保護対応アプリケーションのテスト)](running-your-first-application.md)」に説明されている手順を実行してください。

Microsoft から運用証明書を受信すると、次のファイルがあることになります。

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

これらのファイルを、*GenManifest.exe* およびアプリケーション バイナリ (.exe) と同じディレクトリに格納します。

-   次の手順に従って、運用証明書を使用して新しい MCF ファイルを作成します。

    -   新しいディレクトリを作成し、この新しいディレクトリに対象のファイルを格納します。 Notepad.exe を使用して、アプリケーションの MCF ファイルを作成します。 ファイルの内容は次のとおりです。

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   次のコマンドを実行してアプリケーションに署名します。

        **genmanifest.exe -chain ProductionCertificate.xml** *YourAppName***.mcf** *YourAppName***.exe.man**

        Genmanifest が正常に実行されると、次のテキストのみが表示されます。

        Genmanifest の実行が失敗した場合は、エラー メッセージが表示されます。

    -   *YourAppName*.exe.man は、必ず *YourAppName*.exe と同じディレクトリに配置してください。

### 関連項目

* [使用方法](how-to-use-msipc.md)
* [権限保護対応アプリケーションのテスト](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO3-->


