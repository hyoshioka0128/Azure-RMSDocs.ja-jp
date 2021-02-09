---
title: AD RMS から Azure Information Protection への移行 - フェーズ 5
description: AD RMS から Azure Information Protection への移行のフェーズ 5 には、手順 10 から 12 が含まれます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: fd030502c6d6583e72be63fa424ff8186ebaadc7
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560307"
---
# <a name="migration-phase-5---post-migration-tasks"></a>移行フェーズ 5 - 移行後のタスク

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連する内容**:[AIP の統合ラベル付けクライアントとクラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

AD RMS から Azure Information Protection への移行フェーズ 5 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 10 から手順 12 を説明します。

## <a name="step-10-deprovision-ad-rms"></a>手順 10. AD RMS のプロビジョニング解除

サービス接続ポイント (SCP) を Active Directory から削除し、コンピューターがオンプレミス Rights Management インフラストラクチャを検出しないようにします。 既存のクライアントを移行した場合、レジストリに (たとえば、移行スクリプトを実行して) 構成したリダイレクトがあるため、この操作は省略可能です。 ただし、SCP を削除すると、移行の完了後に新しいクライアントと一部の RMS 関連サービスおよびツールは SCP を見つけられなくなります。 この時点で、すべてのコンピューター接続は Azure Rights Management サービスにアクセスすることになります。

SCP を削除するには、ドメイン エンタープライズ管理者としてログインしていることを確認し、次の手順を使用します。

1. Active Directory Rights Management サービス コンソールで、AD RMS クラスターを右クリックし、**[プロパティ]** をクリックします。

2. [**SCP**] タブをクリックします。

3. [**SCP を変更する**] チェック ボックスを選択します。

4. **[現在の SCP を削除する]** を選択して **[OK]** をクリックします。

次に AD RMS サーバーのアクティビティを監視します。 たとえば、[システム正常性レポートの要求の確認](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee221012(v=ws.10))、[ServiceRequest テーブルの確認](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772686(v=ws.10))、[保護コンテンツに対するユーザー アクセスの監査](https://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)などです。

RMS クライアントがこれらのサーバーと通信していないこと、およびクライアントが Azure Information Protection を正常に使用していることを確認できたら、これらのサーバーから AD RMS サーバーの役割を削除できます。 専用サーバーを使用している場合は、最初にサーバーをシャットダウンするときの警告手順を使用することをお勧めします。 この方法では、サービス継続性のためにこれらのサーバーを再起動する必要がある問題の報告が発生していないことを確認でき、クライアントが Azure Information Protection を使用していない理由を調査する時間を確保できます。

AD RMS サーバーのプロビジョニングを解除した後は、テンプレートとラベルを確認する機会を得ることができます。 たとえば、テンプレートをラベルに変換し、それらを統合して、ユーザーが選択したり、再構成したりすることができないようにします。 これは、既定のテンプレートを発行するのにも適しています。

機密ラベルと統一されたラベル付けクライアントについては、Microsoft 365 security center、Microsoft 365 コンプライアンスセンター、Microsoft 365 Security & コンプライアンスセンターなどのラベル付け管理センターを使用してください。 詳細については、Microsoft 365 のドキュメントを参照してください。

クラシッククライアントを使用している場合は、Azure portal を使用します。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](./configure-policy-templates.md)」を参照してください。

>[!IMPORTANT]
> この移行の終了時には、AD RMS クラスターを Azure Information Protection と hold your key ([HYOK](configure-adrms-restrictions.md)) オプションと共に使用することはできません。 
>
> HYOK でクラシッククライアントを使用している場合は、リダイレクトが配置されているため、使用する AD RMS クラスターには、移行したクラスターのライセンス Url が異なる必要があります。
>
### <a name="additional-configuration-for-computers-that-run-office-2010"></a>Office 2010 を実行するコンピューターの追加構成

> [!IMPORTANT]
> Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「 [AIP and Legacy Windows And Office versions](known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。
> 

移行されたクライアントが Office 2010 を実行している場合、AD RMS サーバーがプロビジョニング解除された後で、保護されたコンテンツを開くときにユーザーが遅延することがあります。 または、保護されたコンテンツを開くための資格情報がないというメッセージが表示されることがあります。 これらの問題を解決するには、これらのコンピューターに対してネットワークリダイレクトを作成し、AD RMS URL FQDN をコンピューターのローカル IP アドレス (127.0.0.1) にリダイレクトします。 これを行うには、各コンピューターでローカルホストファイルを構成するか、DNS を使用します。

- **ローカルホストファイルを使用** したリダイレクト: ローカルホストファイルに次の行を追加します。を `<AD RMS URL FQDN>` AD RMS クラスターの値に置き換えます。プレフィックスや web ページは含まれません。

    ```sh
    127.0.0.1 <AD RMS URL FQDN>
    ```

- **DNS を使用** したリダイレクト: AD RMS URL FQDN の新しいホスト (a) レコードを作成します。このレコードには、IP アドレス127.0.0.1 が使用されています。

## <a name="step-11-complete-client-migration-tasks"></a>手順 11. クライアントの移行タスクを完了する

モバイル デバイス クライアントおよび Mac コンピューターの場合: [AD RMS モバイル デバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11))をデプロイするときに作成した DNS SRV レコードを削除します。

これらの DNS の変更が反映されると、これらのクライアントは Azure Rights Management サービスを自動的に検出して使用を開始します。 ただし、Office Mac を実行する Mac コンピューターは、AD RMS からの情報をキャッシュに入れます。 これらのコンピューターの場合、このプロセスには最大で 30 日かかることがあります。

Mac コンピューターが検出プロセスを直ちに実行するようにするには、キーチェーンで "adal" を検索し、すべての ADAL エントリを削除します。 これらのコンピューターで次のコマンドを実行します。

````sh

rm -r ~/Library/Cache/MSRightsManagement

rm -r ~/Library/Caches/com.microsoft.RMS-XPCService

rm -r ~/Library/Caches/Microsoft\ Rights\ Management\ Services

rm -r ~/Library/Containers/com.microsoft.RMS-XPCService

rm -r ~/Library/Containers/com.microsoft.RMSTestApp

rm ~/Library/Group\ Containers/UBF8T346G9.Office/DRM.plist

killall cfprefsd

````

既存のすべての Windows コンピューターを Azure Information Protection に移行した後は、オンボーディング制御を使い続け、移行プロセス用に作成した **AIPMigrated** グループを残しておく理由はありません。

最初にオンボーディング制御を解除すると、**AIPMigrated** グループと、移行スクリプトをデプロイするために作成した任意のソフトウェア デプロイ方法を削除できます。

オンボーディング制御を解除するには:

1. PowerShell セッションで Azure Rights Management サービスに接続し、メッセージが表示されたら、グローバル管理者の資格情報を指定します。

    ```PowerShell
    Connect-AipService

2. Run the following command, and enter **Y** to confirm:

    ```PowerShell
    Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
    ```

    このコマンドを実行すると、Azure Rights Management 保護サービスのライセンスの強制が解除され、すべてのコンピューターでドキュメントおよび電子メールを保護できるようになります。

3. オンボーディング制御が設定されていないことを確認します。

    ```PowerShell    
    Get-AipServiceOnboardingControlPolicy
    ```

    出力で、**License** が **False** と表示され、**SecurityGroupOjbectId** に対して GUID が表示されないことを確認します。

最後に、Office 2010 を使用していて、Windows タスク スケジューラ ライブラリで "**AD RMS Rights Policy Template Management (Automated) (AD RMS 権利ポリシー テンプレート管理 (自動))**" タスクを有効にしている場合、Azure Information Protection クライアントでは使用されていないため、このタスクを無効にします。 

通常、このタスクはグループ ポリシーを使用して有効にされ、AD RMS デプロイをサポートします。 このタスクは、 **Microsoft**  >  **Windows**  >  **Active Directory Rights Management サービス Client** の場所にあります。 

> [!IMPORTANT]
> Office 2010 の拡張サポートは、2020年10月13日に終了しました。 詳細については、「 [AIP and Legacy Windows And Office versions](known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>手順 12. Azure Information Protection テナント キーを再入力する

AD RMS のデプロイで RMS 暗号化モード1を使用していた場合、このモードでは1024ビットのキーと SHA-1 が使用されるため、この手順を実行する必要があります。 この構成は、十分なレベルの保護を提供するものと見なされます。 マイクロソフトは、1024ビットの RSA キーなどの下位キーの長さの使用を保証していません。また、SHA-1 など、不適切なレベルの保護を提供するプロトコルの使用については推奨しません。

キーを更新すると、RMS 暗号化モード2を使用する保護が適用され、その結果、2048ビットキーと SHA-256 が生成されます。

AD RMS のデプロイで暗号化モード 2 が使用されている場合も、この手順を実行することをお勧めします。新しいキーは、AD RMS キーに対する潜在的なセキュリティ侵害からテナントを保護するのに役立つためです。

Azure Information Protection テナント キーの再入力を行うと ("キーをロールする" とも言われる)、現在アクティブなキーはアーカイブされ、Azure Information Protection は、指定した別のキーの使用を開始します。 この別のキーは、Azure Key Vault で自分で作成した新しいキーとすることも、テナント用に自動的に作成された既定のキーとすることもできます。

あるキーから別のキーへの移動は、すぐには行われませんが、数週間かかります。 即時には行われないために、元のキーの侵害が疑われるまで待たず、移行が完了したらすぐにこの手順を実行してください。

Azure Information Protection テナント キーを更新するには:

- **テナントキーが Microsoft によって管理されている場合**: PowerShell コマンドレットの [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) を実行し、テナント用に自動的に作成されたキーのキー識別子を指定します。 指定する値を特定するには、 [Get AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys) コマンドレットを実行します。 テナント用に自動的に作成されたキーは作成日が最も古いので、次のコマンドを使用して識別することができます。

        
    ```PowerShell
    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1
    ```

- **テナントキーがユーザーによって管理されている場合 (BYOK)**: Azure Key Vault で、Azure Information Protection テナントのキー作成プロセスを繰り返してから、 [AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) コマンドレットをもう一度実行して、この新しいキーの URI を指定します。

Azure Information Protection テナント キーの管理について詳しくは、「[Azure Information Protection テナント キーに対する操作](./operations-tenant-key.md)」を参照してください。


## <a name="next-steps"></a>次のステップ

移行が完了したら、 [分類、ラベル付け、保護に関する AIP の展開ロードマップ](deployment-roadmap-classify-label-protect.md) を確認し、必要に応じてその他の展開タスクを特定します。
