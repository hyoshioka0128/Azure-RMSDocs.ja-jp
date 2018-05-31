---
title: Azure Information Protection クライアント管理者ガイド
description: Windows 用 Azure Information Protection クライアントのデプロイを担当するエンタープライズ ネットワークの管理者向けの手順および情報です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33a5982f-7125-4031-92c2-05daf760ced1
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 17fa8d2269bce0d6ef01506bcbadafd01fc768b6
ms.sourcegitcommit: aae04d78ff301921a4e29ac23bd932fb24a83dbe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444233"
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure Information Protection クライアント管理者ガイド

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

エンタープライズ ネットワークで Azure Information Protection クライアントを担当している場合、または [Azure Information Protection クライアント ユーザー ガイド](client-user-guide.md) に関するページに記載されていない詳細な技術情報が必要な場合は、このガイドの情報をご覧ください。 

次に例を示します。

- このクライアントのさまざまなコンポーネントについて知り、インストールする必要があるかどうかを理解する

- 前提条件、インストール オプションとパラメーター、検証チェックに関する情報を含む、ユーザー向けにクライアントをインストールする方法

- 通常レジストリの編集が必要なカスタムの構成に対応する方法

- クライアント ファイルと使用状況ログを検索する

- クライアントでサポートされているファイルの種類を識別する

- ユーザー用のドキュメント追跡サイトを構成して使用する

- クライアントで PowerShell を使用したコマンドラインでの制御

