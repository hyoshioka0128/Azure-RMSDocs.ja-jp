---
title: Azure Information Protection 統合されたラベル付けクライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/20/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 97390bec6bb31b6445a2975953b996e57865c6f4
ms.sourcegitcommit: 479b3aaea7011750ff85a217298e5ae9185c1dd1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82224718"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection 統合されたラベル付けクライアント-バージョンのリリース履歴とサポートポリシー

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Azure Information Protection 統合されたラベル付けクライアントは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。

通常、数週間の遅延が発生すると、最新の一般公開バージョンが Microsoft Update カタログにも含まれます。これには、 **Microsoft Azure Information Protection** > **Microsoft Azure Information Protection**の製品名と、**更新プログラム**の分類が含まれます。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」を参照してください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection 統合ラベルクライアントの各一般公開 (GA) バージョンは、以降の GA バージョンのリリースから最大6か月間サポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|2.2.21.0|09/03/2019|
|2.2.19.0|08/06/2019|
|2.2.14.0|07/15/2019|
|2.0.779.0|05/01/2019|
|2.0.778.0|04/16/2019|

このページで使用される日付形式は、*月/日/年*です。


### <a name="release-information"></a>リリース情報

次の情報を使用して、Windows 用の Azure Information Protection 統合ラベルクライアントのサポートされているリリースの新機能と変更点を確認してください。 最新のリリースは一番上に表示されます。 このページで使用される日付形式は、*月/日/年*です。

> [!NOTE]
> マイナー修正は記載されていないので、統一されたラベル付けクライアントで問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

