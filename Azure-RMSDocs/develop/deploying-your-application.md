---
title: アプリケーションのデプロイ - AIP
description: このトピックでは、アプリケーションのデプロイの概要について順を追って説明します。
keywords: デプロイ, RMS, AIP
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: b1525665fb488aed1ad98a77ac66f92f7ee4509b
ms.sourcegitcommit: 1cd4edd4ba1eb5e10cb61628029213eda316783a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53266683"
---
# <a name="deploy-into-production"></a>運用環境にデプロイする

このトピックでは、Azure Information Protection (AIP)/Rights Management サービス (RMS) 対応アプリケーションのデプロイ プロセスについて順を追って説明します。

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Information Protection Integration Agreement (IPIA) を申請する
AIP/RMS を使用して開発したアプリケーションをリリースする前に、Microsoft との正式契約を申請して締結する必要があります。

### <a name="begin-the-process"></a>プロセスを開始する
次の情報を記載した電子メールを **IPIA@microsoft.com** に送信して、IPIA を入手します。

**件名:** *会社名*の IPIA 申し込み

電子メールの本文に、次の情報を含めます。
- アプリケーションと製品名
- 要求者の氏名
- 要求者の電子メール アドレス

### <a name="next-steps"></a>次の手順
IPIA 申請が受信されると、(Word 文書形式の) フォームがお客様に送信されます。
IPIA の使用条件を確認し、次の情報をフォームに入力して **IPIA@microsoft.com** に返送します。
- 会社の正式名称
- 法人の都道府県または国
- 会社の URL
- 連絡先の電子メール アドレス
- (省略可能) 会社の追加住所
- 会社のアプリケーションの名前
- アプリケーションの簡単な説明
- *Azure テナント ID*
- アプリケーションの*アプリ ID*
- 緊急時の会社の連絡先、電子メール アドレス、および電話番号

### <a name="completing-the-agreement"></a>契約を締結する
フォームが受信されると、デジタル署名を行うための最終的な IPIA リンクがお客様に送信されます。 お客様の署名後、適切な Microsoft 担当者が署名することで、契約が締結されます。

### <a name="already-have-a-signed-ipia"></a>既に署名済みの IPIA がある場合
署名済みの IPIA が既に存在し、リリースするアプリケーション用に新しい *アプリ ID* を追加する場合は、電子メールに次の情報を記載して **IPIA@microsoft.com** に送信します。
- 会社のアプリケーションの名前
- アプリケーションの簡単な説明
- Azure テナント ID (以前と同じ場合でも記載)
- アプリケーションのアプリ ID
- 緊急時の会社の連絡先、電子メール アドレス、および電話番号

電子メールの送信時には、受領の確認には最大で 72 時間かかることをご了承ください。

## <a name="deploying-to-the-client-environment"></a>クライアント環境にデプロイする

Azure Information Protection (AIP)/Rights Management サービス (RMS) ツールでビルドしたアプリケーションをデプロイするには、エンドユーザーのコンピューターに RMS クライアント 2.1 をデプロイする必要があります。

### <a name="rmsclient21"></a>RMS クライアント 2.1
RMS クライアント 2.1 は、(オンプレミスでインストールされるか、Microsoft のデータセンターにインストールされているかにかかわらず) AIP/RMS 対応アプリケーション経由でやり取りされる情報へのアクセスと使用を保護するためのものです。

RMS クライアント 2.1 は、Windows オペレーティング システムのコンポーネントではありません。 このクライアントはオプションのダウンロードとして配信されており、使用許諾契約書を確認して承諾することでお使いのアプリケーションと一緒に自由に配布できます。

> [!IMPORTANT]
> RMS クライアント 2.1 はアーキテクチャ固有であるため、ターゲット オペレーティング システムのアーキテクチャと一致する必要があります。


## <a name="rmsclient21-installation-options"></a>RMS クライアント 2.1 のインストール オプション

### <a name="creating-your-deployment-package"></a>デプロイ パッケージの作成

RMS クライアント インストーラー パッケージは、お好みのインストール テクノロジを使用してアプリケーションまたはソリューションにバンドルすることをお勧めします。 RMS クライアントは自由に再配布が可能で、他のアプリケーションやソリューションにバンドルできます。

RMS クライアント 2.1 のインストーラーを起動して対話形式で RMS クライアント 2.1 をインストールすることも、サイレント モードでインストールすることもできます。 統合手順は次のとおりです。

-   RMS クライアント 2.1 インストーラーをダウンロードする
-   実行する RMS クライアント 2.1 インストーラーをアプリケーションのインストーラーと統合する

RMS クライアント 2.1 とアプリケーションの統合の例として、[Rights Protected Folder Explorer](https://technet.microsoft.com/library/rights-protected-folder-explorer(v=ws.10).aspx) パッケージがあります。 手順を理解するために、これをご自分でインストールしてみてください。

### <a name="make-rmsclient21-a-pre-requisite-for-your-application-install"></a>RMS クライアント 2.1 をアプリケーションをインストールする際の前提条件とする

この場合、RMS クライアント 2.1 がエンドユーザーのコンピューターに存在しない場合、アプリケーションのインストールが失敗するように前提条件を作成します。

クライアントが存在しない場合は、RMS クライアント 2.1 のコピーをダウンロードできるサイトを知らせるエラー メッセージが表示されるようにします。

クライアントが存在する場合は、アプリケーションのインストールを続行します。

## <a name="enabling-azure-information-protection-services-with-your-application"></a>アプリケーションで Azure Information Protection サービスを有効にする

> [!NOTE]
> 認証用に新しい ADAL モデルに移行した場合は、**SIA** をインストールする必要はありません。 詳細については、「[ADAL authentication for your RMS enabled application (RMS 対応アプリケーションの ADAL 認証)](adal-auth.md)」をご覧ください。
> **Windows 10 のアプリケーション認定を受ける**こともできます。Microsoft Online サインイン アシスタントではなく、ADAL 認証を使用するようにアプリケーションを更新すると、ユーザーと顧客は以下を利用できるようになります。多要素認証を使用する。コンピューターの管理者特権なしで RMS クライアント 2.1 をインストールする

エンドユーザーが Information Protection/サービスを活用できるようにするには、*Online Services サインイン アシスタント (SIA)* をデプロイする必要があります。 アプリケーション開発者には、エンドユーザーが RMS (オンプレミス) または Azure Information Protection のどちらで Information Protection を使用するのかわかりません。


> [!IMPORTANT]
> Azure ベースの RMS でクライアント アプリケーションを実行する場合は、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../requirements.md)」を参照してください。
> Azure RMS での実行に関する詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

-   Microsoft ダウンロード センターから [Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/download/details.aspx?id=28177)をダウンロードします。
-   権利保護に対応したアプリケーションのデプロイにこのサービスを選択する前提条件チェックが含まれていることを確認します。
-   ご自身のテストおよびエンドユーザーによるオンライン サービスの使用に関する詳細については、TechNet トピック「[Rights Management の構成](https://TechNet.Microsoft.Com/library/jj585002.aspx)」をご覧ください。

このガイドを使用してアプリを構成する必要もあります - [App Service アプリケーションを構成して Azure Active Directory ログインを構成する方法](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)。

アプリケーションによる Azure Rights Management サービスでの RMS の使用を有効にする方法の詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」をご覧ください。

## <a name="related-topics"></a>関連項目

* [Microsoft Online Services サインイン アシスタント](https://www.microsoft.com/download/details.aspx?id=28177)
* [Rights Management を構成する](https://TechNet.Microsoft.Com/library/jj585002.aspx)
* [クラウド ベース RMS でのアプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)

