---
title: "Azure Information Protection クライアントをダウンロードしてインストールする | Azure Information Protection"
description: "ユーザーが Windows 用 Azure Information Protection クライアントをインストールし、ドキュメントと電子メールを分類および保護するための手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 22af60687ad030e686ba843ced6d450487353a0e
ms.openlocfilehash: 72266181c5334ed7e03b2022df61c4065f1c3ac7


---

# <a name="download-and-install-the-azure-information-protection-client"></a>Azure Information Protection クライアントをダウンロードしてインストールする

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

**[このバージョンのクライアントはプレビュー段階にあり、変更される可能性があります。]**

管理者が Azure Information Protection クライアントをインストールしない場合、自分でインストールできます。 このクライアントをインストールするには、PC のローカル管理者である必要があります。 

### <a name="office-2010-only"></a>Office 2010 のみ

このバージョンの Office を使用している場合、Azure Information Protection クライアントで、管理者アクセス許可を必要とするレジストリ キーを設定する必要があります。 

指示に従い、クライアントをダウンロードし、インストールしたら、Office 2010 の次のセクションの指示に従います。

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Azure Information Protection クライアントをダウンロードしてインストールするには

1.  [Microsoft ダウンロード サイト](https://www.microsoft.com/en-us/download/details.aspx?id=53018) にアクセスし、Azure Information Protection クライアントの**プレビュー** バージョンをダウンロードします。

2. ダウンロードされた実行可能ファイルをダブルクリックします。 

3. **Azure Information Protection クライアントのインストール** ページで、 
    
    - クラウドに接続できない場合に、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、デモ ポリシーをインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。
    
    - ライセンス条項および使用条件を読み、**[同意する]** をクリックします。

4. 続行を確認するメッセージが表示されたら、**[はい]** をクリックしてインストールが完了するまで待機します。

3. **[閉じる]** をクリックします。 Azure Information Protection クライアントの使用を開始する前に次の操作を行います。

    - コンピューターで Office 2010 を実行している場合、コンピューターを再起動し、最後の手順として次のセクションに進みます。
    
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 インストールはこれで完了となります。クライアントを利用して、文書や電子メールにラベルを付けたり、保護したりできます。

> [!NOTE]
> Windows 7 SP1 を使用する場合、Azure Information Protection クライアントには特定の更新プログラム [KB 2533623](https://support.microsoft.com/en-us/kb/2533623) が必要です。 この更新プログラムが必要な PC にプログラムがインストールされていない場合は、クライアントを使用しようとすると、Azure Information Protection クライアントのすべての機能を使えるようにするには、この更新プログラムをインストールする必要があることを伝えるメッセージが表示されます。

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Office 2010 で Azure Information Protection クライアントをインストールする

前の指示に従い、Azure Information Protection クライアントをインストールしたら、次の操作を行います。

1. Microsoft Word を開きます。 Azure Information Protection クライアントのインストール後に初めて Office 2010 アプリケーションを実行した場合、[**Microsoft Azure Information Protection**] ダイアログ ボックスが表示されます。 このダイアログ ボックスには、サインイン プロセスを完了するには管理者の資格情報が必要であることが記されています。

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[OK]** をクリックします。

2. [**ユーザーアクセス制御**] ダイアログ ボックスが表示された場合、[**はい**] をクリックします。Azure Information Protection でレジストリが更新されます。

インストールはこれで完了となります。Azure Information Protection を利用し、文書や電子メールにラベルを付けたり、保護したりできます。

## <a name="other-instructions"></a>その他の手順
操作方法に関する手順については、「Azure Information Protection ユーザー ガイド」の次のセクションを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報
[Azure Information Protection クライアントのインストール](info-protect-client.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


