---
title: アプリケーションのデプロイ - AIP
description: Azure Information Protection (AIP)/Rights Management Services (RMS) が有効になっているアプリケーションのデプロイプロセスについて説明します。
keywords: デプロイ, RMS, AIP
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 4f4258811ec634a49f84b76fcf1feb41752311df
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564366"
---
# <a name="deploy-into-production"></a>運用環境にデプロイする

このトピックでは Azure Information Protection (AIP)/Rights Management サービス (RMS) が有効なアプリケーションのデプロイ プロセスを説明します。

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Information Protection Integration Agreement (IPIA) を申請する
AIP/RMS で開発されたアプリケーションをリリースする前に、Microsoft との正式な契約を申請し、完了する必要があります。

### <a name="begin-the-process"></a>プロセスを開始する
次の情報を含む電子メールをに送信して、IPIA を入手し <strong>IPIA@microsoft.com</strong> ます。

**件名:***会社名* の IPIA の申請

電子メールの本文には、次の内容を含めます。
- アプリケーションと製品の名前
- 申請者の氏名
- 申請者の電子メール アドレス

### <a name="next-steps"></a>次のステップ
IPIA 申請の受領後、フォームが届きます (Word 文書)。
IPIA の使用条件を確認し、フォームをに返し <strong>IPIA@microsoft.com</strong> ます。次の情報を参照してください。
- 会社の正式名称
- 法人の都道府県または国
- 会社の URL
- 連絡先の電子メール アドレス
- 会社のその他のアドレス (省略可能)
- 会社のアプリケーションの名前
- アプリケーションの簡単な説明
- *Azure のテナント ID*
- アプリケーションの*アプリ ID*
- 緊急時の会社の連絡先、電子メール、電話番号

### <a name="completing-the-agreement"></a>契約の完了
フォームが受領されると、デジタル署名のための最終 IPIA リンクが送信されます。 署名後、適切な Microsoft の担当者による署名が行われ、契約が完了します。

### <a name="already-have-a-signed-ipia"></a>IPIA が署名済みの場合
署名済み IPIA を所有しており、リリースしているアプリケーションに新しい*アプリ ID* を追加したい場合は、電子メールを <strong>IPIA@microsoft.com</strong> に送信し、次の情報を提供してください。
- 会社のアプリケーションの名前
- アプリケーションの簡単な説明
- Azure のテナント ID (以前と同じ場合でも必要です)
- アプリケーションのアプリ ID
- 緊急時の会社の連絡先、電子メール、電話番号

電子メールの送信から受領確認まで、最大で 72 時間お待ちください。

## <a name="deploying-to-the-client-environment"></a>クライアント環境へのデプロイ

Azure Information Protection (AIP)/Rights Management サービス (RMS) ツールでビルドしたアプリケーションをデプロイするには、エンドユーザーのコンピューターに RMS クライアント 2.1 をデプロイする必要があります。

### <a name="rmsclient21"></a>RMS クライアント 2.1
RMS クライアント 2.1 はオンプレミスにインストールされているか、Microsoft データセンターにインストールされているかに関係なく、AIP/RMS が有効なアプリケーションを通じた情報の流れのアクセスと使用を保護するために設計されています。

RMS クライアント 2.1 は、Windows オペレーティング システムのコンポーネントではありません。 このクライアントは、そのライセンス契約の確認と受け入れ内容に基づき、アプリケーションと共に自由に配布できるオプションのワークロードとして出荷されます。

> [!IMPORTANT]
> RMS クライアント 2.1 はアーキテクチャ固有であるため、ターゲット オペレーティング システムのアーキテクチャと一致する必要があります。


## <a name="rmsclient21-installation-options"></a>RMS クライアント 2.1 のインストール オプション

### <a name="creating-your-deployment-package"></a>デプロイ パッケージの作成

