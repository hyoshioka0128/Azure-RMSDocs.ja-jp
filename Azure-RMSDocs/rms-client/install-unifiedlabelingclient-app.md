---
title: Azure Information Protection 統合ラベル付けクライアント (プレビュー) をダウンロードしてインストールする
description: ドキュメントと電子メールを分類および保護できるように、ユーザーが Windows 用 Azure Information Protection 統合ラベル付けクライアントのプレビュー バージョンをインストールするための手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/17/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 5d2f5c07ebc7f4844b0d35879ae00c7b9066cb6d
ms.sourcegitcommit: 6a732226a3c97fc06fcf815fbbb24a2e2faae209
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2018
ms.locfileid: "49359004"
---
# <a name="download-and-install-the-azure-information-protection-unified-labeling-client-preview"></a>Azure Information Protection 統合ラベル付けクライアント (プレビュー) をダウンロードしてインストールする

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

> [!NOTE]
> このクライアントはプレビュー段階にあり、変更される可能性があります。 ここでは統合ラベル付けストアを使用し、Office 365 セキュリティ/コンプライアンス センターから機密ラベルを含むポリシーをダウンロードします。 これらのラベルを使用するには、まずセキュリティ/コンプライアンス センターから発行する必要があります。 [詳細情報](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)

ドキュメントや電子メールにラベルを付けて保護できるように、このプレビュー クライアントをインストールするには対象となる PC のローカル管理者である必要があります。

さらに

- Azure Information Protection 統合ラベル付けクライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。

- Windows 7 SP1 を使用する場合、Azure Information Protection 統合ラベル付けクライアントには特定の更新プログラム KB 2533623 が必要です。 ご利用の PC にこの更新プログラムが必要で、まだインストールされていない場合、インストールは完了しますが、Azure Information Protection クライアントにこの更新プログラムが必要だというメッセージが表示されます。 この更新プログラムがインストールされるまで、Azure Information Protection 統合ラベル付けクライアントの機能すべてを使用できるようにはなりません。 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントをダウンロードしてインストールするには

Azure Information Protection 統合ラベル付けクライアントをインストールする前に、Office 365 セキュリティ/コンプライアンス センターでユーザーに発行される機密レベルがあることを確認します。 

Azure Information Protection 用に Azure portal から現在発行されているラベルがある場合は、[これらのラベル](../configure-policy-migrate-labels.md)をセキュリティ/コンプライアンス センターに移行できます。

1. プレビュー クライアントを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=57440)からダウンロードします。

2. ダウンロードされた実行可能ファイル **AzInfoProtection_For_Unified_Labeling.exe** を実行します。 続行を確認するメッセージが表示されたら、**[はい]** をクリックします。    

3. **Azure Information Protection クライアントのインストール** ページで、     
    - クラウドに接続できない場合に、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、デモ ポリシーをインストールするオプションを選択します。 ご自分のクライアントが Office 365 セキュリティ/コンプライアンス センターに接続されると、このデモ ポリシーは組織のラベル ポリシーに置き換えられます。

    - ライセンス条項および使用条件を読み、**[同意する]** をクリックします。    

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

## <a name="next-steps"></a>次の手順

Office 365 セキュリティ/コンプライアンス センターが現在使用している統合ラベル付けストアの詳細については、「[Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)」 (セキュリティ/コンプライアンス センターでの統合ラベル付け管理の可用性の発表) のブログ記事を参照してください。
