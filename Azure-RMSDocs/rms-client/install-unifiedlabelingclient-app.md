---
title: Azure Information Protection 統合ラベル付けクライアントをダウンロード & インストールする
description: ドキュメントと電子メールを分類して保護できるように、Windows 用の Azure Information Protection 統合ラベルクライアントをインストールするための手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: a7f98ca4414d9258799286753dc8323beb28c087
ms.sourcegitcommit: 7992e1dc791d6d919036f7aa98bcdd21a6c32ad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68427806"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>ユーザー ガイド: Azure Information Protection 統合ラベル付けクライアントをダウンロードしてインストールする

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

管理者が Azure Information Protection 統合されたラベル付けクライアントをインストールしていない場合は、自分で行うことができます。 ドキュメントや電子メールにラベルを付けて保護できるように、このクライアントをインストールするには対象となる PC のローカル管理者である必要があります。

さらに:

- Azure Information Protection 統合ラベル付けクライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。

- Windows 7 SP1 を使用する場合、Azure Information Protection 統合ラベル付けクライアントには特定の更新プログラム KB 2533623 が必要です。 ご利用の PC にこの更新プログラムが必要で、まだインストールされていない場合、インストールは完了しますが、Azure Information Protection クライアントにこの更新プログラムが必要だというメッセージが表示されます。 この更新プログラムがインストールされるまで、Azure Information Protection 統合ラベル付けクライアントの機能すべてを使用できるようにはなりません。 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントをダウンロードしてインストールするには

Azure Information Protection 統合ラベル付けクライアントをインストールする前に、Office 365 の秘密度ラベルを使用していることを管理者またはヘルプデスクに確認してください。

1. [Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から**AzInfoProtection_UL**をダウンロードします。

2. ダウンロードした実行可能ファイルを実行し、続行を確認するメッセージが表示されたら、[**はい]** をクリックします。

3. **[Azure Information Protection クライアントのインストール]** ページ上で、ライセンス条項および条件を読み、 **[同意する]** をクリックします。

4. 続行を確認するメッセージが表示されたら、 **[はい]** をクリックしてインストールが完了するまで待機します。

6. **[閉じる]** をクリックします。 Azure Information Protection 統合ラベル付けクライアントの使用を開始する前に、次の操作を行います。

    - コンピューターで Office 2010 を実行している場合、コンピューターを再起動し、最後の手順として次のセクションに進みます。    
        
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 インストールはこれで完了となります。クライアントを使用して、ドキュメントや電子メールにラベルを付けたり、保護したりできます。

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>Office 2010 で Azure Information Protection 統合ラベル付けクライアントをインストールする

前の指示に従い、Azure Information Protection 統合ラベル付けクライアントをインストールしたら、次の操作を行います。

1. Microsoft Word を開きます。 Azure Information Protection クライアントのインストール後に初めて Office 2010 アプリケーションを実行した場合、 **[Microsoft Azure Information Protection]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、サインイン プロセスを完了するには管理者の資格情報が必要であることが記されています。

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、 **[OK]** をクリックします。

3. **[ユーザーアクセス制御]** ダイアログ ボックスが表示された場合、 **[はい]** をクリックします。Azure Information Protection でレジストリが更新されます。

インストールはこれで完了となります。Azure Information Protection 統合ラベル付けクライアントを利用し、ドキュメントや電子メールにラベルを付けたり、保護したりすることができます。

## <a name="other-instructions"></a>その他の手順    
Azure Information Protection 統合されたラベル付けクライアントユーザーガイドのその他の操作方法については、次を参照してください。

- [目的に合ったトピックをクリックしてください](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
[管理者ガイド](clientv2-admin-guide.md)の「[ユーザー用に Azure Information Protection 統合されたラベル付けクライアントをインストール](clientv2-admin-guide-install.md)する」を参照してください。
