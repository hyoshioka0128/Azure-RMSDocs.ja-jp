---
title: Azure Information Protection の用語
description: Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/04/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 01c2e8d4dd476e0910a75fd5949362225743f322
ms.sourcegitcommit: 4cd90fcf94ac6e2543d8be10e6e29e8218d5fd9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49651961"
---
# <a name="terminology-for-azure-information-protection"></a>Azure Information Protection の用語

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。

|用語|定義|
|--------|--------------|
|AADRM|Azure Rights Management サービス用の PowerShell モジュールの名前です。これは、以前に (Windows) Azure Active Directory Rights Management という名前だったときに、Azure Rights Management の非公式な略語から派生したものです。|
|アクティブ化|Azure Rights Management サービスを有効化して、組織がドキュメントや電子メールを保護できるようにします。 この操作により、Exchange Online と SharePoint Online での IRM 機能も有効になります。|
|Active Directory Rights Management サービス|*AD RMS*という略称で呼ばれることもあります。<br /><br />Windows Server の役割の 1 つで、暗号化とポリシーを使用した権限管理保護により、ドキュメント、ファイル、および電子メールを保護することができます。|
|AD RMS|*Active Directory Rights Management サービス*をご覧ください。|
AzureInformationProtection|Azure Information Protection クライアント用の PowerShell モジュールの名前です。
|Azure Information Protection|ラベルを使用してドキュメントと電子メールの分類と保護を行う、クラウドベースのサービスです。 Azure Rights Management は、暗号化ポリシー、ID ポリシー、承認ポリシーを使用して、保護を提供します。|
Azure Information Protection クライアント|ユーザー、管理者、サービスがラベルと Azure Information Protection ポリシーの設定を使用できるようにする、クライアント側での Azure Information Protection です。|
|Azure Information Protection のラベル|この項目によってドキュメントや電子メールに分類値を適用し、必要に応じてそれらを保護することができます。|
|Azure Information Protection ポリシー|Azure Information Protection のラベルとポリシーの設定を使用するクライアントとサービスに向けた、管理者が定義する構成です。|
|Azure Information Protection スキャナー|Windows Server 上で実行するサービスです。これにより、ローカル フォルダー、ネットワーク共有、SharePoint Server のサイトとライブラリにあるドキュメントの検出、分類、保護を行うことができます。|
|Azure Information Protection ビューアー|保護されたファイルを表示するために、Windows コンピューターやモバイル デバイスで実行するアプリです。|
|Azure Rights Management|*Azure RMS*という略称で呼ばれることもあります。<br /><br />Azure Information Protection で使用される Azure サービスであり、暗号化とポリシーを使用して、ドキュメント、ファイル、および電子メールを保護することができます。  *Azure Rights Management サービス*とも呼ばれます。 以前の名前には次のものがあります。<br /><br />- *Windows Azure Active Directory Rights Management*: Windows Azure AD Rights Management サービスという略称で呼ばれることもあります。<br /><br />- *RMS Online*: 元の推奨名です。エラー メッセージやログ ファイルのエントリで表示されることがあります。|
|Azure RMS|*Azure Rights Management*をご覧ください。|
|既定のテンプレート|Azure Information Protection のサブスクリプションを取得すると自動的に作成される保護テンプレートです。これにより、機密情報が記載されたドキュメントや電子メールの保護をすぐに開始できます。|
|BYOK|*Bring Your Own Key*をご覧ください。|
|Bring Your Own Key|*BYOK*という略称で呼ばれることもあります。<br /><br />組織が Azure Information Protection の独自のテナント キーを生成および管理するときに選択する構成およびトポロジ オプションです。|
|コンテンツ キー|Rights Management を使用して保護されている各ドキュメントまたは電子メールに対して RMS 対応アプリケーションが作成する一意のキーです。情報漏えいの危険性を減らすのに役立ちます。|
|使用処理|コンテンツが Rights Management で保護されているドキュメントや電子メールを、読み取りや使用のために開く操作。 ドキュメントの場合、使用処理には保護されたドキュメントの編集や、新しいコンテンツの追加が含まれます。 電子メール メッセージの場合、使用処理には保護されたメッセージへの返信が含まれます。|
|非アクティブ化|Rights Management サービスを無効化します。組織は Azure Information Protection を使用できなくなります。|
|部門別のテンプレート|組織内のすべてのユーザーではなく選択したユーザーに対して表示されるように構成する、独自に作成する保護テンプレートです。 "*スコープ テンプレート*" とも呼ばれます。|
|対応アプリケーション|Rights Management をネイティブでサポートするアプリケーション。Word や Excel などの Office アプリケーションが含まれます。 独立系ソフトウェア ベンダー (ISV) や開発者も、Rights Management をネイティブでサポートするアプリケーションを作成できます。|
|エンタープライズ権限管理|業界標準の一般的な用語です。暗号化ツールとポリシー承認ツールを組み合わせて組織の機密情報や重要情報を保護する製品やソリューションを説明する際によく使用されます。 Azure Information Protection は、エンタープライズ権限管理 (ERM) ソリューションの一例です。|
|ERM|*エンタープライズ権限管理*をご覧ください。|
|一般保護|任意のファイルの種類を暗号化し、承認されていないユーザーがそのファイルを開けないようにする保護レベル。 ファイルを開いた後は暗号化が解除され、Rights Management をネイティブでサポートしていないアプリケーションで使用できます。|
|HYOK|「*Hold Your Own Key*」を参照してください。|
|Hold Your Own Key|*HYOK* という略称で呼ばれることもあります。<br /><br />通常は規制やコンプライアンス上の理由から、キーをオンプレミスで生成および保存する組織の構成およびトポロジ オプション。|
|キー オブジェクト|テナント キーのコンテキストにおいて、暗号化操作のために Azure Rights Management サービスが必要とするメタデータを含むエンティティ。|
|label|「*Azure Information Protection のラベル*」をご覧ください。|
|情報保護|*IP*という略称で呼ばれることもあります。<br /><br />業界標準の一般的な用語です。データやファイルを未承認のアクセスから保護することを指します。これらのデータやファイルは、電子メールやドキュメント共有によって組織の外部に移動しても引き続き保護されます。 Microsoft Azure Information Protection は、情報保護 (IP) ソリューションの一例です。|
|Information Rights Management|*IRM*という略称で呼ばれることもあります。<br /><br />Exchange Server、Word、および SharePoint Online などの Office サービスと共に使用される用語で、Microsoft Rights Management サービスをサポートする機能を説明します。|
|IRM|*Information Rights Management*をご覧ください。|
|Office Message Encryption|*OME* という略称で呼ばれることもあります。<br /><br />新しい Office 365 Message Encryption 機能には、内部と外部のユーザーに対する同じ電子メール保護、テンプレートの自動更新、Bring Your Own Key (BYOK) シナリオのサポートを提供する Azure Rights Management サービスとのネイティブな統合が含まれています。 以前の OME 実装は外部の受信者のみのために設計されており、メール フロー ルールが必要で、BYOK をサポートしていませんでした。|
|MSDRM|RMS クライアント 1.0 を指す用語として使用されることがあります。新しいクライアントでは、MSIPC という名前に置き換えられています。 この古いクライアントでは、RMS SDK 1.0 を使用して開発されたアプリケーションと、Office 2010 および Office 2007、Exchange 2010 および Exchange 2013、SharePoint 2010 および SharePoint 2007 をサポートしています。|
|MSIPC|RMS クライアント 2.0 を指す用語として使用されることがあります。古い RMS クライアントの MSDRM を置き換えるものです。 この新しいクライアントでは、RMS SDK 2.0 を使用して開発されたアプリケーションと、Office 2016 と Office 2013、SharePoint 2013、RMS 共有アプリケーション、および Azure Information Protection クライアントをサポートしています。|
|ネイティブ保護|すべての対応アプリケーションで使用できる保護レベル。承認されていないユーザーがファイルを開けないようにするだけでなく、読み取り専用や印刷不可など、より厳格なポリシーを適用できます。 また、ファイルが他のユーザーに転送されたり、他のユーザーがアクセスできる公開された場所に保存された場合でも、ファイルに対する保護は維持されます。|
|.pfile|権限管理サービスが一般的に保護するすべてのファイルに付けられるファイル名拡張子。|
|アクセス許可レベル|エンドユーザーと管理者が、役割ベースの構成オプションを選択しやすくするための使用権限の論理的なグループ化。 たとえば、レビュー担当者や共同作成者などがあります。|
|保護|ファイルや電子メール メッセージに権限管理の制御を適用し、暗号化、ID、アクセス制御ポリシーを使用してデータを保護します。|
|保護テンプレート|"*権利ポリシー テンプレート*"、"*Rights Management テンプレート*"、"*RMS テンプレート*" とも呼ばれます。<br /><br />管理者によって管理される保護設定のグループです。承認されたユーザー向けに定義された使用権限と、有効期限やオフライン アクセスのアクセス制御が含まれます。 |
|publish|未承認のアクセスおよび使用を防ぐためにファイルを保護する操作。 保護テンプレートや Azure Information Protection ポリシーと共に用語として使用することで、クライアントやサービスがこれらの項目を使用できるようにすることもできます。|
|Rights Management コネクタ|Exchange Server や SharePoint などのオンプレミス サービスで Azure Rights Management サービスを使用してデータを保護するためにデプロイできる送信プロキシ リレー。|
|Rights Management 発行者|ドキュメントまたは電子メールを保護したアカウントです。|
|Rights Management 所有者|自動的に付与される Rights Management フル コントロール使用権限によって、保護されたドキュメントまたは電子メールのフル コントロールを保持し、いかなる有効期限日またはオフライン設定からも除外されているアカウントです。|
|Rights Management サービス|クラウド バージョンの Rights Management (Azure Rights Management) とオンプレミス バージョンの Rights Management (AD RMS) の両方に適用される一般的な用語。|
|Rights Management 共有アプリケーション|現在は、Azure Information Protection クライアント (インプレース ファイルや電子メールで送信されたファイルを安全に共有できる、Windows やモバイル デバイス向けのオプションのアプリケーション) で置き換えられています。|
|RMS|*Rights Management サービス*をご覧ください。|
|RMS コネクタ|*Rights Management コネクタ*をご覧ください。|
|個人用 RMS|ユーザーの組織が Office 365 または Azure Active Directory のサブスクリプションを保有していない場合にユーザーが Rights Management を使用するための無料のサブスクリプション。|
|RMS 共有アプリ|*Rights Management 共有アプリケーション*をご覧ください。|
|RMS テンプレート|「*保護テンプレート*」をご覧ください。|
|保護のみモード|ラベルを適用する Azure Information Protection ポリシーがない場合の、Azure Information Protection クライアントの操作モード。 このモードでは、分類ラベルが表示されませんが、ユーザーは Rights Management 保護を適用することができます。|
|スキャナー|「*Azure Information Protection スキャナー*」をご覧ください。|
|スーパー ユーザー|高度に信頼されている管理者グループ。権限管理サービスを使用して組織が保護しているファイルの暗号化を解除し、そのファイルにアクセスできます。 通常、法的な電子情報開示や監査チームには、このレベルのアクセス許可が必要です。|
|テナント キー|サーバー ライセンサー証明書 (SLC) キーとも呼ばれます。<br /><br />組織に対して一意のキーであり、このテナント キーにチェーンされているすべての Rights Management 暗号化機能を最終的に保護します。|
|保護の解除|暗号化、ID、使用権限、アクセス制御ポリシーを使用してデータを保護していた保護制御を、ファイルや電子メール メッセージから削除します。|
|ライセンスの使用|権限管理サービスで保護されているファイルや電子メール メッセージを開くユーザーに付与されるドキュメントごとの証明書です。 この証明書は、ファイルや電子メール メッセージに対するユーザーの権限のほか、コンテンツを暗号化する際に使用される暗号化キー、ドキュメントのポリシー内で別途定義されるアクセス制限を含んでいます。|

