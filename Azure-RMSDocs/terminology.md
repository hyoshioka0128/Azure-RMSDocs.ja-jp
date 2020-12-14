---
title: Azure Information Protection の用語 (AIP)
description: Microsoft Azure Information Protection (AIP) に関連する単語、語句、または頭字語で混同されていますか。 この定義は、AIP に固有のものか、このサービスのコンテキストで使用されている場合に特定の意味を持つ用語と略語について検索します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 742877bf-26f5-40e3-b1f7-8475e7c3ce11
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: af5c035a19847eca18a9686cc32895c363c0a926
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384558"
---
# <a name="terminology-for-azure-information-protection"></a>Azure Information Protection の用語

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Microsoft Azure Information Protection に関連する単語、フレーズ、略語で混乱していませんか。 Azure Information Protection に固有の用語と略語、およびこのサービスのコンテキストで使用されるときに特定の意味を持つ用語と略語の定義については以下を参照してください。

## <a name="word-phrase-or-acronym"></a>単語、語句、または頭字語

[A](#a)  | [B](#b)  | [C](#c)  | [D](#d)  | [E](#e)  | [G](#g)  | [H](#h)  | [I](#i)  | [K](#k)  | [L](#l)  | [M](#m) [N](#n)  |  [O](#o)  |  [P](#p)  |  [R](#r)  |  [S](#s)  |  [T](#t)  |  [U](#u)

### <a name="a"></a>A
|項目|定義|
|--------|--------------|
|**AADRM**|保護サービス (Azure Rights Management) 用の最初の PowerShell モジュールの名前です。これは、以前に (Windows) Azure Active Directory Rights Management と呼ばれていた Azure Rights Management の非公式な略語から派生したものです。 </br></br>この PowerShell モジュールは、AIPService モジュールに置き換えられました。|
|**する**|組織がドキュメントと電子メールを保護できるように、Azure Rights Management protection service を有効にします。 </br></br>この操作により、Exchange Online と Microsoft SharePoint の IRM 機能も有効になります。|
|**Active Directory Rights Management サービス**|*AD RMS* という略称で呼ばれることもあります。<br /><br />Windows Server の役割の 1 つで、暗号化とポリシーを使用した権限管理保護により、ドキュメント、ファイル、および電子メールを保護することができます。|
|**AD RMS**|*Active Directory Rights Management サービス* をご覧ください。|
|**AIP** |「 *Azure Information Protection*」を参照してください。|
|**AIPService**|保護サービスの PowerShell モジュールの現在の名前。これは、古い AADRM モジュールに置き換えられます。|
|**AzureInformationProtection**|Azure Information Protection クラシックまたは統合されたラベル付けクライアントの PowerShell モジュールの名前。|
|**Azure Information Protection**|ラベルを使用してドキュメントと電子メールの分類と保護を行う、クラウドベースのサービスです。 </br></br> Azure Rights Management は、暗号化ポリシー、ID ポリシー、承認ポリシーを使用して、保護を提供します。|
|**クラシッククライアントを Azure Information Protection する**|*従来のクライアント* と省略されることもあります。<br /><br />Azure Information Protection の元のクライアント側では、ユーザー、管理者、およびサービスが Azure Information Protection ポリシーのラベルと設定を使用できるようにします。 </br></br> これで、Azure Information Protection 統合されたラベル付けクライアントに置き換えられるようになりました。|
|**Azure Information Protection のラベル**|この項目によってドキュメントや電子メールに分類値を常に適用し、それらを保護することもできます。 </br></br>ラベルが適用されると、ラベル情報はアプリケーションおよびサービスのメタデータに格納され、読み取ったり、必要に応じて操作したりできます。|
|**Azure Information Protection ポリシー**|Azure Information Protection のラベルとポリシーの設定を使用するクライアントとサービスに向けた、管理者が定義する構成です。|
|**Azure Information Protection スキャナー**|Windows Server 上で実行されるサービスで、ネットワーク共有、SharePoint サーバーサイト、およびライブラリのドキュメントを検出、分類、および保護できます。|
|**Azure Information Protection 統合ラベル付けクライアント**|統一された *ラベル付けクライアント* に省略されることがあります。<br /><br />ユーザー、管理者、およびサービスが使用できる Windows コンピューターのクライアントは、Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 セキュリティセンター、および Microsoft 365 コンプライアンスセンターの機密ラベルとラベルポリシー設定を使用します。 </br></br>Azure Information Protection クラシッククライアントを置き換えます。|
|**Azure RMS**|*Azure Rights Management* をご覧ください。|
|**Azure Information Protection ビューアー**|保護されたファイルを表示するために、Windows コンピューターやモバイル デバイスで実行するアプリです。|
|**Azure Rights Management**|*Azure Rights Management サービス* とも呼ばれ、多くの場合、 *Azure RMS* として省略されます。<br /><br />Azure Information Protection で使用される Azure サービスであり、暗号化とポリシーを使用して、ドキュメント、ファイル、および電子メールを保護することができます。 </br></br>以前の名前には次のものがあります。<br /><br />- *Windows Azure Active Directory Rights Management*: Windows Azure AD Rights Management サービスという略称で呼ばれることもあります。<br /><br />- *RMS Online*: 元の推奨名です。エラー メッセージやログ ファイルのエントリで表示されることがあります。|
| | |

### <a name="b"></a>B

|項目|定義|
|--------|--------------|
|**独自のキーを使用する**|*BYOK* という略称で呼ばれることもあります。<br /><br />組織が Azure Information Protection の独自のテナント キーを生成および管理するときに選択する構成およびトポロジ オプションです。|
|**組み込みのラベル付け**|追加のラベル付けクライアントをインストールする必要なしに、機密ラベルをサポートする Microsoft 365 アプリまたはサービス機能。 *ネイティブラベル* 付けとも呼ばれます。|
|**BYOK**|「Bring Your Own Key」を参照してください。|
| | |

### <a name="c"></a>C

|項目|定義|
|--------|--------------|
|**可能性**|**保護のコンテキストのみ**: </br>コンテンツが Rights Management サービスで保護されているドキュメントや電子メールを、読み取りや使用のために開きます。 </br>ドキュメントの場合、使用処理には保護されたドキュメントの編集や、新しいコンテンツの追加が含まれます。 電子メール メッセージの場合、使用処理には保護されたメッセージへの返信が含まれます。<br /><br/>**ラベル付け (保護ありまたはなし) のコンテキストでは、** 次のようになります。 </br>ファイルおよび電子メールのメタデータに格納されているラベル情報を読み取ったり、場合によっては操作します。|
|**コンテンツキー**|Rights Management を使用して保護されている各ドキュメントまたは電子メールに対して RMS 対応アプリケーションが作成する一意のキーです。情報漏えいの危険性を減らすのに役立ちます。|
| | |

### <a name="d"></a>D

|項目|定義|
|--------|--------------|
|**非**|Rights Management サービスを無効化します。組織は Azure Information Protection を使用できなくなります。|
|**既定のテンプレート**|Azure Information Protection のサブスクリプションを取得すると自動的に作成される保護テンプレートです。これにより、機密情報が記載されたドキュメントや電子メールの保護をすぐに開始できます。|
|**部門別のテンプレート**|組織内のすべてのユーザーではなく選択したユーザーに対して表示されるように構成する、独自に作成する保護テンプレートです。 "*スコープ テンプレート*" とも呼ばれます。|
|**二重キーの暗号化** |" *Dke*" とも呼ばれ、2つのキーを使用するコンテンツをセキュリティで保護する方法です。1つは Azure で保持され、もう1つは custer によって保持されます。 </br></br>DKE は、AIP 統合クライアントでのみサポートされており、Microsoft 365 で構成されています。 |
| | |

### <a name="e"></a>E

|項目|定義|
|--------|--------------|
|**対応アプリケーション**|Rights Management をネイティブでサポートするアプリケーション。Word や Excel などの Office アプリケーションが含まれます。 </br></br>独立系ソフトウェア ベンダー (ISV) や開発者も、Rights Management をネイティブでサポートするアプリケーションを作成できます。|
|**エンタープライズ権限管理**|業界標準の一般的な用語です。暗号化ツールとポリシー承認ツールを組み合わせて組織の機密情報や重要情報を保護する製品やソリューションを説明する際によく使用されます。 </br></br>Azure Information Protection は、エンタープライズ権限管理 (ERM) ソリューションの一例です。|
|**ERM**|「エンタープライズ権限管理」を参照してください。|
| | |

### <a name="g"></a>G

|項目|定義|
|--------|--------------|
|**一般的な保護**|任意のファイルの種類を暗号化し、承認されていないユーザーがそのファイルを開けないようにする保護レベル。 </br></br>ファイルを開いた後は暗号化が解除され、Rights Management をネイティブでサポートしていないアプリケーションで使用できます。|
| | |

### <a name="h"></a>H

|項目|定義|
|--------|--------------|
|**独自のキーを保持する**|*HYOK* という略称で呼ばれることもあります。<br /><br />通常は規制やコンプライアンス上の理由から、キーをオンプレミスで生成および保存する組織の構成およびトポロジ オプション。 </br></br>HYOK は、AIP classic クライアントでのみサポートされています。|
|**HYOK**|「*Hold Your Own Key*」を参照してください。|
| | |

### <a name="i"></a>I

|項目|定義|
|--------|--------------|
|**情報の保護**|*IP* という略称で呼ばれることもあります。<br /><br />業界標準の一般的な用語です。データやファイルを未承認のアクセスから保護することを指します。これらのデータやファイルは、電子メールやドキュメント共有によって組織の外部に移動しても引き続き保護されます。 </br></br>Microsoft Azure Information Protection は、情報保護 (IP) ソリューションの一例です。|
|**情報 Rights Management**|*IRM* という略称で呼ばれることもあります。<br /><br />Microsoft Rights Management サービスをサポートする機能を説明するために、Exchange Server、Word、SharePoint などの Office サービスと共に使用される用語。|
|**IRM**|*Information Rights Management* をご覧ください。|
| | |


### <a name="k"></a>K

|項目|定義|
|--------|--------------|
|**key オブジェクト**|テナント キーのコンテキストにおいて、暗号化操作のために Azure Rights Management サービスが必要とするメタデータを含むエンティティ。|
| | |

### <a name="l"></a>L

|項目|定義|
|--------|--------------|
|**label**|「*Azure Information Protection のラベル*」をご覧ください。|
| | |

### <a name="m"></a>M

|項目|定義|
|--------|--------------|
|**Microsoft Information Protection**| *MIP* と略記されることもあります。<br /><br /> 同じラベル付けストア ("統一されたラベル") を使用し、組織の機密情報を保護するための製品および統合機能のフレームワーク。|
|**MIP**| *Microsoft Information Protection* を参照|
|**MSDRM**|RMS クライアント 1.0 を指す用語として使用されることがあります。新しいクライアントでは、MSIPC という名前に置き換えられています。 </br></br>この古いクライアントでは、RMS SDK 1.0 を使用して開発されたアプリケーションと、Office 2010 および Office 2007、Exchange 2010 および Exchange 2013、SharePoint 2010 および SharePoint 2007 をサポートしています。|
|**MSIPC**|RMS クライアント 2.0 を指す用語として使用されることがあります。古い RMS クライアントの MSDRM を置き換えるものです。 </br></br>この新しいクライアントでは、RMS SDK 2.0 を使用して開発されたアプリケーションと、Office 365 ProPlus、Office 2019、Office 2016、Office 2013、SharePoint 2013、および Azure Information Protection クライアントをサポートしています。|
| | |

### <a name="n"></a>×

|項目|定義|
|--------|--------------|
|**ネイティブ保護**|すべての対応アプリケーションで使用できる保護レベル。承認されていないユーザーがファイルを開けないようにするだけでなく、読み取り専用や印刷不可など、より厳格なポリシーを適用できます。 </br></br>また、ファイルが他のユーザーに転送されたり、他のユーザーがアクセスできる公開された場所に保存された場合でも、ファイルに対する保護は維持されます。|
| | |

### <a name="o"></a>O

|項目|定義|
|--------|--------------|
|**Office Message Encryption**|*OME* という略称で呼ばれることもあります。<br /><br />新しい Office 365 メッセージ暗号化機能には、Azure Rights Management サービスとの統合が組み込まれています。これにより、内部および外部ユーザーに同じ電子メール保護を提供し、テンプレートを自動更新し、独自のキー (BYOK) シナリオのサポートを提供します。 </br></br>以前の OME 実装は外部の受信者のみのために設計されており、メール フロー ルールが必要で、BYOK をサポートしていませんでした。|
| | |

### <a name="p"></a>P

|項目|定義|
|--------|--------------|
|**. pfile**|権限管理サービスが一般的に保護するすべてのファイルに付けられるファイル名拡張子。|
|**アクセス許可レベル**|エンドユーザーと管理者が、役割ベースの構成オプションを選択しやすくするための使用権限の論理的なグループ化。 たとえば、レビュー担当者や共同作成者などがあります。|
|**防止**|ファイルや電子メール メッセージに権限管理の制御を適用し、暗号化、ID、アクセス制御ポリシーを使用してデータを保護します。|
|**保護のみモード**|ラベルを適用する Azure Information Protection ポリシーがない場合の、Azure Information Protection クライアントの操作モード。 </br></br>このモードでは、分類ラベルが表示されませんが、ユーザーは Rights Management 保護を適用することができます。|
|**保護テンプレート**|"*権利ポリシー テンプレート*"、"*Rights Management テンプレート*"、"*RMS テンプレート*" とも呼ばれます。<br /><br />管理者によって管理される保護設定のグループです。承認されたユーザー向けに定義された使用権限と、有効期限やオフライン アクセスのアクセス制御が含まれます。 |
|**投稿**|未承認のアクセスおよび使用を防ぐためにファイルを保護する操作。 </br></br>保護テンプレートや Azure Information Protection ポリシーと共に用語として使用することで、クライアントやサービスがこれらの項目を使用できるようにすることもできます。|
| | |

### <a name="r"></a>R

|項目|定義|
|--------|--------------|
|**Rights Management コネクタ**|Exchange Server や SharePoint などのオンプレミス サービスで Azure Rights Management サービスを使用してデータを保護するためにデプロイできる送信プロキシ リレー。|
|**Rights Management 発行者**|ドキュメントまたは電子メールを保護したアカウントです。|
|**Rights Management 所有者**|自動的に付与される Rights Management フル コントロール使用権限によって、保護されたドキュメントまたは電子メールのフル コントロールを保持し、いかなる有効期限日またはオフライン設定からも除外されているアカウントです。|
|**Rights Management サービス**|クラウド バージョンの Rights Management (Azure Rights Management) とオンプレミス バージョンの Rights Management (AD RMS) の両方に適用される一般的な用語。|
|**Rights Management 共有アプリケーション**|Azure Information Protection クライアントに置き換えられました。|
|**RMS**|*Rights Management サービス* をご覧ください。|
|**RMS コネクタ**|「Rights Management コネクタ」を参照してください。|
|**個人向け RMS**|ユーザーの組織が Office 365 または Azure Active Directory のサブスクリプションを保有していない場合にユーザーが Rights Management を使用するための無料のサブスクリプション。|
|**RMS 共有アプリ**|「Rights Management 共有アプリケーション」を参照してください。|
|**RMS テンプレート**|「*保護テンプレート*」をご覧ください。|

### <a name="s"></a>S

|項目|定義|
|--------|--------------|
|**スキャナー**|「*Azure Information Protection スキャナー*」をご覧ください。|
|**スーパーユーザー**|高度に信頼されている管理者グループ。権限管理サービスを使用して組織が保護しているファイルの暗号化を解除し、そのファイルにアクセスできます。 </br></br>通常、法的な電子情報開示や監査チームには、このレベルのアクセス許可が必要です。|

### <a name="t"></a>T

|項目|定義|
|--------|--------------|
|**テナントキー**|*サーバーライセンサー証明書 (SLC) キー* とも呼ばれます。<br /><br />組織に対して一意のキーであり、このテナント キーにチェーンされているすべての Rights Management 暗号化機能を最終的に保護します。|

### <a name="u"></a>U

|項目|定義|
|--------|--------------|
|**統一されたラベル**| " *統合秘密度" ラベル* とも呼ばれます。<br /><br /> Microsoft Information Protection framework をサポートするアプリ、クライアント、およびサービスによって適用できるラベル。分類および必要に応じて保護を適用します。 </br></br>Office アプリとサービスでは、統合ラベルは機密ラベルとして実装されます。|
|**保護の解除**|暗号化、ID、使用権限、アクセス制御ポリシーを使用してデータを保護していた保護制御を、ファイルや電子メール メッセージから削除します。|
|**ライセンスの使用**|権限管理サービスで保護されているファイルや電子メール メッセージを開くユーザーに付与されるドキュメントごとの証明書です。 </br></br>この証明書は、ファイルや電子メール メッセージに対するユーザーの権限のほか、コンテンツを暗号化する際に使用される暗号化キー、ドキュメントのポリシー内で別途定義されるアクセス制限を含んでいます。|

## <a name="next-steps"></a>次のステップ

AIP 名の詳細については、「 [Azure Information Protection](aka.md)」を参照してください。