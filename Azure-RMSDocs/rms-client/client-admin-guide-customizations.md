---
title: "Azure Information Protection クライアントのカスタム構成"
description: "Windows 用 Azure Information Protection クライアントのカスタマイズに関する情報。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 9e7e5e67b664d177f60a445aa54df3f6072ff9c7
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2017
---
# <a name="custom-configurations-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントのカスタム構成

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

以下の情報を使用して、詳細構成を行います。これらの構成は、Azure Information Protection クライアントを管理する際に、特定のシナリオまたはユーザーのサブセットで必要となる場合があります。

これらの設定には、レジストリの編集が必要なものや、Azure Portal で構成する必要のある詳細設定を使用するものなどがあります。設定はこの後にクライアントに公開され、ダウンロードされます。 また、一部の設定は Azure Information Protection クライアントのプレビュー バージョンでのみ使用可能である場合があります。 これらの設定については、最小のクライアント バージョンが記載されています。 一般提供バージョンのクライアントでサポートされている設定と構成については、最小のクライアント バージョン番号は記載されていません。

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>ポータルでクライアントの詳細構成設定を構成する方法

この構成は、現在プレビューの段階です。

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザーのウィンドウで、セキュリティ管理者または全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。

2. 最初の [Azure Information Protection] ブレードで、**[スコープ付きポリシー]** を選択します。

3. **[Azure Information Protection - スコープ付きポリシー]** ブレードで、詳細設定を含めるために、ポリシーの横にあるコンテキスト メニュー (**...**) を選択します。 次に **[詳細設定]** を選択します。
    
    スコープ付きポリシーだけでなく、グローバル ポリシーの詳細設定も構成できます。

4. **[詳細設定]** ブレードで、詳細設定の名前と値を入力し、**[保存して閉じる]** を選択します。

5. **[発行]** をクリックして、このポリシーのユーザーが開いていたすべての Office アプリケーションを再起動するようにしてください。

6. 設定が不要になり、既定の動作に戻す場合は、**[詳細設定]** ブレードで、不要になった設定の横にあるコンテキスト メニュー (**...**) を選択し、**[削除]** を選択します。 次に **[保存して閉じる]** をクリックして変更したポリシーを再発行します。

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>AD RMS 専用コンピューターのサインイン プロンプトが表示されないようにする

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続しようとします。 AD RMS とのみ通信するコンピューターの場合、この構成では不必要なサインイン プロンプトがユーザーに表示されます。 レジストリを編集し、このサインイン プロンプトが表示されないようにすることができます。

次の値の名前を検索し、値データを **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

