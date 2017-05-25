---
title: "Azure RMS の機能 - Azure Information Protection"
description: "Azure RMS の機能、Azure RMS で使用される暗号化制御、およびこのプロセスがどのように機能するかについてのステップ バイ ステップの図を詳細に説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/28/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3d53e57b8bff94c39426b37755c643c1dc9d9fde
ms.sourcegitcommit: dd5a63bfee309c8b68ee9f8cd071a574ab0f6b4a
ms.translationtype: HT
ms.contentlocale: ja-JP
---
# <a name="how-does-azure-rms-work-under-the-hood"></a>Azure RMS の機能の 詳細

>*適用対象: Azure Information Protection、Office 365*

Azure RMS の動作について理解しておく 1 つの重要な点は、Rights Management サービス (および Microsoft) は情報保護プロセスの一部としてユーザーのデータを見たり保存したりしないことです。 ユーザーが保護した情報は、ユーザーが Azure に明示的に保存したり、Azure に情報を保存する別のクラウド サービスを使用しない限り、Azure に送信されたり保存されたりすることはありません。 Azure RMS は、単純に、承認されたユーザーおよびサービス以外のものが文書のデータを読めないようにします。

- データは、アプリケーション レベルで暗号化されており、そのドキュメントの承認済みの使用を定義するポリシーが含まれています。

- 保護されたドキュメントが、正当なユーザーによって使用されるとき、または承認されたサービスによって処理される場合は、ドキュメント内のデータの暗号化が解除され、ポリシーで定義されている権利が適用されます。

大まかに言えば、次の図でこのプロセスのしくみを確認できます。 秘密の調合が含まれるドキュメントは保護されていて、権限を持つユーザーまたはサービスは正常に開くことができます。 ドキュメントは、コンテンツ キー (この図で緑のキー) によって保護されています。 コンテンツ キーはドキュメントごとに一意であり、Azure Information Protection テナント ルート キー (この図で赤色のキー) によって保護されているファイル ヘッダーに配置されます。 マイクロソフトがテナント キーを生成して管理することも、ユーザーが独自のテナント キーを生成して管理することもできます。

Azure RMS が暗号化および復号化、承認、制限の適用を行う保護プロセス全体を通じて、秘密の調合は Azure に送信されません。

![Azure RMS がファイルを保護する方法](../media/AzRMS_SecretColaFormula_final.png)

