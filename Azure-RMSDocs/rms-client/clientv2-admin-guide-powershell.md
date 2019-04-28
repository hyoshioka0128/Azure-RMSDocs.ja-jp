---
title: PowerShell を使用して、Azure Information Protection でラベル付けのクライアントの統合
description: 手順と、Azure Information Protection を管理する管理者向けの情報は、PowerShell を使用してラベル付けのクライアントを統合します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f3a0d3b3974714135289a8f3b262666b63739330
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181856"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理者ガイド: Azure Information Protection の統合されたクライアントで PowerShell の使用

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*
>
> "*手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたラベル付けクライアントをインストールするときに、PowerShell コマンドが自動的にインストールします。 自動化のためのスクリプトに追加できるコマンドを実行することでクライアントを管理できます。

PowerShell モジュールのコマンドレットがインストールされている**AzureInformationProtection**、ラベル付けのコマンドレットがあります。 以下に例を示します。

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|共有フォルダーで、ファイルの内容を検査したあと、指定した条件に基づいて、ラベル付けされていないファイルに自動的にラベルを付与します。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|独自の別のユーザー アカウントを使用して対話形式でファイルをラベルします。|

> [!TIP]
> 260 文字よりも長いパスとともにコマンドレットを使用するには、Windows 10 バージョン 1607 以降で利用できる次の[グループ ポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)を使用します。<br /> **ローカル コンピューター ポリシー** > **コンピューターの構成** > **管理用テンプレート** > **すべての設定** > **NTFS** > **Win32 の長いパスを有効にする** 
> 
> Windows Server 2016 の場合、Windows 10 用の最新の管理用テンプレート (.admx) をインストールすれば、同じグループ ポリシー設定を使用できます。
>
> 詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

このモジュールは、**\ProgramFiles (x86)\Microsoft Azure Information Protection** にインストールされ、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>AzureInformationProtection モジュールを使用するための前提条件

に加えて、AzureInformationProtection モジュールのインストールの前提条件、追加の前提条件の場合は Azure Information Protection のラベル付けコマンドレットを使用します。

1. Azure Rights Management サービスをアクティブ化する必要があります。

2. 自分のアカウントを使って他のユーザーのファイルから保護を削除するには: 

    - 組織のスーパー ユーザー機能を有効にし、自分のアカウントを Azure Rights Management のスーパー ユーザーとして構成する必要があります。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>前提条件 1: Azure Rights Management サービスをアクティブ化する必要があります

保護を適用する、Azure Information Protection テナントがアクティブでない場合の手順を参照してください。 [Azure Rights Management のアクティブ化](../activate-service.md)します。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。

ファイルから保護を削除するには、Rights Management の使用権限を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../configure-super-users.md)」をご覧ください。


## <a name="next-steps"></a>次の手順
PowerShell セッションでは、コマンドレットのヘルプの種類`Get-Help <cmdlet name> -online`します。 以下に例を示します。 

    Get-Help Set-AIPFileLabel -online

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)
