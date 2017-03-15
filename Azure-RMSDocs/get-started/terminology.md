---
title: "Azure Information Protection の用語"
description: "Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/08/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5fecc61fb77625047a5ebedad4ff906fe8c27bbe
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="terminology-for-azure-information-protection"></a>Azure Information Protection の用語

>*適用対象: Azure Information Protection、Office 365*

Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。

|用語|定義|
|--------|--------------|
|AADRM|Azure Rights Management 用の Windows PowerShell モジュールの名前です。これは、以前に (Windows) Azure Active Directory Rights Management という名前だったときに、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] の非公式な略語から派生したサービスです。|
|アクティブ化|[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] サービスを有効化して、組織がドキュメントや電子メールを保護できるようにします。 この操作により、Exchange Online と SharePoint Online の Rights Management 機能も有効になります。|
|Active Directory Rights Management サービス|*AD RMS*という略称で呼ばれることもあります。<br /><br />Windows Server の役割の&1; つで、暗号化とポリシーを使用した権限管理保護により、ドキュメント、ファイル、および電子メールを保護することができます。|
|AD RMS|*Active Directory Rights Management サービス*をご覧ください。|
|Azure Information Protection|分類、ラベル付け、保護を使用してドキュメントと電子メールを保護するクラウドベースのサービスです。 Azure Rights Management は、暗号化ポリシー、ID ポリシー、承認ポリシーを使用して、保護を提供します。|
|Azure Rights Management|*Azure RMS*という略称で呼ばれることもあります。<br /><br />Azure Information Protection で使用される Azure サービスであり、暗号化とポリシーを使用して、ドキュメント、ファイル、および電子メールを保護することができます。  *Azure Rights Management サービス*とも呼ばれます。 以前の名前には次のものがあります。<br /><br />- *Windows Azure Active Directory Rights Management*: Windows Azure AD Rights Management サービスという略称で呼ばれることもあります。<br /><br />- *RMS Online*: 元の推奨名です。エラー メッセージやログ ファイルのエントリで表示されることがあります。|
|Azure RMS|*Azure Rights Management*をご覧ください。|
|BYOK|*Bring Your Own Key*をご覧ください。|
|Bring Your Own Key|*BYOK*という略称で呼ばれることもあります。<br /><br />組織が Azure Information Protection の独自のテナント キーを生成および管理するときに選択する構成およびトポロジ オプションです。|
|コンテンツ キー|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を使用して保護されている各ドキュメントまたは電子メールに対して RMS 対応アプリケーションが作成する一意のキーです。情報漏えいの危険性を減らすのに役立ちます。|
|使用処理|読み取りや使用のために、[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] で保護されているファイルのロックを解除する操作。|
|非アクティブ化|Rights Management サービスを無効化します。組織は Azure Information Protection を使用できなくなります。|
|部門別のテンプレート|権限ポリシー テンプレート (カスタム テンプレート) を作成して、組織内のすべてのユーザーではなく、選択したユーザーに表示するように構成します。|
|対応アプリケーション|Rights Management をネイティブでサポートするアプリケーション。Word や Excel などの Office アプリケーションが含まれます。 独立系ソフトウェア ベンダー (ISV) や開発者も、[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をネイティブでサポートするアプリケーションを作成できます。|
|エンタープライズ権限管理|業界標準の一般的な用語です。暗号化ツールとポリシー承認ツールを組み合わせて組織の機密情報や重要情報を保護する製品やソリューションを説明する際によく使用されます。 Azure Information Protection は、エンタープライズ権限管理 (ERM) ソリューションの一例です。|
|ERM|*エンタープライズ権限管理*をご覧ください。|
|一般保護|任意のファイルの種類を暗号化し、承認されていないユーザーがそのファイルを開けないようにする保護レベル。 ファイルを開いた後は暗号化が解除され、[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をネイティブでサポートしていないアプリケーションで使用できます。|
|HYOK|「*Hold Your Own Key*」を参照してください。|
|Hold Your Own Key|*HYOK* という略称で呼ばれることもあります。<br /><br />通常は規制やコンプライアンス上の理由から、キーをオンプレミスで生成および保存する組織の構成およびトポロジ オプション。|
|情報保護|*IP*という略称で呼ばれることもあります。<br /><br />業界標準の一般的な用語です。データやファイルを未承認のアクセスから保護することを指します。これらのデータやファイルは、電子メールやドキュメント共有によって組織の外部に移動しても引き続き保護されます。 Microsoft Azure Information Protection は、情報保護 (IP) ソリューションの一例です。|
|Information Rights Management|*IRM*という略称で呼ばれることもあります。<br /><br />Exchange Server、Word、および SharePoint Online などの Office サービスと共に使用される用語で、Microsoft Rights Management サービスをサポートする機能を説明します。|
|IRM|*Information Rights Management*をご覧ください。|
|MSDRM|RMS クライアント 1.0 を指す用語として使用されることがあります。新しいクライアントでは、MSIPC という名前に置き換えられています。 この古いクライアントでは、RMS SDK 1.0 を使用して開発されたアプリケーションと、Office 2010 および Office 2007、Exchange 2010 および Exchange 2013、SharePoint 2010 および SharePoint 2007 をサポートしています。|
|MSIPC|RMS クライアント 2.0 を指す用語として使用されることがあります。古い RMS クライアントの MSDRM を置き換えるものです。 この新しいクライアントでは、RMS SDK 2.0 を使用して開発されたアプリケーションと、Office 2016 と Office 2013、SharePoint 2013、RMS 共有アプリケーション、および Azure Information Protection クライアントをサポートしています。|
|ネイティブ保護|すべての対応アプリケーションで使用できる保護レベル。承認されていないユーザーがファイルを開けないようにするだけでなく、読み取り専用や印刷不可など、より厳格なポリシーを適用できます。 また、ファイルが他のユーザーに転送されたり、他のユーザーがアクセスできる公開された場所に保存された場合でも、ファイルに対する保護は維持されます。|
|.pfile|権限管理サービスが一般的に保護するすべてのファイルに付けられるファイル名拡張子。|
|。ppdf|電子メールで共有するためにファイル (Word、Excel、PowerPoint、または PDF) の PDF コピーが権限管理サービスによって自動的に作成されるときに付けられるファイル名拡張子。この拡張子を持つファイルは、あらゆるデバイスで読み取ることができます (編集はできません)。|
|アクセス許可レベル|エンドユーザーと管理者が、役割ベースの構成オプションを選択しやすくするための使用権限の論理的なグループ化。 たとえば、レビュー担当者や共同作成者などがあります。|
|保護|ファイルや電子メール メッセージに権限管理の制御を適用し、暗号化、ID、アクセス制御ポリシーを使用してデータを保護します。|
|publish|未承認のアクセスおよび使用を防ぐためにファイルを保護する操作。|
|Rights Management コネクタ|Exchange Server や SharePoint などのオンプレミス サービスで Azure Rights Management サービスを使用してデータを保護するためにデプロイできる送信プロキシ リレー。|
|Rights Management サービス|クラウド バージョンの [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] ([!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]) とオンプレミス バージョンの [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] (AD RMS) の両方で使用される一般的な用語です。|
|Rights Management 共有アプリケーション|現在は、Azure Information Protection クライアント (インプレース ファイルや電子メールで送信されたファイルを安全に共有できる、Windows および主要なモバイル デバイス向けのオプションのアプリケーション) で置き換えられています。|
|RMS|*Rights Management サービス*をご覧ください。|
|RMS コネクタ|*Rights Management コネクタ*をご覧ください。|
|個人用 RMS|ユーザーの組織が Office 365 または Azure Active Directory のサブスクリプションを保有していない場合にユーザーが [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を使用するための無料のサブスクリプション。|
|RMS 共有アプリ|*Rights Management 共有アプリケーション*をご覧ください。|
|保護のみモード|ラベルを適用する Azure Information Protection ポリシーがない場合の、Azure Information Protection クライアントの操作モード。 このモードでは、分類ラベルが表示されませんが、ユーザーは Rights Management 保護を適用することができます。|
|スーパー ユーザー|高度に信頼されている管理者グループ。権限管理サービスを使用して組織が保護しているファイルの暗号化を解除し、そのファイルにアクセスできます。 通常、法的な電子情報開示や監査チームには、このレベルのアクセス許可が必要です。|
|テナント キー|サーバー ライセンサー証明書 (SLC) キーとも呼ばれます。<br /><br />組織に対して一意のキーであり、このテナント キーにチェーンされているすべての [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 暗号化機能を最終的に保護します。|
|保護の解除|ファイルや電子メール メッセージから、暗号化、ID、アクセス制御ポリシーを使用してデータを保護していた権限管理の制御を削除します。|
|ライセンスの使用|権限管理サービスで保護されているファイルや電子メール メッセージを開くユーザーに付与されるドキュメントごとの証明書です。 この証明書は、ファイルや電子メール メッセージに対するユーザーの権限のほか、コンテンツを暗号化する際に使用される暗号化キー、ドキュメントのポリシー内で別途定義されるアクセス制限を含んでいます。|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