このクライアントは Azure Information Protection クライアント (クラシック) に置き換わるものです。 従来のクライアントとの機能を比較するには、「 [Windows コンピューターのラベル付けクライアント](use-client.md#compare-the-labeling-clients-for-windows-computers)」を参照してください。

## <a name="version-261110"></a>バージョン2.6.111.0 

**リリース**03/09/2020

**新機能:**

- [スキャナー](../deploy-aip-scanner.md)の一般公開バージョン。オンプレミスのデータストアのドキュメントを検査してラベル付けします。 

- [スキャナー](../deploy-aip-scanner.md)関連:
    - [SharePoint オンプレミスおよびサブサイトの検出が容易に](https://docs.microsoft.com/azure/information-protection/quickstart-findsensitiveinfo#permission-users-to-scan-sharepoint-repositories)なりました。 各サイトの設定は必須ではなくなりました。 
    - [SQL チャンクのサイズ変更](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#storage-requirements-and-capacity-planning-for-sql-server)の詳細プロパティが追加されました。
    - 管理者は、既存の[スキャンを停止し](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#stop-a-scan)、既定のラベルが変更された場合に再スキャンを実行できるようになりました。
    - 既定では、スキャナーは、高速なスキャンのために最小のテレメトリを設定し、ログのサイズを小さくし、情報の種類をデータベースにキャッシュするようになりました。 [スキャナーの最適化](https://docs.microsoft.com/azure/information-protection/deploy-aip-scanner#optimizing-the-performance-of-the-scanner)の詳細についてはこちらをご覧ください。 
    - スキャナーはデータベースとサービスの個別の配置をサポートするようになりましたが、 **Sysadmin**権限はデータベースの配置にのみ必要です。
    - スキャナーのパフォーマンスが向上しました。 

- PST、rar、7zip、および MSG ファイルからの保護の削除を有効にするための[PowerShell](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-powershell)コマンドレットの**set-aipfilelabel**の変更。 この機能は既定で無効になっており、[ここで](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#enable-removal-of-protection-from-compressed-files)説明するように、 [Set labelpolicy](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations)コマンドレットを使用して有効にする必要があります。  

- Azure Information Protection の管理者がファイルに対して pfile 拡張機能を使用するかどうかを制御できるようになりました。 [保護されたファイルの種類の変更](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#change-which-file-types-to-protect)に関する詳細情報。 

- アプリケーションと変数に対して動的な視覚的マーキングのサポートが追加されました。 [視覚的なマーキングのラベルを構成](https://docs.microsoft.com/azure/information-protection/configure-policy-markings)する方法については、こちらを参照してください。 

- [自動および推奨ラベルに対するカスタマイズ可能なポリシーのヒント](use-client.md)が強化されました。   

- 統一されたラベル付けクライアントで Office アプリを使用して、[オフラインラベル機能](https://docs.microsoft.com/azure/information-protection/rms-client/clientv2-admin-guide-customizations#support-for-disconnected-computers)のサポートが追加されました。


**修正:**

- RightFax によって作成された、保護された TIFF ファイルと TIFF ファイルを開こうとしてユーザーが失敗したインスタンスでは、TIFF ファイルが開き、予想どおりに安定した状態が維持されるようになりました。  
- 保護された txt ファイルと PDF ファイルの以前の破損が解決されます。
- Log Analytics の**自動**と**手動**の間に一貫性のないラベル付けが修正されました。 
- 新しいメールとユーザーの最後に開いた電子メールの間で、予期しない継承の問題が解決されました。  
- .Msg ファイルの保護が正常に機能するようになりました。 
- Office ユーザー定義の設定から追加された共同所有者のアクセス許可が、期待どおりに適用されるようになりました。 
- [アクセス許可のダウングレードを入力する] をオンにすると、他のオプションが既に選択されている場合はテキストを入力できなくなります。 


## <a name="version-25330"></a>バージョン2.5.33.0

**リリース**日: 10/23/2019

09/09/2020 でサポート

**新機能:**

- [スキャナー](../deploy-aip-scanner.md)のプレビューバージョン。オンプレミスのデータストアを検査してラベル付けします。 このバージョンのスキャナーでは、次のことを行います。
    
    - 同じスキャナープロファイルを使用するようにスキャナーを構成するときに、複数のスキャナーが同じ SQL Server データベースを共有できます。 この構成により、複数のスキャナーの管理が容易になり、スキャン時間が短縮されます。 この構成を使用する場合は、スキャナーのインストールが完了するのを待ってから、同じプロファイルを使用して別のスキャナーをインストールします。
    
    - スキャナーをインストールするときにプロファイルを指定する必要があります。スキャナーデータベースには**\<AIPScannerUL_ profile_name>** という名前が付けられます。 *プロファイル*パラメーターは、Set-AIPScanner にも必須です。
    
    - ドキュメントにラベルが既に付いている場合でも、すべてのドキュメントに既定のラベルを設定できます。 スキャナープロファイルまたはリポジトリの設定で、[ラベルの再設定 **] オプションを** **[オン**] に設定し、新しい [既定の**ラベルを強制**する] チェックボックスをオンにします。
    
    - すべてのドキュメントから既存のラベルを削除できます。ラベルによって以前に適用されていた場合、この操作には保護の削除が含まれます。 ラベルとは独立して適用された保護が保持されます。 このスキャナーの構成は、スキャナープロファイルまたはリポジトリの設定で次の設定を使用して実現されます。
        - **コンテンツに基づいてファイルにラベルを付ける**:**オフ**
        - **既定のラベル**:**なし**
        - **ファイル**のラベルの再設定: **[** **既定のラベルを強制**する] チェックボックスがオンになっている
    
    - 従来のクライアントのスキャナーと同様、既定では、スキャナーは Office ファイルと PDF ファイルを保護します。 [PowerShell の詳細設定](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)を使用すると、他の種類のファイルを保護できます。
    
    - スキャナーサイクルの開始と終了に関するイベント Id は、Windows イベントログには書き込まれません。 代わりに、この情報に Azure portal を使用します。
    
    - 既知の問題: 新しいラベルと名前が変更されたラベルは、スキャナープロファイルまたはリポジトリの設定の既定のラベルとして選択できません。 回避策:
        - 新しいラベルの場合: Azure portal で、グローバルポリシーまたはスコープポリシーに使用する[ラベルを追加](../configure-policy-add-remove-label.md)します。
        - 名前を変更したラベルの場合: Azure portal を閉じてから再度開きます。
    
    Azure Information Protection クライアント (クラシック) からスキャナーをアップグレードすることができます。 アップグレード後に新しいデータベースが作成されると、スキャナーは初回実行時にすべてのファイルを再スキャンします。 手順については、管理者ガイドの「 [Azure Information Protection スキャナーをアップグレードする](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を参照してください。
    
    詳細については、ブログ投稿のお知らせを参照してください。統合された[ラベル付け AIP スキャナーのプレビューにより、スケールアウトなど](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)ができます。

- PowerShell コマンドレットの[セット-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)は、ファイルに非対話形式でラベルを付ける場合の新しいパラメーター (*AppId*、 *appsecret*、 *TenantId*、 *DelegatedUser*、 *OnBehalfOf*) を備えています。また、新しい手順では、アプリを Azure AD に登録します。 シナリオ例としては、スキャナーや、ドキュメントにラベルを付けるための自動 PowerShell スクリプトがあります。 手順については、管理者ガイドの「[非対話形式でファイルにラベルを付ける方法](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。
    
    *DelegatedUser*は、統合されたラベル付けクライアントの最後のプレビューバージョン以降の新しいパラメーターであり、登録済みアプリの API アクセス許可が変更されたことに注意してください。

- [保護するファイルの種類を変更](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)するための新しい PowerShell ラベルポリシーの詳細設定。

- 新しい PowerShell ラベルポリシーの詳細設定を[使用して、ラベルの移行ルールを SharePoint プロパティに拡張](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-sharepoint-properties)します。

- 一致したカスタム機密情報の種類が[Azure Information Protection analytics](../reports-aip.md)に送信されます。

- 適用されたラベルには、[色が構成され](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)ている場合、ラベルに構成されている色が表示されます。

- ラベルに保護設定を追加または変更すると、クライアントは、ドキュメントが次に保存されるときに、これらの最新の保護設定でラベルを再適用します。 同様に、スキャナーは、強制モードでドキュメントが次回スキャンされるときに、これらの最新の保護設定でラベルを再適用します。

- 1つのクライアントからファイルをエクスポートし、切断されたコンピューターに手動でコピーすることによって、切断された[コンピューターをサポート](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)します。 この構成は、ファイルエクスプローラー、PowerShell、およびスキャナーを使用したラベル付けでサポートされていることに注意してください。 この構成は、Office アプリのラベル付けではサポートされていません。

- %Localappdata%\Microsoft\MSIP\Logs からすべてのログファイルを収集し、.zip 形式の1つの圧縮されたファイルに保存する新しいコマンドレットである[Export](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)。 このファイルは、報告された問題の調査に役立つログファイルを送信するように要求された場合に Microsoft サポートに送信できます。

**修正:**

- ファイルエクスプローラーを使用して保護されたファイルを正常に変更できます。ファイルのパスワードが削除されたら、右クリックします。

- ネイティブ保護されたファイルをビューアーで正常に開くには、[名前を付けて保存]、[エクスポート (エクスポート) [] の使用権限](../configure-usage-rights.md#usage-rights-and-descriptions)を必要としません。

- ラベルとポリシー設定は[、クリア-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)を実行しなくても期待どおりに更新されます。または、%LocalAppData%\Microsoft\MSIP\mip フォルダーを手動で削除します。

**追加の変更**

- [設定をリセット](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)すると、\\%LocalAppData%\Microsoft\MSIP\mip\\*\<ProcessName\>* \ mip フォルダーではなく、%LocalAppData%\Microsoft\MSIP\mip*\<\> ProcessName*フォルダーが削除されるようになりました。

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)に、保護されたドキュメントのコンテンツ ID が含まれるようになりました。


## <a name="next-steps"></a>次のステップ

インストールするクライアントが適切かどうかは確認できません。  「 [Windows コンピューターに使用するラベル付けクライアントを選択](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

このクライアントをインストールして使用する方法の詳細については、次を参照してください。 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-unifiedlabelingclient-app.md)

- 管理者向け: Azure Information Protection 統一された[ラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)

