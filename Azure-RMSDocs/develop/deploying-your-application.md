---
# required metadata

title: アプリケーションのデプロイ | Azure RMS
description: このトピックでは、権利保護に対応したアプリケーションのデプロイ オプションについて概説し、順を追って各操作を説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4B785564-6839-49ED-A243-E2A6DFF88B2E
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 運用前環境にデプロイする


このトピックでは、権利保護に対応したアプリケーションのデプロイ オプションについて概説し、順を追って各操作を説明します。

## 運用環境の使用許諾契約書の要求

 Rights Management サービス SDK 2.1 を使用して開発されたアプリケーションを解放するには、運用環境の使用許諾契約を申請して、運用証明書を取得する必要があります。

> [!IMPORTANT]
> Azure ベースの RMS でクライアント アプリケーションを実行する場合は、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)」を参照してください。
> Azure RMS での実行に関する詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

運用環境の使用許諾契約書に申請することで、証明書を取得できます。

[RMLA@microsoft.com](mailto:rmla@microsoft.com) に電子メール メッセージを送信 し、次の情報を含めます。

- 会社の正式名称
- 会社の住所 (市区町村、都道府県、国またはリージョン、および 郵便番号を含む)
- 会社の宛先 (市区町村、都道府県、国またはリージョン、および 郵便番号を含む)
- 会社の電話番号、FAX 番号
- 会社の URL
- 法人の国またはリージョン
- アプリケーションまたは製品名
- 要求者の氏名
- 要求者の役職または職位
- 要求者の電子メール アドレス

電子メール アカウントは必須ではありませんが、アプリケーション プロセスの通信は通常、電子メールで行われます。 Microsoft Outlook.com で無料の電子メール アカウントを取得できます。 アカウントがなく、アカウントを必要としていない場合、次のアドレスにタイプ入力した申請書を送信できます。

      Active Directory Rights Management License Agreements (ADRMLA)

      Microsoft Corporation

      One Microsoft Way

      Redmond, WA 98052-6399

契約書を要求するときに、次を実行してください。
- 契約書に表示されるため、情報は英語で入力してください。
- 要求されるすべての情報を送信してください。 情報が不足しているか不完全な場合、要求の処理が遅れることがあります。

Active Directory Rights Management ライセンス契約 (ADRMLA) チームは、電子メールによる要求には 3 営業日以内に応答します。郵送で要求を送信した場合、応答にかかる期間はそれより長くなります。 応答には、使用許諾契約書用紙と詳細な手順が含まれます。 契約書のすべてのページを読み、署名してから ADRMLA チームに返送してください。 使用許諾契約書のフォントを変更したり、段落の書式を変更したりしないでください。

ADRMLA チームから受信した手順に従ってください。 この手順では、証明書要求を満たすために必要なデジタル情報の項目が一覧表示されます。 この手順に従うことにより、遅延を減らすことができます。

運用証明書が作成されると、ADRMLA チームによってユーザーに転送されます。 証明書への ADRMLA チームの応答は、電子メールの場合は最大で 15 営業日、郵送の場合はそれより長くかかる場合があることに注意してください。


## Rights Management Service Client 2.1 のインストールのオプションと要件

RMS SDK 2.1 を使用するため、Active Directory Rights Management サービス Client 2.1 をエンドユーザーのコンピューターにデプロイする必要があります。

### RMS クライアント 2.1

RMS クライアント 2.1 は、(オンプレミスでインストールされるか、Microsoft のデータセンターにインストールされているかにかかわらず) RMS を使用するアプリケーション経由でやり取りされる情報のアクセスと使用を保護することを目的として、クライアント コンピューター向けに設計されたソフトウェアです。

RMS クライアント 2.1 は、Windows オペレーティング システムのコンポーネントではありません。 RMS クライアント 2.1 は、個別のダウンロードとして提供されています。使用許諾契約書を確認して承諾することで、サードパーティ製ソフトウェアと一緒に自由に配布できるため、クライアントは環境内の RMS サーバーを使用してデプロイすることで、権利保護されたコンテンツにアクセスできるようになります。


> [!IMPORTANT] AD RMS クライアント 2.1 はアーキテクチャ固有であり、ターゲット オペレーティング システムのアーキテクチャと一致する必要があります。


## RMS クライアント 2.1 のインストールの選択

-   **RMS クライアント 2.1 の再配布**

    RMS クライアント インストーラー パッケージは、お使いのアプリケーションまたは推奨されるインストール テクノロジによるソリューションを使用してバンドルすることをお勧めします。 RMS クライアントは自由に再配布でき、他のアプリケーションや IT ソリューションにバンドルできます。

    RMS クライアント 2.1 のインストーラーを起動し、対話形式で RMS クライアント 2.1 をインストールすることも、サイレント モードでインストールすることもできます。 統合手順は次のとおりです。

    -   RMS クライアント 2.1 インストーラーをダウンロードする
    -   アプリケーションのインストーラーを使用して実行する RMS クライアント 2.1 インストーラーを統合する

    RMS クライアント 2.1 をアプリケーションに統合する良い例として、RMS SDK 2.1 のインストーラー パッケージと権利保護されているフォルダー エクスプローラー パッケージの 2 つが挙げられます。 手順を理解するために、これらをご自分でインストールしてみてください。

-   **RMS クライアント 2.1 をアプリケーションをインストールする際の前提条件とする**

    この場合、RMS クライアント 2.1 がエンドユーザーのコンピューターに存在しない場合、アプリケーションのインストールが失敗するように前提条件を作成します。

    クライアントが存在しない場合は、RMS クライアント 2.1 のコピーをダウンロードできるサイトを知らせるエラー メッセージが表示されるようにします。

    クライアントが存在する場合は、アプリケーションのインストールを続行します。

## アプリケーションで Azure Rights Management サービスを有効にする

> [!NOTE]
> 認証用に新しい ADAL モデルに移行した場合は、SIA をインストールする必要はありません。 詳細については、「[ADAL authentication for your RMS enabled application (RMS 対応アプリケーションの ADAL 認証)](adal-auth.md)」をご覧ください。
> あるいは、**Windows 10 のアプリケーション認定を受ける**ことができます。 - Microsoft Online サインイン アシスタントではなく、ADAL 認証を使用するようにアプリケーションを更新すると、ユーザーと顧客は多要素認証を利用したり、コンピューターの管理者特権なしで RMS クライアント 2.1 をインストールしたりできるようになります。


エンドユーザーが Azure Rights Management サービスを活用できるようにするには、*Online Services サインイン アシスタント (SIA)* をデプロイする必要があります。 アプリケーション開発者には、エンドユーザーが RMS (オンプレミス) と Azure Rights Management services (クラウド サービス) のどちらを使用するのかわかりません。


> [!IMPORTANT]
> Azure RMS で RMS SDK 2.1 クライアント アプリケーションを実行するには、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)」を参照してください。

-   Microsoft ダウンロード センターから [Microsoft Online Services サインイン アシスタント](http://www.microsoft.com/en-us/download/details.aspx?id=28177)をダウンロードします。
-   権利保護に対応したアプリケーションのデプロイにこのサービスを選択する前提条件チェックが含まれていることを確認します。
-   ご自身のテストおよびエンドユーザーによるオンライン サービスの使用に関する詳細については、TechNet トピック「[Rights Management の構成](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)」をご覧ください。

アプリケーションによる Azure Rights Management サービスでの RMS の使用を有効にする方法の詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」をご覧ください。

## 関連項目

* [Microsoft Online Services サインイン アシスタント](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Rights Management を構成する](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)
 

 


<!--HONumber=Jun16_HO2-->


