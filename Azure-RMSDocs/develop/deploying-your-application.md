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
ms.openlocfilehash: c600f6e332ec230d73c90faafe8fb602e1d3dd88
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570695"
---
# <a name="deploy-into-production"></a>運用環境にデプロイする

このトピックでは Azure Information Protection (AIP)/Rights Management サービス (RMS) が有効なアプリケーションのデプロイ プロセスを説明します。

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Information Protection Integration Agreement (IPIA) を申請する
AIP/RMS で開発されたアプリケーションをリリースする前に、Microsoft との正式な契約を申請し、完了する必要があります。

### <a name="begin-the-process"></a>プロセスを開始する
次の情報を記載した電子メールを <strong>IPIA@microsoft.com</strong> に送信して、IPIA を入手します。

**件名:** *会社名* の IPIA 申し込み

電子メールの本文に、次の情報を含めます。
- アプリケーションと製品名
- 要求者の氏名
- 要求者の電子メール アドレス

### <a name="next-steps"></a>次のステップ
IPIA 申請が受信されると、(Word 文書形式の) フォームがお客様に送信されます。
IPIA の使用条件を確認し、次の情報をフォームに入力して <strong>IPIA@microsoft.com</strong> に返送します。
- 会社の正式名称
- 法人の都道府県または国
- 会社の URL
- 連絡先の電子メール アドレス
- (省略可能) 会社の追加住所
- 会社のアプリケーションの名前
- アプリケーションの簡単な説明
- *Azure テナント ID*
- アプリケーションの *アプリ ID*
- 緊急時の会社の連絡先、電子メール アドレス、および電話番号

### <a name="completing-the-agreement"></a>契約の完了
フォームが受信されると、デジタル署名を行うための最終的な IPIA リンクがお客様に送信されます。 お客様の署名後、適切な Microsoft 担当者が署名することで、契約が締結されます。

### <a name="already-have-a-signed-ipia"></a>既に署名済みの IPIA がある場合
署名済みの IPIA が既に存在し、リリースするアプリケーション用に新しい *アプリ ID* を追加する場合は、電子メールに次の情報を記載して <strong>IPIA@microsoft.com</strong> に送信します。
- 会社のアプリケーションの名前
- アプリケーションの簡単な説明
- Azure のテナント ID (以前と同じ場合でも必要です)
- アプリケーションのアプリ ID
- 緊急時の会社の連絡先、電子メール アドレス、および電話番号

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

RMS クライアント 2.1 とアプリケーションの統合例が [Rights Protected Folder エクスプローラー](/previous-versions/orphan-topics/ws.10/hh538204(v=ws.10))です。 方法を理解するため、自分でインストールしてみてください。

### <a name="make-rmsclient21-a-pre-requisite-for-your-application-install"></a>RMS クライアント 2.1 をアプリケーションをインストールする際の前提条件とする

ここでは、RMS クライアント 2.1 がエンドユーザーのコンピューターにない場合にアプリケーションのインストールが失敗するように、前提条件を作成します。

クライアントが存在しない場合、RMS クライアント 2.1 のコピーをダウンロードできる場所をユーザーに通知するエラー メッセージを提供します

クライアントが存在する場合は、アプリケーションのインストールを続行します。

## <a name="enabling-azure-information-protection-services-with-your-application"></a>アプリケーションでの Azure Information Protection サービスの有効化

> [!NOTE]
> 認証のために新しい ADAL モデルに移行している場合は、**SIA** をインストールする必要はありません。 詳細については、[RMS 対応アプリケーションの ADAL 認証](adal-auth.md)に関するページを参照してください。
> また、**Windows 10 のアプリケーションを認定する** こともできます - アプリケーションを更新して Microsoft Online サインイン アシスタントではなく ADAL 認証が使用されるようにすることで、多要素認証の使用、コンピューターの管理権限を必要としない RMS クライアント 2.1 のインストールが可能になります

エンド ユーザーが Information Protection サービスを活用するには、*Online Services サインイン アシスタント (SIA)* をデプロイする必要があります。 アプリケーション開発者はエンドユーザーが (オンプレミスの) RMS と Azure Information Protection のどちらを使用して Information Protection を使用するかわかりません。


> [!IMPORTANT]
> Azure ベースの RMS を使用してクライアント アプリケーションを実行している場合は、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS requirements: Cloud subscriptions that support Azure RMS](../requirements.md)」(Azure RMS 要件: Azure RMS をサポートするクラウド サブスクリプション) を参照してください。
> Azure RMS を使用した実行の詳細については、[クラウド ベースの RMS を使用するためのサービス アプリケーションの有効化](how-to-use-file-api-with-aadrm-cloud.md)に関するページを参照してください。

-   Microsoft ダウンロード センターから [Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/download/details.aspx?id=28177)をダウンロードします。
-   権利保護に対応したアプリケーションのデプロイにこのサービス選択のための前提条件チェックが含まれるようにしてください。
-   独自のテストおよびエンドユーザーによるオンライン サービスの使用については、[Rights Management の構成](../deployment-roadmap.md)に関する TechNet のトピックを参照してください。

このガイドはアプリの構成でも必要になります - 「[Azure Active Directory ログインを使用するよう App Service アプリを構成する](/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)」

Azure Rights Management サービスで RMS を使用するためのアプリケーションの有効化については、[クラウド ベースの RMS を使用するためのアプリケーションの有効化](how-to-use-file-api-with-aadrm-cloud.md)に関するページを参照してください。

## <a name="related-topics"></a>関連トピック

* [Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/download/details.aspx?id=28177)
* [Rights Management の構成](../deployment-roadmap.md)
* [クラウド ベースの RMS を使用するためのアプリケーションの有効化](how-to-use-file-api-with-aadrm-cloud.md)