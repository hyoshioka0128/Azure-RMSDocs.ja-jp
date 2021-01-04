---
title: Azure Information Protection 統合ラベルクライアントをインストールするための追加の要件
description: エンタープライズネットワークに統一されたラベル付けクライアントをインストールするための追加システム要件を理解する必要がある管理者向けの情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/27/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c93b0a338f25b058e517c4c2bb746ccaa6e41a69
ms.sourcegitcommit: 0ac52ea741f205692406f0f82c74c65c23ee3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/27/2020
ms.locfileid: "97792315"
---
# <a name="additional-requirements-for-installing-the-unified-labeling-client-on-enterprise-networks"></a>エンタープライズネットワークに統一されたラベル付けクライアントをインストールするための追加の要件

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP For windows And office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。*
>
>***手順**: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 従来のクライアントについては、「 [従来のクライアント管理者ガイド](client-admin-guide-install.md)」を参照してください。

Azure Information Protection 統合されたラベル付けクライアントをエンタープライズネットワークにインストールする前に、コンピューターに必要なオペレーティングシステムのバージョンとアプリケーションがあることを確認してください。 Azure Information Protection: [Azure Information Protection の要件](../requirements.md)を確認してください。 

次に、Azure Information Protection 統合されたラベル付けクライアントをインストールするために必要な追加の項目があることを確認します。

> [!NOTE]
> これらの要件のすべてが、インストールソフトウェアによって検証されるわけではありません。
>

## <a name="microsoft-net-framework-requirements"></a>Microsoft .NET Framework の要件

既定では Azure Information Protection 統合されたラベル付けクライアントの完全インストールには、Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。 

このフレームワークがインストールされていない場合は、実行可能ファイルインストーラーのセットアップウィザードによって、この前提条件のダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。  

[Azure Information Protection ビューアー](clientv2-view-use-files.md)を独自にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。 

> [!IMPORTANT]
> Microsoft .NET Framework 4.5.2 の最小バージョンがインストールされていない場合は、インストールソフトウェアによってダウンロードまたはインストール *されません* 。
> 

### <a name="disable-exploit-protection-net-2-or-3-only"></a>Exploit protection を無効にする (.NET 2 または3のみ)

AIP クライアントは、 [Exploit protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) が有効になっている .net 2 または3のコンピューターではサポートされていません。 

このような場合は、.NET バージョンをアップグレードすることをお勧めします。 

.NET バージョン2または3を保持する必要がある場合は、AIP クライアントをインストールする前に、 [Exploit protection を無効](../known-issues.md#known-issues-for-aip-and-exploit-protection) にしてください。

## <a name="windows-powershell-minimum-requirements"></a>Windows PowerShell の最小要件

クライアントの PowerShell モジュールには、Windows PowerShell 4.0 の最小バージョンが必要です。

以前のオペレーティングシステムで作業している場合は、すべての PowerShell を手動で実行しなければならない場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](https://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 

> [!IMPORTANT]
> インストーラーでは、この前提条件を確認したりインストールしたりすることは *ありません* 。 
>
> 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「`$PSVersionTable`」と入力します。  
> 


## <a name="screen-resolution-requirements"></a>画面の解像度の要件

解像度が **800x600** 以下のクライアントコンピューターでは、エクスプローラーでファイルまたはフォルダーを右クリックして [ **分類と保護の Azure Information Protection** ] ダイアログボックスを完全に表示することはできません。   

## <a name="admin-permissions"></a>管理者のアクセス許可

Azure Information Protection の統合ラベル付けクライアントをインストールするには、クライアントコンピューターに対するローカルの管理アクセス許可が必要です。
        
## <a name="windows-10-requirements"></a>Windows 10 要件

Office 2010 を実行しているコンピューターには、クライアントインストールに含まれている **Microsoft Online Services サインインアシスタントバージョン 7.250.4303.0** が必要です。 

新しいバージョンのサインインアシスタントがある場合は、Azure Information Protection 統合ラベル付けクライアントをインストールする前にアンインストールしてください。 

たとえば、バージョンを確認し、[**コントロールパネル]** プログラムを使用してサインインアシスタントをアンインストールし、[  >    >  **プログラムのアンインストールまたは変更**] を使用します。 

Windows 10 バージョン 1809 の場合のみ、17763.348 より前のオペレーティング システム ビルドでは、Office アプリケーションに正しい Information Protection バーが確実に表示されるように、[2019 年 3 月 1 日—KB4482887 (OS ビルド 17763.348)](https://support.microsoft.com/help/4482887/windows-10-update-kb4482887) がインストールされます。 Office 365 1902 以降をお持ちの場合、この更新プログラムは必要ありません。    

## <a name="configure-your-group-policy-to-prevent-disabling-aip"></a>AIP が無効にならないようにグループポリシーを構成する

Office バージョン2013以降では、Office アプリケーション用の **Microsoft Azure Information Protection** アドインが常に有効になるように、グループポリシーを構成することをお勧めします。  このアドインがなければ、ユーザーは Office アプリケーションでドキュメントや電子メールにラベルを付けることができません。   

Word、Excel、PowerPoint、および Outlook では、 [office 2013 および office 2016 プログラムのグループポリシー設定が原因で、「アドインが読み込まれていません](https://support.microsoft.com/help/2733070/no-add-ins-loaded-due-to-group-policy-settings-for-office-2013-and-off)」に記載されている **管理対象アドインの** グループポリシー設定の一覧を使用します。 

AIP に次のプログラム識別子 (ProgID) を指定し、オプションを1に設定します。この **アドインは常に有効になっ** ています。

|Application  |ProgID  |
|---------|---------|
|Word     |     `MSIP.WordAddin`    |
|Excel     |  `MSIP.ExcelAddin`       |
|PowerPoint     |   `MSIP.PowerPointAddin`      |
|Outlook | `MSIP.OutlookAddin` |
| | | 
    

## <a name="next-steps"></a>次のステップ

引き続き管理者ガイドを参照してください  [。 Azure Information Protection 統合されたラベル付けクライアントをユーザーにインストール](clientv2-admin-guide-install.md)します。

詳細については、次を参照してください。

- [クライアントのファイルと使用状況ログ](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)