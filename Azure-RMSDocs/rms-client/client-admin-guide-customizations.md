---
title: "Azure Information Protection クライアントのカスタム構成"
description: "Windows 用 Azure Information Protection クライアントのカスタマイズに関する情報。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ab5465db1527e6236d2dca466936c36b260f03d
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# Azure Information Protection クライアントのカスタム構成
<a id="custom-configurations-for-the-azure-information-protection-client" class="xliff"></a>

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012*

Azure Information Protection クライアントを管理するときに特定のシナリオまたはユーザーのサブセットで必要となる可能性がある詳細構成には、次の情報を使用します。 

## AD RMS 専用コンピューターのサインイン プロンプトが表示されないようにする
<a id="prevent-sign-in-prompts-for-ad-rms-only-computers" class="xliff"></a>

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続しようとします。 その結果、AD RMS とだけ通信するコンピューターの場合、不必要なサインイン プロンプトがユーザーに表示されます。 レジストリを編集し、このサインイン プロンプトが表示されないようにすることができます。

次の値の名前を検索し、値データを **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

この設定に関係なく、Azure Information Protection クライアントは標準 [RMS サービス検索プロセス](../rms-client/client-deployment-notes.md#rms-service-discovery)に従い、その AD RMS クラスターを検出します。

## 別のユーザーでのサイン イン
<a id="sign-in-as-a-different-user" class="xliff"></a>

通常、運用環境では、Azure Information Protection クライアントを使用しているときに別のユーザーとしてサインインする必要はありません。 ただし、複数のテナントがある場合は管理者としてこのようなサインインが必要になることがあります。 たとえば、組織が使用する Office 365 や Azure テナントに加えてテスト テナントがある場合などです。

現在サインインしているアカウントを確認するには、**[Microsoft Azure Information Protection]** ダイアログ ボックスを使用します。Office アプリケーションを開き、**[ホーム]** タブの **[保護]** グループで、**[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

特に、管理者アカウントを使用している場合は、表示されるサインイン アカウントのドメイン名を必ず確認してください。 たとえば、2 つのテナントに "admin" アカウントがある場合、アカウント名は正しくてもドメインを間違えてサインインするという失敗が起こりやすくなります。 このような状況では、Azure Information Protection ポリシーのダウンロードが失敗したり、目的のラベルや機能が表示されなかったりする可能性があります。

別のユーザーでサイン インする方法は以下の通りです。

1. レジストリ エディターを使って **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** に移動し、**TokenCache** の値 (およびその値に関連する値) を削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするように求めるプロンプトが Office アプリケーションで表示されない場合、**[Microsoft Azure Information Protection]** ダイアログ ボックスに戻り、更新された **[クライアント ステータス]** セクションの **[サインイン]** をクリックします。

補足:

- シングル サインオンを使用する場合は、レジストリを編集した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection クライアントは、現在サインインしているユーザーアカウントを使用して、自動的に認証を行います。

- Azure Rights Management サービスの環境を再初期化 (ブートストラップ) するには、[RMS Analyzer ツール](https://www.microsoft.com/en-us/download/details.aspx?id=46437)の **[リセット]** オプションを使用します。

- 現在ダウンロードされている Azure Information Protection ポリシーを削除したい場合は、**%localappdata%\Microsoft\MSIP** フォルダーから **Policy.msip** ファイルを削除します。

## エクスプ ローラーの [Hide the Classify and Protect]\(分類の非表示と保護) メニュー オプション
<a id="hide-the-classify-and-protect-menu-option-in-windows-file-explorer" class="xliff"></a>

Azure Information Protection クライアントのバージョンが 1.3.0.0 以降である場合は、レジストリを編集することで、この詳細構成を構成することができます。 

次の DWORD 値の名前を (任意の値と共に) 作成します。

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## 切断されたコンピューターのサポート
<a id="support-for-disconnected-computers" class="xliff"></a>

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続し、Azure Information Protection の最新のポリシーのダウンロードを試みます。 一定期間インターネットに接続できないコンピュータをお持ちの場合は、レジストリを編集することでサービスに接続しようとしないように設定することができます。 次の値の名前を検索し、値を **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

クライアントの **%localappdata%\Microsoft\MSIP** フォルダーの中に、**Policy.msip** という名前の有効なポリシー ファイルがあることを確認してください。 必要に応じて、Azure Portal からポリシーをエクスポートしたり、クライアントのコンピューターにエクスポートされたファイルをコピーできます。 このメソッドを使用して、古いポリシー ファイルを公開されている最新のポリシーに置き換えることもできます。

## Exchange メッセージ分類との統合によるモバイル デバイスのラベル付けソリューション
<a id="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution" class="xliff"></a>

Outlook on the web はまだ Azure Information Protection の分類と保護の機能をネイティブにサポートしていませんが、Exchange メッセージ分類を使用して Azure Information Protection ラベルをモバイル ユーザーに拡張して適用できます。

このソリューションを実現するには: 

1. [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell コマンドレットを使用して、Azure Information Protection ポリシーのラベル名にマップする名前プロパティでメッセージの分類を作成します。 

2. 各ラベルの Exchange トランスポート ルールを作成します。メッセージのプロパティに構成した分類が含まれる場合はルールを適用し、メッセージ ヘッダーを設定するメッセージ プロパティを変更します。 

    メッセージ ヘッダーについては、Azure Information Protection ラベルを使って送信および分類した電子メールのインターネット ヘッダーを調べることによって、指定する情報を見つけます。 ヘッダー **msip_labels** と、そのすぐあとに続く文字列 (セミコロンまでが対象) を探します。 前の例を使用すると、次のようになります。
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    ルール内のメッセージ ヘッダーの場合は、ヘッダーとして **msip_labels** を指定し、ヘッダー値としてこの文字列の残りの部分を指定します。 たとえば、
    
    ![例: 特定の Azure Information Protection ラベルのメッセージ ヘッダーを設定する Exchange Online トランスポート ルール](../media/exchange-rule-for-message-header.png)

テストを行う場合は、トランスポート ルールを作成または編集する際に、しばしば遅延が発生することがある (たとえば、1 時間の遅延) という点を念頭においてください。 このルールが有効になった場合、ユーザーが Outlook on the web、または Rights Management による保護をサポートするモバイル デバイス クライアントを使用すると、次のことが起こります。 

- ユーザーが Exchange のメッセージ分類を選択して電子メールを送信します。

- Exchange ルールにより Exchange の分類が検出され、ルールに従ってメッセージ ヘッダーが変更されて、Azure Information Protection の分類が追加されます。

- Azure Information Protection クライアントを実行する受信者が Outlook で電子メールを表示すると、Azure Information Protection の割り当てられたラベル、および対応する電子メールのヘッダー、フッター、または透かしが表示されます。 

Azure Information Protection ラベルが Rights Management による保護を適用する場合は、メッセージ セキュリティを変更するオプションを選択してルールの構成に追加し、Rights Management による保護を適用して、RMS テンプレートまたは [転送不可] オプションを選択します。

リバース マッピングを行うようにトランスポート ルールを構成することもできます。Azure Information Protection ラベルが検出された場合は、対応する Exchange メッセージ分類を設定します。 このためには、次の操作を行います。

- Azure Information Protection のラベルごとに、**msip_labels** ヘッダーにラベル名 (**General** など) が含まれている場合に適用されるトランスポート ルールを作成し、このラベルにマップするメッセージ分類を適用します。


## 次のステップ
<a id="next-steps" class="xliff"></a>
これで Azure Information Protection クライアントのカスタマイズができました。次に、このクライアントのサポートに必要な追加情報を記載した以下の記事をご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
