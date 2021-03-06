---
title: Azure RMS テンプレートの更新 - AIP
description: Azure Rights Management サービスを使用する場合、テンプレートは自動的にクライアント コンピューターにダウンロードされるので、ユーザーはアプリケーションからテンプレートを選択できます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 44925ad0a2c384978d3f91c1d40a5b6b11d5a2a6
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181499"
---
# <a name="refreshing-templates-for-users-and-services"></a>ユーザーとサービスのためのテンプレートの更新

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection の Azure Rights Management サービスを使用する場合、テンプレートは自動的にクライアント コンピューターにダウンロードされるので、ユーザーはアプリケーションからテンプレートを選択できます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。

|アプリケーションまたはサービス|変更後のテンプレートの更新方法|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />トランスポート ルールと Outlook Web アプリに該当 |1 時間以内の自動更新 - 追加の手順は必要ありません。<br /><br />[Office 365 Message Encryption と新機能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)を利用している場合、これが該当します。 信頼された発行ドメイン (TPD) をインポートし、Azure Rights Management サービスを使用するように Exchange Online を既に構成している場合、同じ手順で Exchange Online の新機能を有効にします。|
|Azure Information Protection クライアント|Azure Information Protection ポリシーがクライアントに更新されるたびに自動的に更新されます。<br /><br /> - Azure Information Protection バーをサポートしている Office アプリケーションが開いたとき。 <br /><br /> - ファイルまたはフォルダーを分類して保護するために右クリックしたとき。 <br /><br /> - ラベル付けおよび保護のために PowerShell コマンドレット (Get-AIPFileStatus および Set-AIPFileLabel) を実行するとき。<br /><br /> - Azure Information Protection スキャナー サービスが開始され、ローカル ポリシーが 1 時間前よりも古いとき。 また、スキャナー サービスは 1 時間おきに変更を確認し、次のスキャン サイクルには変更を適用します。<br /><br /> - 24 時間ごと。<br /><br /> さらに、このクライアントは Office と密接に統合されているため、Office 365 アプリ、Office 2019、Office 2016、または Office 2013 で更新されたテンプレートはすべて、Azure Information Protection クライアントでも更新されます。|
|Azure Information Protection 統合ラベル付けクライアント|4 時間ごとに自動で更新されます (Office アプリごとに)。<br /><br /> さらに、このクライアントは Office と密接に統合されているため、Office 365 アプリ、Office 2019、Office 2016、または Office 2013 で更新されたテンプレートはすべて、Azure Information Protection 統合ラベル付けクライアントでも更新されます。|
|Office 365 アプリ、Office 2019、Office 2016、および Office 2013|自動更新 - スケジュールどおりに更新されます。<br /><br />- 以降のバージョンの Office の場合: 既定の更新間隔は、7 日ごとです。<br /><br />スケジュールに先立って強制的に更新するには、以下の「[Office 365 アプリ、Office 2019、Office 2016、Office 2013:変更されたカスタム テンプレートを強制的に更新する方法](#office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-a-changed-custom-template)」セクションを参照してください。|
|Office 2010|ユーザーが Windows からサインアウトして、もう一度サインインし、最大で 1 時間待つと自動的に更新されます。|
|Exchange On-Premises と Rights Management コネクタ<br /><br />トランスポート ルールと Outlook Web アプリに該当|自動更新 - 追加の手順は必要ありません。 ただし、Outlook Web アプリは UI を一日キャッシュします。|
|Office 2019 for Mac と Office 2016 for Mac|自動更新 - 追加の手順は必要ありません。|
|Mac コンピューター用 RMS 共有アプリ|自動更新 - 追加の手順は必要ありません。|
|[機密機能をサポートしている](https://support.office.com/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US&ui=en-US&rs=en-US#bkmk_whereavailable) Office アプリ|これらのクライアントはテンプレートをダウンロードしませんが、これらにオンラインでアクセスします。追加の手順は必要ありません。|

クライアント アプリケーションがテンプレートをダウンロードする必要がある場合 (最初または変更の更新)、ダウンロードが完了し、新規または更新されたテンプレートが完全に機能するまで最大 15 分待機します。 待機時間はテンプレートの構成のサイズや複雑さ、ネットワークの接続などの要素によって異なります。 

## <a name="office-365-apps-office-2019-office-2016-and-office-2013-how-to-force-a-refresh-for-a-changed-custom-template"></a>Office 365 アプリ、Office 2019、Office 2016、Office 2013:変更されたカスタム テンプレートの更新を強制する方法
Office 365 アプリ、Office 2019、Office 2016、または Office 2013 を実行しているコンピューター上でレジストリを編集すると、変更されたテンプレートがコンピューター上で、既定値よりも短い周期で更新されるように自動スケジュールを変更できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターを誤って使用すると、重大な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 マイクロソフトは、レジストリ エディターを誤って使用したために発生した問題を解決できることを保証できません。 レジストリ エディターは、各自の責任で使用してください。

### <a name="to-change-the-automatic-schedule"></a>自動スケジュールを変更するには

1.  レジストリ エディターを使用して、次のレジストリ値のいずれかを作成し設定します。

    - 日数 (1 日以降) では、更新頻度を設定します。**TemplateUpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の情報を使用します。

        **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **次のように入力します。** REG_DWORD

        **値:** TemplateUpdateFrequency

    - 秒 (1 秒間の最小値) の更新頻度を設定します。**TemplateUpdateFrequencyInSeconds** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (秒数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の情報を使用します。

        **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **次のように入力します。** REG_DWORD

        **値:** TemplateUpdateFrequencyInSeconds

    これらのレジストリ値の両方ではなく、一方のみを作成して設定するようにしてください。 両方が存在する場合、 **TemplateUpdateFrequency** は無視されます。

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションとエクスプローラーのインスタンスを再起動します。

### <a name="to-force-an-immediate-refresh"></a>直ちに更新するには

1. レジストリ エディターを使用して、 **LastUpdatedTime** 値のデータを削除します。 たとえば、"**2015-04-20T15:52**" と表示されている場合は、この 2015-04-20T15:52 を削除して、何も表示されていない状態にします。 次の情報を使用して、このレジストリ値データを削除するレジストリ パスを見つけてください。

   **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template\\<*user_alias*>

   **次のように入力します。** REG_SZ

   **値:** LastUpdatedTime

   > [!TIP]
   > レジストリ パスの <*MicrosoftRMS_FQDN*> は、Microsoft RMS サービスの FQDN を指します。 この値を確認するには:
   > 
   > Azure RMS 用の [Get-AadrmConfiguration](/powershell/module/aadrm/get-aadrmconfiguration) コマンドレットを実行します。 Azure RMS 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[AADRM PowerShell モジュールのインストール](install-powershell.md)」を参照してください。
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


## <a name="see-also"></a>関連項目
[Azure Information Protection ポリシーでテンプレートを構成して管理する](configure-policy-templates.md)

