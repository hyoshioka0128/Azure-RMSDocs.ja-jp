---
title: "Azure Information Protection クライアントをダウンロードしてインストールする"
description: "ユーザーが Windows 用 Azure Information Protection クライアントをインストールし、ドキュメントと電子メールを分類および保護するための手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/17/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 37bddeed5b81ce1cd6b881db0b71345bcf4cad49
ms.lasthandoff: 02/24/2017


---

# <a name="download-and-install-the-azure-information-protection-client"></a>Azure Information Protection クライアントをダウンロードしてインストールする

管理者が Azure Information Protection クライアントをインストールしない場合、自分でインストールできます。 このクライアントをインストールするには、PC のローカル管理者である必要があります。 

さらに

- Azure Information Protection クライアントでは、Microsoft .NET Framework 4.6.2 の最小バージョンが必要になります。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。

- Windows 7 SP1 を使用する場合、Azure Information Protection クライアントには特定の更新プログラム [KB 2533623](https://support.microsoft.com/kb/2533623) が必要です。 この更新プログラムが必要な PC に更新プログラムがインストールされていない場合、インストールは完了しますが、Azure Information Protection クライアントのすべての機能を使用できるようにするには、この更新プログラムをインストールする必要があることを伝えるメッセージが表示されます。 

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Azure Information Protection クライアントをダウンロードしてインストールするには    

1.  Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) ページに移動します。

    このページには、使用する可能性のあるあらゆる一般的なデバイスへのリンクが含まれているので、保護されたファイルを開くのに必要なビューアー アプリを簡単にダウンロードすることができます。 ここではクライアントを完全にインストールして、ファイルのラベル付けと保護ができるようにします。 

2. **Azure Information Protection クライアント** セクションを見つけて、Windows アイコンをクリックします。 **[ダウンロード]** をクリックし、**AzInfoProtection.exe** ファイルを保存します。     

3. ダウンロードした実行可能ファイルを実行します。 続行を確認するメッセージが表示されたら、[ **はい**] をクリックします。    

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

- [作業内容](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
管理者ガイドの「[How to install the Azure Information Protection client for users](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users)」 (ユーザー向けの Azure Information Protection クライアントのインストール方法) を参照してください。
 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  

