---
title: "Azure Information Protection クライアントのインストール | Azure Information Protection"
description: "Office アプリケーションに Information Protection バーを追加して、ドキュメントや電子メールに分類ラベルを選択できるようにするクライアントのインストール手順です。"
manager: mbaldwin
ms.date: 09/13/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 2ecdfe905694b3d14727abdb5e6176d24f675d2e
ms.openlocfilehash: cd6684dd25a721272c073fcc972724a6b81c0c72


---

# Azure Information Protection クライアントのインストール

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection を使ってドキュメントや電子メール メッセージを分類するには、まず Azure Information Protection クライアントをインストールする必要があります。 インストールすると、組織の分類ラベルを表示する Information Protection バーがお使いの Office アプリケーションに追加され、また、**[保護]** という名前のボタンの付いた、新しい**保護**グループが **[ホーム]** タブに表示されます (Word、Excel、PowerPoint)。

次の図は、この Information Protection バーと、[既定のポリシー](configure-policy-default.md)のラベルを示しています。

![Azure Information Protection バーと既定のポリシー](../media/info-protect-bar-default.png)

Azure Information Protection クライアントを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードします。

クライアントをインストールする前に、以下で必要なオペレーティング システムのバージョンとアプリケーションがあることを確認してください: 「[Azure Information Protection の要件](requirements-azure-infoprotect.md)」。


## Azure Information Protection クライアントを手動でインストールするには

1. [クライアントをダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=53018)したら、**AzInfoProtection.exe** を実行し、指示に従ってクライアントをインストールします。 このインストールには、ローカルの管理アクセス許可が必要です。

    Office 365 または Azure Active Directory に接続できないが、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、デモ ポリシーをインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。 

2. Azure Information Protection クライアントの使用を開始するには: コンピューターで Office 2010 が実行されている場合は、コンピューターを再起動します。 その他のバージョンの Office では、すべての Office アプリケーションを再起動します。

## ユーザー向けに Azure Information Protection クライアントをインストールするには

- スクリプトを作成し、コマンド ライン オプションを使用して Azure Information Protection クライアントのインストールを自動化することができます。 インストール オプションを参照するには、`AzInfoProtection.exe /help` を実行してください。

    たとえば、サイレント モードでクライアントをインストールするには、以下の手順に従ってください。 `AzInfoProtection.exe /passive | quiet`


## Azure Information Protection クライアントをアンインストールするには

次のどの方法も使用できます。

- コントロール パネルを使って、プログラムをアンインストールします。**[Microsoft Azure Information Protection]**  >  **[アンインストール]** をクリックします。

- **AzInfoProtection.exe** を再実行し、**[セットアップの変更]** ページの **[アンインストール]** をクリックします。 

- [実行] `AzInfoProtection.exe /uninstall`


## インストール、接続の状態を確認するには、または問題を報告するには

1. Office アプリケーションを開き、**[ホーム]** タブの**保護**グループで、**[保護]**、**[ヘルプとフィードバック]** の順にクリックします。

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、以下を書き留めます。

    - クライアントが組織の Azure Information Protection サービスに前回接続したときに指定した**最終接続**値。 クライアントはサービスへの接続時に、現在のポリシーからの変更を見つけると最新のポリシーを自動的にダウンロードします。 表示された時刻以降にポリシーを変更している場合は、Office アプリケーションを閉じて再度開きます。

    - Azure Information Protection に対するお客様の認証に使用するアカウントを識別する、表示されているユーザー名。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントに一致する必要があります。

    - Azure Information Protection クライアントのバージョン。

    - **[フィードバックの送信]** リンク。これを使用して、調査用に Information Protection チームに送信される電子メール メッセージにクライアント ログを自動的にアタッチできます。

    - **[診断の実行]** リンク: 現在、この機能は実装されていません。

## Azure Information Protection バーのショートカット キー

キーボード ショートカットを使用して、Azure Information Protection バーにアクセスするには、次のキーの組み合わせを使用します:

- **Ctrl** + **Shift** + **~** キーを押します。 

次に、Tab キーを使用してバーのラベルと他のコントロール (**[ラベルの非表示]** アイコンと **[ラベルの削除]** アイコン) を選び、Enter キーで選択します。


## ファイルの場所

クライアント ファイル:   

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアント ログ ファイルと現在インストールされているポリシー ファイル:

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**


## 次のステップ

Information Protection バー上のラベルを変更するには、Azure Information Protection ポリシーを構成する必要があります。 詳しくは、「[Configuring Azure Information Protection policy](configure-policy.md)」 (Azure Information Protection ポリシーの構成) をご覧ください。

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」をご覧ください。 



<!--HONumber=Sep16_HO2-->


