---
title: 暗号化設定を操作する方法 | Azure RMS
description: Azure RMS の暗号化パッケージおよび暗号化パッケージを使用するためのコード スニペットを紹介します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 0caabd18ef06af0daaff44e8829b3bd9750a788b
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68791929"
---
# <a name="how-to-work-with-encryption-settings"></a>方法: 暗号化設定の操作

このトピックでは、暗号化パッケージについて概説し、その使い方を示すいくつかのコード スニペットを紹介します。

## <a name="support-for-aes-256-the-new-default"></a>AES 256 のサポート, 新しい既定

*AES 256* ベースの暗号化は新しい既定なので、RMS SDK 2.1 の 2015 年 3 月の更新プログラムがビルドされていることを想定しており、コードを追加する必要はありません。 *AES 256* で強化されたセキュリティ メリットを得るには、このリリースでアプリケーションを更新することを強くお勧めします。

> [!IMPORTANT]
> *AES 256* で保護されたファイルの消費量のサポートは、[2014 年 10 月のリリース](release-notes-rtm.md)より開始されています。 2014 年 10 月より前の SDK のバージョンでビルドされたアプリケーションを実行している場合、この更新プログラムによってアプリケーションは中断されます。 ビルドしているアプリケーションの顧客が更新後の SDK を使用していない場合、最新バージョンのアプリケーションにすぐに更新する意向があることを確認してください。

 
## <a name="api-encryption-support"></a>API 暗号化のサポート

[2015 年 3 月の更新](release-notes-rtm.md)より、次の 3 つのフラグが API および関連する暗号化パッケージに組み込まれています。

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (非推奨のアルゴリズムとも呼ばれます)

暗号化パッケージ フラグ (「[Preferred encryption](https://msdn.microsoft.com/library/dn974065.aspx)」(推奨される暗号化) を参照) はライセンス プロパティ フラグ (*IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE*) と併用できます。

新しいライセンス プロパティの使用方法を示すいくつかの単純なコード スニペットは次のとおりです。

## <a name="deprecated-algorithms"></a>非推奨のアルゴリズム

API の *IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS* フラグは非公開となりました。 今後、このフラグを参照しても、アプリケーションでコンパイルされませんが、このフラグを使用して既にビルドされたアプリケーションではこのフラグを API コード内でプライベートに使用するため、引き続き機能します。

フラグを 1 つ変更するだけで、古い非推奨の暗号化アルゴリズムのフラグの機能を利用できます。 次のコード スニペットの例をご覧ください。

## <a name="protect-files-with-aes-256-cbc4k"></a>AES 256 CBC4K によるファイルの保護

コードの変更は必要ありません。*AES 256* CBC4K は既定値です。

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);


## <a name="protect-files-with-aes-128-cbc4k"></a>AES 128 CBC4K によるファイルの保護

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);


## <a name="protect-files-with-aes-128-ecb-deprecated-algorithms"></a>AES 128 ECB (非推奨のアルゴリズム) によるファイルの保護

この例は*非推奨のアルゴリズム*をサポートする新しい方法も示しています。

    C++

    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID,
                                    0,
                                    NULL,
                                    &amp;pLicenseHandle);

    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;

    hr = IpcSetLicenseProperty(pLicenseHandle,
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);

