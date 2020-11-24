---
title: Azure Information Protection で対称キーを更新する方法
description: この記事では、Azure Information Protection で対称キーを更新する手順について説明します。
keywords: ''
author: msmbaldwin
manager: barbkess
ms.author: mbaldwin
ms.date: 03/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0b8c8f0-6ed5-48bb-8155-ac4f319ec178
ms.custom: dev
ms.openlocfilehash: 539ad36df7d2c74a00650347abb8ed067dd743c7
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570022"
---
# <a name="how-to-renew-the-symmetric-key-in-azure-information-protection"></a>方法: Azure Information Protection で対称キーを更新する

**対称キー** は、対称キー暗号化方式でメッセージを暗号化および復号化するシークレットです。  

Azure Active Directory (Azure AD) では、アプリケーションを表すサービス プリンシパル オブジェクトを作成するプロセスで、アプリケーションを検証するための 256 ビット対称キーも生成されます。 この対称キーは、既定では 1 年間有効です。 

次の手順では、対称キーを更新する方法を示します。 

## <a name="prerequisites"></a>前提条件

* 「[Azure AD Powershell Reference](/powershell/msonline/)」(Azure AD Powershell リファレンス) の説明に従って、Azure Active Directory (Azure AD) PowerShell モジュールをインストールする必要があります。


## <a name="renewing-the-symmetric-key-after-expiry"></a>有効期限が切れた対称キーの更新

アプリケーションに関連付けられている対称キーの有効期限が切れた場合、新しいサービス プリンシパルを作成する必要はありません。 代わりに、Microsoft Online Services (MSol) によって提供される [PowerShell コマンドレット](/powershell/module/msonline)を使って、既存のサービス プリンシパルに新しい対称キーを発行できます。

このプロセスを説明するために、コマンドを使用して新しいサービスプリンシパルを既に作成しているとし [`New-MsolServicePrincipal`](/powershell/msonline/v1/new-msolserviceprincipalcredential) ます。

```
New-MsolServicePrincipalCredential -ServicePrincipalName "SupportExampleApp"
```

作成プロセスでは、次に示すように対称キーと **AppPrincipalId** が作成されます。

```
The following symmetric key was created as one was not supplied
ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

DisplayName : SupportExampleApp
ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
TrustedForDelegation : False
AccountEnabled : True
Addresses : []
KeyType : Symmetric
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

この対称キーの有効期限は、2018 年 3 月 22 日午後 3 時 27 分 53 秒です。 この時刻以降もサービス プリンシパルを使用するには、対称キーを更新する必要があります。 これを行うには、コマンドを使用し [`New-MsolServicePrincipalCredential`](/powershell/msonline/v1/new-msolserviceprincipalcredential) ます。 

```
New-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963
```

このコマンドでは、指定した **AppPrincipalId** の新しい対称キーが作成されます。

```
The following symmetric key was created as one was not supplied ON8YYaMYNmwSfMX625Ei4eC6N1zaeCxbc219W090v28-
```
コマンドを使用して、 [`GetMsolServicePrincipalCredential`](/powershell/msonline/v1/get-msolserviceprincipalcredential) 新しい対称キーが正しいサービスプリンシパルに関連付けられていることを確認できます (図を参照)。 このコマンドでは、現在サービス プリンシパルに関連付けられているすべてのキーが一覧表示されることに注意してください。

```
Get-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963 -ReturnKeyValues $true

Type : Symmetric
Value :
KeyId : c1ac145f-e899-4c90-8a02-2cef40054fc5
StartDate : 3/24/2017 10:11:07 PM
EndDate : 3/24/2018 10:11:07 PM
Usage : Verify

Type : Symmetric
Value :
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

対称キーが正しいサービス プリンシパルに実際に関連付けられていることを確認した後は、サービス プリンシパルの認証パラメーターを新しいキーで更新できます。 

コマンドを使用して古い対称キーを削除し、コマンドを使用してキーが削除されていることを [`Remove-MsolServicePrincipalCredential`](/powershell/msonline/v1/remove-msolserviceprincipalcredential) 確認でき `Get-MsolServicePrincipalCredential` ます。

```
Remove-MsolServicePrincipalCredential -KeyId acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe -ObjectId 0ee53770-ec86-409e-8939-6d8239880518
```

## <a name="related-topics"></a>関連トピック

* [方法: クラウドベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)
* [Azure Active Directory MSOnline Powershell リファレンス](/powershell/msonline/)