---
title: ログ & Azure Information Protection からの保護の使用状況を分析します
description: Azure Information Protection から保護サービスの使用状況ログを使用する方法について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a735f3f7-6eb2-4901-9084-8c3cd3a9087e
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: c18c3e6524e6c42ee4b639b42778a8a8217b12d0
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136800"
---
# <a name="logging-and-analyzing-the-protection-usage-from-azure-information-protection"></a>Azure Information Protection からの保護の使用状況のログと分析

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

この情報は、Azure Information Protection から保護サービス (Azure Rights Management) の使用状況ログを使用する方法を理解するのに役立ちます。 この保護サービスは、組織のドキュメントと電子メールのデータ保護を提供し、すべての要求をログに記録できます。 これらの要求には、ユーザーがドキュメントや電子メールを保護していて、このコンテンツも利用している場合に、このサービスのために管理者が実行した操作や、Azure Information Protection のデプロイをサポートするために Microsoft オペレーターが実行した操作が含まれます。 

これらの保護の使用状況ログを使用して、次のビジネスシナリオをサポートできます。

-   **ビジネス情報を分析する**

    保護サービスによって生成されたログは、ユーザーが選択したリポジトリ (データベース、オンライン分析処理 (OLAP) システム、マップ削減システムなど) にインポートして、情報を分析し、レポートを生成することができます。 たとえば、保護されているデータにだれがアクセスしているかを識別できます。 保護されているどのデータにアクセスしているか、どのデバイスから、およびどの場所からアクセスしているかを特定できます。 また、保護されているコンテンツを正常に読むことができたかどうかを調べることができます。 さらに、保護されている重要なドキュメントを読んだユーザーを識別することもできます。

-   **不正使用を監視する**

    保護の使用に関する情報は、ほぼリアルタイムで使用できるので、会社の保護サービスの使用を継続的に監視できます。 ログの 99.9% は、操作を開始してから 15 分以内にサービスで使用できます。

    たとえば、保護されているデータを標準勤務時間外に読むユーザーの数が突然増加した場合に警告を受け取りたい場合があります。この場合、悪意のあるユーザーが競合他社に売り渡すために情報を収集している可能性があります。 また、明らかに同じユーザーが短時間に 2 つの異なる IP アドレスからデータにアクセスした場合、これはユーザー アカウントが侵害されたことを示している可能性があります。

-   **科学捜査上の分析を実行する**

    情報漏えいが発生した場合、特定のドキュメントにだれが最近アクセスしたか、および疑わしいユーザーが最近どの情報にアクセスしたかをたずねられる可能性があります。 保護されたコンテンツを使用するユーザーは、これらのファイルを電子メールで移動したり、USB ドライブまたはその他の記憶装置にコピーしたりしても、Azure Information Protection によって保護されているドキュメントと画像を開くために Rights Management ライセンスを常に取得する必要があるため、このような質問に答えることができます。 これは、Azure Information Protection を使用してデータを保護する際に、フォレンジック分析のための明確な情報源としてこれらのログを使用できることを意味します。

この使用状況ログだけでなく、次のログ オプションもあります。

|ログ オプション|説明|
|----------------|---------------|
|管理ログ|保護サービスの管理タスクをログに記録します。 たとえば、このサービスが非アクティブ化されていて、スーパー ユーザー機能が有効で、ユーザーがサービスに対する管理者権限を委任されている場合などです。 <br /><br />詳細については、PowerShell コマンドレットの[Get-AipServiceAdminLog](/powershell/module/aipservice/get-aipserviceadminlog)に関する説明を参照してください。|
|ドキュメント追跡|ユーザーが Azure Information Protection クライアントで追跡したドキュメントを追跡したり取り消したりできるようにします。 ユーザーに代わって、グローバル管理者がこれらのドキュメントを追跡することもできます。 <br /><br />詳細については、「[Azure Information Protection のドキュメント追跡の構成と使用](./rms-client/client-admin-guide-document-tracking.md)」をご覧ください。|
|クライアント イベント ログ|Azure Information Protection クライアントの使用状況アクティビティ。ローカルの Windows **[アプリケーションとサービス]** イベント ログ、**[Azure Information Protection]** に記録されます。 <br /><br />詳細については、「[Azure Information Protection クライアントの使用状況ログ](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)」をご覧ください。|
|クライアントのログ ファイル|Azure Information Protection クライアントのトラブルシューティング ログは、**%localappdata%\Microsoft\MSIP** に格納されています。 <br /><br />これらのファイルは Microsoft サポート用です。|

