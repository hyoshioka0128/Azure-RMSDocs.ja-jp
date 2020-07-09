---
title: Azure RMS のしくみ - Azure Information Protection
description: Azure RMS の動作のしくみ、使われている暗号化の制御、およびこのプロセスが動作する詳細な手順の図を示します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9604ca61aff2d01d66e6f328b88ca264ab031785
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136649"
---
# <a name="how-does-azure-rms-work-under-the-hood"></a>Azure RMS が動作する しくみ

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure RMS の動作方法について理解しておく必要がある重要な点は、Azure Information Protection のこのデータ保護サービスでは、保護プロセスの一環としてユーザーのデータが見られたり保存されたりしないということです。 ユーザーが保護した情報は、ユーザーが Azure に明示的に保存したり、Azure に情報を保存する別のクラウド サービスを使用しない限り、Azure に送信されたり保存されたりすることはありません。 Azure RMS は単に、ドキュメント内のデータを、承認されたユーザーとサービスしか読み取ることができないようにするだけです。

- データは、アプリケーション レベルで暗号化されており、そのドキュメントの承認された使用を定義するポリシーを含みます。

- 保護されたドキュメントが正当なユーザーによって使われたり、承認されたサービスによって処理されたりすると、ドキュメント内のデータの暗号化が解除され、ポリシーで定義されている権利が適用されます。

次の図は、このプロセスの概要を示したものです。 秘密の調合を含むドキュメントが保護されており、承認されたユーザーまたはサービスによって正常に開かれます。 ドキュメントは、コンテンツ キー (この図では緑の鍵) によって保護されています。 コンテンツ キーはドキュメントごとに固有であり、Azure Information Protection のテナント ルート キー (図では赤の鍵) によって保護されてファイル ヘッダーに配置されています。 Microsoft がテナント キーを生成して管理することも、ユーザーが独自のテナント キーを生成して管理することもできます。

Azure RMS が暗号化および復号化、承認、制限の適用を行う保護プロセス全体を通じて、秘密の調合は Azure に送信されません。

![Azure RMS がファイルを保護する方法](./media/AzRMS_SecretColaFormula_final.png)

処理については、この記事の「[Azure RMS の動作のチュートリアル: 初めての使用、コンテンツ保護、コンテンツ消費](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption)」を参照してください。

Azure RMS が使うアルゴリズムとキー長に関する技術的な詳細は、次のセクションをご覧ください。

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Azure RMS で使用される暗号化制御: アルゴリズムとキーの長さ
この技術のしくみを詳しく知る必要がない場合であっても、この技術で使われている暗号化制御について質問されることがあるかもしれません。 たとえば、セキュリティ保護が業界標準であることを確認する場合などです。


