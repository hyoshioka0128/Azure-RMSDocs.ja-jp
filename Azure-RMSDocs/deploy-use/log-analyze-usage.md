---
# required metadata

title: Azure Rights Management の利用状況をログに記録して分析する | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management の利用状況をログに記録して分析する
このトピックでは、Azure Rights Management (Azure RMS) で使用状況ログを使用する方法について説明します。 Azure Rights Management サービスは、組織のために処理したすべての要求のログを記録します。このログには、組織内のユーザーからの要求、Rights Management 管理者が実行した操作、Azure Rights Management デプロイをサポートするために Microsoft オペレーターが実行した操作などが含まれます。

これらの Azure Rights Management ログを使用すると、次のビジネス シナリオをサポートできます。

-   **ビジネス情報を分析する**

    Azure Rights Management で生成されるログを、選択したリポジトリ (データベース、オンライン分析処理 (OLAP) システム、MapReduce システムなど) にインポートすることによって、情報を分析してレポートを生成できます。 たとえば、RMS で保護されているデータにだれがアクセスしているかを識別できます。 RMS で保護されているどのデータにアクセスしているか、どのデバイスから、およびどの場所からアクセスしているかを特定できます。 また、保護されているコンテンツを正常に読むことができたかどうかを調べることができます。 さらに、保護されている重要なドキュメントを読んだユーザーを識別することもできます。

-   **不正使用を監視する**

    Azure Rights Management のログ情報はほぼリアルタイムに提供されるため、組織での Rights Management の使用状況を途切れなく監視できます。 ログの 99.9% は、RMS が操作を実行してから 15 分以内に提供されます。

    たとえば、RMS で保護されているデータを標準勤務時間外に読むユーザーの数が突然増加した場合に警告を受け取りたい場合があります。この場合、悪意のあるユーザーが競合他社に売り渡すために情報を収集している可能性があります。 また、明らかに同じユーザーが短時間に 2 つの異なる IP アドレスからデータにアクセスした場合、これはユーザー アカウントが侵害されたことを示している可能性があります。

-   **フォレンジック分析の実行**

    情報漏えいが発生した場合、特定のドキュメントにだれが最近アクセスしたか、および疑わしいユーザーが最近どの情報にアクセスしたかをたずねられる可能性があります。 Azure Rights Management およびログを使用すれば、このような質問に答えることができます。保護されているコンテンツを使用するユーザーが Azure Rights Management で保護されているドキュメントおよび画像を開くには、常に Rights Management ライセンスを取得する必要があるためです。これは、ファイルがメールで転送されたり、USB ドライブなどのストレージ デバイスにコピーされたりした場合も同様です。 このため、Azure Rights Management を使用してデータを保護していれば、Azure Rights Management ログを科学捜査上の分析のための最終的な情報源として活用できます。

