---
title: Azure Information Protection の用語
description: Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: ebea973acb5a45949d140e6bfcf8333b9da4add1
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136884"
---
# <a name="terminology-for-azure-information-protection"></a>Azure Information Protection の用語

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。

## <a name="word-phrase-or-acronym"></a>単語、語句、または頭字語

|用語|定義|
|--------|--------------|
|AADRM|保護サービス (Azure Rights Management) 用の最初の PowerShell モジュールの名前です。これは、以前に (Windows) Azure Active Directory Rights Management と呼ばれていた Azure Rights Management の非公式な略語から派生したものです。 この PowerShell モジュールは、AIPService モジュールに置き換えられました。|
|アクティブ化|組織がドキュメントと電子メールを保護できるように保護サービス (Azure Rights Management) を有効にする。 この操作により、Exchange Online と Microsoft SharePoint の IRM 機能も有効になります。|
|Active Directory Rights Management サービス|多くの場合、**「AD RMS」という略称で呼ばれます。<br /><br />Windows Server の役割の 1 つで、暗号化とポリシーを使用した権限管理保護により、ドキュメント、ファイル、および電子メールを保護することができます。|
|AD RMS|*Active Directory Rights Management サービス*をご覧ください。|
|AIPService|保護サービスの PowerShell モジュールの現在の名前。これは、古い AADRM モジュールに置き換えられます。|
AzureInformationProtection|Azure Information Protection クライアント (クラシック) 用の PowerShell モジュールの名前と、Azure Information Protection 統合されたラベル付けクライアントの名前。
|Azure Information Protection|ラベルを使用してドキュメントと電子メールの分類と保護を行う、クラウドベースのサービスです。 Azure Rights Management は、暗号化ポリシー、ID ポリシー、承認ポリシーを使用して、保護を提供します。|
Azure Information Protection クライアント (クラシック)|*従来のクライアント*と省略されることもあります。<br /><br />Azure Information Protection の元のクライアント側では、ユーザー、管理者、およびサービスが Azure Information Protection ポリシーのラベルと設定を使用できるようにします。 これで、Azure Information Protection 統合されたラベル付けクライアントに置き換えられるようになりました。|
|Azure Information Protection のラベル|この項目によってドキュメントや電子メールに分類値を常に適用し、それらを保護することもできます。 ラベルが適用されると、ラベル情報はアプリケーションおよびサービスのメタデータに格納され、読み取ったり、必要に応じて操作したりできます。|
|Azure Information Protection ポリシー|Azure Information Protection のラベルとポリシーの設定を使用するクライアントとサービスに向けた、管理者が定義する構成です。|
|Azure Information Protection スキャナー|Windows Server 上で実行されるサービスで、ネットワーク共有、SharePoint サーバーサイト、およびライブラリのドキュメントを検出、分類、および保護できます。|
|Azure Information Protection 統合ラベル付けクライアント|統一された*ラベル付けクライアント*に省略されることがあります。<br /><br />ユーザー、管理者、およびサービスが使用できる Windows コンピューターのクライアントは、Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 セキュリティセンター、および Microsoft 365 コンプライアンスセンターの機密ラベルとラベルポリシー設定を使用します。 Azure Information Protection クライアント (クラシック) を置き換えます。|
|Azure RMS|**「Azure Rights Management」を参照してください。|
|Azure Information Protection ビューアー|保護されたファイルを表示するために、Windows コンピューターやモバイル デバイスで実行するアプリです。|
|Azure Rights Management|*Azure RMS* という略称で呼ばれることもあります。<br /><br />Azure Information Protection で使用される Azure サービスであり、暗号化とポリシーを使用して、ドキュメント、ファイル、および電子メールを保護することができます。  *Azure Rights Management サービス*とも呼ばれます。 以前の名前には次のものがあります。<br /><br />- *Windows Azure Active Directory Rights Management*: Windows Azure AD Rights Management サービスという略称で呼ばれることもあります。<br /><br />- *RMS Online*: 元の推奨名です。エラー メッセージやログ ファイルのエントリで表示されることがあります。|
|既定のテンプレート|Azure Information Protection のサブスクリプションを取得すると自動的に作成される保護テンプレートです。これにより、機密情報が記載されたドキュメントや電子メールの保護をすぐに開始できます。|
|BYOK|**「Bring Your Own Key」を参照してください。|
|Bring Your Own Key|*BYOK* という略称で呼ばれることもあります。<br /><br />組織が Azure Information Protection の独自のテナント キーを生成および管理するときに選択する構成およびトポロジ オプションです。|
|組み込みのラベル付け|Office 365 アプリまたはサービス機能で、ラベル付けクライアントをインストールしなくても、機密ラベルをサポートすることができます。 *ネイティブラベル*付けとも呼ばれます。|
|コンテンツ キー (content key)|Rights Management を使用して保護されている各ドキュメントまたは電子メールに対して RMS 対応アプリケーションが作成する一意のキーです。情報漏えいの危険性を減らすのに役立ちます。|
|使用処理|保護のみのコンテキスト: ドキュメントまたは電子メールを開いて、そのコンテンツが rights management サービスによって保護されている場合にその内容を読み取りまたは使用します。 ドキュメントの場合、使用処理には保護されたドキュメントの編集や、新しいコンテンツの追加が含まれます。 電子メール メッセージの場合、使用処理には保護されたメッセージへの返信が含まれます。<br /><br />ラベル付け (保護ありまたはなし) のコンテキスト: ファイルと電子メールのメタデータに格納されているラベル情報を読み取って操作すること。|
|非アクティブ化|Rights Management サービスを無効化します。組織は Azure Information Protection を使用できなくなります。|
|部門別のテンプレート|組織内のすべてのユーザーではなく選択したユーザーに対して表示されるように構成する、独自に作成する保護テンプレートです。 "*スコープ テンプレート*" とも呼ばれます。|
|対応アプリケーション|Rights Management をネイティブでサポートするアプリケーション。Word や Excel などの Office アプリケーションが含まれます。 独立系ソフトウェア ベンダー (ISV) や開発者も、Rights Management をネイティブでサポートするアプリケーションを作成できます。|
|エンタープライズ権限管理|業界標準の一般的な用語です。暗号化ツールとポリシー承認ツールを組み合わせて組織の機密情報や重要情報を保護する製品やソリューションを説明する際によく使用されます。 Azure Information Protection は、エンタープライズ権限管理 (ERM) ソリューションの一例です。|
|ERM|**「エンタープライズ権限管理」を参照してください。|
|一般保護|任意のファイルの種類を暗号化し、承認されていないユーザーがそのファイルを開けないようにする保護レベル。 ファイルを開いた後は暗号化が解除され、Rights Management をネイティブでサポートしていないアプリケーションで使用できます。|
|HYOK|「*Hold Your Own Key*」を参照してください。|
|Hold Your Own Key|*HYOK* という略称で呼ばれることもあります。<br /><br />通常は規制やコンプライアンス上の理由から、キーをオンプレミスで生成および保存する組織の構成およびトポロジ オプション。|
|キー オブジェクト|テナント キーのコンテキストにおいて、暗号化操作のために Azure Rights Management サービスが必要とするメタデータを含むエンティティ。|
|label|「*Azure Information Protection のラベル*」をご覧ください。|
|情報保護|*IP* という略称で呼ばれることもあります。<br /><br />業界標準の一般的な用語です。データやファイルを未承認のアクセスから保護することを指します。これらのデータやファイルは、電子メールやドキュメント共有によって組織の外部に移動しても引き続き保護されます。 Microsoft Azure Information Protection は、情報保護 (IP) ソリューションの一例です。|
|Information Rights Management|*IRM* という略称で呼ばれることもあります。<br /><br />Microsoft Rights Management サービスをサポートする機能を説明するために、Exchange Server、Word、SharePoint などの Office サービスと共に使用される用語。|
|IRM|*Information Rights Management* をご覧ください。|
|Office Message Encryption|*OME* という略称で呼ばれることもあります。<br /><br />新しい Office 365 Message Encryption 機能には、内部と外部のユーザーに対する同じ電子メール保護、テンプレートの自動更新、Bring Your Own Key (BYOK) シナリオのサポートを提供する Azure Rights Management サービスとのネイティブな統合が含まれています。 以前の OME 実装は外部の受信者のみのために設計されており、メール フロー ルールが必要で、BYOK をサポートしていませんでした。|
|Microsoft Information Protection| *MIP*と略記されることもあります。<br /><br /> 同じラベル付けストア ("統一されたラベル") を使用し、組織の機密情報を保護するための製品および統合機能のフレームワーク。|
|MIP| *Microsoft Information Protection*を参照|
|MSDRM|RMS クライアント 1.0 を指す用語として使用されることがあります。新しいクライアントでは、MSIPC という名前に置き換えられています。 この古いクライアントでは、RMS SDK 1.0 を使用して開発されたアプリケーションと、Office 2010 および Office 2007、Exchange 2010 および Exchange 2013、SharePoint 2010 および SharePoint 2007 をサポートしています。|
|MSIPC を右クリックし|RMS クライアント 2.0 を指す用語として使用されることがあります。古い RMS クライアントの MSDRM を置き換えるものです。 この新しいクライアントでは、RMS SDK 2.0 を使用して開発されたアプリケーションと、Office 365 ProPlus、Office 2019、Office 2016、Office 2013、SharePoint 2013、および Azure Information Protection クライアントをサポートしています。|
|ネイティブ保護|すべての対応アプリケーションで使用できる保護レベル。承認されていないユーザーがファイルを開けないようにするだけでなく、読み取り専用や印刷不可など、より厳格なポリシーを適用できます。 また、ファイルが他のユーザーに転送されたり、他のユーザーがアクセスできる公開された場所に保存された場合でも、ファイルに対する保護は維持されます。|
|.pfile|権限管理サービスが一般的に保護するすべてのファイルに付けられるファイル名拡張子。|
|アクセス許可レベル|エンドユーザーと管理者が、役割ベースの構成オプションを選択しやすくするための使用権限の論理的なグループ化。 たとえば、レビュー担当者や共同作成者などがあります。|
|保護|ファイルや電子メール メッセージに権限管理の制御を適用し、暗号化、ID、アクセス制御ポリシーを使用してデータを保護します。|
|保護テンプレート|"*権利ポリシー テンプレート*"、"*Rights Management テンプレート*"、"*RMS テンプレート*" とも呼ばれます。<br /><br />管理者によって管理される保護設定のグループです。承認されたユーザー向けに定義された使用権限と、有効期限やオフライン アクセスのアクセス制御が含まれます。 |
|[発行]|未承認のアクセスおよび使用を防ぐためにファイルを保護する操作。 保護テンプレートや Azure Information Protection ポリシーと共に用語として使用することで、クライアントやサービスがこれらの項目を使用できるようにすることもできます。|
|Rights Management コネクタ|Exchange Server や SharePoint などのオンプレミス サービスで Azure Rights Management サービスを使用してデータを保護するためにデプロイできる送信プロキシ リレー。|
|Rights Management 発行者|ドキュメントまたは電子メールを保護したアカウントです。|
|Rights Management 所有者|自動的に付与される Rights Management フル コントロール使用権限によって、保護されたドキュメントまたは電子メールのフル コントロールを保持し、いかなる有効期限日またはオフライン設定からも除外されているアカウントです。|
|Rights Management サービス|クラウド バージョンの Rights Management (Azure Rights Management) とオンプレミス バージョンの Rights Management (AD RMS) の両方に適用される一般的な用語。|
|Rights Management 共有アプリケーション|Azure Information Protection クライアントに置き換えられました。|
|RMS|*Rights Management サービス*をご覧ください。|
|RMS コネクタ|**「Rights Management コネクタ」を参照してください。|
|個人向け RMS|ユーザーの組織が Office 365 または Azure Active Directory のサブスクリプションを保有していない場合にユーザーが Rights Management を使用するための無料のサブスクリプション。|
|RMS 共有アプリ|**「Rights Management 共有アプリケーション」を参照してください。|
|RMS テンプレート|「*保護テンプレート*」をご覧ください。|
|保護のみモード|ラベルを適用する Azure Information Protection ポリシーがない場合の、Azure Information Protection クライアントの操作モード。 このモードでは、分類ラベルが表示されませんが、ユーザーは Rights Management 保護を適用することができます。|
|スキャナー|「*Azure Information Protection スキャナー*」をご覧ください。|
|スーパー ユーザー|高度に信頼されている管理者グループ。権限管理サービスを使用して組織が保護しているファイルの暗号化を解除し、そのファイルにアクセスできます。 通常、法的な電子情報開示や監査チームには、このレベルのアクセス許可が必要です。|
|テナント キー|*サーバーライセンサー証明書 (SLC) キー*とも呼ばれます。<br /><br />組織に対して一意のキーであり、このテナント キーにチェーンされているすべての Rights Management 暗号化機能を最終的に保護します。|
|統一されたラベル| "*統合秘密度" ラベル*とも呼ばれます。<br /><br /> Microsoft Information Protection framework をサポートするアプリ、クライアント、およびサービスによって適用できるラベル。分類および必要に応じて保護を適用します。 Office アプリとサービスでは、統合ラベルは機密ラベルとして実装されます。|
|保護の解除|暗号化、ID、使用権限、アクセス制御ポリシーを使用してデータを保護していた保護制御を、ファイルや電子メール メッセージから削除します。|
|ライセンスの使用|権限管理サービスで保護されているファイルや電子メール メッセージを開くユーザーに付与されるドキュメントごとの証明書です。 この証明書は、ファイルや電子メール メッセージに対するユーザーの権限のほか、コンテンツを暗号化する際に使用される暗号化キー、ドキュメントのポリシー内で別途定義されるアクセス制限を含んでいます。|

