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
** この SDK コンテンツは最新のものではありません。 しばらくの間、[最新版](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)の文書は MSDN でご覧ください。 **
# アプリケーションのデプロイ


このトピックでは、権利保護に対応したアプリケーションのデプロイ オプションについて概説し、順を追って各操作を説明します。

> [!IMPORTANT]
> ベスト プラクティスとして、はじめに RMS サーバーに対して RMS 運用前環境で Rights Management サービス SDK 2.1 アプリケーションをテストすることをお勧めします。 その後で、顧客に Azure RMS サービスでのアプリケーションの使用を勧める場合は、その環境でのテストに移行します。 詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

 

## Active Directory Rights Management サービス Client 2.1 のインストール オプション

運用証明書を使用してマニフェスト ファイルを作成すると、アプリケーションをデプロイする準備ができます。 RMS SDK 2.1 を使用するため、Active Directory Rights Management サービス Client 2.1 をエンドユーザーのコンピューターにデプロイする必要があります。

### AD RMS クライアント 2.1

AD RMS クライアント 2.1 は、(オンプレミスでインストールされるか、Microsoft のデータセンターでインストールされるかにかかわらず) RMS を使用するアプリケーション経由でやり取りされる情報のアクセスおよび使用を保護することを目的として、クライアント コンピューター向けに設計されたソフトウェアです。

AD RMS クライアント 2.1 は、Windows オペレーティング システムのコンポーネントではありません。 AD RMS クライアント 2.1 は、個別のダウンロードとして提供されています。使用許諾契約書を確認して承諾することで、サードパーティ製ソフトウェアと一緒に自由に配布できるため、クライアントは環境内の RMS サーバーを使用してデプロイすることで、権利保護されたコンテンツにアクセスできるようになります。

> [!IMPORTANT] AD RMS クライアント 2.1 はアーキテクチャ固有であり、ターゲット オペレーティング システムのアーキテクチャと一致する必要があります。


## AD RMS クライアント 2.1 のインストールの選択

-   **AD RMS クライアント 2.1 を再配布する**

    RMS クライアント インストーラー パッケージは、お使いのアプリケーションまたは推奨されるインストール テクノロジによるソリューションを使用してバンドルすることをお勧めします。 RMS クライアントは自由に再配布でき、他のアプリケーションや IT ソリューションにバンドルできます。

    AD RMS クライアント 2.1 のインストーラーを起動し、対話形式で AD RMS クライアント 2.1 をインストールすることも、サイレント モードでインストールすることもできます。 統合手順は次のとおりです。

    -   RMS クライアント 2.1 インストーラーをダウンロードする
    -   アプリケーションのインストーラーを使用して実行する AD RMS クライアント 2.1 インストーラーを統合する

    AD RMS クライアント 2.1 をアプリケーションに統合する良い例として、RMS SDK 2.1 のインストーラー パッケージと権利保護されているフォルダー エクスプ ローラー パッケージの 2 つが挙げられます。 手順を理解するために、これらをご自分でインストールしてみてください。

-   **AD RMS クライアント 2.1 をアプリケーションをインストールする際の前提条件とする**

    この場合、AD RMS クライアント 2.1 がエンドユーザーのコンピューターに存在しない場合、アプリケーションのインストールが失敗するように前提条件を作成します。

    クライアントが存在しない場合は、AD RMS クライアント 2.1 のコピーをダウンロードできるサイトを知らせるエラー メッセージが表示されるようにします。

    クライアントが存在する場合は、アプリケーションのインストールを続行します。

## アプリケーションで Azure Rights Management サービスを有効にする

> [!NOTE]
> 認証用に新しい ADAL モデルに移行した場合は、SIA をインストールする必要はありません。 詳細については、「ADAL authentication for your RMS enabled application (RMS 対応アプリケーションの ADAL 認証)」をご覧ください。

- **Windows 10 のアプリケーション認定を受ける**: Microsoft Online サインイン アシスタントではなく、ADAL 認証を使用するようにアプリケーションを更新すると、ユーザーと顧客は以下を利用できるようになります。
  - 多要素認証を使用する
  - コンピューターの管理者特権なしで RMS 2.1 クライアントをインストールする
 
  エンドユーザーが Azure Rights Management サービスを活用できるようにするには、*Online Services サインイン アシスタント*をデプロイする必要があります。 アプリケーション開発者には、エンドユーザーが RMS (オンプレミス) と Azure Rights Management services (クラウド サービス) のどちらを使用するのかわかりません。

> [!IMPORTANT]
> Azure RMS で RMS SDK 2.1 クライアント アプリケーションを実行するには、Azure RMS テナントを要求する必要があります。 <rmcstbeta@microsoft.com> にテナントを要求する電子メールを送信してください。

-   Microsoft ダウンロード センターから [Microsoft Online Services サインイン アシスタント](http://www.microsoft.com/en-us/download/details.aspx?id=28177)をダウンロードします。
-   権利保護に対応したアプリケーションのデプロイにこのサービスを選択する前提条件チェックが含まれていることを確認します。
-   ご自身のテストおよびエンドユーザーによるオンライン サービスの使用に関する詳細については、TechNet トピック「[Rights Management の構成](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)」をご覧ください。

アプリケーションによる Azure Rights Management サービスでの RMS の使用を有効にする方法の詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」をご覧ください。

## 関連項目

* [How-to use (使用方法)](how-to-use-msipc.md)
* [Microsoft Online Services サインイン アシスタント](http://www.microsoft.com/en-us/download/details.aspx?id=28177)
* [Rights Management を構成する](https://TechNet.Microsoft.Com/en-us/library/jj585002.aspx)
* [クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)
 

 





<!--HONumber=Jun16_HO1-->