この設定に関係なく、Azure Information Protection クライアントは標準 [RMS サービス検索プロセス](../rms-client/client-deployment-notes.md#rms-service-discovery)に従い、その AD RMS クラスターを検出します。

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

通常、運用環境では、Azure Information Protection クライアントを使用しているときに別のユーザーとしてサインインする必要はありません。 ただし管理者の場合は、テスト段階のときに別ユーザーとしてサインインする必要がある場合があります。 

現在サインインしているアカウントを確認するには、**[Microsoft Azure Information Protection]** ダイアログ ボックスを使用します。Office アプリケーションを開き、**[ホーム]** タブの **[保護]** グループで、**[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 適切ではないアカウントが使用された場合は、Azure Information Protection ポリシーのダウンロードが失敗することや、目的のラベルや機能が表示されないことがあります。

別のユーザーでサイン インする方法は以下の通りです。

1. Azure Information Protection クライアントのバージョンに応じて次の操作を行います。 
    
    - 一般公開バージョンの Azure Information Protection クライアントの場合: レジストリ エディターを使用して **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** に移動し、**TokenCache** の値 (およびそれに関連する値のデータ) を削除します。
    
    - 現在のプレビュー バージョンの Azure Information Protection クライアントの場合: **%localappdata%\Microsoft\MSIP** に移動して、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするように求めるプロンプトが Office アプリケーションで表示されない場合、**[Microsoft Azure Information Protection]** ダイアログ ボックスに戻り、更新された **[クライアント ステータス]** セクションの **[サインイン]** をクリックします。

補足:

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- シングル サインオンを使用する場合は、レジストリを編集した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection クライアントは、現在サインインしているユーザーアカウントを使用して、自動的に認証を行います。

- Azure Rights Management サービスのユーザー設定をリセットする場合は、**[ヘルプとフィードバック]** オプションを使用します。

- 現在ダウンロードされている Azure Information Protection ポリシーを削除したい場合は、**%localappdata%\Microsoft\MSIP** フォルダーから **Policy.msip** ファイルを削除します。

- 現在のプレビュー バージョンの Azure Information Protection クライアントをお持ちの場合は、**[ヘルプとフィードバック]** の **[設定のリセット]** オプションからサインアウトして、現在ダウンロードされている Azure Information Protection ポリシーを削除できます。

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>エクスプローラーの [Hide the Classify and Protect]\(分類の非表示と保護) メニュー オプション

この構成オプションは、現在プレビューの段階です。

Azure Information Protection クライアントのバージョンが 1.3.0.0 以降である場合は、レジストリを編集することで、この詳細構成を構成できます。 

次の DWORD 値の名前を (任意の値と共に) 作成します。

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>切断されたコンピューターのサポート

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続し、Azure Information Protection の最新のポリシーのダウンロードを試みます。 一定期間インターネットに接続できないコンピューターをお持ちの場合は、レジストリを編集することでサービスに接続しようとしないように設定することができます。 

次の値の名前を検索し、値を **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

クライアントの **%LocalAppData%\Microsoft\MSIP** フォルダーの中に、**Policy.msip** という名前の有効なポリシー ファイルがあることを確認してください。 必要に応じて、Azure Portal からポリシーをエクスポートしたり、クライアントのコンピューターにエクスポートされたファイルをコピーできます。 この方法を使用して、古いポリシー ファイルを公開されている最新のポリシーに置き換えることもできます。

ポリシーをエクスポートすると、Azure Information Protection クライアントのさまざまなバージョンに対応するさまざまなバージョンのポリシーが含まれる圧縮ファイルがダウンロードされます。

1. ファイルを解凍し、次の表を利用して必要なポリシー ファイルを特定します。 
    
    |［ファイル名］|対応するクライアント バージョン|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |バージョン 1.2|
    |Policy1.2.msip |バージョン 1.3 - 1.7|
    |Policy1.3.msip |バージョン 1.8 以降|
    
2. 特定したファイルの名前を **Policy.msip** に変更し、Azure Information Protection 保護クライアントがインストールされているコンピューターの **%LocalAppData%\Microsoft\MSIP** フォルダーにコピーします。 


## <a name="hide-the-do-not-forward-button-in-outlook"></a>Outlook の [転送不可] ボタンを非表示にする

この構成オプションは、現在プレビューの段階です。

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 また、この設定にはプレビュー バージョンの Azure Information Protection クライアント (最小バージョン **1.8.41.0**) が必要です。

この設定を構成すると、Outlook のリボンの **[転送不可]** ボタンが非表示になります。 Office メニューからでは、このオプションは非表示になりません。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **DisableDNF**

- 値: **True**

## <a name="make-the-custom-permissions-options-unavailable-to-users"></a>ユーザーがカスタムのアクセス許可オプションを使用できなくする

この構成オプションは、現在プレビューの段階です。

> [!IMPORTANT]
> Word、Excel、PowerPoint、エクスプローラーのユーザー定義アクセス許可用に構成されたラベルがある場合は、このオプションを使わないでください。 このオプションを使うと、ラベルが適用されるときに、ユーザーにカスタム アクセス許可を構成するメッセージが表示されません。 その結果、ドキュメントにはラベルが付きますが、意図したようには保護されません。

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

この設定を構成してユーザーのポリシーを発行すると、ユーザーは次の場所でカスタムのアクセス許可オプションを選択できなくなります。

- Office アプリケーション: **[ホーム]** タブ > **[保護]** グループ > **[保護]** > **[カスタムのアクセス許可]**

- エクスプローラー: 右クリック > **[分類して保護する]** > **[カスタムのアクセス許可]**

この設定は、Office メニュー オプションから構成できるカスタムのアクセス許可には影響しません。 

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableCustomPermissions**

- 値: **False**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Azure Information Protection バーを完全に非表示にする

この構成では、Azure Portal で構成する必要のある詳細設定を使用します。 また、この設定にはプレビュー バージョンの Azure Information Protection クライアント (最小バージョン **1.9.58.0**) が必要です。

この設定を構成してユーザーのポリシーを発行し、ユーザーが Office アプリケーションで Azure Information Protection バーを表示しないように選択すると、バーは非表示のままになります。 これが起こるのは、ユーザーが **[ホーム]** タブ、**[保護]** グループ、**[保護]** ボタンから **[バーの表示]** オプションをクリアするときです。 **[このバーを閉じる]** アイコンを使用してバーを閉じた場合、この設定は何も影響を与えません。

Azure Information Protection バーが非表示のままであっても、推奨の分類を構成している場合やドキュメントや電子メールにラベルを指定する必要がある場合、ユーザーは一時的に表示されるバーからラベルを選択できます。 また、この設定は、手動または自動分類などの、自分や他のユーザーが構成したラベルや、既定ラベルの設定には影響を与えません。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableBarHiding**

- 値: **True**

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Exchange メッセージ分類との統合によるモバイル デバイスのラベル付けソリューション

Outlook on the web はまだ Azure Information Protection の分類と保護の機能をネイティブにサポートしていませんが、Exchange メッセージ分類を使用して Azure Information Protection ラベルをモバイル ユーザーに拡張して適用できます。

このソリューションを実現するには: 

1. [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell コマンドレットを使用して、Azure Information Protection ポリシーのラベル名にマップする名前プロパティでメッセージの分類を作成します。 

2. 各ラベルの Exchange トランスポート ルールを作成します。メッセージのプロパティに構成した分類が含まれる場合はルールを適用し、メッセージ ヘッダーを設定するメッセージ プロパティを変更します。 

    メッセージ ヘッダーについては、Azure Information Protection ラベルを使って送信および分類した電子メールのインターネット ヘッダーを調べることによって、指定する情報を見つけることができます。 ヘッダー **msip_labels** と、そのすぐあとに続く文字列 (セミコロンまでが対象) を探します。 前の例を使用すると、次のようになります。
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    ルール内のメッセージ ヘッダーの場合は、ヘッダーとして **msip_labels** を指定し、ヘッダー値としてこの文字列の残りの部分を指定します。 たとえば、
    
    ![例: 特定の Azure Information Protection ラベルのメッセージ ヘッダーを設定する Exchange Online トランスポート ルール](../media/exchange-rule-for-message-header.png)

この構成のテストを行う前に、トランスポート ルールを作成または編集すると遅延 (たとえば、1 時間の遅延) がよく発生することを念頭においてください。 このルールが有効になった場合、ユーザーが Outlook on the web または Rights Management による保護をサポートするモバイル デバイス クライアントを使用すると、次のことが起こります。 

- ユーザーが Exchange のメッセージ分類を選択して電子メールを送信します。

- Exchange ルールにより Exchange の分類が検出され、ルールに従ってメッセージ ヘッダーが変更されて、Azure Information Protection の分類が追加されます。

- Azure Information Protection クライアントをインストール済みである受信者が Outlook で電子メールを表示すると、Azure Information Protection の割り当てられたラベルや、対応する電子メールのヘッダー、フッター、または透かしが表示されます。 

Azure Information Protection ラベルが Rights Management による保護を適用する場合は、この保護をルールの構成に追加します。メッセージ セキュリティを変更するオプションを選択して、Rights Management による保護を適用し、RMS テンプレートまたは [転送不可] オプションを選択します。

また、トランスポート ルールを構成して、リバース マッピングを行うことができます。 Azure Information Protection ラベルが検出された場合は、対応する Exchange メッセージの分類を設定します。

- Azure Information Protection のラベルごとに: **msip_labels** ヘッダーにラベル名 (**General** など) が含まれている場合に適用されるトランスポート ルールを作成し、このラベルにマップするメッセージ分類を適用します。


## <a name="next-steps"></a>次のステップ
これで Azure Information Protection クライアントのカスタマイズができました。次に、このクライアントのサポートに必要な追加情報を記載した以下の記事をご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
