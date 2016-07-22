---
title: "Azure Rights Management の使用停止と非アクティブ化 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0b1c2064-0d01-45ae-a541-cebd7fd762ad
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: 8c114336551417fdbf1503ffc8350e3fc28e9c95


---

# Azure Rights Management の使用停止と非アクティブ化

*適用対象: Azure Rights Management、Office 365*

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) を使用すると、組織がコンテンツを保護するかどうかをいつでも制御できます。また、この情報保護ソリューションの使用をやめた場合でも、以前に保護されていたコンテンツから締め出されることはありません。 以前に保護されていたコンテンツに引き続きアクセスする必要がない場合、サービスを無効にして Azure Rights Management のサブスクリプションの有効期限を終わらせることができます。 たとえば、これは、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を運用環境にデプロイする前のテストが完了した場合も該当します。

ただし、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を運用環境にデプロイした場合、サービスを無効にする前に Azure Rights Management テナント キーのコピーを用意し、サブスクリプションの期限が切れる前にサービスを無効にします。これにより、サービスを無効にした後でも、Azure Rights Management で保護されていたコンテンツに引き続きアクセスできるようになります。 BYOK (Bring Your Own Key) を使用し、HSM で独自のキーを生成し管理している場合、Azure Rights Management テナント キーが既に与えられています。 ただし、そのキーが Microsoft により管理されていた場合 (既定) は、「[Azure Rights Management テナント キーに対する操作](operations-tenant-key.md)」のテナント キーのエクスポートの手順を参照してください。

> [!TIP]
> サブスクリプションの有効期限が切れた後も、延長された期間中、Azure Rights Management テナントでコンテンツを利用できます。 ただし、テナント キーをエクスポートすることはできなくなります。

Azure Rights Management テナント キーがある場合は、オンプレミスで Rights Management (AD RMS) をデプロイし、信頼された発行ドメイン (TPD) としてテナント キーをインポートできます。 Azure Rights Management デプロイメントは次の方法で使用停止できます。

