---
title: "Azure Information Protection クライアントのインストール | Azure Information Protection"
description: "Office アプリケーションに Information Protection バーを追加して、ドキュメントや電子メールに分類ラベルを選択できるようにするクライアントのインストール手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4445adff-4c5a-450f-aff8-88bf5bd4ca78
translationtype: Human Translation
ms.sourcegitcommit: 23c437479c756f2a9335606e686f117d514a38f6
ms.openlocfilehash: 71972b0a057b1958dfa5e5b4af41b65d5080a086


---

# <a name="installing-the-azure-information-protection-client"></a>Azure Information Protection クライアントのインストール

>*適用対象: Azure Information Protection*

Azure Information Protection を使ってドキュメントや電子メール メッセージを分類するには、まず Azure Information Protection クライアントをインストールする必要があります。 インストールすると、組織の分類ラベルを表示する Information Protection バーがお使いの Office アプリケーションに追加され、また、**[保護]** という名前のボタンの付いた、新しい**保護**グループが **[ホーム]** タブに表示されます (Word、Excel、PowerPoint)。

次の図は、この Information Protection バーと、[既定のポリシー](../deploy-use/configure-policy-default.md)のラベルを示しています。

![Azure Information Protection バーと既定のポリシー](../media/info-protect-bar-default.png)

Azure Information Protection クライアントを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードします。 現時点では、一般公開 (GA) バージョンとプレビュー バージョンをインストールすることができます。 プレビュー バージョンには評価の目的で新しい機能が含まれており、変更される可能性があります。 詳細については、ブログ投稿のお知らせ「[Azure Information Protection December preview now available (Azure Information Protection の 12 月のプレビュー版が利用可能になりました)](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/)」を参照してください。

