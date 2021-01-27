---
title: Azure RMS テンプレートの更新 - AIP
description: Azure Rights Management サービスを使用する場合、テンプレートは自動的にクライアント コンピューターにダウンロードされるので、ユーザーはアプリケーションからテンプレートを選択できます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ROBOTS: NOINDEX
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ad85c6f833bd866cebab65e883a7fee169a75b96
ms.sourcegitcommit: f6d536b6a3b5e14e24f0b9e58d17a3136810213b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98808773"
---
# <a name="refreshing-templates-for-users-and-services"></a>ユーザーとサービスのためのテンプレートの更新

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、Microsoft 365 ドキュメントの「秘密度ラベルの暗号化を使用して、 [秘密度ラベル](/microsoft-365/compliance/sensitivity-labels) の詳細と [コンテンツへのアクセスを制限する](/microsoft-365/compliance/encryption-sensitivity-labels) 」を参照してください。 *

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
>

Azure Information Protection から Azure Rights Management サービスを使用すると、ユーザーがアプリケーションから保護テンプレートを選択できるように、クライアントコンピューターに保護テンプレートが自動的にダウンロードされます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。

|アプリケーションまたはサービス|変更後のテンプレートの更新方法|
|--------------------------|---------------------------------------------|
|**Exchange Online**<br /><br />トランスポート ルールと Outlook Web アプリに該当 |1 時間以内の自動更新 - 追加の手順は必要ありません。|
|**Azure Information Protection クラシック クライアント**|Azure Information Protection ポリシーがクライアントに更新されるたびに自動的に更新されます。<br /><br /> - Azure Information Protection バーをサポートしている Office アプリケーションが開いたとき。 <br /><br /> - ファイルまたはフォルダーを分類して保護するために右クリックしたとき。 <br /><br /> - ラベル付けおよび保護のために PowerShell コマンドレット (Get-AIPFileStatus および Set-AIPFileLabel) を実行するとき。<br /><br /> - Azure Information Protection スキャナー サービスが開始され、ローカル ポリシーが 1 時間前よりも古いとき。 また、スキャナー サービスは 1 時間おきに変更を確認し、次のスキャン サイクルには変更を適用します。<br /><br /> - 24 時間ごと。<br /><br /> また、このクライアントは Office と緊密に統合されているため、Microsoft 365 アプリ、Office 2019、Office 2016、または Office 2013 の更新されたテンプレートも Azure Information Protection クライアントに対して更新されます。|
|**Azure Information Protection 統合ラベル付けクライアント**|Office アプリの場合、テンプレートはアプリが開かれるたびに自動的に更新されます。<br /><br /> また、このクライアントは Office と緊密に統合されているため、Microsoft 365 アプリ、Office 2019、Office 2016、または Office 2013 用に更新されたテンプレートも Azure Information Protection 統合されたラベル付けクライアントに対して更新されます。<br /><br /> ファイルエクスプローラー、PowerShell、およびスキャナーの場合、クライアントはテンプレートをダウンロードせず、オンラインでアクセスします。追加の手順は必要ありません。|
|**Microsoft 365 アプリ、Office 2019、Office 2016、および Office 2013**|自動更新 - スケジュールどおりに更新されます。<br /><br />- 以降のバージョンの Office の場合: 既定の更新間隔は 7 日ごとです。<br /><br />スケジュールよりも早く強制的に更新するには、次の「 [Microsoft 365 アプリ、office 2019、office 2016、および office 2013: テンプレートを強制的に更新する方法](#microsoft-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates)」セクションを参照してください。|
|**Office 2010**|ユーザーが Windows からサインアウトして、もう一度サインインし、最大で 1 時間待つと自動的に更新されます。 <br><br>**重要**: Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「[AIP と従来の Windows および Office バージョン](known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。|
|**Exchange On-Premises と Rights Management コネクタ**<br /><br />トランスポート ルールと Outlook Web アプリに該当|自動更新 - 追加の手順は必要ありません。 ただし、Outlook Web アプリは UI を一日キャッシュします。|
|**Office 2019 for Mac と Office 2016 for Mac**|保護されたコンテンツを開くと自動的に更新されます。 強制的に更新するには、次のセクションの「 [office 2019 For mac And office 2016 For mac: テンプレートを強制的に更新する方法](#office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates)」を参照してください。|
|**Mac コンピューター用 RMS 共有アプリ**|自動更新 - 追加の手順は必要ありません。|
|**[組み込みラベル](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)付き Office 365 ProPlus**|この組み込みのラベル付けソリューションでは、テンプレートはダウンロードされませんが、オンラインでアクセスします。追加の手順は必要ありません。|
| | |

クライアントアプリケーションがテンプレートをダウンロードする必要がある場合 (最初または変更用に更新)、ダウンロードが完了して新しいテンプレートまたは更新されたテンプレートが完全に機能するまで、最大30分待機するように準備します。 待機時間はテンプレートの構成のサイズや複雑さ、ネットワークの接続などの要素によって異なります。 

## <a name="microsoft-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates"></a>Microsoft 365 アプリ、Office 2019、Office 2016、および Office 2013: テンプレートを強制的に更新する方法
Microsoft 365 アプリ、Office 2019、Office 2016、または Office 2013 を実行するコンピューターでレジストリを編集することにより、変更されたテンプレートがコンピューター上で既定値よりも頻繁に更新されるように、自動スケジュールを変更できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターの使用方法を誤ると、重大な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 レジストリ エディターの使用方法を誤った結果生じた問題については、解決できる保証はありません。 レジストリ エディターは、各自の責任で使用してください。

### <a name="to-change-the-automatic-schedule"></a>自動スケジュールを変更するには

1.  レジストリ エディターを使用して、次のレジストリ値のいずれかを作成し設定します。
    
    - 更新頻度を日単位で設定するには (最短 1 日): **TemplateUpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の情報を使用します。

        **レジストリパス**: HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **種類**:REG_DWORD

        **値**: TemplateUpdateFrequency

    - 更新頻度を秒単位で設定するには (最短 1 秒): **TemplateUpdateFrequencyInSeconds** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (秒数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の情報を使用します。

        **レジストリパス**: HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **種類**:REG_DWORD

        **値**: TemplateUpdateFrequencyInSeconds

    これらのレジストリ値の両方ではなく、一方のみを作成して設定するようにしてください。 両方が存在する場合、 **TemplateUpdateFrequency** は無視されます。

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションとエクスプローラーのインスタンスを再起動します。

### <a name="to-force-an-immediate-refresh"></a>直ちに更新するには

1. レジストリ エディターを使用して、**LastUpdatedTime** 値のデータを削除します。 たとえば、このデータに **2015-04-20T15:52** が表示されている場合、この 2015-04-20T15:52 を削除して、データが表示されないようにします。 次の情報を使用して、このレジストリ値データを削除するレジストリ パスを見つけてください。

   **レジストリパス**: HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\ < *MicrosoftRMS_FQDN*> テンプレート \\ < *user_alias*>

   **種類**: REG_SZ

   **値**: LastUpdatedTime

   > [!TIP]
   > レジストリ パスの <*MicrosoftRMS_FQDN*> は、Microsoft RMS サービスの FQDN を指します。 この値を確認するには:
   > 
   > Azure Information Protection に対して [AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration) コマンドレットを実行します。 AIPService PowerShell モジュールをまだインストールしていない場合は、「 [AIPService powershell モジュールのインストール](install-powershell.md)」を参照してください。
   > 
   > 出力から、**LicensingIntranetDistributionPointUrl** の値を確認します。
   > 
   > 例: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
   > 
   > この値から、**https://** 文字列と **/_wmcs/licensing** 文字列を削除します。 残りの値が、Microsoft RMS サービスの FQDN です。 この例では、Microsoft RMS サービスの FQDN は次の値になります。
   > 
   > **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2. **%localappdata%\Microsoft\MSIPC\Templates** フォルダーとその中に含まれているすべてのファイルを削除します。

3. Office アプリケーションとエクスプローラーのインスタンスを再起動します。

## <a name="office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates"></a>Office 2019 for Mac および Office 2016 for Mac: テンプレートを強制的に更新する方法

これらのバージョンの Office for Mac では、保護されたコンテンツを開くとき、または暗号化を適用するために新しく構成された秘密度ラベルを使用してコンテンツを保護するときに、テンプレートが更新されます。 テンプレートを強制的に更新する必要がある場合は、次の手順を実行します。 ただし、この手順のコマンドを実行すると、テンプレート、キーチェーン内の RMS トークンキャッシュ、および以前に開かれた保護されたコンテンツのローカル使用ライセンスが削除されます。 そのため、以前に開いた保護されたコンテンツを開くには、もう一度認証を行う必要があり、インターネットに接続している必要があります。

1. ターミナルを開き、次のコマンドを入力します。
    
    ```sh
    defaults write ~/Library/Containers/com.microsoft.Outlook/Data/Library/Preferences/com.microsoft.Outlook ResetRMSCache 1
    ```

2. Mac 用 Outlook を再起動します。

3. 新しい電子メールを作成し、[ **暗号化**] を選択して、 **資格情報を確認** します。


## <a name="see-also"></a>参照
[Azure Information Protection ポリシーでテンプレートを構成して管理する](configure-policy-templates.md)