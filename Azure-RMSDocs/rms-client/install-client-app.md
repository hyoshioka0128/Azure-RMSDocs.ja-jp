---
title: Azure Information Protection クラシッククライアントをダウンロード & インストールする
description: ドキュメントと電子メールを分類して保護するために、ユーザーが Windows 用の Azure Information Protection クラシッククライアントをインストールする手順を説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: f27be62467939d116bf36aaee4189911f096aa52
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385133"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-classic-client"></a>ユーザーガイド: Azure Information Protection クラシッククライアントをダウンロードしてインストールする

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、「統一された [ラベル付けユーザーガイド](install-unifiedlabelingclient-app.md)」を参照してください。

> [!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

管理者が Azure Information Protection クライアントをインストールしない場合、自分でインストールできます。 ドキュメントや電子メールにラベルを付けて保護できるように、このクライアントをインストールするには対象となる PC のローカル管理者である必要があります。

さらに:

- Azure Information Protection クライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。


## <a name="to-download-and-install-the-azure-information-protection-client"></a>Azure Information Protection クライアントをダウンロードしてインストールするには

Azure Information Protection classic クライアントは、2021年3月に非推奨となる予定です。 

AIP クラシック クライアントをデプロイするには、サポート チケットを作成してダウンロード アクセスを取得します。

1. **AzInfoProtection.exe** ファイルを実行して、インストールを開始します。 続行を確認するメッセージが表示されたら、[**はい**] をクリックします。    

1. **Azure Information Protection クライアントのインストール** ページで、     
    - クラウドに接続できない場合に、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、デモ ポリシーをインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。    

    - ライセンス条項および使用条件を読み、**[同意する]** をクリックします。    

1. 続行を確認するメッセージが表示されたら、**[はい]** をクリックしてインストールが完了するまで待機します。    

1. **[閉じる]** をクリックします。 Azure Information Protection クライアントの使用を開始する前に次の操作を行います。    

    - コンピューターで Office 2010 を実行している場合、コンピューターを再起動し、最後の手順として次のセクションに進みます。    
        
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 インストールはこれで完了となります。クライアントを使用して、ドキュメントや電子メールにラベルを付けたり、保護したりできます。    

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Office 2010 で Azure Information Protection クライアントをインストールする    
前の指示に従い、Azure Information Protection クライアントをインストールしたら、次の操作を行います。    

1. Microsoft Word を開きます。 Azure Information Protection クライアントのインストール後に初めて Office 2010 アプリケーションを実行した場合、[**Microsoft Azure Information Protection**] ダイアログ ボックスが表示されます。 このダイアログ ボックスには、サインイン プロセスを完了するには管理者の資格情報が必要であることが記されています。

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[OK]** をクリックします。

3. [**ユーザーアクセス制御**] ダイアログ ボックスが表示された場合、[**はい**] をクリックします。Azure Information Protection でレジストリが更新されます。

インストールはこれで完了となります。Azure Information Protection を利用し、文書や電子メールにラベルを付けたり、保護したりできます。

## <a name="other-instructions"></a>その他の手順    
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
[管理者ガイド](client-admin-guide.md)の「[Install the Azure Information Protection client for users](client-admin-guide-install.md)」(ユーザー向けに Azure Information Protection クライアントをインストールする) を参照してください。
 
  