処理の詳細については、この記事の「[Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」セクションを参照してください。

Azure RMS が使用するアルゴリズムおよびキー長に関する技術的詳細については、次のセクションを参照してください。

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Azure RMS で使用される暗号化の制御:アルゴリズムとキーの長さ
自分で RMS がどのように機能するかを知る必要がなくても、セキュリティ保護が業界標準であることを確認するために、使用している暗号化制御に関してたずねられることがあります。


|暗号化コントロール|Azure RMS での使用|
|-|-|
|アルゴリズム:AES<br /><br />キーの長さ: 128 ビットと 256 ビット [[1]](#footnote-1)|ドキュメントの保護|
|アルゴリズム:RSA<br /><br />キーの長さ: 2048 ビット [[2]](#footnote-2)|キーの保護|
|SHA-256|証明書の署名|

###### <a name="footnote-1"></a>脚注 1: 

ファイルの拡張子が .ppdf のとき、またはファイルが保護されたテキスト ファイルまたはイメージ ファイル (.ptxt や .pjpg など) のときは、汎用的な保護およびネイティブ保護のために Azure Information Protection クライアントと Rights Management 共有アプリケーションは 256 ビットを使用します。

###### <a name="footnote-2"></a>脚注 2:

2048 ビットは、Azure Rights Management サービスがアクティブ化されているときのキーの長さです。 1024 ビットは、省略可能な次のシナリオでサポートされています。

- AD RMS クラスターが暗号化モード 1 で実行され、暗号化モード 2 にアップグレードできない場合の、オンプレミスからの移行中。

- 移行前にオンプレミスで作成された、アーカイブされたキー。これにより、AD RMS で保護されたコンテンツが、Azure Rights Management への移行後も開いた状態を続行できます。

- お客様が、Azure Key Vault を使用して独自キーの使用 (BYOK) を選択した場合。 最小キー サイズは 2048 ビットが推奨ですが、必須ではありません。

### <a name="how-the-azure-rms-cryptographic-keys-are-stored-and-secured"></a>Azure RMS 暗号化キーの格納とセキュリティ保護のしくみ

Azure RMS は、Azure RMS によって保護されているドキュメントまたは電子メールごとに、1 つの AES キー (コンテンツ キー) を作成します。このキーはドキュメントに埋め込まれ、ドキュメントの各エディションを通じて保持されます。 

コンテンツ キーは、組織の RSA キー (Azure Information Protection テナント キー) によってドキュメントのポリシーの一部として保護されます。このポリシーも、ドキュメントの作成者によって署名されます。 このテナント キーは、Azure Rights Management サービスによって組織のために保護されているすべてのドキュメントおよび電子メールで共通です。このキーは、ユーザー管理のテナント キー ("Bring Your Own Key" または BYOK と呼ばれます) を組織が使用している場合、Azure Information Protection 管理者にしか変更できません。 

このテナント キーは、Microsoft のオンライン サービスによって、高度に制御された環境で、厳しい監視の下に保護されています。 ユーザー管理のテナント キー (BYOK) を使用すると、各 Azure リージョンでハイエンド ハードウェア セキュリティ モジュール (HSM) のアレイが使用され、このセキュリティが強化されます。どのような状況でも、キーが抽出、エクスポート、または共有されることはありません。 テナント キーおよび BYOK の詳細については、「[Azure Information Protection テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。

Windows デバイスに送信されるライセンスと証明書は、クライアントのデバイス秘密キーによって保護されます。このキーは、デバイスのユーザーが初めて Azure RMS を使用したときに作成されます。 一方、この秘密キーは、クライアント上の DPAPI によって保護されます。DPAPI は、ユーザーのパスワードから派生したキーを使用して、これらのシークレットを保護します。 モバイル デバイスでは、キーは 1 回しか使われず、クライアントに格納されないため、これらのキーをデバイス上で保護する必要はありません。 


## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Azure RMS の動作のチュートリアル:初めての使用、コンテンツ保護、コンテンツ消費
Azure RMS の動作方法をさらに詳しく理解するため、[Azure Rights Management サービスがアクティブ化](../deploy-use/activate-service.md)された後、ユーザーが初めて Windows コンピューターで Rights Management サービスを使用し (**ユーザー環境の初期化**とも呼ばれます)、**コンテンツ (ドキュメントまたは電子メール) を保護**し、他のユーザーによって保護されているコンテンツを**消費する** (開いて使用する) ときの、一般的なフローを説明します。

ユーザー環境が初期化された後、ユーザーはそのコンピューターでドキュメントを保護したり、保護されているドキュメントを消費したりできます。

> [!NOTE]
> このユーザーが別の Windows コンピューターに移動する場合、または別のユーザーがこの同じ Windows コンピューターを使用する場合は、初期化プロセスが繰り返されます。

### <a name="initializing-the-user-environment"></a>ユーザー環境の初期化
ユーザーが Windows コンピューターでコンテンツを保護したり保護されているコンテンツを消費したりできるためには、その前にデバイスでユーザー環境を準備する必要があります。 これは 1 回限りのプロセスであり、ユーザーがコンテンツの保護または保護されたコンテンツの消費を行おうとしたときに、ユーザーの介入なしに自動的に行われます。

![RMS クライアントのアクティブ化フロー - 手順 1、クライアントの認証](../media/AzRMS.png)

**手順 1 の処理**: コンピューターの RMS クライアントは、最初に Azure Rights Management サービスに接続し、Azure Active Directory アカウントを使用してユーザーを認証します。

ユーザーのアカウントが Azure Active Directory と統合されている場合、この認証は自動的に行われ、ユーザーが資格情報の入力を求められることはありません。

![RMS クライアントのアクティブ化 - 手順 2、証明書がクライアントにダウンロードされる](../media/AzRMS_useractivation2.png)

**手順 2 の処理**: ユーザー認証の後、接続は組織の Azure Information Protection テナントに自動的にリダイレクトされます。このテナントは、保護されたコンテンツの消費およびコンテンツのオフライン保護のためにユーザーが Azure Rights Management サービスの認証を受けられるように証明書を発行します。

ユーザーの証明書のコピーは Azure に保存され、ユーザーが別のデバイスに移動した場合は、同じキーを使用して証明書が作成されます。

### <a name="content-protection"></a>コンテンツの保護
ユーザーがドキュメントを保護するとき、RMS クライアントは保護されていないドキュメントに対して次の操作を実行します。

![RMS ドキュメントの保護 - 手順 1、ドキュメントが暗号化される](../media/AzRMS_documentprotection1.png)

**手順 1 の処理**: RMS クライアントは、ランダムなキー (コンテンツ キー) を作成し、このキーを使用して、AES 対称暗号化アルゴリズムでドキュメントを暗号化します。

![RMS ドキュメントの保護 - 手順 2、ポリシーが作成される](../media/AzRMS_documentprotection2.png)

**手順 2 の処理**: RMS クライアントは次に、ユーザーまたはグループの[使用権限](../deploy-use/configure-usage-rights.md)や、その他の制限事項 (有効期限の日付など) が記載されたドキュメント用のポリシーを含む証明書を作成します。 コンテンツを保護する時点で、これらの設定は管理者が事前に構成または指定したテンプレート内に定義することができます ("アドホック ポリシー" とも呼ばれます)。   

選択したユーザーとグループの識別に使用するメイン Azure AD 属性は、Azure AD ProxyAddresses 属性です。この属性には、ユーザーまたはグループのすべての電子メール アドレスが格納されます。 ただし、AD ProxyAddresses 属性に値を持たないユーザー アカウントの場合は、このユーザーの UserPrincipalName 値が代わりに使用されます。

RMS クライアントは、ユーザー環境の初期化時に取得した組織のキーを使用して、ポリシーおよび対称コンテンツ キーを暗号化します。 また、RMS クライアントは、ユーザーの環境が初期化されたときに取得したユーザーの証明書でポリシーに署名します。

![RMS ドキュメントの保護 - 手順 3、ポリシーがドキュメントに埋め込まれる](../media/AzRMS_documentprotection3.png)

**手順 3 の処理**: 最後に、RMS クライアントは前に暗号化したドキュメントの本文と共にポリシーをファイルに埋め込みます。これらすべてが、保護されたドキュメントを構成します。

このドキュメントは、任意の場所に保存することも任意の方法を使用して共有することもでき、ポリシーは常に暗号化されたドキュメントと共にあります。

### <a name="content-consumption"></a>コンテンツの消費
ユーザーが保護されたドキュメントを消費しようとすると、RMS クライアントは最初に Azure Rights Management サービスにアクセスを要求します。

![RMS ドキュメントの消費 - 手順 1、ユーザーが認証され、権限のリストを取得する](../media/AzRMS_documentconsumption1.png)

**手順 1 の処理**: 認証されたユーザーは、ドキュメントのポリシーとユーザーの証明書を Azure Rights Management サービスに送信します。 サービスはポリシーを復号化して評価し、ユーザーがドキュメントに対して設定している権限のリストを作成します (ある場合)。 ユーザーを識別するには、ユーザーのアカウントと、そのユーザーがメンバーであるグループ用の Azure AD ProxyAddresses 属性を使用します。 パフォーマンス上の理由から、グループのメンバーシップは [キャッシュ](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management) されます。 ユーザー アカウントの Azure AD ProxyAddresses 属性に値がない場合は、Azure AD UserPrincipalName の値が代わりに使用されます。

![RMS ドキュメントの消費 - 手順 2、使用ライセンスがクライアントに返される](../media/AzRMS_documentconsumption2.png)

**手順 2 の処理**: その後、サービスは、復号化されたポリシーから AES コンテンツ キーを抽出します。 このキーは、要求で取得されたユーザーの公開 RSA キーで暗号化されます。

再暗号化されたコンテンツ キーは、ユーザー権利のリストと共に暗号化された使用ライセンスに埋め込まれて、RMS クライアントに返されます。

![RMS ドキュメントの消費 - 手順 3、ドキュメントが復号化され、権限が適用される](../media/AzRMS_documentconsumption3.png)

**手順 3 の処理**: 最後に、RMS クライアントは暗号化された使用ライセンスを取得し、独自のユーザー秘密キーで暗号化を解除します。 これにより、RMS クライアントは必要に応じてドキュメント本文の暗号化を解除し、画面に表示できます。

また、クライアントは権限のリストを復号化してアプリケーションに渡します。アプリケーションはユーザー インターフェイスにそれらの権限を適用します。

> [!NOTE]
> 組織の外部にいるユーザーが保護しているコンテンツを消費する場合でも、消費フローは同じです。 このシナリオでの変更点は、ユーザーの認証方法です。 詳細については、「[保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか。](../get-started/faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)」を参照してください。


### <a name="variations"></a>バリエーション
前のチュートリアルでは標準的なシナリオをカバーしましたが、いくつかのバリエーションがあります。

-   **モバイル デバイス**:モバイル デバイスが Azure Rights Management サービスでファイルを保護または消費するときのプロセス フローはとても簡単です。 モバイル デバイスでは、コンテンツを保護または消費するための各トランザクションは独立しているので、ユーザー初期化プロセスは行われません。 Windows コンピューターと同じように、モバイル デバイスは Azure Rights Management サービスに接続して認証します。 コンテンツを保護する場合、モバイル デバイスはポリシーを送信し、Azure Rights Management サービスは発行ライセンスとドキュメントを保護する対称キーをモバイル デバイスに送信します。 コンテンツを消費する場合、モバイル デバイスは、Azure Rights Management サービスに接続して認証するときに、ドキュメントのポリシーを Azure Rights Management サービスに送信し、ドキュメントを消費するための使用ライセンスを要求します。 応答として、Azure Rights Management サービスは必要なキーと制限をモバイル デバイスに送信します。 どちらのプロセスも、TLS を使用してキーの交換およびその他の通信を保護します。

-   **RMS コネクタ**:Azure Rights Management サービスを RMS コネクタで使用するときのプロセス フローは同じです。 唯一の違いは、コネクタがオンプレミス サービス (Exchange Server や SharePoint Server など) と Azure Rights Management サービスの間のリレーとして機能することです。 コネクタ自体は、ユーザー環境の初期化や暗号化または復号化などのいかなる操作も実行しません。 コネクタは、通常は AD RMS サーバーに送られる通信をリレーするだけであり、両側で使用されているプロトコルの変換を処理します。 このシナリオでは、Azure Rights Management サービスをオンプレミス サービスと併用できます。

-   **汎用的な保護 (.pfile)**:Azure Rights Management サービスがファイルを一般的に保護するときは、RMS クライアントがすべての権限を許可するポリシーを作成する点を除けば、フローは基本的にコンテンツ保護と同じです。 ファイルを消費するときは、対象のアプリケーションに渡される前に暗号化が解除されます。 このシナリオでは、RMS をネイティブにサポートしない場合であっても、すべてのファイルを保護できます。

-   **保護された PDF (.ppdf)**: Azure Rights Management サービスは、Office ファイルをネイティブに保護するときは、そのファイルのコピーも作成して同じ方法で保護します。 唯一の違いは、ファイルのコピーが PPDF ファイル形式であり、Azure Information Protection クライアント ビューアーと RMS 共有アプリケーションは表示するために開く方法だけを認識していることです。 このシナリオでは、保護された添付ファイルを電子メールで送信できます。モバイル デバイスの受信者は、モバイル デバイスに保護された Office ファイルをネイティブにサポートするアプリがない場合であっても、常にファイルを読むことができます。

## <a name="next-steps"></a>次のステップ

Azure Rights Management サービスの詳細については、**概要と詳細**のセクションの他の記事を使用してください。たとえば、既存のアプリケーションと Azure Rights Management を統合して情報保護ソリューションを提供する方法を確認するには、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」を参照してください。 

「[ Azure Information Protection の用語](../get-started/terminology.md)」を確認して、Azure Rights Management サービスの構成や使用で目にする用語を理解できるようにします。また、デプロイを開始する前に、「[Requirements for Azure Information Protection](../get-started/requirements-azure-rms.md)」 (Azure Information Protection の要件) も確認しておいてください。 すぐに自分で試してみる場合は、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」をご利用ください。

データ保護を組織にデプロイする準備ができたら、「[Azure Information Protection デプロイ ロードマップ](../plan-design/deployment-roadmap.md)」で、デプロイの手順と具体的な操作手順へのリンクを参照してください。

> [!TIP]
> 追加情報やサポートが必要な場合は、「[Azure Information Protection の情報とサポート](../get-started/information-support.md)」のリソースとリンクをご利用ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]