---
title: "AD RMS から Azure Rights Management への移行 - フェーズ 1 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/23/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.sourcegitcommit: f7dd88d90357c99c69fe4fdde67c1544595e02f8
ms.openlocfilehash: defe008a9b78026ccac584bb06762228456a2916


---

# 移行フェーズ 1 - AD RMS のサーバー側の構成

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*

AD RMS から Azure Rights Management (Azure RMS) への移行フェーズ 1 では、次の情報を活用してください。 これらの手順では、「[AD RMS から Azure Rights Management への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 1 から手順 4 を説明します。


## 手順 1: Azure Rights Management Administration Tool をダウンロードする
Microsoft ダウンロード センターに移動し、 [Azure Rights Management Administration Tool](http://go.microsoft.com/fwlink/?LinkId=257721)をダウンロードします。このファイルには、Windows PowerShell 用の Azure RMS 管理モジュールが含まれています。

ツールをインストールします。 手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

## 手順 2. AD RMS から構成データをエクスポートし、それを Azure RMS にインポートする
この手順は、2 段階の処理です。

1.  信頼された発行ドメイン (TPD) を .xml ファイルにエクスポートすることによって、AD RMS から構成データをエクスポートします。 このプロセスは、すべての移行について同じです。

2.  構成データを Azure RMS にインポートします。 現在の AD RMS のデプロイ構成と、Azure RMS テナント キーに対する優先トポロジに応じて、この手順のプロセスは異なります。

### 構成データを AD RMS からエクスポートする
すべての AD RMS クラスター上の、組織のコンテンツを保護していたすべての信頼された発行ドメインに対して、次の手順を実行します。 ライセンス専用クラスターでこれを実行する必要はありません。

> [!NOTE]
> Windows Server 2003 Rights Management を使用している場合は、これらの手順ではなく、「[Windows RMS から異なるインフラストラクチャの AD RMS への移行](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)」の記事の「[SLC、TUD、TPD、および RMS の秘密キーのエクスポート](http://technet.microsoft.com/library/jj835767%28v=ws.10%29.aspx)」の手順を実行してください。

#### 構成データ (信頼された発行ドメインの情報) をエクスポートするには

1.  AD RMS の管理権限を持つユーザーとして AD RMS クラスターにログオンします。

2.  AD RMS 管理コンソール (**Active Directory Rights Management サービス**) から、AD RMS クラスター名を展開し、 **[信頼ポリシー]**を展開し、 **[信頼された発行ドメイン]**をクリックします。

3.  結果ウィンドウで信頼された発行ドメインを選択し、操作ウィンドウから [ **信頼された発行ドメインのエクスポート**] をクリックします。

4.  **[信頼された発行ドメインのエクスポート]** ダイアログ ボックスで:

    -   **[名前を付けて保存]** をクリックし、パスとファイル名を指定して保存します。 ファイル名の拡張子としては必ず **.xml** を指定します (自動的には付加されません)。

    -   強いパスワードを指定して確認します。 このパスワードを覚えておいてください。後で、構成データを Azure RMS にインポートするときに必要になります。

    -   信頼されたドメイン ファイルを RMS バージョン 1.0 で保存するチェック ボックスをオンにしないでください。

信頼された発行ドメインをすべてエクスポートしたら、このデータを Thales から Azure RMS ハードウェア セキュリティ モジュール (HMS) にインポートする手順を開始できます。 詳細については、 

### 構成データを Azure RMS にインポートする
正確な手順は、現在の AD RMS のデプロイ構成と、Azure RMS テナント キーの優先トポロジによって異なります。

現在の AD RMS のデプロイでは、次のいずれかの構成をサーバー ライセンス証明書 (SLC) キーに使用します。

-   AD RMS データベースでのパスワード保護。 これが既定の構成です。

-   Thales ハードウェア セキュリティ モジュール (HSM) を使用する HSM 保護。

-   Thales 以外のサプライヤーのハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護。

-   外部暗号プロバイダーを使用して保護されたパスワード。

> [!NOTE]
> AD RMS でのハードウェア セキュリティ モジュールの使用に関する詳細については、「 [AD RMS でのハードウェア セキュリティ モジュールの使用](http://technet.microsoft.com/library/jj651024.aspx)」を参照してください。

Azure RMS テナント キー トポロジには、テナント キーをマイクロソフトが管理するか (**マイクロソフト管理**) またはユーザーが自分で管理するか (**顧客管理**) の 2 つのオプションがあります。 顧客管理の Azure RMS テナント キーは、“Bring Your Own Key” (BYOK) と呼ばれることもあり、Thales のハードウェア セキュリティ モジュール (HSM) が必要です。 詳細については、記事「[Azure Rights Management テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

> [!IMPORTANT]
> 現在、Exchange Online は Azure RMS BYOK と互換性がありません。  移行後に BYOK を使用し、Exchange Online を使用する場合は、この構成により Exchange Online の IRM 機能が制限されることを理解しておきます。 「[BYOK の料金と制限事項](byok-price-restrictions.md)」の情報は、移行に最適な Azure RMS テナント キー トポロジの選択に役立ちます。

次の表を参考にして、移行に使用する手順を識別してください。 記載されていない組み合わせはサポートされません。

|現在の AD RMS のデプロイ|選択する Azure RMS テナント キー トポロジ|移行手順|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS データベースでのパスワード保護|マイクロソフト管理|後で説明される「**ソフトウェアで保護されたキーからソフトウェアで保護されたキーへの移行**」の手順を参照してください。<br /><br />これは最も簡単な移行パスであり、Azure RMS に構成データを転送するだけで済みます。|
|Thales nShield ハードウェア セキュリティ モジュール (HSM) を使用する HSM 保護|お客様が管理 (BYOK)|後で説明される「**HSM で保護されたキーから HSM で保護されたキーへの移行**」の手順を参照してください。<br /><br />BYOK ツールセットが必要であり、キーをオンプレミス HSM から Azure RMS HSM に転送した後、構成データを Azure RMS に転送する 2 つの手順で行います。|
|AD RMS データベースでのパスワード保護|お客様が管理 (BYOK)|後で説明される「**ソフトウェアで保護されたキーから HSM で保護されたキー**への移行」の手順を参照してください。<br /><br />BYOK ツールセットが必要であり、最初にソフトウェア キーを抽出してオンプレミス HSM にインポートし、オンプレミス HSM から Azure RMS HSM にキーを転送した後、最後に構成データを Azure RMS に転送する 3 つの手順で行います。|
|Thales 以外のサプライヤーのハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護|お客様が管理 (BYOK)|この HSM から Thales nShield ハードウェア セキュリティ モジュール (HSM) にキーを転送する方法については、HSM のサプライヤーに問い合わせてください。 後で説明される「**HSM で保護されたキーから HSM で保護されたキー**への移行」の手順に従います。|
|外部暗号プロバイダーを使用して保護されたパスワード|お客様が管理 (BYOK)|Thales nShield ハードウェア セキュリティ モジュール (HSM) にキーを転送する方法については、暗号プロバイダーのサプライヤーに問い合わせてください。 後で説明される「**HSM で保護されたキーから HSM で保護されたキー**への移行」の手順に従います。|
これらの手順を開始する前に、信頼された発行ドメインをエクスポートしたときに作成した .xml ファイルにアクセスできることを確認します。 たとえば、これらは AD RMS サーバーからインターネットに接続されたワークステーションに移動する USB ドライブに保存されている可能性があります。

> [!NOTE]
> ただし、このデータは秘密キーを含むので、これらのファイルを保存し、セキュリティのベスト プラクティスを使用して保護します。


手順 2 を完了するには、移行パスに応じた手順を選択します。 


- [ソフトウェア キーからソフトウェア キーへ](migrate-softwarekey-to-softwarekey.md)
- [HSM キーから HSM キーへ](migrate-hsmkey-to-hsmkey.md)
- [ソフトウェア キーから HSM キーへ](migrate-softwarekey-to-hsmkey.md)


## 手順 3. RMS テナントをアクティブ化する
この手順の詳細は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の記事で説明しています。


> [!TIP]
> Office 365 サブスクリプションがある場合、Office 365 管理センターまたは Azure クラシック ポータルから Azure RMS をアクティブ化できます。 Azure クラシック ポータルを使用することをお勧めします。この管理ポータルを使用して次の手順を完了するためです。

**Azure RMS テナントが既にアクティブ化されている場合はどうすればよいですか。** 組織の Azure RMS サービスが既にアクティブ化されている場合は、ユーザーが既に Azure RMS を使用してコンテンツを保護し、AD RMS の既存のキー (およびテンプレート) ではなく、自動的に生成されたテナント キー (および既定のテンプレート) を使用している可能性があります。 これは、イントラネット上で適切に管理されたコンピューターではほとんど起こりません。AD RMS インフラストラクチャ用に自動的に構成されるためです。 ただし、イントラネットへの接続の頻度が低いワークグループのコンピューターでは発生する可能性があります。 残念ながら、このようなコンピューターの識別は困難です。そのため、AD RMS から構成データをインポートする前に、サービスをアクティブ化しないようにお勧めします。

Azure RMS テナントが既にアクティブ化されていて、前述のようなコンピューターを識別できる場合は、手順 5 の説明に従って、それらのコンピューターで CleanUpRMS_RUN_Elevated.cmd スクリプトを実行してください。 このスクリプトを実行すると、それらのコンピューターで強制的にユーザーの環境が再初期化されるため、更新されたテナント キーとインポートされたテンプレートがダウンロードされます。

さらに、移行後に使用するカスタム テンプレートを作成した場合は、それをエクスポートしてインポートする必要があります。 これについては次の手順で説明します。 

## 手順 4. インポートされたテンプレートを構成する
インポートしたテンプレートは **アーカイブ済み**という既定の状態なので、ユーザーが Azure RMS でこれらのテンプレートを使用できるようにする場合は、この状態を **公開済み** に変更する必要があります。

AD RMS からインポートしたテンプレートの外観と動作は、Azure クラシック ポータルで作成するカスタム テンプレートと同じです。 インポートしたテンプレートを公開に変更し、ユーザーがアプリケーションからそれらを表示して選択できるようにする方法は、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

新しくインポートしたテンプレートを公開するだけでなく、移行を続ける前に行う必要があるテンプレートの重要な変更が 2 つあります。 移行プロセス中のユーザーに対するエクスペリエンスを一貫したものにするため、インポートしたテンプレートに変更を加えないでください。また、Azure RMS に付属する 2 つの既定のテンプレートを公開したり、この時点で新しいテンプレートを作成したりしないでください。 代わりに、移行プロセスが完了するまで待ち、AD RMS サーバーを使用停止にします。

この手順で必要な場合があるテンプレートの変更:

- 移行前に Azure RMS でカスタム テンプレートを作成した場合は、手動でエクスポートしてインポートする必要があります。

- AD RMS のテンプレートが **ANYONE** グループを使用していた場合は、同等のグループと権限を手動で追加する必要があります。

## 移行前にカスタム テンプレートを作成した場合の手順

Azure RMS をアクティブ化する前でも後でも、移行前にカスタム テンプレートを作成した場合は、**公開済み**に設定してあっても、移行後にユーザーはテンプレートを使用できません。 ユーザーが使用できるようにするには、最初に次のようにする必要があります。 

1. [Get-AadrmTemplate](https://msdn.microsoft.com/library/dn727079.aspx) を実行して、そのようなテンプレートを識別し、テンプレート ID を記録しておきます。 

2. Azure RMS PowerShell コマンドレット [Export-AadrmTemplate](https://msdn.microsoft.com/library/dn727078.aspx) を使用して、テンプレートをエクスポートします。

3. Azure RMS PowerShell コマンドレット [Import-AadrmTemplate](https://msdn.microsoft.com/library/dn727077.aspx) を使用して、テンプレートをインポートします。

その後は、移行後に作成した他のテンプレートと同様に、これらのテンプレートを発行したりアーカイブしたりできます。


## AD RMS のテンプレートが **ANYONE** グループを使用していた場合の手順

AD RMS のテンプレートが **ANYONE** グループを使用していた場合、テンプレートを Azure RMS にインポートすると、このグループは自動的に削除されます。同等のグループまたはユーザーおよび同じ権限を、インポートされたテンプレートに手動で追加する必要があります。 Azure RMS 用の同等グループの名前は **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<テナント名>.onmicrosoft.com** です。 たとえば Contoso では、このグループは **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com** のようになります。

AD RMS テンプレートに ANYONE グループが含まれるかどうかわからない場合は、次のサンプルの Windows PowerShell スクリプトを使用してこれらのテンプレートを識別できます。 AD RMS での Windows PowerShell の使用に関する詳細については、「[Using Windows PowerShell to Administer AD RMS (Windows PowerShell を使用した AD RMS の管理)](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)」を参照してください。

Azure クラシック ポータルの既定の権限ポリシー テンプレートの 1 つをコピーした場合、組織の自動作成されたグループが表示され、その後 **[権限]** ページで **[ユーザー名]** を特定できます。 ただし、手動で作成またはインポートしたテンプレートに Azure クラシック ポータルを使用してこのグループを追加することはできないため、代わりに次の Azure RMS PowerShell オプションのいずれかを使用する必要があります。

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) PowerShell コマンドレットを使用して、"AllStaff" グループおよび権限を権限定義オブジェクトとして定義し、ANYONE グループに加えて元のテンプレートで既に権限を付与されていた他の各グループまたはユーザーに対してこのコマンドを再度実行します。 その後、[Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) コマンドレットを使用して、これらの権限定義オブジェクトをテンプレートに追加します。

-   [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) コマンドレットを使用して、テンプレートを .XML ファイルにエクスポートします。このファイルを編集して、"AllStaff" グループおよび権限を既存のグループおよび権限に追加してから、[Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) コマンドレットを使用してこの変更を Azure RMS にインポートします。

> [!NOTE]
> この同等グループ "AllStaff" は、AD RMS の ANYONE グループとまったく同じではありません。"AllStaff" グループには、Azure テナントのすべてのユーザーが含まれます。一方、ANYONE グループには、認証されたすべてのユーザーが含まれ、組織外のユーザーが含まれる場合があります。
> 
> こうしうた 2 つのグループの違いにより、"AllStaff" グループだけでなく外部ユーザーも追加しなければならない場合があります。 グループの外部の電子メール アドレスは、現在サポートされていません。


### ANYONE グループを含む AD RMS テンプレートを識別するためのサンプル Windows PowerShell スクリプト
このセクションに含まれるサンプル スクリプトを使用すると、前のセクションで説明したように、ANYONE グループが定義されている AD RMS テンプレートを識別できます。

**免責事項:** このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスではサポートされません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。*

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```


## 次のステップ
「[フェーズ 2 - クライアント側の構成](migrate-from-ad-rms-phase2.md)」に進みます。




<!--HONumber=Jun16_HO4-->


