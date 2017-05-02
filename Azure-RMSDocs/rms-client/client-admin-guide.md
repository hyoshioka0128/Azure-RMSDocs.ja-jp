---
title: "Azure Information Protection クライアント管理者ガイド"
description: "Windows 用 Azure Information Protection クライアントのデプロイを担当するエンタープライズ ネットワークの管理者向けの手順および情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 74abbe0db07a155afe500388810945a3ff5a35a5
ms.sourcegitcommit: 3ff6c072a228994308402778c493727cc682c6b7
translationtype: HT
---
# <a name="azure-information-protection-client-administrator-guide"></a>Azure Information Protection クライアント管理者ガイド

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*


エンタープライズ ネットワークで Azure Information Protection クライアントを担当している場合、または「[Azure Information Protection クライアントユーザー ガイド](client-user-guide.md)」には記載されていない詳細な技術情報が必要な場合は、以下の情報を参照してください。

Azure Information Protection クライアントには次のものが含まれます。

- Office アドオン。ユーザーが分類ラベルを選択するための Azure Information Protection バーと、追加オプションのためのリボンの **[保護]** ボタンをインストールします。

- エクスプローラー。ユーザーがファイルに分類ラベルと保護を適用するための右クリック オプション。

- ネイティブ アプリケーションで開くことができないときに、保護されたファイルを表示するビューアー。

- ファイルに対して分類ラベルと保護を適用および削除するための PowerShell モジュール。

- Azure Rights Management (Azure RMS) または Active Directory Rights Management サービス (AD RMS) と通信する Rights Management クライアント。

Azure Information Protection クライアントは、Azure サービス (Azure Information Protection とそのデータ保護サービス、Azure Rights Management) と併用すると最適です。 ただし、いくつか制限はありますが、オンプレミス バージョンの Rights Management である AD RMS でも使用できます。 Azure Information Protection と AD RMS でサポートされている機能の包括的な比較については、「[Azure Information Protection と AD RMS の比較](../understand-explore/compare-azure-rms-ad-rms.md)」をご覧ください。 