推奨されるインストール技術を使用したアプリケーションまたはソリューションで RMS クライアント インストーラー パッケージをバンドルすることをお勧めします。 RMS クライアントは他のアプリケーションやソリューションと共に自由に再配布できます。

RMS クライアント 2.1 は RMS クライアント 2.1 のインストーラーを起動した対話形式か、サイレント モードによってインストールすることができます。 統合の手順は次のとおりです。

-   RMS クライアント 2.1 インストーラーをダウンロードする
-   実行する RMS クライアント 2.1 インストーラーをアプリケーションのインストーラーと統合する

RMS クライアント 2.1 とアプリケーションの統合例が [Rights Protected Folder エクスプローラー](https://technet.microsoft.com/library/rights-protected-folder-explorer(v=ws.10).aspx)です。 方法を理解するため、自分でインストールしてみてください。

### <a name="make-rmsclient21-a-pre-requisite-for-your-application-install"></a>RMS クライアント 2.1 をアプリケーションをインストールする際の前提条件とする

ここでは、RMS クライアント 2.1 がエンドユーザーのコンピューターにない場合にアプリケーションのインストールが失敗するように、前提条件を作成します。

クライアントが存在しない場合、RMS クライアント 2.1 のコピーをダウンロードできる場所をユーザーに通知するエラー メッセージを提供します

クライアントが存在する場合は、アプリケーションのインストールを続行します。

## <a name="enabling-azure-information-protection-services-with-your-application"></a>アプリケーションでの Azure Information Protection サービスの有効化

> [!NOTE]
> 認証のために新しい ADAL モデルに移行している場合は、**SIA** をインストールする必要はありません。 詳細については、[RMS 対応アプリケーションの ADAL 認証](adal-auth.md)に関するページを参照してください。
> また、**Windows 10 のアプリケーションを認定する**こともできます - アプリケーションを更新して Microsoft Online サインイン アシスタントではなく ADAL 認証が使用されるようにすることで、多要素認証の使用、コンピューターの管理権限を必要としない RMS クライアント 2.1 のインストールが可能になります

エンド ユーザーが Information Protection サービスを活用するには、*Online Services サインイン アシスタント (SIA)* をデプロイする必要があります。 アプリケーション開発者はエンドユーザーが (オンプレミスの) RMS と Azure Information Protection のどちらを使用して Information Protection を使用するかわかりません。


> [!IMPORTANT]
> Azure ベースの RMS を使用してクライアント アプリケーションを実行している場合は、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS requirements: Cloud subscriptions that support Azure RMS](../requirements.md)」(Azure RMS 要件: Azure RMS をサポートするクラウド サブスクリプション) を参照してください。
> Azure RMS を使用した実行の詳細については、[クラウド ベースの RMS を使用するためのサービス アプリケーションの有効化](how-to-use-file-api-with-aadrm-cloud.md)に関するページを参照してください。

-   Microsoft ダウンロード センターから [Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/download/details.aspx?id=28177)をダウンロードします。
-   権利保護に対応したアプリケーションのデプロイにこのサービス選択のための前提条件チェックが含まれるようにしてください。
-   独自のテストおよびエンドユーザーによるオンライン サービスの使用については、[Rights Management の構成](https://TechNet.Microsoft.Com/library/jj585002.aspx)に関する TechNet のトピックを参照してください。

このガイドはアプリの構成でも必要になります - 「[Azure Active Directory ログインを使用するよう App Service アプリを構成する](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)」

Azure Rights Management サービスで RMS を使用するためのアプリケーションの有効化については、[クラウド ベースの RMS を使用するためのアプリケーションの有効化](how-to-use-file-api-with-aadrm-cloud.md)に関するページを参照してください。

## <a name="related-topics"></a>関連トピック

* [Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/download/details.aspx?id=28177)
* [Rights Management の構成](https://TechNet.Microsoft.Com/library/jj585002.aspx)
* [クラウド ベースの RMS を使用するためのアプリケーションの有効化](how-to-use-file-api-with-aadrm-cloud.md)