**このドキュメントでわからない問題がある場合は**、 [Azure Information Protection についての Yammer サイト](https://www.yammer.com/AskIPTeam)をご覧ください。 

## <a name="technical-overview-of-the-azure-information-protection-client"></a>Azure Information Protection クライアントの技術的概要

Azure Information Protection クライアントには次のものが含まれます。

- Office アドイン。ユーザーが分類ラベルを選択するための Azure Information Protection バーと、追加オプションのためのリボンの **[保護]** ボタンをインストールします。 Outlook の場合、**[転送不可]** ボタンはリボンでも使用できます。

- エクスプローラー。ユーザーがファイルに分類ラベルと保護を適用するための右クリック オプション。

- ネイティブ アプリケーションで開くことができないときに、保護されたファイルを表示するビューアー。

- ファイルに対して分類ラベルと保護を適用および削除するための PowerShell モジュール。 
    
    このモジュールには、Windows Server 上でサービスとして実行される [Azure Information Protection スキャナー](../deploy-use/deploy-aip-scanner.md) をインストールし、構成するためのコマンドレットが含まれます。 このサービスを利用すると、ネットワーク共有や SharePoint Server ライブラリなど、データ ストアのファイルを検出、分類、保護できます。

- Azure Rights Management (Azure RMS) または Active Directory Rights Management サービス (AD RMS) と通信する Rights Management クライアント。

Azure Information Protection クライアントは、Azure サービス (Azure Information Protection とそのデータ保護サービス、Azure Rights Management) と併用すると最適です。 ただし、いくつか制限はありますが、オンプレミス バージョンの Rights Management である AD RMS でも使用できます。 Azure Information Protection と AD RMS でサポートされている機能の包括的な比較については、「[Azure Information Protection と AD RMS の比較](../understand-explore/compare-azure-rms-ad-rms.md)」をご覧ください。 

AD RMS を所有していて、Azure Information Protection に移行する場合は、「[AD RMS から Azure Information Protection に移行する](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」をご覧ください。


## <a name="should-you-deploy-the-azure-information-protection-client"></a>Azure Information Protection クライアントのデプロイが必要な場合

次のいずれかが当てはまる場合は、Azure Information Protection クライアントをデプロイします。

- Office アプリケーション (Word、Excel、PowerPoint、Outlook) 内からラベルを選んで、ドキュメントとメール メッセージを分類 (および必要に応じて保護) したい。

- 追加のファイルの種類、複数選択、およびフォルダーをサポートするエクスプローラーを使って、ドキュメントとメール メッセージを分類 (および必要に応じて保護) したい。

- PowerShell コマンドを使って、ドキュメントを分類 (および必要に応じて保護) するスクリプトを実行したい。

- オンプレミスで保存されているファイルを検出し、分類する (さらに、任意で保護する) サービスを実行することがあります。

- ファイルを表示するネイティブ アプリケーションがインストールされていないか、ドキュメントを開くことができない場合に、保護されているドキュメントを表示したい。

- エクスプローラーまたは PowerShell コマンドを使って、単にファイルを保護したい。

- ユーザーと管理者が保護されたドキュメントの追跡および取り消しを行えるようにしたい。

- データ回復のために一括してファイルやコンテナーから暗号化を解除 (保護解除) したい。

- Office 2010 を実行していて、Azure Rights Management サービスを使ってドキュメントとメール メッセージを保護したい。

下の画像では、Office アプリケーションの Azure Information Protection クライアント アドイン、組織の分類ラベル、リボンの新しい **[保護]** ボタンを確認できます。

![Azure Information Protection バーと既定のポリシー](../media/word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-client"></a>Azure Information Protection クライアントのインストールとサポート

Windows Update、実行可能ファイル、または Windows インストーラー ファイルを利用して Azure Information Protection クライアントをインストールできます。 各選択肢の詳細については、「[Install the Azure Information Protection client for users](client-admin-guide-install.md)」 (ユーザー向けに Azure Information Protection クライアントをインストールする) を参照してください。  

クライアントのインストールに関するサポート情報については、次のセクションを利用してください。 

### <a name="installation-checks-and-troubleshooting"></a>インストールのチェックとトラブルシューティング

クライアントがインストールされたら、**[ヘルプとフィードバック]** オプションで **[Microsoft Azure Information Protection]** ダイアログ ボックスを開きます。

- Office アプリケーションから、**[ホーム]** タブの **[保護]** グループで、**[保護]**、**[ヘルプとフィードバック]** の順に選択します。

- エクスプローラーから単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、**[分類して保護する]**、**[ヘルプとフィードバック]** の順に選択します。 

#### <a name="help-and-feedback-section"></a>**[ヘルプとフィードバック]** セクション

既定では、**詳細を表示するリンク**から [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) の Web サイトに移動しますが、Azure Information Protection ポリシー内で[ポリシー設定](../deploy-use/configure-policy-settings.md)の 1 つとしてカスタム URL の構成を行えます。

**[フィードバックの送信]** リンクを使って、Information Protection チームに提案または要求を送信します。 テクニカル サポートの場合はこのオプションを使わず、代わりに「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」をご覧ください。 

**ログのエクスポート**は、Azure Information Protection クライアントのログ ファイルの収集と添付を自動的に行うもので、Microsoft サポートから要求された場合にこれらのログ ファイルを送信します。 このオプションは、エンド ユーザーがログ ファイルをヘルプ デスクに送信するために使用することもできます。

**[設定のリセット]** を選択すると、ユーザーがサインアウトした状態になり、現在ダウンロードされている Azure Information Protection ポリシーが削除され、Azure Rights Management サービスのユーザー設定がリセットされます。

##### <a name="more-information-about-the-reset-settings-option"></a>[設定のリセット] オプションの詳細

- このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 

- ファイルがロックされている場合を除き、この操作は、次の場所のすべてのファイルを削除します。 これらのファイルには、クライアント証明書、Rights Management テンプレート、Azure Information Protection ポリシーおよびキャッシュされたユーザーの資格情報が含まれます。 クライアント ログ ファイルは削除されません。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 次のレジストリ キーと設定が削除されます。 これらいずれかのレジストリ キーの設定にカスタムの値がある場合、クライアントをリセットした後に、設定を再構成する必要があります。 
    
    通常、エンタープライズ ネットワークでは、グループ ポリシーをコンピューター上で更新するときに、これらの設定が自動的に再適用される場合、設定はグループ ポリシーを使用して構成されます。 ただし、スクリプトで一度構成されているか、手動で構成されている設定がある場合があります。 これらの場合、設定を再構成するには、追加の手順を行う必要があります。 たとえば、AD RMS から移行しても、内部ネットワーク上にまだサービス接続ポイントがあるため、Azure Information Protection へのリダイレクトの設定を構成するには、コンピューターでスクリプトが一度実行される場合があります。 クライアントをリセットした後、コンピューターでこのスクリプトをもう一度実行する必要があります。
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- 現在サインインしているユーザーは、サインアウトします。

#### <a name="client-status-section"></a>**クライアント ステータス** セクション

**接続**の値を使って、表示されているユーザー名が Azure Information Protection 認証に使用されるアカウントを識別するか確認します。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントに一致する必要があります。 また、アカウントも、Azure Information Protection 用に構成されたテナントに属している必要があります。

表示されているユーザーとは別のユーザーでサインインする必要がある場合は、[別のユーザーでのサインイン](client-admin-guide-customizations.md#sign-in-as-a-different-user)に関するページのカスタマイズをご覧ください。

**[前回の接続]** には、クライアントが組織の Azure Information Protection サービスに前回接続した時刻が表示されます。 この情報と **[<日時> に Information Protection ポリシーがインストールされました]** を使用して、Azure Information Protection ポリシーが最後にインストールまたは更新された日時を確認できます。 クライアントはサービスへの接続時に、現在のポリシーからの変更を見つけると最新のポリシーを自動的にダウンロードし、24 時間ごとに確認を行います。 表示された時刻以降にポリシーを変更している場合は、Office アプリケーションを閉じて再度開きます。

**このクライアントには Office Professional Plus 用のライセンスがありません**というメッセージが表示された場合、Azure Information Protection クライアントはインストールされている Office のエディションが Rights Management による保護の適用をサポートしていないことを検出しています。 この検出が行われると、保護を適用するラベルは Azure Information Protection バーには表示されません。

**[バージョン]** 情報を使用して、どちらのバージョンのクライアントがインストールされているか確認します。 **新機能**のリンクをクリックし、クライアントの[バージョン リリース履歴](client-version-release-history.md)を読むことで、使用しているクライアントが最新のリリースバージョンかどうかや、各バージョンの修正と新しい機能を確認できます。

## <a name="support-for-multiple-languages"></a>複数言語のサポート

Azure Information Protection クライアントでは、Office 365 でサポートされる言語と同じ言語がサポートされます。 サポートされる言語の一覧については、Office の「[ご利用いただける国と地域](https://products.office.com/business/international-availability)」ページの「**Office 365、Exchange Online Protection、Power BI**」セクションを参照してください。

これらの言語については、Azure Information Protection クライアントのメニュー オプション、ダイアログ ボックス、およびメッセージがユーザーの言語で表示されます。 言語を検出するインストーラーが 1 つあるため、他言語の Azure Information Protection クライアントをインストールするための追加の構成は必要ありません。 

ただし、Azure Information Protection ポリシーでラベルを構成するときは、指定するラベルの名前と説明は自動的には翻訳されません。 2017 年 8 月 30 日以降、最新の[既定のポリシー](../deploy-use/configure-policy-default.md)には一部の言語のサポートが含まれるようになりました。 ユーザーに希望する言語でラベルが表示されるようにするには、独自の翻訳を指定し、その翻訳を使用するように Azure Information Protection ポリシーを構成する必要があります。 詳細については、「[Azure Information Protection で他の言語用ラベルを構成する方法](../deploy-use/configure-policy-languages.md)」を参照してください。 視覚的なマーキングは翻訳されず、複数の言語をサポートしていません。

## <a name="upgrading-and-maintaining-the-azure-information-protection-client"></a>Azure Information Protection クライアントのアップグレードと保守

Azure Information Protection チームは、Azure Information Protection クライアントの新機能や機能修正を定期的に更新しています。 アナウンスは、チームの [Yammer サイト](https://www.yammer.com/AskIPTeam)に投稿されます。

実行可能ファイルまたは Windows インストーラー ファイルを使用してクライアントをインストールした場合は、Microsoft ダウンロード センターから新しいリリースを手動でダウンロードして、クライアントの更新プログラムをインストールする必要があります。 Windows Update を使用してクライアントをインストールした場合、新リリースは、リリース後数週間以内にダウンロード項目のカタログに自動的に追加されます。 

Azure Information Protection クライアントのサポート ポリシー、現在サポートされているバージョン、サポートされているリリースの新機能や機能変更については、[バージョン リリース履歴とサポート ポリシー](../rms-client/client-version-release-history.md)に関する記事をご覧ください。 

## <a name="uninstalling-the-azure-information-protection-client"></a>Azure Information Protection クライアントのアンインストール

クライアントは、以下のいずれかの方法でアンインストールできます。

- コントロール パネルを使って、プログラムをアンインストールします。**[Microsoft Azure Information Protection]**  >  **[アンインストール]** をクリックします。

- 実行可能ファイル (例: **AzInfoProtection.exe**) を再実行し、**[セットアップの変更]** ページの **[アンインストール]** をクリックします。 

- **/uninstall** を付けて実行可能ファイルを実行します。 例: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>次の手順
クライアントをインストールする方法については、「[Install the Azure Information Protection client for users](client-admin-guide-install.md)」 (ユーザー向けに Azure Information Protection クライアントをインストールする) を参照してください。

クライアントを既にインストールしている場合、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