AD RMS を所有していて、Azure Information Protection に移行する場合は、「[AD RMS から Azure Information Protection に移行する](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」をご覧ください。

**このドキュメントでわからないことがある場合は**、 [Azure Information Protection についての Yammer サイト](https://www.yammer.com/AskIPTeam)をご覧ください。 


## <a name="should-you-deploy-the-azure-information-protection-client"></a>Azure Information Protection クライアントのデプロイが必要な場合

次のいずれかが当てはまる場合は、Azure Information Protection クライアントをデプロイします。

- Office アプリケーション (Word、Excel、PowerPoint、Outlook) 内からラベルを選んで、ドキュメントとメール メッセージを分類 (および必要に応じて保護) したい。

- 追加のファイルの種類、複数選択、およびフォルダーをサポートするエクスプローラーを使って、ドキュメントとメール メッセージを分類 (および必要に応じて保護) したい。

- PowerShell コマンドを使って、ドキュメントを分類 (および必要に応じて保護) するスクリプトを実行したい。

- ファイルを表示するネイティブ アプリケーションがインストールされていないか、ドキュメントを開くことができない場合に、保護されているドキュメントを表示したい。

- エクスプローラーまたは Powershell コマンドを使って、単にファイルを保護したい。

- ユーザーと管理者が保護されたドキュメントの追跡および取り消しを行えるようにしたい。

- データ回復のために一括してファイルやコンテナーから暗号化を解除 (保護解除) したい。

- Office 2010 を実行していて、Azure Rights Management サービスを使ってドキュメントとメール メッセージを保護したい。

次の例では、Office アプリケーションの Azure Information Protection クライアント アドオン、組織に対する分類ラベル、リボンの新しい **[保護]** ボタンが示されています。

![Azure Information Protection バーと既定のポリシー](../media/word2016-calloutsv2.png)

## <a name="how-to-install-the-azure-information-protection-client-for-users"></a>ユーザー向けに Azure Information Protection クライアントをインストールする方法

クライアントをインストールする前に、「[Azure Information Protection の要件](../get-started/requirements-azure-rms.md)」で Azure Information Protection クライアントに必要なオペレーティング システムのバージョンとアプリケーションがあることを確認してください。 

Azure Information Protection クライアントの追加の前提条件:

- Azure Information Protection クライアントを完全にインストールするには、既定では Microsoft .NET Framework 4.6.2 の最小バージョンが必要です。これがない場合、インストーラーでこの必須コンポーネントのダウンロードとインストールが試行されます。 この必須コンポーネントがクライアントのインストール時にインストールされたら、コンピューターの再起動が必要になります。 推奨はされていませんが、カスタム インストール パラメーターを使用してこの要件を省略できます。

- Azure Information Protection ビューアーを別にインストールする場合は、Microsoft .NET Framework 4.5.2 の最小バージョンが必要です。これがない場合、インストーラーではダウンロードまたはインストールされません。

- PowerShell モジュールには、Windows PowerShell バージョン 4.0 が必要で、以前のオペレーティング システムにインストールする必要がある場合があります。 詳細については、「[How to Install Windows PowerShell 4.0](http://social.technet.microsoft.com/wiki/contents/articles/21016.how-to-install-windows-powershell-4-0.aspx)」(Windows PowerShell 4.0 のインストール方法) を参照してください。 インストーラーでは、この前提条件のチェックやインストールは行われません。 実行中の Windows PowerShell のバージョンを確認するには、PowerShell セッションで「**$PSVersionTable**」と入力します。

- Windows 7 Service Pack 1 を実行しているコンピューターには、KB 2533623 が必要です。 この更新プログラムの詳細については、「[マイクロソフト セキュリティ アドバイザリ: 安全でないライブラリの読み込みにより、リモートでコードが実行される](https://support.microsoft.com/en-us/kb/2533623)」を参照してください。 この更新プログラムは直接インストールすることもでき、また、その更新プログラムを包括する別の更新プログラムによって置き換えられることもあります。
    
    この必要な更新プログラムがインストールされていない場合、クライアントのインストールにより、インストールが必要だと警告が表示されます。 クライアントのインストール後にこの更新プログラムをインストールできますが、一部の操作はブロックされ、メッセージが再び表示されます。  

> [!NOTE]
> インストールには、ローカルの管理アクセス許可が必要です。

Azure Information Protection クライアントは、Microsoft Update カタログにも含まれているので、カタログを使用する任意のソフトウェア更新プログラム サービスを使用して、クライアントをインストールおよび更新することができます。 

1. Azure Information Protection クライアントを [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードします。 
    
    プレビュー バージョンが利用可能な場合は、このバージョンはテスト用にのみ使用してください。 運用環境でのエンド ユーザー向けのものではありません。 

2. 既定のインストールは、実行可能ファイル (たとえば **AzInfoProtection.exe**) を実行するだけです。 一方、インストール オプションを表示するには、**/help** を付けて実行可能ファイルを実行します。`AzInfoProtection.exe /help`

    サイレント モードでクライアントをインストールする例: `AzInfoProtection.exe /quiet`
    
    PowerShell コマンドレットだけをサイレント インストールする例: `AzInfoProtection.exe  PowerShellOnly=true /quiet`
    
    ヘルプ画面に表示されていない追加のパラメーター:
    
    - Office 2010 を実行するコンピューターにクライアントをインストールするとき、ユーザーがそのコンピューターのローカル管理者ではない場合またはそのユーザーを表示したくない場合は、**ServiceLocation** パラメーターを指定します。 [詳細情報](#more-information-about-the-servicelocation-installation-parameter) 
    
    - **DowngradeDotNetRequirement**: MICROSOFT.NET Framework 4.6.2 のバージョンの要件を省略する場合にこのパラメータを使用します。 [詳細情報](#more-information-about-the-downgradedotnetrequirement-installation-parameter)

3. 対話形式でインストールする場合、Office 365 または Azure Active Directory に接続できないが、デモンストレーション用にローカル ポリシーを使って Azure Information Protection のクライアント側を表示し、操作するには、**デモ ポリシー**をインストールするオプションを選択します。 クライアントの Azure Information Protection サービスへの接続時に、このデモ ポリシーは、組織の Azure Information Protection ポリシーに置き換えられます。
    
4. インストールを完了するには: 

    - お使いのコンピューターが Office 2010 を実行する場合は、コンピューターを再起動します。 
        
        ServiceLocation パラメーターを指定してクライアントをインストールしなかった場合は、Azure Information Protection バーを使う Office アプリケーション (Word など) を初めて開くときに、この初回使用時にレジストリを更新するプロンプトを確認する必要があります。 [サービス検索](../rms-client/client-deployment-notes.md#rms-service-discovery)はレジストリ キーの設定に使用されます。 
    
    - その他のバージョンの Office では、Office アプリケーションとエクスプローラーのインスタンスをすべて再起動します。 
        
5. 既定で %temp% フォルダに作成されるインストール ログ ファイルを確認することで、インストールが成功したか確認できます。 インストール パラメーター **/log** を使用してこの場所を変更できます。 
 
    このファイルの名前は次の形式です: `Microsoft_Azure_Information_Protection_<number>_<number>_MSIP.Setup.Main.msi.log`
    
    例: **Microsoft_Azure_Information_Protection_20161201093652_000_MSIP.Setup.Main.msi.log**
    
    このログ ファイルで、次の文字列を検索します: **製品: Microsoft Azure Information Protection -- インストールを正しく完了しました。** インストールに失敗した場合、このログ ファイルには、問題の特定と解決に役立つ詳細が含まれます。

### <a name="more-information-about-the-servicelocation-installation-parameter"></a>ServiceLocation インストール パラメーターの詳細について

Office 2010 を使っていてローカル管理者権限を持たないユーザーのためにクライアントをインストールするときは、ServiceLocation パラメーターと Azure Rights Management サービスの URL を指定します。 このパラメーターと値により、次のレジストリ キーが作成され、設定されます。

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation

HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\EnterprisePublishing

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\ServiceLocation\Activation

次の手順で、ServiceLocation パラメーターに指定する値を特定します。 

#### <a name="to-identify-the-value-to-specify-for-the-servicelocation-parameter"></a>ServiceLocation パラメーターに指定する値を特定するには

1. PowerShell セッションから、最初に [Connect-AadrmService](https://docs.microsoft.com/powershell/aadrm/vlatest/connect-aadrmservice) を実行し、管理者の資格情報を指定して Azure Rights Management サービスに接続します。 [Get-AadrmConfiguration](https://docs.microsoft.com/powershell/aadrm/vlatest/get-aadrmconfiguration) を実行します。 
 
    Azure Rights Management サービス用の PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

2. 出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。

    例: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**

3. この値から、**/_wmcs/licensing** 文字列を削除します。 例: **https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

    残りの文字列は、ServiceLocation パラメーターに指定する値です。

Office 2010 と Azure RMS のクライアントのサイレント インストールの例: `AzInfoProtection.exe /quiet ServiceLocation=https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com`


### <a name="more-information-about-the-downgradedotnetrequirement-installation-parameter"></a>DowngradeDotNetRequirement インストール パラメーターの詳細について

Windows Update を使用して自動アップグレードをサポートし、Office アプリケーションとの信頼性の高い統合のため、Azure Information Protection クライアントは Microsoft .NET Framework バージョン 4.6.2 を使用します。 既定では、インストールのこのバージョンを確認し、ない場合はインストールしようとします。 インストール後はコンピューターの再起動が必要です。

この Microsoft .NET Framework の新しいバージョンのインストールが現実的ではない場合は、**DowngradeDotNetRequirement = True** パラメーターと値を使用してクライアントをインストールすることで、Microsoft .NET Framework バージョン 4.5.1 がインストールされていれば要件を省略できます。

例: `AzInfoProtection.exe DowngradeDotNetRequirement=True`

このパラメータは、Azure Information Protection クライアントがMicrosoft .NET Framework の以前のバージョンと共に使用すると Office アプリケーションがハングする問題が報告されていることを把握したうえで注意して使用することをお勧めします。 ハングすることがある場合は、その他のトラブルシューティングを行う前に推奨されているバージョンにアップグレードしてください。 

Windows Update を使用して Azure Information Protection クライアントを最新の状態に保っている場合は、別のソフトウェアの展開方法でクライアントを新しいバージョンに保つ必要があることにも注意してください。

## <a name="additional-checks-and-troubleshooting"></a>追加のチェックとトラブルシューティング

**[ヘルプとフィードバック]** オプションで **[Microsoft Azure Information Protection]** ダイアログ ボックスを開きます。

- Office アプリケーションから、**[ホーム]** タブの **[保護]** グループで、**[保護]**、**[ヘルプとフィードバック]** の順に選択します。

- エクスプローラーから単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、**[分類して保護する]**、**[ヘルプとフィードバック]** の順に選択します。 

### <a name="help-and-feedback-section"></a>**[ヘルプとフィードバック]** セクション

既定では、**詳細を表示するリンク**から [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) の Web サイトに移動しますが、Azure Information Protection ポリシー内で[ポリシー設定](../deploy-use/configure-policy-settings.md)の 1 つとしてカスタム URL の構成を行えます。

**[フィードバックの送信]** リンクを使って、Information Protection チームに提案または要求を送信します。 テクニカル サポートの場合はこのオプションを使わず、代わりに「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」をご覧ください。 

**ログのエクスポート**は、Azure Information Protection クライアントのログ ファイルの収集と添付を自動的に行うもので、Microsoft サポートから要求された場合にこれらのログ ファイルを送信します。 このオプションは、エンド ユーザーがログ ファイルをヘルプ デスクに送信するために使用することもできます。

診断情報を取得し、クライアントをリセットするには、**[診断の実行]** を選択します。 診断テストが完了したら、**[結果のコピー]** をクリックして情報を電子メールに貼り付け、ヘルプ デスクまたは Microsoft サポートに送信できます。 テストの完了時に、クライアントをリセットすることもできます。

**[リセット]** オプションの詳細:

- このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 

- ファイルがロックされていない限り、この操作で **%localappdata%\Microsoft\MSIPC** 内のすべてのファイルが削除されます。これは、クライアント証明書と Rights Management テンプレートが格納されている場所です。 この操作では、Azure Information Protection ポリシーまたはクライアント ログ ファイルは削除されません。また、ユーザーはサインアウトされません。

- **HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC** のレジストリ キーと設定は削除されます。 このレジストリ キーの設定を構成する場合 (たとえば、AD RMS から移行しても、社内ネットワークにサービス接続ポイントがあるため、Azure Information Protection テナントへのリダイレクト設定を構成する場合)、クライアントのリセット後にレジストリ設定を構成し直す必要があります。

- クライアントをリセットした後は、クライアントの証明書と最新のテンプレートのダウンロードを行い、ユーザー環境を再初期化する必要があります。 再初期化を実行するには、すべての Office インスタンスを終了し、Office アプリケーションを再起動します。 この操作で、最新の Azure Information Protection ポリシーをダウンロードしたことも確認されます。 この確認が完了するまで、診断テストは再実行しないでください。


### <a name="client-status-section"></a>**クライアント ステータス** セクション

**接続**の値を使って、表示されているユーザー名が Azure Information Protection 認証に使用されるアカウントを識別するか確認します。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントと一致し、Azure Information Protection 用に構成されたテナントに属している必要があります。

表示されているユーザーとは別のユーザーでサインインする必要がある場合は、このページの[別のユーザーでのサイン イン](#sign-in-as-a-different-user)セクションをご覧ください。

**前回の接続**はに、クライアントが Azure Information Protection サービスに対して最後に接続した日時が表示され、**Information Protection ポリシーがインストールされた日時**の日付と時間と共に使用することで、Azure Information Protection ポリシーが最後にインストールまたは更新された日時を確認できます。 クライアントはサービスへの接続時に、現在のポリシーからの変更を見つけると最新のポリシーを自動的にダウンロードし、24 時間ごとに確認を行います。 表示された時刻以降にポリシーを変更している場合は、Office アプリケーションを閉じて再度開きます。

**このクライアントには Office Professional Plus 用のライセンスがありません**というメッセージが表示された場合、Azure Information Protection クライアントはインストールされている Office のエディションが Rights Management による保護の適用をサポートしていないことを検出しています。 この検出が行われると、保護を適用するラベルは Azure Information Protection バーには表示されません。

**[バージョン]** 情報を使用して、どちらのバージョンのクライアントがインストールされているか確認します。 **新機能**のリンクをクリックし、クライアントの[バージョン リリース履歴](client-version-release-history.md)を読むことで、使用しているクライアントが最新のリリースバージョンかどうかや、各バージョンの修正と新しい機能を確認できます。

## <a name="custom-configurations"></a>カスタム構成

特定のシナリオまたはユーザーのサブセットで必要となる可能性のある詳細構成には、次の情報を使用します。 

### <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>AD RMS 専用コンピューターのサインイン プロンプトが表示されないようにする

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続しようとします。 その結果、AD RMS とだけ通信するコンピューターの場合、不必要なサインイン プロンプトがユーザーに表示されます。 レジストリを編集し、このサインイン プロンプトが表示されないようにすることができます。

次の値の名前を検索し、値データを **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

この設定に関係なく、Azure Information Protection クライアントは標準 [RMS サービス検索プロセス](../rms-client/client-deployment-notes.md#rms-service-discovery)に従い、その AD RMS クラスターを検出します。

### <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

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

### <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>エクスプ ローラーの [Hide the Classify and Protect] (分類の非表示と保護) メニュー オプション

Azure Information Protection クライアントのバージョンが 1.3.0.0 以降である場合は、レジストリを編集することで、この詳細構成を構成することができます。 

次の DWORD 値の名前を (任意の値と共に) 作成します。

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

### <a name="support-for-disconnected-computers"></a>切断されたコンピューターのサポート

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続し、Azure Information Protection の最新のポリシーのダウンロードを試みます。 一定期間インターネットに接続できないコンピュータをお持ちの場合は、レジストリを編集することでサービスに接続しようとしないように設定することができます。 次の値の名前を検索し、値を **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

クライアントの **%localappdata%\Microsoft\MSIP** フォルダーの中に、**Policy.msip** という名前の有効なポリシー ファイルがあることを確認してください。 必要に応じて、Azure Portal からポリシーをエクスポートしたり、クライアントのコンピューターにエクスポートされたファイルをコピーできます。 このメソッドを使用して、古いポリシー ファイルを公開されている最新のポリシーに置き換えることもできます。

## <a name="to-uninstall-the-azure-information-protection-client"></a>Azure Information Protection クライアントをアンインストールするには

次のどの方法も使用できます。

- コントロール パネルを使って、プログラムをアンインストールします。**[Microsoft Azure Information Protection]**  >  **[アンインストール]** をクリックします。

- 実行可能ファイル (例: **AzInfoProtection.exe**) を再実行し、**[セットアップの変更]** ページの **[アンインストール]** をクリックします。 

- **/uninstall** を付けて実行可能ファイルを実行します。 例: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアントをインストールしたので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