クライアントをインストールする前に、「[Azure Information Protection の要件](../get-started/requirements-azure-rms.md)」で Azure Information Protection クライアントに必要なオペレーティング システムのバージョンとアプリケーションがあることを確認してください。 また、プレビュー バージョンのクライアントについては、Windows 7 SP1 を実行しているコンピューターには [KB 2533623](https://support.microsoft.com/en-us/kb/2533623) が必要ですが、こちらはクライアントのインストール後にインストールできます。 この更新プログラムが必要でインストールされていない場合は、インストールが求められます。

## <a name="to-install-the-azure-information-protection-client-manually"></a>Azure Information Protection クライアントを手動でインストールするには

1. [クライアントをダウンロード](https://www.microsoft.com/en-us/download/details.aspx?id=53018)したら、**AzInfoProtection.exe** などの実行可能ファイルを実行し、指示に従ってクライアントをインストールします。 このインストールには、ローカルの管理アクセス許可が必要です。

    Office 365 または Azure Active Directory に接続できないが、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、デモ ポリシーをインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。 

2. Azure Information Protection クライアントの使用を開始するには: コンピューターで Office 2010 が実行されている場合は、コンピューターを再起動します。 その他のバージョンの Office では、すべての Office アプリケーションを再起動します。

## <a name="to-install-the-azure-information-protection-client-for-users"></a>ユーザー向けに Azure Information Protection クライアントをインストールするには

スクリプトを作成し、コマンド ライン オプションを使用して Azure Information Protection クライアントのインストールを自動化することができます。 インストール オプションを表示するには、**/help** を付けて実行可能ファイルを実行します。 たとえば、`AzInfoProtection.exe /help` と指定します。

サイレント モードでクライアントをインストールするには、`AzInfoProtection.exe /passive | quiet` を実行します。

一般公開バージョンの Azure Information Protection クライアントは、Microsoft Update カタログにも含まれているので、カタログを使用する任意のソフトウェア更新プログラム サービスを使用して、クライアントをインストールおよび更新することができます。 プレビュー バージョンのクライアントは Microsoft Update カタログに含まれていません。

## <a name="to-uninstall-the-azure-information-protection-client"></a>Azure Information Protection クライアントをアンインストールするには

次のどの方法も使用できます。

- コントロール パネルを使って、プログラムをアンインストールします。**[Microsoft Azure Information Protection]**  >  **[アンインストール]** をクリックします。

- 実行可能ファイル (例: **AzInfoProtection.exe**) を再実行し、**[セットアップの変更]** ページの **[アンインストール]** をクリックします。 

- **/uninstall** を付けて実行可能ファイルを実行します。 例: `AzInfoProtection.exe /uninstall`


## <a name="to-verify-installation-connection-status-or-report-a-problem"></a>インストール、接続の状態を確認するには、または問題を報告するには

1. Office アプリケーションを開き、**[ホーム]** タブの**保護**グループで、**[保護]**、**[ヘルプとフィードバック]** の順にクリックします。

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、以下を書き留めます。

    - **[クライアント ステータス]** セクションの **[バージョン]** 値を使用して、インストールが成功したことを確認します。 また、クライアントが組織の Azure Information Protection サービスに最後に接続した時間と、Azure Information Protection ポリシーが最後にインストールまたは更新された時間を確認します。 クライアントはサービスへの接続時に、現在のポリシーからの変更を見つけると最新のポリシーを自動的にダウンロードします。 表示された時刻以降にポリシーを変更している場合は、Office アプリケーションを閉じて再度開きます。
    
        Azure Information Protection に対するユーザー認証に使用するアカウントを識別する表示ユーザー名も確認します。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントと一致し、Azure Information Protection 用に構成されたテナントに属している必要があります。

    - **[ヘルプとフィードバック]** セクション: **詳細情報リンク**の既定のリンク先は [Azure Information Protection](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection) Web サイトですが、独自の URL を指定できます。この指定は、Azure Information Protection ポリシーの中の[ポリシー設定](../deploy-use/configure-policy-settings.md)の 1 つとして行います。
        
        **[フィードバックの送信]** リンクを使用すると、クライアントのログが Information Protection チームへの電子メール メッセージに自動的に添付され、問題の調査に使用されます。 
    
        診断情報を取得し、クライアントをリセットするには、**[診断の実行]** をクリックします。 診断テストが完了したら、**[結果のコピー]** をクリックして情報を電子メールに貼り付け、ヘルプ デスクまたは Microsoft サポートに送信できます。 テストの完了時に、クライアントをリセットすることもできます。
        
        **[リセット]** オプションの詳細:
        
        - このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 
        
        - ファイルがロックされていない限り、この操作で **%localappdata%\Microsoft\MSIPC** 内のすべてのファイルが削除されます。これは、クライアント証明書と Rights Management テンプレートが格納されている場所です。 この操作では、Azure Information Protection ポリシーまたはクライアント ログ ファイルは削除されません。また、ユーザーはサインアウトされません。
        
        - **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC** のレジストリ キーと設定は削除されます。 このレジストリ キーの設定を構成する場合 (たとえば、AD RMS から移行しても、社内ネットワークにサービス接続ポイントがあるため、Azure Information Protection テナントへのリダイレクト設定を構成する場合)、クライアントのリセット後にレジストリ設定を構成し直す必要があります。
        
        - クライアントのリセット後に、ユーザー環境を再初期化する必要があります ("ブートストラップ" とも呼ばれます)。再初期化によって、クライアントの証明書と最新のテンプレートがダウンロードされます。 再初期化を実行するには、すべての Office インスタンスを終了し、Office アプリケーションを再起動します。 この操作で、最新の Azure Information Protection ポリシーをダウンロードしたことも確認されます。 この確認が完了するまで、診断テストは再実行しないでください。


## <a name="usage-logging"></a>使用状況ログの記録

**[この機能が動作するにはプレビュー バージョンのクライアントが必要です。この機能は変更される可能性があります。]**

プレビュー バージョンの Azure Information Protection クライアントでは、ユーザー アクティビティはローカル Windows イベント ログの **[アプリケーションとサービス]** > **[Azure Information Protection]** に記録されます。 イベントには次の情報が含まれます。

- 日付、クライアントのバージョン、ポリシー ID

- サインインしたユーザー名、コンピューター名

- ファイル名と場所

- 操作:

    - ラベルの設定: 情報 ID 101
    
    - ラベルの設定 (下位): 情報 ID 102
    
    - ラベルの設定 (上位): 情報 ID 103
    
    - ラベルの削除: 情報 ID 104
   
    - 推奨されるヒント: 情報 ID 105
    
    - カスタム保護の適用: 情報 ID 201
    
    - カスタム保護の削除: 情報 ID 202
    
    - サインイン (操作): 情報 ID 902
    
    - ポリシーのダウンロード (操作): 情報 ID 901
    
- 操作ソース:
    
    - 手動 
    
    - 推奨
    
    - 自動  
    
    - システム (サインインおよびダウンロードポリシー用)
    
- 操作前後のラベル 
    
- 操作前後の保護
    
- ユーザーの理由 (該当する場合)
    

## <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Azure Information Protection バーのショートカット キー

キーボード ショートカットを使用して、Azure Information Protection バーにアクセスするには、次のキーの組み合わせを使用します:

- **Ctrl** + **Shift** + **~** キーを押します。 

次に、Tab キーを使用してバーのラベルと他のコントロール (**[ラベルの非表示]** アイコンと **[ラベルの削除]** アイコン) を選び、Enter キーで選択します。


## <a name="file-locations"></a>ファイルの場所

クライアント ファイル:   

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアント ログ ファイルと現在インストールされているポリシー ファイル:

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>次のステップ

Information Protection バー上のラベルを変更するには、Azure Information Protection ポリシーを構成する必要があります。 詳しくは、「[Configuring Azure Information Protection policy](../deploy-use/configure-policy.md)」 (Azure Information Protection ポリシーの構成) をご覧ください。

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」をご覧ください。

クライアントのリリース バージョン情報を確認するには、「[バージョン リリース履歴](client-version-release-history.md)」を参照してください。



<!--HONumber=Dec16_HO1-->


