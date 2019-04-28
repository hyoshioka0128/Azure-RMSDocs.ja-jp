---
title: ダウンロードとインストールが、Azure Information Protection クライアントのラベル付けを統合
description: ユーザーを分類して、ドキュメントや電子メールを保護できるように、Windows 用 Azure Information Protection の統一されたラベル付けクライアントをインストールする手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 563ddb6d91ef59ee96cf00dba973b7e612bbc780
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180955"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-unified-labeling-client"></a>ユーザー ガイド: ダウンロードして、Azure Information Protection の統一されたラベル付けクライアントのインストール

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> "*手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

管理者がの Azure Information Protection の統合されたラベル付けクライアントがインストールされない場合は、自身でを行うことができます。 ドキュメントや電子メールにラベルを付けて保護できるように、このクライアントをインストールするには対象となる PC のローカル管理者である必要があります。

さらに:

- Azure Information Protection 統合ラベル付けクライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。

- Windows 7 SP1 を使用する場合、Azure Information Protection 統合ラベル付けクライアントには特定の更新プログラム KB 2533623 が必要です。 ご利用の PC にこの更新プログラムが必要で、まだインストールされていない場合、インストールは完了しますが、Azure Information Protection クライアントにこの更新プログラムが必要だというメッセージが表示されます。 この更新プログラムがインストールされるまで、Azure Information Protection 統合ラベル付けクライアントの機能すべてを使用できるようにはなりません。 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントをダウンロードしてインストールするには

Azure Information Protection の統合されたラベル付けクライアントをインストールする前に Office 365 の機密ラベルを使用している、管理者やヘルプ デスクに確認します。

1. ダウンロード**AzInfoProtection_UL.exe**から、 [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)します。

2. ダウンロードされた実行可能ファイルの実行を続行する場合をクリックします**はい**します。

3. **[Azure Information Protection クライアントのインストール]** ページ上で、ライセンス条項および条件を読み、**[同意する]** をクリックします。

4. 続行を確認するメッセージが表示されたら、**[はい]** をクリックしてインストールが完了するまで待機します。

6. **[閉じる]** をクリックします。 Azure Information Protection 統合ラベル付けクライアントの使用を開始する前に、次の操作を行います。

    - コンピューターで Office 2010 を実行している場合、コンピューターを再起動し、最後の手順として次のセクションに進みます。    
        
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 インストールはこれで完了となります。クライアントを使用して、ドキュメントや電子メールにラベルを付けたり、保護したりできます。

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>Office 2010 で Azure Information Protection 統合ラベル付けクライアントをインストールする

前の指示に従い、Azure Information Protection 統合ラベル付けクライアントをインストールしたら、次の操作を行います。

1. Microsoft Word を開きます。 Azure Information Protection クライアントのインストール後に初めて Office 2010 アプリケーションを実行した場合、**[Microsoft Azure Information Protection]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、サインイン プロセスを完了するには管理者の資格情報が必要であることが記されています。

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[OK]** をクリックします。

3. **[ユーザーアクセス制御]** ダイアログ ボックスが表示された場合、**[はい]** をクリックします。Azure Information Protection でレジストリが更新されます。

インストールはこれで完了となります。Azure Information Protection 統合ラベル付けクライアントを利用し、ドキュメントや電子メールにラベルを付けたり、保護したりすることができます。

## <a name="other-instructions"></a>その他の手順    
Azure Information Protection から複数の操作手順については、クライアント ユーザー ガイドのラベル付けを統合しました。

- [目的に合ったトピックをクリックしてください](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
参照してください[ユーザーの Azure Information Protection の統合されたラベル付けクライアントをインストール](clientv2-admin-guide-install.md)から、[管理者ガイド](clientv2-admin-guide.md)します。