> [!NOTE]
> Azure Rights Management の管理タスクのログ記録だけに関心があり、Rights Management の利用状況追跡は望まない場合は、Azure Rights Management の [Get-AadrmAdminLog](https://msdn.microsoft.com/library/azure/dn629430.aspx) Windows PowerShell コマンドレットを使用できます。
> 
> Azure クラシック ポータルを通じて、**RMS の概要**、**RMS のアクティブ ユーザー**、**RMS デバイス プラットフォーム**、**RMS アプリケーションの使用状況**など、概要レベルの使用状況レポートを使用することもできます。 Azure クラシック ポータルからこれらのレポートにアクセスするには、**[Active Directory]** をクリックし、ディレクトリを選択して開いてから、**[レポート]** をクリックします。

次のセクションでは、Azure Rights Management の使用状況ログの詳細について説明します。

## Azure Rights Management の使用状況ログを有効にする方法
2016 年 2 月以降、Azure Rights Management の使用状況ログは、すべてのお客様を対象に既定で有効になります。 2016 年 2 月より前に Azure RMS サービスをアクティブ化したお客様と 2016 年 2 月以降にこのサービスをアクティブ化するお客様がこれに該当します。 

> [!NOTE]
> ログ ストレージやログ機能に対する追加費用は発生しません。
> 
> 2016 年 2 月より前に Azure RMS の使用状況ログを使用するには、Azure のサブスクリプションのほか、Azure 上に十分なストレージが必要でしたが、これらが不要になります。



## Azure Rights Management の使用状況ログにアクセスして使用する方法
Azure Rights Management は、ログを Azure ストレージ アカウントに一連の BLOB として書き込みます。 各 BLOB には、W3C 拡張ログ形式の 1 つ以上のログ レコードが含まれています。 BLOB の名前は、作成された順序を表す数字です。 ログの内容と作成の詳細については、このドキュメントの後半の「[Azure Rights Management の使用状況ログを解釈する方法](#how-to-interpret-your-azure-rights-management-usage-logs)」セクションで説明します。

Azure Rights Management 操作の実行後、ログがストレージ アカウントに書き込まれるまで若干時間がかかります。 ほとんどのログは 15 分以内に表示されます。 ログはローカル ストレージ (ローカル フォルダー、データベース、MapReduce リポジトリなど) にダウンロードすることをお勧めします。

使用状況ログをダウンロードするには、Windows PowerShell の Azure RMS 管理モジュールを使用します。 インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。 この Windows PowerShell モジュールを既にダウンロードしている場合は、次のコマンドを実行してバージョン番号が **2.4.0.0** 以上であることを確認します。 `(Get-Module aadrm -ListAvailable).Version` 

### PowerShell を使用して使用状況ログをダウンロードするには

1.  **[管理者として実行]** オプションを選択して Windows PowerShell を起動し、[Connect-AadrmService](https://msdn.microsoft.com/library/azure/dn629415.aspx) コマンドレットを使用して Azure Rights Management サービスに接続します。

    ```
    Connect-AadrmService
    ```
    
2.  次のコマンドを実行して、特定の日付のログをダウンロードします。 

    ```
    Get-AadrmUserLog -Path <location> -fordate <date>
    ```

    たとえば、E: ドライブに Logs という名前のフォルダーを作成した場合は、次のようになります。
    
    * 特定の日付 (2016/2/1 など) のログをダウンロードするには、次のコマンドを実行します。 `Get-AadrmUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * 日付範囲 (2016/2/1 ～ 2016/2/14 など) を指定してログをダウンロードするには、次のコマンドを実行します。 `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

この例のように日付のみを指定すると、時刻はローカル時刻の 00 時 00 分 00 秒と見なされて UTC に変換されます。 -fromdate パラメーターまたは -todate パラメーター (たとえば、-fordate "2/1/2016 15:00:00") を使用して時刻を指定すると、日付と時刻は UTC に変換されます。 Get-AadrmUserLog コマンドは、その UTC の時間帯のログを取得します。

ダウンロード対象に 1 日未満を指定することはできません。

既定では、このコマンドレットは、ログをダウンロードするときに 3 つのスレッドを使用します。 十分なネットワーク帯域幅があり、ログをダウンロードする際に必要な時間を短縮したい場合は、- NumberOfThreads パラメーターを使用します。このパラメーターは、1 ～ 32 の値をサポートします。 たとえば、次のコマンドを実行すると、コマンドレットは 10 個のスレッドを生成してログをダウンロードします。 `Get-AadrmUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> [Microsoft のログ パーサー](https://www.microsoft.com/download/details.aspx?id=24659)を利用して、ダウンロードしたすべてのログ ファイルを CSV 形式で集計できます。このログ パーサーは既知のさまざまなログ形式間で変換を行うためのツールです。 また、このツールを使用すると、データを SYSLOG 形式に変換したり、データベースにインポートしたりできます。 このツールをインストールしたら、`LogParser.exe /?` を実行してこのツールのヘルプおよび使い方を表示します。 
>
> たとえば、次のコマンドを実行すると、すべての情報を .log ファイル形式にインポートできます。 `logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

#### Azure RMS 使用状況ログを 2016 年 2 月 22 日のログの変更の前に手動で有効にした場合


ログの変更前に使用状況ログを使用していた場合は、構成済みの Azure ストレージ アカウントの使用状況ログがあります。 このログの変更の一環として、Microsoft がこれらのログをストレージ アカウントから新しい Azure RMS 管理ストレージ アカウントにコピーすることはありません。 前に生成されたログのライフサイクルは、ユーザーの側で管理していただく必要があります。ユーザーは、[Get-AadrmUsageLog](https://msdn.microsoft.com/library/dn629401.aspx) コマンドレットを使用して古いログをダウンロードできます。 例:

- 使用可能なログを E:\logs フォルダーにダウンロードするには:  `Get-AadrmUsageLog -Path "E:\Logs"`
    
- 特定の範囲の BLOB をダウンロードするには:  `Get-AadrmUsageLog –Path "E:\Logs" –FromCounter 1024 –ToCounter 2047`

次のいずれかに該当する場合は、Get-AadrmUsageLog コマンドレットを使用してログをダウンロードする必要はありません。

-  2016 年 2 月 22 日以前に Azure Rights Management をアクティブ化したが、使用状況ログの機能は有効にしていない。

- 2016 年 2 月 22 日より後に Azure Rights Management をアクティブ化した。

## Azure Rights Management の使用状況ログを解釈する方法
Azure Rights Management の使用状況ログを解釈するには、次の情報を活用してください。

### ログ シーケンス
Azure Rights Management は、ログを一連の BLOB として書き込みます。 

ログ内の各エントリには、UTC のタイムスタンプがあります。 Azure Rights Management は複数のデータ センターにまたがる複数のサーバー上で実行されるため、タイムスタンプで並べ替えられたログであっても、それらが順序どおりではないように見える場合があります。 しかし、その差はわずかであり、通常 1 分以内です。 ほとんどの場合、ログの分析でこれが問題になることはありません。

### BLOB の形式
各 BLOB は、W3C 拡張ログ形式です。 BLOB は、次の 2 行で始まります。

**#Software: RMS**

**#Version: 1.1**

最初の行は、これらが Azure Rights Management ログであることを示します。 2 番目の行は、BLOB の残りの部分がバージョン 1.1 の仕様に準拠していることを示します。 これらのログを解析するアプリケーションでは、上の 2 つの行を検証してから BLOB の残りを解析することをお勧めします。

3 番目の行には、タブで区切られたフィールド名が列挙されます。

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip**

後続の各行はログ レコードです。 フィールド値の順序は前の行と同じで、タブで区切られます。 フィールドを解釈するには、次の表を参照してください。

|フィールド名|W3C データ型|説明|値の例|
|--------------|-----------------|---------------|-----------------|
|date|日付|要求が処理された UTC 日付。<br /><br />ソースは、要求にサービスを提供したサーバーのローカル クロックです。|2013-06-25|
|time|時刻|要求が処理された UTC 時間 (24 時間形式)。<br /><br />ソースは、要求にサービスを提供したサーバーのローカル クロックです。|21:59:28|
|row-id|テキスト|このログ レコードの固有 GUID。<br /><br />この値は、ログを別の形式に集約またはコピーするときに役立ちます。|1c3fe7a9-d9e0-4654-97b7-14fafa72ea63|
|request-type|名前|要求された RMS API の名前。|AcquireLicense|
|user-id|文字列|要求を行ったユーザー。<br /><br />この値は単一引用符で囲まれます。 要求の種類が匿名の場合、値は ”です。|‘joe@contoso。com’|
|結果|文字列|要求が正常に処理された場合は‘Success’ です。<br /><br />要求が失敗した場合はエラーの種類が単一引用符で囲まれて示されます。|‘Success’|
|correlation-id|テキスト|特定の要求に対する RMS クライアント ログとサーバー ログ間で共通の GUID。<br /><br />この値はクライアントの問題を解決するために役立ちます。|cab52088-8925-4371-be34-4b71a3112356|
|content-id|テキスト|保護されたコンテンツ (ドキュメントなど) を示す、波かっこで囲まれた GUID。<br /><br />このフィールドには request-type が AcquireLicense の場合にのみ値が含まれ、それ以外の場合は空白になります。|{bb4af47b-cfed-4719-831d-71b98191a4f2}|
|owner-email|文字列|ドキュメントの所有者の電子メール アドレス。|alice@contoso.com|
|issuer|文字列|ドキュメントの発行者の電子メール アドレス。|alice@contoso.com (または) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'|
|Template-id|文字列|ドキュメントを保護するために使用されるテンプレートの ID。|{6d9371a6-4e2d-4e97-9a38-202233fed26e}|
|File-name|文字列|保護されたドキュメントのファイル名。|TopSecretDocument.docx|
|Date-published|日付|ドキュメントが保護された日付。|2015-10-15T21:37:00|
|c-info|文字列|要求を行っているクライアント プラットフォームに関する情報。<br /><br />この文字列はアプリケーション (オペレーティング システム、ブラウザーなど) によって異なります。|'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64'|
|c-ip|住所|要求を行ったクライアントの IP アドレス。|64.51.202.144|

#### user-id フィールドの例外
通常、user-id フィールドは要求を行ったユーザーを示しますが、値が実際のユーザーにマップされない例外が 2 つあります。

-   値 **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**。

    これは、Office 365 サービス (Exchange Online や SharePoint Online など) が要求を行っていることを示します。 この文字列で、 *&lt;YourTenantID&gt;* はテナントの GUID、 *&lt;region&gt;* はテナントが登録されている地域です。 たとえば、 **na** は北アメリカを表し、 **eu** はヨーロッパを表し、 **ap** はアジアを表します。

-   RMS コネクタを使用している場合

    このコネクタから要求は、RMS コネクタのインストール時に RMS が自動的に生成したサービス プリンシパル名でログに記録されます。

#### 一般的な要求の種類
Azure Rights Management には多くの要求の種類がありますが、次の表に一般的に使用される要求の種類を示します。

|要求の種類|説明|
|----------------|---------------|
|AcquireLicense|Windows ベースのマシンのクライアントが RMS で保護されているコンテンツのライセンスを要求しています。|
|AcquirePreLicense|ユーザーに代わってクライアントが、RMS で保護されているコンテンツのライセンスを要求しています。|
|AcquireTemplates|テンプレート ID に基づいてテンプレートを取得するための呼び出しが行われました。|
|AcquireTemplateInformation|サービスからテンプレートの ID を取得するための呼び出しが行われました。|
|AddTemplate|Azure クラシック ポータルから、テンプレートを追加するための呼び出しが行われます。|
|BECreateEndUserLicenseV1|モバイル デバイスから、エンド ユーザー ライセンスを作成するための呼び出しが行われます。|
|BEGetAllTemplatesV1|モバイル デバイス (バックエンド) から、すべてのテンプレートを取得するための呼び出しが行われます。|
|Certify|クライアントが保護のために内容を証明しています。|
|Decrypt|クライアントが RMS で保護されているコンテンツを復号化しようとしています。|
|DeleteTemplateById|Azure クラシック ポータルから、テンプレート ID でテンプレートを削除するための呼び出しが行われます。|
|ExportTemplateById|Azure クラシック ポータルから、テンプレート ID に基づいてテンプレートをエクスポートするための呼び出しが行われます。|
|FECreateEndUserLicenseV1|AcquireLicense 要求と同じですが、要求元はモバイル デバイスです。|
|FECreatePublishingLicenseV1|Certify および GetClientLicensorCert の組み合わせと同じですが、要求元はモバイル クライアントです。|
|FEGetAllTemplates|モバイル デバイス (フロントエンド) から、テンプレートを取得するための呼び出しが行われます。|
|GetAllTemplates|Azure クラシック ポータルから、すべてのテンプレートを取得するための呼び出しが行われます。|
|GetClientLicensorCert|クライアントは Windows ベースのコンピューターから発行元証明書 (後でコンテンツの保護に使用する) を要求しています。|
|GetConfiguration|Azure RMS テナントの構成を取得するために、Azure PowerShell コマンドレットが呼ばれます。|
|GetConnectorAuthorizations|RMS コネクタから、構成をクラウドから取得するための呼び出しが行われます。|
|GetTenantFunctionalState|Azure クラシック ポータルが、Azure RMS がアクティブかどうかを調べています。|
|GetTemplateById|Azure クラシック ポータルから、テンプレート ID を指定してテンプレートを取得するための呼び出しが行われます。|
|ExportTemplateById|Azure クラシック ポータルから、テンプレート ID を指定してテンプレートをエクスポートするための呼び出しが行われています。|
|FindServiceLocationsForUser|Certify または AcquireLicense の呼び出しに使用される URL を照会するための呼び出しが行われます。|
|ImportTemplate|Azure クラシック ポータルから、テンプレートをインポートするための呼び出しが行われます。|
|ServerCertify|RMS 対応クライアント (SharePoint など) から、サーバーを認証するための呼び出しが行われます。|
|SetUsageLogFeatureState|使用状況ログを有効にするための呼び出しが行われます。|
|SetUsageLogStorageAccount|Azure RMS ログの場所を指定するための呼び出しが行われます。|
|SignDigest|署名にキーが使用される場合に呼び出しが行われます。 通常、これは AcquireLicence (または FECreateEndUserLicenseV1)、Certify、GetClientLicensorCert (または FECreatePublishingLicenseV1) ごとに 1 回呼び出されます。|
|UpdateTemplate|Azure クラシック ポータルから、既存のテンプレートを更新するための呼び出しが行われます。|

## Windows PowerShell の参照情報
2016 年 2 月以降、Azure RMS 使用状況ログに必要となる唯一の Windows PowerShell コマンドレットは、[Get-AadrmUserLog](https://msdn.microsoft.com/library/azure/mt653941.aspx) です。 

この変更の前は次のコマンドレットが Azure RMS 使用状況ログに必要でしたが、現在は推奨されていません。  

-   [Disable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629404.aspx)

-   [Enable-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629421.aspx)

-   [Get-AadrmUsageLog](https://msdn.microsoft.com/library/azure/dn629401.aspx)

-   [Get-AadrmUsageLogFeature](https://msdn.microsoft.com/library/azure/dn629425.aspx)

-   [Get-AadrmUsageLogLastCounterValue](https://msdn.microsoft.com/library/azure/dn629423.aspx)

-   [Get-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629419.aspx)

-   [Set-AadrmUsageLogStorageAccount](https://msdn.microsoft.com/library/azure/dn629426.aspx)

Azure RMS ログが変更される以前から独自の Azure ストレージにログがある場合は、従来どおりこれらの古いコマンドレット (Get-AadrmUsageLog と Get-AadrmUsageLogLastCounterValue) を使用してダウンロードすることができます。 ただし、新しい使用状況ログはすべて新しい Azure RMS ストレージに書き込まれるため、Get-AadrmUserLog を使用してダウンロードする必要があります。

Azure Rights Management 用 Windows PowerShell の使用の詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](administer-powershell.md)」を参照してください。





<!--HONumber=Apr16_HO3-->


