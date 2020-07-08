---
title: Azure Information Protection クライアントをダウンロードしてインストールする
description: ユーザーが Windows 用 Azure Information Protection クライアントをインストールし、ドキュメントと電子メールを分類および保護するための手順です。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 05/03/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 1a6c9076f29d588464c03b33140a454a541b2891
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86046421"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-client"></a>ユーザー ガイド: Azure Information Protection クライアントをダウンロードしてインストールする

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


管理者が Azure Information Protection クライアントをインストールしない場合、自分でインストールできます。 ドキュメントや電子メールにラベルを付けて保護できるように、このクライアントをインストールするには対象となる PC のローカル管理者である必要があります。

さらに:

- Azure Information Protection クライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。


## <a name="to-download-and-install-the-azure-information-protection-client"></a>Azure Information Protection クライアントをダウンロードしてインストールするには    

1. Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) ページに移動します。

    このページには、使用する可能性のあるあらゆる一般的なデバイスへのリンクが含まれているので、保護されたファイルを開くのに必要なビューアー アプリを簡単にダウンロードすることができます。 PC のローカル管理者でない場合でも、Windows 用のビューアー アプリをインストールすることはできます。 ただし、次の手順では、クライアントを完全にインストールして、ファイルのラベル付けと保護ができるようにします。 

2. **Azure Information Protection クライアント** セクションを見つけて、Windows アイコンをクリックします。 **[ダウンロード]** をクリックし、**AzInfoProtection.exe** ファイルを保存します。     

3. ダウンロードした実行可能ファイルを実行します。 続行を確認するメッセージが表示されたら、[**はい**] をクリックします。    

4. **Azure Information Protection クライアントのインストール** ページで、     
    - クラウドに接続できない場合に、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、デモ ポリシーをインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。    

    - ライセンス条項および使用条件を読み、**[同意する]** をクリックします。    

5. 続行を確認するメッセージが表示されたら、**[はい]** をクリックしてインストールが完了するまで待機します。    

6. **[閉じる]** をクリックします。 Azure Information Protection クライアントの使用を開始する前に次の操作を行います。    

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

- [実行する操作](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
[管理者ガイド](client-admin-guide.md)の「[Install the Azure Information Protection client for users](client-admin-guide-install.md)」(ユーザー向けに Azure Information Protection クライアントをインストールする) を参照してください。
 
  
