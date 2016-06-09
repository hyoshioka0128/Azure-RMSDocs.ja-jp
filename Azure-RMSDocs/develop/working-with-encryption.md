---
# required metadata

title: 暗号化の操作 |Azure RMS
description: 暗号化パッケージの概要
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: B1D2C227-F43D-4B18-9956-767B35145792
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** この SDK コンテンツは最新のものではありません。 しばらくの間、[最新版](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)の文書は MSDN でご覧ください。 **
# 暗号化の操作

このトピックでは、暗号化パッケージについて概説し、その使い方を示すいくつかのコード スニペットを紹介します。

## AES 256 のサポート, 新しい既定

*AES 256* ベースの暗号化は新しい既定なので、RMS SDK 2.1 の 2015 年 3 月の更新プログラムがビルドされていることを想定しており、コードを追加する必要はありません。 *AES 256* で強化されたセキュリティ メリットを得るには、このリリースでアプリケーションを更新することを強くお勧めします。

> [!IMPORTANT]
> *AES 256* で保護されたファイルの消費量のサポートは、[2014 年 10 月のリリース](release-notes-rtm.md)より開始されています。 2014 年 10 月より前の SDK のバージョンでビルドされたアプリケーションを実行している場合、この更新プログラムによってアプリケーションは中断されます。 ビルドしているアプリケーションの顧客が更新後の SDK を使用していない場合、最新バージョンのアプリケーションにすぐに更新する意向があることを確認してください。

 
## API 暗号化のサポート

[2015 年 3 月の更新](release-notes-rtm.md)より、次の 3 つのフラグが API および関連する暗号化パッケージに組み込まれています。

-   IPC\_ENCRYPTION\_PACKAGE\_AES256\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_CBC4K
-   IPC\_ENCRYPTION\_PACKAGE \_AES128\_ECB (非推奨アルゴリズムとも呼ばれます)

暗号化パッケージ フラグ (「[**Preferred encryption (推奨される暗号化)**](/rights-management/sdk/2.1/api/win/constants#msipc_preferred_encryption)」を参照) は新しいライセンス プロパティ フラグ (**IPC\_LI\_PREFERRED\_ENCRYPTION\_PACKAGE**) と併用できます。

新しいライセンス プロパティの使用方法を示すいくつかの単純なコード スニペットは次のとおりです。

## 非推奨のアルゴリズム

API の **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** フラグは非公開となりました。 今後、このフラグを参照しても、アプリケーションでコンパイルされませんが、このフラグを使用して既にビルドされたアプリケーションではこのフラグを API コード内でプライベートに使用するため、引き続き機能します。

フラグを 1 つ変更するだけで、古い非推奨の暗号化アルゴリズムのフラグの機能を利用できます。 次のコード スニペットの例をご覧ください。

## AES 256 CBC4K によるファイルの保護

コードの変更は必要ありません。*AES 256* CBC4K は既定値です。

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    

## AES 128 CBC4K によるファイルの保護

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    
    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_CBC4K; 
    
    hr = IpcSetLicenseProperty(pLicenseHandle, 
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE,
                           &amp;dwEncryptionMode);
    

## AES 128 ECB (非推奨アルゴリズム) によるファイルの保護

この例は*非推奨アルゴリズム*をサポートする新しい方法も示しています。

    
    hr = IpcCreateLicenseFromTemplateID(pcTil-&gt;aTi[0].wszID, 
                                    0, 
                                    NULL, 
                                    &amp;pLicenseHandle);
    
    DWORD dwEncryptionMode = IPC_ENCRYPTION_PACKAGE_AES128_ECB;
    
    hr = IpcSetLicenseProperty(pLicenseHandle, 
                           false,
                           IPC_LI_PREFERRED_ENCRYPTION_PACKAGE, 
                           &amp;dwEncryptionMode);
    
 

 





<!--HONumber=Jun16_HO1-->


