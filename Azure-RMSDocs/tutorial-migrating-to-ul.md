---
title: チュートリアル - Azure Information Protection (AIP) クラシック クライアントから統合ラベル付けソリューションへの移行
description: Azure Information Protection (AIP) クラシック クライアントから統合ラベル付けクライアントへの移行に関するステップバイステップのチュートリアルです。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/19/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 746e1a8763c94a3193b7719d5af9326c2d274347
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97805922"
---
# <a name="tutorial-migrating-from-the-azure-information-protection-aip-classic-client-to-unified-labeling-solution"></a>チュートリアル:Azure Information Protection (AIP) クラシック クライアントから統合ラベル付けソリューションへの移行

>***適用対象**:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***関連する内容**:[Windows 用 Azure Information Protection クラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の Azure Information Protection のクラシック クライアントとラベル管理は、2021 年 3 月 31 日をもって非推奨になります。
> 
> この期間に、Azure Information Protection クラシック クライアントの現在のすべてのお客様が、Microsoft Information Protection の統合ラベル付けソリューションを使用する AIP 統合ラベル付けに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
>

このチュートリアルでは、クラシック クライアントから組織の Azure Information Protection のデプロイを、および Azure portal でのラベルとラベル付けポリシーの管理を、統合ラベル付けソリューションと [Microsoft 365 の秘密度ラベル](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)に移行する方法について説明します。

**必要な時間**:移行を完了するために必要な時間は、お使いのポリシーの複雑さと使用する AIP 機能によって異なります。 バックグラウンドで移行する間は、クラシック クライアントを使用し続けることができます。

このチュートリアルでは、各手順の概要について説明し、詳細については、Microsoft ドキュメントの他の場所にある関連セクションを参照してください。

このチュートリアルでは、次のことについて説明します。
> [!div class="checklist"]
> * 移行の計画についての詳細
> * ラベルを統合ラベル付けプラットフォームに移行する
> * 新しいラベル付け管理センターで詳細設定を構成する方法の詳細
> * ポリシーを統合ラベル付けプラットフォームにコピーする
> * 統合ラベル付けクライアントのデプロイ

## <a name="why-migrate-to-the-unified-labeling-solution"></a>統合ラベル付けソリューションへ移行する理由

[クラシック クライアントの非推奨化が予定されている](https://aka.ms/aipclassicsunset)ことに加えて、統合ラベル付けソリューションに移行することで、デジタル資産全体の機密データを効果的に保護できます。 移行が完了したら、Microsoft 365 クラウド サービス、オンプレミス、サードパーティの SaaS アプリケーションで Microsoft Information Protection (MIP) を使用します。

MIP では、多くの基本的な情報保護機能に対して組み込みのラベル付けサービスをサポートしているため、組み込みのラベル付けでサポートされていない追加機能に対してのみクライアントの使用を予約できます。

- デプロイして維持する追加ソフトウェアが少なくなることで、**メンテナンス コストを削減する**
- 追加のアドインを必要とせずに、**Office のパフォーマンスを向上させる**
- ラベル付け管理センターを使用して、AIP、Office 365、Windows での **ラベル付けと保護ポリシーの管理を効率化する**。 

    サポートされている管理センターには、Microsoft 365 コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 セキュリティ/コンプライアンス センターが含まれます。

詳細については、[統合ラベル付けの移行に関するブログ](https://techcommunity.microsoft.com/t5/microsoft-security-and/understanding-unified-labeling-migration/ba-p/783185)をご覧ください。

## <a name="planning-your-migration"></a>移行を計画する

AIP クラシック クライアントで使用できるほとんどの機能は、統合ラベル付けクライアントでも使用できますが、一部の機能はまだ完全には使用できず、統合ラベル付け用に構成が異なっているものがあります。

統合ラベル付けクライアント使用時に、使用する Information Protection の機能がどのように異なるかを理解するには、次の記事を確認してください。

- [Microsoft 365 の組み込みラベル付け機能の詳細](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)
- [Windows コンピューターのラベル付けソリューションを比較する](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)
- [統合ラベル付け管理センターで、既定ではサポートされていないラベル設定を管理する方法の詳細](configure-policy-migrate-labels.md#label-settings-that-are-not-supported-in-the-admin-centers)

> [!TIP]
> エンド ユーザーの動作に影響を与えるクライアントの違いが文書化されている場合は、統合ラベル付けクライアントをデプロイし、新しいポリシーを発行する前に、これらの変更をユーザーに効果的に伝えることをお勧めします。

移行を計画し、発生する変更を理解したら、続けて、[ラベルを統合ラベル付けプラットフォームに移行します](#migrating-labels-to-the-unified-labeling-platform)。

## <a name="migrating-labels-to-the-unified-labeling-platform"></a>ラベルを統合ラベル付けプラットフォームに移行する

移行を計画し、クライアントの違いを管理する方法を検討したら、統合ラベル付けをアクティブ化し、ラベルを移行する準備が整います。

移行中も、Azure portal の Azure Information Protection 領域にある AIP クラシック クライアントとポリシーを使用し続けることができます。 2 つのクライアントが、追加の構成なしで同時に動作できます。

1. 次のいずれかのロールを使用して、管理者として [Azure portal](https://portal.azure.com) にサインインします。

    - **コンプライアンス管理者**
    - **コンプライアンス データ管理者**
    - **セキュリティ管理者**
    - **グローバル管理者**
    

1. Azure Information Protection 領域の左側にある **[管理]** の下で、 **[統合ラベル付け]** を選択します。

    ページの上部にある :::image type="icon" source="media/qs-tutor/activate.PNG" border="false"::: **[アクティブ化]** を選択して、統合ラベル付けを有効にします。

    ラベルが Azure Information Protection から統合ラベル付けプラットフォームにコピーされ、両方のシステムに格納されるようになります。

    ラベル付け管理センターを開き、表示されるラベルと Azure Information Protection 領域を比較します。 この 2 つのリストは同じであるはずです。 たとえば、Microsoft 365 セキュリティ/コンプライアンス センターと比較すると、次のようになります。

    :::image type="content" source="media/qs-tutor/compare-migrated-labels-small.png" alt-text="Azure portal とセキュリティ/コンプライアンス センター間で移行されたラベルを比較する" lightbox="media/qs-tutor/compare-migrated-labels.png":::

    > [!NOTE]
    > 必要に応じて、移行が完了するまで、両方のシステムでラベルの使用を継続します。 詳細については、「[ラベル付け編集の同期](#synchronizing-labeling-edits)」を参照してください。

続けて、[ポリシーを統合ラベル付けプラットフォームにコピーします](#copy-policies-to-the-unified-labeling-platform)。

### <a name="synchronizing-labeling-edits"></a>ラベル付け編集の同期

ラベルをラベル付け管理センター (Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター、または Microsoft 365 セキュリティ/コンプライアンス センターなど) に移行した後は、Azure portal 内で移行済みラベルに編集を行うと、管理センター内で同じラベルに自動的に同期されて、統合ラベル付けが行われます。

その逆で、管理センター内の移行済みラベルに編集が行われても、Azure portal には同期され "*ません*"。 管理センターで編集を行い、Azure portal でそれらを更新する必要がある場合は、ポータルに戻って更新を発行します。

**Azure portal で更新されたラベルを発行するには**、次のようにします。

1. Azure Information Protection 領域の左側にある **[管理]** の下で、 **[統合ラベル付け]** を選択します。

1. :::image type="icon" source="media/i-publish.PNG" border="false"::: **[発行]** を選択します。 

> [!NOTE]
> この手順が必要になるのは、統合ラベル付けプラットフォームで移行済みラベルを編集し、その編集を Azure portal で同期する必要がある場合のみです。 

### <a name="migrating-labels-via-powershell"></a>PowerShell を使用してラベルを移行する

PowerShell を使用して、GCC High 環境の場合など、既存のラベルを移行することもできます。

[New-Label](/powershell/module/exchange/new-label) コマンドレットを使用して、既存の秘密度ラベルを移行します。

たとえば、秘密度ラベルに暗号化が含まれている場合、**New-Label** コマンドレットを次のように使用できます。

```PowerShell
New-Label -Name 'aipscopetest' -Tooltip 'aipscopetest' -Comment 'admin notes' -DisplayName 'aipscopetest' -Identity 'b342447b-eab9-ea11-8360-001a7dda7113' -EncryptionEnabled $true -EncryptionProtectionType 'template' -EncryptionTemplateId 'a32027d7-ea77-4ba8-b2a9-7101a4e44d89' -EncryptionAipTemplateScopes "['allcompany@labelaction.onmicrosoft.com','admin@labelaction.onmicrosoft.com']"
```

GCC、GCC High、および DoD 環境での作業の詳細については、[Azure Information Protection Premium Government サービスの説明](/enterprise-mobility-security/solutions/ems-aip-premium-govt-service-description#label-migration)に関する記事をご覧ください。 

## <a name="copy-policies-to-the-unified-labeling-platform"></a>ポリシーを統合ラベル付けプラットフォームにコピーする

Azure portal に保存しているすべてのポリシーを統合ラベル付けプラットフォームでそのまま使用できるようにコピーします。

現在のところ、この機能はプレビュー段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。

> [!NOTE]
> ポリシーのコピーには、一定の制限があります。 一から始めて、ラベル付け管理センターで手動でポリシーを作成することもできます。 詳細については、[Microsoft 365 のドキュメント](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)を参照してください。
> 

**ポリシーをコピーするには**、次のようにします。 

1. 次の項目について検討し、この時点でポリシーをコピーすることを確認します。

    |考慮事項  |説明  |
    |---------|---------|
    |**ポリシーをコピーすると、"*すべて*" のポリシーがコピーされる**     |     ポリシーのコピーで、特定のポリシーだけをコピーすることはできません。現在は、すべてのポリシーをコピーするか、まったくしないのどちらかです。   |
    |**コピーすると、ポリシーが自動的に発行される**     |  統合ラベル付けクライアントにコピーしたポリシーは、統合ラベル付けがサポートされているすべてのクライアントに自動的に発行されます。 <br /><br />   **重要**:ポリシーを発行しない場合は、コピーしないでください。     |
    |**コピーすると、同じ名前の既存のポリシーが上書きされる**     |   管理センターに同じ名前のポリシーが既に存在する場合、ポリシーをコピーすると、そのポリシーで定義されているすべての設定が上書きされます。   <br /><br />Azure portal からコピーされるすべてのポリシーには、`AIP_<policy name>` という構文で名前が付けられます。    |
    |**一部のクライアント設定はコピーされない**     | 一部のクライアント設定は、統合ラベル付けプラットフォームにコピーされないため、移行後に手動で構成する必要があります。 <br /><br />詳細については、「[ラベル付け詳細設定を構成する](#configuring-advanced-labeling-settings)」を参照してください|
    | | |

1. 次のいずれかのロールを使用して、管理者として [Azure portal](https://portal.azure.com) にサインインします。

    - **コンプライアンス管理者**
    - **コンプライアンス データ管理者**
    - **セキュリティ管理者**
    - **グローバル管理者**


1. Azure Information Protection 領域の左側にある **[管理]** の下で、 **[統合ラベル付け]** を選択します。

1. :::image type="icon" source="media/i-copy-policies.PNG" border="false"::: **[ポリシーのコピー]** を選択します (プレビュー)。 Azure portal に保存しているすべてのポリシーが管理センターにコピーされます。

    同じ名前のポリシーが管理センターに既に存在する場合、そのポリシーは Azure portal の設定で上書きされます。

    > [!IMPORTANT]
    > Microsoft Cloud App Security および Azure Information Protection ラベルを現在使用している場合は、ポリシーが 1 人のユーザーに限定されている場合であっても、ラベルの最小セットを持つポリシーを少なくとも 1 つ、ラベル付け管理センターに発行していることを確認します。 
    >
    > このポリシーは、ラベル付け管理センター内のすべてのラベルを識別して Microsoft Cloud App Security ポータルで表示するために Microsoft Cloud App Security に必要です。

ラベルとポリシーの両方を移行したので、続けて、[ラベル付け詳細設定を構成](#configuring-advanced-labeling-settings)し、移行されなかった詳細構成に対応します。

## <a name="configuring-advanced-labeling-settings"></a>ラベル付け詳細設定を構成する

[計画段階](#planning-your-migration)で説明したように、ラベル付け詳細設定の一部は自動的には移行されず、統合ラベル付けプラットフォーム用に再構成する必要があります。

詳細については、次を参照してください。

- [PowerShell でラベル付け詳細設定を構成する](#configure-advanced-labeling-settings-in-powershell)
- [ラベル付け管理センターでラベル条件を定義する](#define-label-conditions-in-the-labeling-admin-center)

### <a name="configure-advanced-labeling-settings-in-powershell"></a>PowerShell でラベル付け詳細設定を構成する

1. Office 365 セキュリティ/コンプライアンス センター PowerShell モジュールに接続します。 詳細については、[セキュリティ/コンプライアンス センター PowerShell のドキュメント](https://docs.microsoft.com/powershell/exchange/connect-to-scc-powershell)をご覧ください。

1. ラベル付け詳細設定を定義するには、**Set-Label** コマンドレットを使用し、**AdvancedSettings** パラメーター、設定を適用するラベル、および設定を定義するためのキーと値のペアを指定します。
    
    使用する構文は以下のとおりです。

    ```PowerShell
    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{<Key>="<value1>,<value2>"}
    ```

    各値の説明:
    - **`<LabelGUIDorName>`** にラベル名または GUID を使用して、ラベルを識別します
    - **`<Key>`** は、デバイスに設定するキーまたは詳細設定の名前です
    - **`<Value>`** は、定義する設定値です。 値を引用符で囲み、複数の値はコンマで区切ります。 空白はサポートされていません。

1. まず、次の詳細設定を構成します。

    - [ラベルの色を指定する](rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)
    - [親ラベルに既定のサブラベルを指定する](rms-client/clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [ラベルを構成して Outlook で S/MIME 保護を適用する](rms-client/clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [カスタム プロパティを使用してラベルを定義する](rms-client/clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions) 
    - [ラベルの翻訳を定義する](https://docs.microsoft.com/powershell/module/exchange/set-label)。 

    使用できる詳細構成の詳細については、「[管理者ガイド:Azure Information Protection 統合ラベル付けクライアントのカスタム構成](rms-client/clientv2-admin-guide-customizations.md)」を参照してください。

> [!NOTE]
> 統合ラベル付けプラットフォーム用に定義した設定を活用するには、エンド ユーザーのコンピューターに統合ラベル付けクライアントがインストールされている必要があります。 
>
> これらの詳細設定は、Office 365 によって提供される組み込みのラベル付けのみを使用しているユーザーは利用できません。
> 

### <a name="define-label-conditions-in-the-labeling-admin-center"></a>ラベル付け管理センターでラベル条件を定義する

統合ラベル付け条件は、Azure portal で作成されたものよりも柔軟性が高く、精度も向上します。 

統合ラベル付け条件機能を活用するには、以下のラベル付け管理センターでラベル付け条件を手動で作成します。

- Microsoft 365 コンプライアンス センター
- Microsoft 365 セキュリティ センター
- Microsoft 365 セキュリティ/コンプライアンス センター

詳細については、Microsoft 365 のドキュメントの[秘密度ラベルでできること](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#what-sensitivity-labels-can-do)に関する記事をご覧ください。

> [!TIP]
> Office 365 DLP または Microsoft Cloud App Security で使用するために作成されたカスタムの機密情報の種類がある場合は、それらをそのまま統合ラベル付けに適用します。 詳細については、[Microsoft 365 のドキュメント](https://docs.microsoft.com/microsoft-365/compliance/apply-sensitivity-label-automatically)を参照してください。
>  

## <a name="deploy-a-unified-labeling-client"></a>統合ラベル付けクライアントをデプロイする

統合ラベル付けポリシーとラベルを確実に使用できるように、ユーザーのコンピューター全体で統合ラベル付けをサポートするクライアントをデプロイします。 

ユーザーは、ラベル付け管理センターに接続し、統合ラベル付けポリシーを取得できる、サポートされているクライアントを持っている必要があります。 

詳細については、次を参照してください。
- [Windows 以外のプラットフォーム](#non-windows-platforms)
- [Windows プラットフォーム](#windows-platforms)
- [クラシック クライアントのエンドユーザーに表示される変更](#what-changes-for-classic-client-end-users)

### <a name="non-windows-platforms"></a>Windows 以外のプラットフォーム

Windows 以外のプラットフォームを使用しているユーザーの場合、統合ラベル付け機能が Office クライアントに直接組み込まれ、発行したラベルをすぐに使用できます。 

統合ラベル付け機能を組み込んだ Office クライアントには次のものがあります。 

- macOS 用の Office クライアント
- Office for the web (プレビュー)
- Outlook Web App
- モバイル用 Outlook

これらのプラットフォームの統合ラベル付けの詳細については、Microsoft サポート サイトの [Office でファイルとメールに秘密度ラベルを適用する](https://support.microsoft.com/office/apply-sensitivity-labels-to-your-files-and-email-in-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)に関するページをご覧ください。 

### <a name="windows-platforms"></a>Windows プラットフォーム

Microsoft 365 Apps for Enterprise がインストールされている Windows コンピューターの場合は、Office バージョン 1910 以降で提供されている組み込みのラベル付けサポートを使用するか、Azure Information Protection 統合ラベル付けクライアントをインストールして、AIP 機能をエクスプローラーまたは PowerShell に拡張します。

詳細については、次を参照してください。 

- [Windows コンピューターのラベル付けソリューションを比較する](rms-client/use-client.md#compare-the-labeling-solutions-for-windows-computers)
- [クイック スタート: Azure Information Protection (AIP) 統合ラベル付けクライアントのデプロイ](quickstart-deploy-client.md)

Azure Information Protection 統合ラベル付けクライアントは、[Microsoft ダウンロード センター](https://aka.ms/aipclient)からダウンロードできます。 

クライアントをデプロイするには、**AzInfoProtection_UL** ファイルを必ず使用します。 現在コンピューターにクラシック クライアントがインストールされている場合は、統合ラベル付けクライアントをインストールすると、インプレース アップグレードが実行されます。

> [!NOTE]
> 組み込みのラベル付けを使用するタイミングを決定するとき、および統合ラベル付けクライアントを使用するタイミングを決定するときは、組織で現在必要な AIP 機能を検討します。 
>> 

### <a name="what-changes-for-classic-client-end-users"></a>クラシック クライアントのエンドユーザーに表示される変更

Azure Information Protection クラシック クライアントを使用しているエンド ユーザーにとって最も目に見える大きな違いは、Office アプリの **[保護]** ボタンが **[秘密度]** ボタンに置き換わっていることです。 

秘密度ラベルと統合ラベル付けによってサポートされる追加機能を利用すると、エンド ユーザーの Office アプリにもそれらの変更が表示されるようになります。

次に例を示します。

- **Windows AIP クラシック クライアント**

    :::image type="content" source="media/infoprotect-protectbutton-pulldown.png" alt-text="クラシック クライアントの [保護] ボタン":::

- **Windows AIP 統合ラベル付けクライアント**

    :::image type="content" source="media/qs-tutor/sample-aip-client-office.PNG" alt-text="Microsoft Office の統合ラベル付けクライアントのサンプル ボタン":::

> [!TIP]
> ラベルを発行済みで、組み込みサポートを使用しているクライアントに **[秘密度]** ボタンが表示されない場合は、必要に応じて、関連するトラブルシューティング ガイドを確認してください。
>
 
## <a name="next-steps"></a>次のステップ

ラベル、ポリシー、およびデプロイされたクライアントを必要に応じて移行した後は、Microsoft 365 コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 セキュリティ/コンプライアンス センターなどの[ラベル付け管理センターでラベル付けとラベル付けポリシーを管理](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)します。

統合ラベル付けプラットフォームを使用すると、Azure portal の Azure Information Protection 領域に戻るだけで、次のことができます。

- [AIP スキャナーを使用する](deploy-aip-scanner.md)
- [AIP 分析を使用してアクティビティのラベル付けを監視する](reports-aip.md)

エンドユーザーは、Web、Mac、iOS、Android 用の最新の Office アプリと Microsoft 365 Apps for Enterprise に組み込まれているラベル付け機能を利用することをお勧めします。 

組み込みのラベル付けによってまだサポートされていない追加の AIP 機能を使用するには、Windows 用の最新の統合ラベル付けクライアントを使用することをお勧めします。