|暗号化制御|Azure RMS での用途|
|-|-|
|アルゴリズム: AES<br /><br />キーの長さ: 128 ビットと 256 ビット [[1]](#footnote-1)|コンテンツの保護|
|アルゴリズム: RSA<br /><br />キーの長さ: 2048 ビット [[2]](#footnote-2)|キーの保護|
|SHA-256|証明書の署名|

###### <a name="footnote-1"></a>脚注 1 

次のシナリオでは、Azure Information Protection クライアントによって 256 ビットが使用されます。

- 汎用的な保護 (.pfile)。

- PDF 暗号化用の ISO 標準を使用してドキュメントが保護されている場合、または結果としての保護されたドキュメントのファイル名拡張子が .ppdf である場合、PDF ドキュメントに対するネイティブ保護。

- テキスト ファイルまたはイメージ ファイル (.ptxt や .pjpg など) のネイティブ保護。

###### <a name="footnote-2"></a>脚注 2

Azure Rights Management サービスがアクティブになっているときのキーの長さは、2048 ビットです。 以下のオプション シナリオでは、1024 ビットがサポートされます。

- オンプレミスからの移行中に、AD RMS クラスターが暗号化モード 1 で実行している場合。

- 移行前にオンプレミスで作成されてアーカイブされたキーの場合、以前に AD RMS によって保護されていたコンテンツを、移行後も引き続き Azure Rights Management サービスで開くことができるようにする場合。

### <a name="how-the-azure-rms-cryptographic-keys-are-stored-and-secured"></a>Azure RMS 暗号化キーの格納方法と保護方法

Azure RMS によって保護されるドキュメントまたはメールごとに、Azure RMS は 1 つの AES キー ("コンテンツ キー") を作成します。そのキーは、ドキュメントに埋め込まれ、ドキュメントの各エディションを通じて保持されます。 

コンテンツ キーはドキュメントのポリシーの一部として組織の RSA キー ("Azure Information Protection テナント キー") で保護され、ポリシーもドキュメントの作成者によって署名されます。 このテナント キーは組織の Azure Rights Management サービスによって保護されるすべてのドキュメントとメールに共通であり、組織が顧客によって管理されるテナント キー ("Bring Your Own Key" (BYOK) と呼ばれます) を使っている場合、このキーを変更できるのは Azure Information Protection 管理者だけです。 

このテナント キーは、Microsoft のオンライン サービスにより、高度に制御された環境と厳しい監視の下で保護されます。 顧客が管理するテナント キー (BYOK) を使う場合は、どのような状況でもキーを抽出、エクスポート、または共有する機能を持たない、Azure リージョンごとのハイエンド ハードウェア セキュリティ モジュール (HSM) のアレイを使うことで、このセキュリティが強化されます。 テナント キーと BYOK については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

Windows デバイスに送信されるライセンスと証明書は、クライアントのデバイス秘密キーで保護されます。このキーは、デバイスのユーザーが Azure RMS を初めて使ったときに作成されます。 この秘密キーはさらに、クライアント上の DPAPI で保護されます。DPAPI は、ユーザーのパスワードから作成されたキーを使って、これらのシークレットを保護します。 モバイル デバイスでは、キーは 1 回しか使われず、クライアントに格納されないので、デバイスでこれらのキーを保護する必要はありません。 


## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Azure RMS の動作のチュートリアル: 初めての使用、コンテンツ保護、コンテンツ消費
Azure RMS の動作をさらに詳しく理解するため、[Azure Rights Management サービスがアクティブ化](activate-service.md)された後、ユーザーが初めて Windows コンピューター上の Rights Management サービスを使い (**ユーザー環境の初期化**またはブートストラップと呼ばれることもあります)、**コンテンツ (ドキュメントまたはメール) を保護**した後、他のユーザーによって保護されているコンテンツを**消費** (開いて使う) するときの一般的なフローを見ていきます。

ユーザー環境が初期化された後、そのユーザーはそのコンピューターでドキュメントを保護したり、保護されているドキュメントを消費したりできます。

> [!NOTE]
> このユーザーが別の Windows コンピューターを使う場合、または別のユーザーがこの同じ Windows コンピューターを使う場合は、初期化プロセスが繰り返されます。

### <a name="initializing-the-user-environment"></a>ユーザー環境の初期化
ユーザーが Windows コンピューターでコンテンツを保護する場合、または保護されたコンテンツを消費する場合は、その前に、デバイスでユーザー環境を準備する必要があります。 これは 1 回限りのプロセスであり、ユーザーがコンテンツを保護したり保護されたコンテンツを消費したりしようとすると、ユーザーの介入なしに自動的に行われます。

![RMS クライアント アクティブ化フロー - ステップ 1: クライアントの認証](./media/AzRMS.png)

**ステップ 1 で行われること**: コンピューター上の RMS クライアントは、最初に、Azure Rights Management サービスに接続し、Azure Active Directory アカウントを使ってユーザーを認証します。

ユーザーのアカウントが Azure Active Directory と統合されている場合、この認証は自動的に行われ、ユーザーが資格情報の入力を求められることはありません。

![RMS クライアント アクティブ化 - ステップ 2: 証明書がクライアントにダウンロードされる](./media/AzRMS_useractivation2.png)

**ステップ 2 で行われること**: ユーザーが認証された後、接続は組織の Azure Information Protection テナントに自動的にリダイレクトされます。テナントは、ユーザーが保護されたコンテンツを消費したり、オフラインでコンテンツを保護したりするために、Azure Rights Management サービスへの認証を実行できる証明書を発行します。

これらの証明書の 1 つとして権利アカウント証明書 (RAC) があります。 この証明書は、Azure Active Directory するためにユーザーを認証し、31日間有効です。 証明書は、ユーザー アカウントが Azure Active Directory にあり、アカウントが有効になっている場合、RMS クライアントによって自動的に更新されます。 この証明書は、管理者が構成することはできません。 

この証明書のコピーは Azure に保存され、ユーザーが別のデバイスに移動した場合は、同じキーを使用して証明書が作成されます。

### <a name="content-protection"></a>コンテンツの保護
ユーザーがドキュメントを保護すると、RMS クライアントは保護されていないドキュメントに対して次の操作を実行します。

![RMS ドキュメントの保護 - ステップ 1: ドキュメントが暗号化される](./media/AzRMS_documentprotection1.png)

**ステップ 1 で行われること**: RMS クライアントは、ランダムなキー (コンテンツ キー) を作成し、このキーと AES 対称暗号化アルゴリズムを使って、ドキュメントを暗号化します。

![RMS ドキュメントの保護 - ステップ 2: ポリシーが作成される](./media/AzRMS_documentprotection2.png)

**ステップ 2 で行われること**: RMS クライアントは、ドキュメントに対するポリシーを含む証明書を作成します。ポリシーには、ユーザーまたはグループに対する[使用権限](configure-usage-rights.md)と、有効期限などの他の制限事項が含まれます。 これらの設定は、それ以前に管理者が構成するテンプレートで定義することも、またはコンテンツを保護するときに指定することも ("アドホック ポリシー" とも呼ばれます) できます。   

選択されたユーザーやグループの識別に使われるメインの Azure AD 属性は、Azure AD の ProxyAddresses 属性であり、この属性にはユーザーまたはグループのすべてのメール アドレスが格納されます。 ただし、ユーザー アカウントの AD ProxyAddresses 属性に値が何も含まれない場合は、ユーザーの UserPrincipalName の値が代わりに使われます。

その後、RMS クライアントは、ユーザー環境の初期化時に取得された組織のキーを使って、ポリシーと対称コンテンツ キーを暗号化します。 また、RMS クライアントは、ユーザー環境の初期化時に取得されたユーザーの証明書でポリシーに署名します。

![RMS ドキュメントの保護 - ステップ 3: ポリシーがドキュメントに埋め込まれる](./media/AzRMS_documentprotection3.png)

**手順3で**行われること: 最後に、RMS クライアントは、以前に暗号化されたドキュメントの本文と共にポリシーをファイルに埋め込みます。これは、保護されたドキュメントを構成します。

このドキュメントは、任意の方法を使って、任意の場所に格納したり共有したりでき、ポリシーは暗号化されたドキュメントと共に常に存在します。

### <a name="content-consumption"></a>コンテンツの消費
ユーザーが保護されたドキュメントの消費を望むと、RMS クライアントは最初に Azure Rights Management サービスへのアクセスを要求します。

![RMS ドキュメントの消費 - ステップ 1: ユーザーが認証されて、権限の一覧を取得する](./media/AzRMS_documentconsumption1.png)

**ステップ 1 で行われること**: 認証されたユーザーは、ドキュメントのポリシーとユーザーの証明書を Azure Rights Management サービスに送信します。 サービスはポリシーの暗号化を解除して評価し、ユーザーがドキュメントに対して持っている権限の一覧を作成します (ある場合)。 ユーザーを識別するには、Azure AD の ProxyAddresses 属性が、ユーザーのアカウントとユーザーがメンバーであるグループに対して使われます。 パフォーマンス上の理由から、グループ メンバーシップは[キャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)されます。 ユーザー アカウントの Azure AD ProxyAddresses 属性に値がない場合は、Azure AD UserPrincipalName の値が代わりに使われます。

![RMS ドキュメントの消費 - ステップ 2: 使用ライセンスがクライアントに返される](./media/AzRMS_documentconsumption2.png)

**ステップ 2 で行われること**: その後、サービスは暗号化解除されたポリシーから AES コンテンツ キーを抽出します。 このキーは、要求で取得されたユーザーの公開 RSA キーで暗号化されます。

再暗号化されたコンテンツ キーは、暗号化された使用ライセンスとユーザー権限の一覧に埋め込まれて、RMS クライアントに返されます。

![RMS ドキュメントの消費 - ステップ 3: ドキュメントが暗号化解除されて、権限が適用される](./media/AzRMS_documentconsumption3.png)

**ステップ 3 で行われること**: 最後に、RMS クライアントは暗号化された使用ライセンスを取得し、独自のユーザー秘密キーで暗号化を解除します。 これにより、RMS クライアントは必要に応じてドキュメント本文の暗号化を解除し、画面にレンダリングできます。

また、クライアントは、権限一覧の暗号化を解除してアプリケーションに渡し、アプリケーションのユーザー インターフェイスにそれらの権限を適用します。

> [!NOTE]
> 組織の外部のユーザーが組織で保護されているコンテンツを消費するときのフローも同じです。 このシナリオで異なる点は、ユーザーを認証する方法です。 詳細については、「[保護されたドキュメントを社外のユーザーと共有する場合、そのユーザーはどのようにして認証されますか](./faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)」を参照してください。


### <a name="variations"></a>バリエーション
これまでに示した流れは標準的なシナリオのものですが、いくつかのバリエーションがあります。

- **電子メールの保護**: Exchange Online と新しい機能を備えた Office 365 Message Encryption を使ってメール メッセージを保護するとき、消費するための認証では、ソーシャル ID プロバイダーとのフェデレーションまたはワンタイム パスコードを使うこともできます。 その後のプロセス フローは、送信メールの一時的なキャッシュ コピーを介して Web ブラウザー セッションのサービス側でコンテンツの消費が行われるのを除けば、よく似ています。

- **モバイル デバイス**: モバイル デバイスが Azure Rights Management サービスでファイルを保護または消費するときのプロセス フローはとても簡単です。 モバイル デバイスでは、(コンテンツを保護または消費するための) 各トランザクションが独立しているため、最初にユーザー初期化プロセスを行う必要はありません。 Windows コンピューターと同様に、モバイル デバイスは Azure Rights Management サービスに接続して認証を行います。 コンテンツを保護するには、モバイル デバイスはポリシーを送信し、Azure Rights Management サービスはドキュメントを保護するための発行ライセンスと対称キーを送信します。 コンテンツを消費するには、モバイル デバイスは、Azure Rights Management サービスに接続して認証を行うときに、Azure Rights Management サービスにドキュメント ポリシーを送信し、ドキュメントを消費するための使用ライセンスを要求します。 応答で、Azure Rights Management サービスはモバイル デバイスに必要なキーと制限を送信します。 どちらのプロセスも、TLS を使って、キーの交換およびその他の通信を保護します。

- **RMS コネクタ**: Azure Rights Management サービスが RMS コネクタで使われるときも、プロセス フローは変わりません。 唯一の違いは、コネクタがオンプレミスのサービス (Exchange Server や SharePoint Server など) と Azure Rights Management サービスの間のリレーとして機能することです。 コネクタ自体は、ユーザー環境の初期化、暗号化、暗号化解除など、いかなる操作も実行しません。 コネクタは、通常は AD RMS サーバーに送られる通信をリレーするだけであり、両側で使用されているプロトコルの変換を処理します。 このシナリオでは、Azure Rights Management サービスをオンプレミス サービスと併用できます。

- **一般的な保護 (.pfile)**: Azure Rights Management サービスが一般的にファイルを保護しているときは、RMS クライアントがすべての権限を許可するポリシーを作成する点を除き、フローは基本的にコンテンツ保護の場合と同じです。 ファイルが消費されるときは、ターゲット アプリケーションに渡される前にファイルが暗号化解除されます。 このシナリオでは、ファイルが RMS をネイティブにサポートしない場合でも、すべてのファイルを保護できます。

- **Microsoft アカウント**: Microsoft アカウントで認証されていれば、Azure Information Protection で消費用の電子メール アドレスを承認できます。 ただし、Microsoft アカウントが認証に使用されている場合、アプリケーションによっては、保護されたコンテンツを開けない場合があます。 詳細については、[こちら](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents)を参照してください。

## <a name="next-steps"></a>次の手順

Azure Rights Management サービスについては、「**理解と調査**」セクションの「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」などの他の記事で、既存のアプリケーションを Azure Rights Management と統合して情報保護ソリューションを提供する方法を学習してください。 

「[Azure Information Protection の用語](./terminology.md)」で、Azure Rights Management サービスを構成および使用するときに目にする用語をよく理解してください。また、展開を始める前に、「[Azure Information Protection の要件](requirements.md)」も確認してください。 すぐにご自分で試してみる場合は、[ポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)に関するチュートリアルをご利用ください。

組織へのデータ保護の展開を始める準備ができた場合は、「[Azure Information Protection デプロイ ロードマップ](deployment-roadmap.md)」で、展開の手順と、具体的な操作手順へのリンクをご覧ください。

> [!TIP]
> 追加情報やヘルプについては、「[Azure Information Protection の情報とサポート](information-support.md)」のリソースとリンクをご覧ください。
