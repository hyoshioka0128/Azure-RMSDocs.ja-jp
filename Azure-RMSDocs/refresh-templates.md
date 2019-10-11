---
title: Azure RMS テンプレートの更新 - AIP
description: Azure Rights Management サービスを使用する場合、テンプレートは自動的にクライアント コンピューターにダウンロードされるので、ユーザーはアプリケーションからテンプレートを選択できます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/09/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6d2e845b9738a5697c2d658025e249d9ba5226c8
ms.sourcegitcommit: be8ccf7248e0e504d73b3cd2f58fb2d0c4455ad3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72236808"
---
# <a name="refreshing-templates-for-users-and-services"></a>ユーザーとサービスのためのテンプレートの更新

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection から Azure Rights Management サービスを使用すると、ユーザーがアプリケーションから保護テンプレートを選択できるように、クライアントコンピューターに保護テンプレートが自動的にダウンロードされます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。

|アプリケーションまたはサービス|変更後のテンプレートの更新方法|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />トランスポート ルールと Outlook Web アプリに該当 |1 時間以内の自動更新 - 追加の手順は必要ありません。|
|Azure Information Protection クライアント|Azure Information Protection ポリシーがクライアントに更新されるたびに自動的に更新されます。<br /><br /> - Azure Information Protection バーをサポートしている Office アプリケーションが開いたとき。 <br /><br /> - ファイルまたはフォルダーを分類して保護するために右クリックしたとき。 <br /><br /> - ラベル付けおよび保護のために PowerShell コマンドレット (Get-AIPFileStatus および Set-AIPFileLabel) を実行するとき。<br /><br /> - Azure Information Protection スキャナー サービスが開始され、ローカル ポリシーが 1 時間前よりも古いとき。 また、スキャナー サービスは 1 時間おきに変更を確認し、次のスキャン サイクルには変更を適用します。<br /><br /> - 24 時間ごと。<br /><br /> さらに、このクライアントは Office と密接に統合されているため、Office 365 アプリ、Office 2019、Office 2016、または Office 2013 で更新されたテンプレートはすべて、Azure Information Protection クライアントでも更新されます。|
|Azure Information Protection 統合ラベル付けクライアント|4 時間ごとに自動で更新されます (Office アプリごとに)。<br /><br /> さらに、このクライアントは Office と密接に統合されているため、Office 365 アプリ、Office 2019、Office 2016、または Office 2013 で更新されたテンプレートはすべて、Azure Information Protection 統合ラベル付けクライアントでも更新されます。|
|Office 365 アプリ、Office 2019、Office 2016、および Office 2013|自動更新 - スケジュールどおりに更新されます。<br /><br />- 以降のバージョンの Office の場合: 既定の更新間隔は7日ごとです。<br /><br />スケジュールに先立って強制的に更新するには、以下の「[Office 365 アプリ、Office 2019、Office 2016、Office 2013:テンプレートを強制的に更新する方法 @ no__t-0|
|Office 2010|ユーザーが Windows からサインアウトして、もう一度サインインし、最大で 1 時間待つと自動的に更新されます。|
|Exchange On-Premises と Rights Management コネクタ<br /><br />トランスポート ルールと Outlook Web アプリに該当|自動更新 - 追加の手順は必要ありません。 ただし、Outlook Web アプリは UI を一日キャッシュします。|
|Office 2019 for Mac と Office 2016 for Mac|保護されたコンテンツを開くと自動的に更新されます。 強制的に更新するには、次のセクションを参照してください。 [Office 2019 for Mac および Office 2016 for Mac:テンプレートを強制的に更新する方法 @ no__t-0|
|Mac コンピューター用 RMS 共有アプリ|自動更新 - 追加の手順は必要ありません。|
|[機密機能をサポートしている](https://support.office.com/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US&ui=en-US&rs=en-US#bkmk_whereavailable) Office アプリ|これらのクライアントはテンプレートをダウンロードしませんが、これらにオンラインでアクセスします。追加の手順は必要ありません。|

クライアントアプリケーションがテンプレートをダウンロードする必要がある場合 (最初または変更用に更新)、ダウンロードが完了して新しいテンプレートまたは更新されたテンプレートが完全に機能するまで、最大30分待機するように準備します。 待機時間はテンプレートの構成のサイズや複雑さ、ネットワークの接続などの要素によって異なります。 

## <a name="office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-templates"></a>Office 365 アプリ、Office 2019、Office 2016、Office 2013:テンプレートを強制的に更新する方法
Office 365 アプリ、Office 2019、Office 2016、または Office 2013 を実行しているコンピューター上でレジストリを編集すると、変更されたテンプレートがコンピューター上で、既定値よりも短い周期で更新されるように自動スケジュールを変更できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターを誤って使用すると、重大な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 マイクロソフトは、レジストリ エディターを誤って使用したために発生した問題を解決できることを保証できません。 レジストリ エディターは、各自の責任で使用してください。

### <a name="to-change-the-automatic-schedule"></a>自動スケジュールを変更するには

1.  レジストリ エディターを使用して、次のレジストリ値のいずれかを作成し設定します。
    
    - 更新頻度を日単位で設定するには (1 日以上):**TemplateUpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の情報を使用します。

        **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **種類:** REG_DWORD

        **値:** TemplateUpdateFrequency

    - 更新頻度を秒単位で設定するには (最小値は1秒):**TemplateUpdateFrequencyInSeconds** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (秒数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の情報を使用します。

        **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **種類:** REG_DWORD

        **値:** TemplateUpdateFrequencyInSeconds

    これらのレジストリ値の両方ではなく、一方のみを作成して設定するようにしてください。 両方が存在する場合、 **TemplateUpdateFrequency** は無視されます。

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションとエクスプローラーのインスタンスを再起動します。

### <a name="to-force-an-immediate-refresh"></a>直ちに更新するには

1. レジストリ エディターを使用して、 **LastUpdatedTime** 値のデータを削除します。 たとえば、"**2015-04-20T15:52**" と表示されている場合は、この 2015-04-20T15:52 を削除して、何も表示されていない状態にします。 次の情報を使用して、このレジストリ値データを削除するレジストリ パスを見つけてください。

   **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template\\<*user_alias*>

   **種類:** REG_SZ

   **値:** LastUpdatedTime

   > [!TIP]
   > レジストリ パスの <*MicrosoftRMS_FQDN*> は、Microsoft RMS サービスの FQDN を指します。 この値を確認するには:
   > 
   > Azure Information Protection に対して[AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)コマンドレットを実行します。 AIPService PowerShell モジュールをまだインストールしていない場合は、「 [AIPService powershell モジュールのインストール](install-powershell.md)」を参照してください。
   > 
   > 出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。
   > 
   > 以下に例を示します。**LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
   > 
   > この値から、**https://** 文字列と **/_wmcs/licensing** 文字列を削除します。 残りの値が、Microsoft RMS サービスの FQDN です。 この例では、Microsoft RMS サービスの FQDN は次の値になります。
   > 
   > **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2. **%localappdata%\Microsoft\MSIPC\Templates** フォルダーとその中に含まれているすべてのファイルを削除します。

3. Office アプリケーションとエクスプローラーのインスタンスを再起動します。

## <a name="office-2019-for-mac-and-office-2016-for-mac-how-to-force-a-refresh-for-templates"></a>Office 2019 for Mac および Office 2016 for Mac:テンプレートを強制的に更新する方法

これらのバージョンの Office for Mac では、保護されたコンテンツを開くとき、または暗号化を適用するために新しく構成された秘密度ラベルを使用してコンテンツを保護するときに、テンプレートが更新されます。 テンプレートを強制的に更新する必要がある場合は、次の手順を実行します。 ただし、この手順のコマンドを実行すると、テンプレート、キーチェーン内の RMS トークンキャッシュ、および以前に開かれた保護されたコンテンツのローカル使用ライセンスが削除されます。 そのため、以前に開いた保護されたコンテンツを開くには、もう一度認証を行う必要があり、インターネットに接続している必要があります。

1. ターミナルを開き、次のコマンドを入力します。
    
        defaults write ~/Library/Containers/com.microsoft.Outlook/Data/Library/Preferences/com.microsoft.Outlook ResetRMSCache 1

2. Mac 用 Outlook を再起動します。

3. 新しい電子メールを作成し、 **[暗号化]** を選択して、**資格情報を確認**します。


## <a name="see-also"></a>関連項目
[Azure Information Protection ポリシーでテンプレートを構成して管理する](configure-policy-templates.md)