|条件|… 手順|
|----------------------------|--------------|
|すべてのユーザーに Rights Management を引き続き利用させたいが、Azure RMS ではなくオンプレミス ソリューションを利用する場合    →|この変更後に保護されたコンテンツを既存ユーザーが使用するときにユーザーをオンプレミス デプロイに移動させるには、[Set-AadrmMigrationUrl](https://msdn.microsoft.com/library/azure/dn629429.aspx) コマンドレットを使用します。 ユーザーが保護されたコンテンツを使用する際に、自動的に AD RMS インストールを利用するようになります。<br /><br />この変更前に保護されたコンテンツをユーザーが使用できるようにするには、RMS クライアント デプロイ ノートの[サービスの検出に関するセクション](../rms-client/client-deployment-notes.md)の説明に従って Office 2016 または Office 2013 の **LicensingRedirection** レジストリ キーを利用するか、または「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って Office 2010 の **LicenseServerRedirection** レジストリ キーを利用して、クライアントをオンプレミス デプロイにリダイレクトします。|
|Rights Management テクノロジの使用を完全に停止する場合|指定の管理者に [スーパー ユーザー権限](../deploy-use/configure-super-users.md)を与え、その管理者に [RMS 保護ツール](http://www.microsoft.com/en-us/download/details.aspx?id=47256)を提供します。<br /><br />この管理者はこのツールを利用して、Azure Rights Management で保護されていたフォルダーのファイルを一括で復号できます。これにより、ファイルの保護が解除され、Azure RMS や AD RMS などの Rights Management テクノロジがなくても読み取ることができるようになります。 このツールは Azure RMS と AD RMS の両方に対応します。Azure RMS を無効にする前または後に、あるいは前後で処理を組み合わせて、ファイルを復号できます。|
|Azure RMS で保護されていたファイルの一部を特定できないか、読み取れなかった保護ファイルを自動的にユーザーが読み取れるようにする場合|RMS クライアント デプロイ ノートの[サービスの検出に関するセクション](../rms-client/client-deployment-notes.md)の説明に従って Office 2016 と Office 2013 の **LicensingRedirection** レジストリ キーを利用するか、または「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って Office 2010 の **LicenseServerRedirection** レジストリ キーを利用して、すべてのクライアント コンピューターにレジストリ設定をデプロイします。<br /><br />さらに、「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って、**DisableCreation** を **1** に設定して、ユーザーが新しいファイルを保護できないようにするための別のレジストリ設定をデプロイします。|
|読み取れなかったファイルに、制御された手動回復サービスを実行する場合|データ回復グループの指定ユーザーに[スーパー ユーザー権限](../deploy-use/configure-super-users.md)を付与したえうえで [RMS 保護ツール](http://www.microsoft.com/en-us/download/details.aspx?id=47256)を提供して、標準ユーザーから要求されたときにそれらのユーザーがファイルの保護を解除できるようにします。<br /><br />すべてのコンピューターで、「[Office Registry Settings (Office レジストリ設定)](https://technet.microsoft.com/library/dd772637%28v=ws.10%29.aspx)」の説明に従って、**DisableCreation** を **1** に設定して、ユーザーが新しいファイルを保護できないようにするためのレジストリ設定をデプロイします。|
この表に記載された各手順の詳細については、以下のリソースをご覧ください。

-   AD RMS とデプロイメントの参照に関する詳細については、「 [Active Directory Rights Management サービスの概要](https://technet.microsoft.com/library/hh831364.aspx)」をご覧ください。

-   Azure RMS テナント キーを TPD ファイルとしてインポートする方法については、「 [信頼された発行ドメインを追加する](https://technet.microsoft.com/library/cc771460.aspx)」をご覧ください。

-   移行 URL を設定するために Azure RMS 用の Windows PowerShell モジュールをインストールする場合、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

組織の Azure RMS を無効にする用意ができたら、次の手順に従います。

## Rights Management の非アクティブ化
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を非アクティブ化するには、次のいずれかの手順を使用します。

> [!TIP]
> Windows PowerShell の [Disable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629422.aspx) コマンドレットを使用して [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を非アクティブ化することもできます。

#### Office 365 管理センターから Rights Management を非アクティブ化するには

1.  Office 365 デプロイの管理者である[職場または学校のアカウントで Office 365 にサインイン](https://portal.office.com/) します。

2.  Office 365 管理センターが自動的に表示されない場合は、左上のアプリ ランチャー アイコンを選択し、**[管理]** を選択します。 [ **管理** ] タイルは、Office 365 管理者に対してのみ表示されます。

    > [!TIP]
    > 管理センターのヘルプについては、「 [Office 365 管理センターについて - 管理者向けヘルプ](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)」を参照してください。

3.  左ペインで、 **[サービス設定]**を展開します。

4.  [ **Rights Management**] をクリックします。

5.  [ **Rights Management** ] ページで、[ **管理**] をクリックします。

6.  [ **Rights Management** ] ページで、[ **非アクティブ化**] をクリックします。

7.  [ **Rights Management を非アクティブ化しますか?**] というメッセージが表示されたら、[ **非アクティブ化**] をクリックします。

[ **Rights Management がアクティブ化されていません** ] というテキストとアクティブ化するオプションが表示されます。

#### Azure クラシック ポータルから Rights Management を非アクティブ化するには

1.  [Azure クラシック ポータル](http://go.microsoft.com/fwlink/p/?LinkID=275081)にサインインします。

2.  左ペインで、[ **ACTIVE DIRECTORY**] をクリックします。

3.  [ **active directory** ] ページで、[ **RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択し、**[非アクティブ化]** をクリックし、操作を確定します。

これで、[ **Rights Management のステータス** ] に [ **非アクティブ** ] と表示され、[ **非アクティブ化** ] オプションが [ **アクティブ化**] に置き換えられます。






<!--HONumber=Jun16_HO4-->