さらに、Azure portal でレポートを作成するために、Azure Information Protection クライアントの使用状況ログと、Azure Information Protection スキャナーからの情報が収集され、集計されます。 詳細については、[Azure Information Protection のレポート作成](reports-aip.md)に関するページを参照してください。

保護サービスの使用状況ログの詳細については、次のセクションを参照してください。 

## <a name="how-to-enable-logging-for-protection-usage"></a>保護の使用のログ記録を有効にする方法
保護の使用状況ログは、すべてのお客様に既定で有効になっています。 

ログ ストレージやログ機能に対する追加費用は発生しません。

## <a name="how-to-access-and-use-your-protection-usage-logs"></a>保護の使用状況ログにアクセスして使用する方法
Azure Information Protection は、テナントに対して自動的に作成される Azure ストレージアカウントにログを一連の blob として書き込みます。 各 BLOB には、W3C 拡張ログ形式の 1 つ以上のログ レコードが含まれています。 BLOB の名前は、作成された順序を表す数字です。 ログの内容と作成の詳細については、このドキュメントの後半の「[Azure Rights Management の使用状況ログを解釈する方法](#how-to-interpret-your-usage-logs)」セクションで説明します。

保護アクションの後にログがストレージアカウントに表示されるまでに時間がかかることがあります。 ほとんどのログは 15 分以内に表示されます。 ログはローカル ストレージ (ローカル フォルダー、データベース、MapReduce リポジトリなど) にダウンロードすることをお勧めします。

使用状況ログをダウンロードするには、Azure Information Protection に AIPService PowerShell モジュールを使用します。 インストール手順については、「 [AIPService PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

### <a name="to-download-your-usage-logs-by-using-powershell"></a>PowerShell を使用して使用状況ログをダウンロードするには

1.  [**管理者として実行**] オプションを使用して Windows PowerShell を起動し、 [Connect-aipservice](/powershell/module/aipservice/connect-aipservice)コマンドレットを使用して Azure Information Protection に接続します。

    ```
    Connect-AipService
    ```
    
2.  次のコマンドを実行して、特定の日付のログをダウンロードします。 

    ```
    Get-AipServiceUserLog -Path <location> -fordate <date>
    ```

    たとえば、E: ドライブに Logs という名前のフォルダーを作成した場合は、次のようになります。
    
    * 特定の日付 (たとえば 2016/2/1) のログをダウンロードするには、次のコマンドを実行します。`Get-AipServiceUserLog -Path E:\Logs -fordate 2/1/2016`
    
    * 特定の日付範囲 (たとえば 2016/2/1 から 2016/2/14 まで) のログをダウンロードするには、次のコマンドを実行します。`Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016` 

この例のように日付のみを指定すると、時刻はローカル時刻の 00 時 00 分 00 秒と見なされて UTC に変換されます。 -fromdate パラメーターまたは -todate パラメーター (たとえば、-fordate "2/1/2016 15:00:00") を使用して時刻を指定すると、日付と時刻は UTC に変換されます。 次に、Get AipServiceUserLog コマンドを実行すると、その UTC 期間のログが取得されます。

ダウンロード対象に 1 日未満を指定することはできません。

既定では、このコマンドレットは、ログをダウンロードするときに 3 つのスレッドを使用します。 十分なネットワーク帯域幅があり、ログをダウンロードする際に必要な時間を短縮したい場合は、- NumberOfThreads パラメーターを使用します。このパラメーターは、1 ～ 32 の値をサポートします。 たとえば、次のコマンドを実行すると、ログをダウンロードするためのスレッドが 10 個生成されます。`Get-AipServiceUserLog -Path E:\Logs -fromdate 2/1/2016 –todate 2/14/2016 -numberofthreads 10`


> [!TIP]
> [Microsoft のログ パーサー](https://www.microsoft.com/download/details.aspx?id=24659)を利用して、ダウンロードしたすべてのログ ファイルを CSV 形式で集計できます。このログ パーサーは既知のさまざまなログ形式間で変換を行うためのツールです。 また、このツールを使用すると、データを SYSLOG 形式に変換したり、データベースにインポートしたりできます。 このツールをインストールしたら、`LogParser.exe /?` を実行してこのツールのヘルプおよび使い方を表示します。 
>
> たとえば、次のコマンドを実行すると、すべての情報を .log ファイル形式にインポートできます。`logparser –i:w3c –o:csv "SELECT * INTO AllLogs.csv FROM *.log"`

## <a name="how-to-interpret-your-usage-logs"></a>使用状況ログを解釈する方法
保護の使用状況ログを解釈するには、次の情報を参考にしてください。

### <a name="the-log-sequence"></a>ログ シーケンス
Azure Information Protection は、ログを一連の blob として書き込みます。

ログ内の各エントリには、UTC のタイムスタンプがあります。 保護サービスは複数のデータセンターにまたがる複数のサーバーで実行されるため、タイムスタンプで並べ替えられている場合でも、ログが順序どおりではないように見えることがあります。 しかし、その差はわずかであり、通常 1 分以内です。 ほとんどの場合、ログの分析でこれが問題になることはありません。

### <a name="the-blob-format"></a>BLOB の形式
各 BLOB は、W3C 拡張ログ形式です。 BLOB は、次の 2 行で始まります。

**#Software: RMS**

**#Version: 1.1**

最初の行は、これらが Azure Information Protection からの保護ログであることを示しています。 2 番目の行は、BLOB の残りの部分がバージョン 1.1 の仕様に準拠していることを示します。 これらのログを解析するアプリケーションでは、上の 2 つの行を検証してから BLOB の残りを解析することをお勧めします。

3 番目の行には、タブで区切られたフィールド名が列挙されます。

**#Fields: date            time            row-id        request-type           user-id       result          correlation-id          content-id                owner-email           issuer                     template-id             file-name                  date-published      c-info         c-ip            admin-action            acting-as-user**

後続の各行はログ レコードです。 フィールド値の順序は前の行と同じで、タブで区切られます。 フィールドを解釈するには、次の表を参照してください。


|   フィールド名   | W3C データ型 |                                                                                                                                                                          説明                                                                                                                                                                          |                                                            値の例                                                            |
|----------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
|      日付      |     Date      |                                                                                                                     要求が処理された UTC 日付。<br /><br />ソースは、要求にサービスを提供したサーバーのローカル クロックです。                                                                                                                     |                                                             2013-06-25                                                              |
|      time      |     Time      |                                                                                                            要求が処理された UTC 時間 (24 時間形式)。<br /><br />ソースは、要求にサービスを提供したサーバーのローカル クロックです。                                                                                                            |                                                              21:59:28                                                               |
|     row-id     |     Text      |                                                                           このログ レコードの固有 GUID。 値が存在しない場合は、correlation-id の値を使用してエントリを識別します。<br /><br />この値は、ログを別の形式に集約またはコピーするときに役立ちます。                                                                           |                                                1c3fe7a9-d9e0-4654-97b7-14fafa72ea63                                                 |
|  request-type  |     名前      |                                                                                                                                                            要求された RMS API の名前。                                                                                                                                                            |                                                           AcquireLicense                                                            |
|    user-id     |    String     |                                                               要求を行ったユーザー。<br /><br />この値は単一引用符で囲まれます。 顧客管理 (BYOK) の Azure RMS テナント キーからの呼び出しには **"** の値があり、これは要求の種類が匿名のときにも適用されます。                                                                |                                                          ‘joe@contoso.com’                                                          |
|     結果     |    String     |                                                                                                                  要求が正常に処理された場合は 'Success' です。<br /><br />要求が失敗した場合はエラーの種類が単一引用符で囲まれて示されます。                                                                                                                   |                                                              'Success'                                                              |
| correlation-id |     Text      |                                                                                                 特定の要求に対する RMS クライアント ログとサーバー ログ間で共通の GUID。<br /><br />この値はクライアントの問題を解決するために役立ちます。                                                                                                 |                                                cab52088-8925-4371-be34-4b71a3112356                                                 |
|   content-id   |     Text      |                                                                      保護されたコンテンツ (ドキュメントなど) を示す、波かっこで囲まれた GUID。<br /><br />このフィールドには request-type が AcquireLicense の場合にのみ値が含まれ、それ以外の場合は空白になります。                                                                       |                                               {bb4af47b-cfed-4719-831d-71b98191a4f2}                                                |
|  owner-email   |    String     |                                                                                                                       ドキュメントの所有者の電子メール アドレス。<br /><br /> 要求の種類が RevokeAccess の場合、このフィールドは空白になります。                                                                                                                        |                                                          alice@contoso.com                                                          |
|     発行者     |    String     |                                                                                                                          ドキュメントの発行者の電子メール アドレス。 <br /><br /> 要求の種類が RevokeAccess の場合、このフィールドは空白になります。                                                                                                                          |                       alice@contoso.com (または) FederatedEmail.4c1f4d-93bf-00a95fa1e042@contoso.onmicrosoft.com'                       |
|  template-id   |    String     |                                                                                                                    ドキュメントを保護するために使用されるテンプレートの ID。 <br /><br /> 要求の種類が RevokeAccess の場合、このフィールドは空白になります。                                                                                                                     |                                               {6d9371a6-4e2d-4e97-9a38-202233fed26e}                                                |
|   file-name    |    String     | Windows 用 Azure Information Protection クライアントを使用して追跡される保護されたドキュメント名。 <br /><br />現時点では、(Office 文書などの) 一部のファイルには、実際のファイル名ではなく GUID が表示されます。<br /><br /> 要求の種類が RevokeAccess の場合、このフィールドは空白になります。 |                                                       TopSecretDocument.docx                                                        |
| date-published |     Date      |                                                                                                                          ドキュメントが保護された日付。<br /><br /> 要求の種類が RevokeAccess の場合、このフィールドは空白になります。                                                                                                                           |                                                         2015-10-15T21:37:00                                                         |
|     c-info     |    String     |                                                                                   要求を行っているクライアント プラットフォームに関する情報。<br /><br />この文字列はアプリケーション (オペレーティング システム、ブラウザーなど) によって異なります。                                                                                   | 'MSIPC;version=1.0.623.47;AppName=WINWORD.EXE;AppVersion=15.0.4753.1000;AppArch=x86;OSName=Windows;OSVersion=6.1.7601;OSArch=amd64' |
|      c-ip      |    Address    |                                                                                                                                                       要求を行ったクライアントの IP アドレス。                                                                                                                                                        |                                                            64。51。202。144                                                            |
|  admin-action  |     Bool      |                                                                                                                                    管理者が管理者モードでドキュメント追跡サイトにアクセスしたかどうかを示します。                                                                                                                                    |                                                                True                                                                 |
| acting-as-user |    String     |                                                                                                                               管理者がドキュメント追跡サイトにアクセスする場合に使用するユーザーの電子メール アドレス。                                                                                                                                |                                                          'joe@contoso.com'                                                          |

#### <a name="exceptions-for-the-user-id-field"></a>user-id フィールドの例外
通常、user-id フィールドは要求を行ったユーザーを示しますが、値が実際のユーザーにマップされない例外が 2 つあります。

-   値 **'microsoftrmsonline@&lt;YourTenantID&gt;.rms.&lt;region&gt;.aadrm.com'**。

    これは、Exchange Online や Microsoft SharePoint などの Office 365 サービスが要求を行っていることを示します。 この文字列では、 * &lt; tenantid &gt; *はテナントの GUID であり、 * &lt; region &gt; *はテナントが登録されているリージョンです。 たとえば、**na** は北アメリカを表し、**eu** はヨーロッパを表し、**ap** はアジアを表します。

-   RMS コネクタを使用している場合

    このコネクタからの要求は、RMS コネクタのインストール時に自動的に生成されたサービス プリンシパル名 **Aadrm_S-1-7-0** でログに記録されます。

#### <a name="typical-request-types"></a>一般的な要求の種類
保護サービスには多くの要求の種類がありますが、次の表に、最も一般的に使用される要求の種類を示します。

|要求の種類|説明|
|----------------|---------------|
|AcquireLicense|Windows ベースのコンピューターのクライアントが、保護されたコンテンツのライセンスを要求しています。|
|AcquirePreLicense|ユーザーに代わってクライアントが、保護されたコンテンツのライセンスを要求しています。|
|AcquireTemplates|テンプレート ID に基づいてテンプレートを取得するための呼び出しが行われました。|
|AcquireTemplateInformation|サービスからテンプレートの ID を取得するための呼び出しが行われました。|
|AddTemplate|Azure Portal から、テンプレートを追加するための呼び出しが行われます。|
|AllDocsCsv|ドキュメント追跡サイトから呼び出し、**[すべてのドキュメント]** ページから CSV ファイルをダウンロードします。|
|BECreateEndUserLicenseV1|モバイル デバイスから、エンド ユーザー ライセンスを作成するための呼び出しが行われます。|
|BEGetAllTemplatesV1|モバイル デバイス (バックエンド) から、すべてのテンプレートを取得するための呼び出しが行われます。|
|Certify|クライアントは保護されたコンテンツの使用および作成に関してユーザーを証明しています。|
|DeleteTemplateById|Azure Portal から、テンプレート ID でテンプレートを削除するための呼び出しが行われます。|
|DocumentEventsCsv|ドキュメント追跡サイトから呼び出し、単一ドキュメントの .CSV ファイルをダウンロードします。|
|ExportTemplateById|Azure Portal から、テンプレート ID に基づいてテンプレートをエクスポートするための呼び出しが行われます。|
|FECreateEndUserLicenseV1|AcquireLicense 要求と同じですが、要求元はモバイル デバイスです。|
|FECreatePublishingLicenseV1|Certify および GetClientLicensorCert の組み合わせと同じですが、要求元はモバイル クライアントです。|
|FEGetAllTemplates|モバイル デバイス (フロントエンド) から、テンプレートを取得するための呼び出しが行われます。|
|FindServiceLocationsForUser|Certify または AcquireLicense の呼び出しに使用される URL を照会するための呼び出しが行われます。|
|GetAllDocs|ドキュメント追跡サイトから呼び出し、ユーザーの **[すべてのドキュメント]** ページを読み込むか、テナントのすべてのドキュメントを検索します。 この値は、admin-action フィールドと acting-as-admin フィールドで使用します。<br /><br />- admin-action が空: ユーザーには、自分のドキュメントの **[すべてのドキュメント]** ページが表示されます。<br /><br />- admin-action が true で acting-as-user が空: 管理者には、テナントのすべてのテナントが表示されます。<br /><br />- admin-action が true で acting-as-user が空ではない: 管理者には、ユーザーの **[すべてのドキュメント]** ページが表示されます。|
|GetAllTemplates|Azure Portal から、すべてのテンプレートを取得するための呼び出しが行われます。|
|GetClientLicensorCert|クライアントは Windows ベースのコンピューターから発行元証明書 (後でコンテンツの保護に使用する) を要求しています。|
|GetConfiguration|Azure RMS テナントの構成を取得するために、Azure PowerShell コマンドレットが呼ばれます。|
|GetConnectorAuthorizations|RMS コネクタから、構成をクラウドから取得するための呼び出しが行われます。|
|GetRecipients|ドキュメント追跡サイトから呼び出し、単一ドキュメントのリスト ビューに移動します。|
|GetSingle|ドキュメント追跡サイトから呼び出し、**[シングル ドキュメント]** ページに移動します。|
|GetTenantFunctionalState|Azure portal は、保護サービス (Azure Rights Management) がアクティブになっているかどうかを確認しています。|
|GetTemplateById|Azure Portal から、テンプレート ID を指定してテンプレートを取得するための呼び出しが行われます。|
|KeyVaultDecryptRequest|クライアントが RMS で保護されているコンテンツを復号化しようとしています。 Azure Key Vault の顧客管理のテナント キー (BYOK) にのみ適用されます。|
|KeyVaultGetKeyInfoRequest|Azure Key Vault で Azure Information Protection テナント キーとして使用するように指定したキーがアクセス可能であり、既に使用されていないことを確認する呼び出しを行います。|
|KeyVaultSignDigest|署名に Azure Key Vault の顧客管理のキー (BYOK) が使用される場合に呼び出しが行われます。 通常、これは AcquireLicence (または FECreateEndUserLicenseV1)、Certify、GetClientLicensorCert (または FECreatePublishingLicenseV1) ごとに 1 回呼び出されます。|
|KMSPDecrypt|クライアントが RMS で保護されているコンテンツを復号化しようとしています。 従来の顧客管理のテナント キー (BYOK) にのみ適用されます。|
|KMSPSignDigest|署名に従来の顧客管理のキー (BYOK) が使用される場合に呼び出しが行われます。 通常、これは AcquireLicence (または FECreateEndUserLicenseV1)、Certify、GetClientLicensorCert (または FECreatePublishingLicenseV1) ごとに 1 回呼び出されます。|
|LoadEventsForMap|ドキュメント追跡サイトから呼び出し、単一ドキュメントのマップ ビューに移動します。|
|LoadEventsForSummary|ドキュメント追跡サイトから呼び出し、単一ドキュメントのタイムライン ビューに移動します。|
|LoadEventsForTimeline|ドキュメント追跡サイトから呼び出し、単一ドキュメントのマップ ビューに移動します。|
|ImportTemplate|Azure Portal から、テンプレートをインポートするための呼び出しが行われます。|
|RevokeAccess|ドキュメント追跡サイトから呼び出し、ドキュメントを取り消します。|
|SearchUsers |ドキュメント追跡サイトから呼び出し、テナント内のすべてのユーザーを検索します。|
|ServerCertify|RMS 対応クライアント (SharePoint など) から、サーバーを認証するための呼び出しが行われます。|
|SetUsageLogFeatureState|使用状況ログを有効にするための呼び出しが行われます。|
|SetUsageLogStorageAccount|Azure Rights Management サービス ログの場所を指定するための呼び出しが行われます。|
|UpdateNotificationSettings|ドキュメント追跡サイトから呼び出し、単一ドキュメントの通知設定を変更します。|
|UpdateTemplate|Azure Portal から、既存のテンプレートを更新するための呼び出しが行われます。|


## <a name="powershell-reference"></a>PowerShell リファレンス

保護の使用状況ログにアクセスするために必要な PowerShell コマンドレットは、 [Get-AipServiceUserLog](/powershell/module/aipservice/get-aipserviceuserlog)だけです。 

Azure Information Protection に PowerShell を使用する方法の詳細については、「 [powershell を使用した Azure Information Protection からの保護の管理](administer-powershell.md)」を参照してください。
