---
title: Azure Information Protection の中央レポート機能
description: 中央レポート機能を使用して、Azure Information Protection ラベルの導入を追跡し、機密情報を含むファイルを特定する方法
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/13/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 85ca097a1808c2940ce534c7ce3d0542aaf3f27a
ms.sourcegitcommit: 0f9e2ba05b61f8db08387576a697b8deff45fd36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2018
ms.locfileid: "51611422"
---
# <a name="central-reporting-for-azure-information-protection"></a>Azure Information Protection の中央レポート機能

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> 現在のところ、この機能はプレビュー段階で、変更される可能性があります。 この機能が一般公開になったときに、このプレビュー期間中に収集されたすべてのデータがサポートされなくなる可能性があります。


中央レポート機能に Azure Information Protection の分析を使用して、Azure Information Protection ラベルの導入を追跡し、ラベル付きのドキュメントや電子メールへのユーザー アクセスと、分類への変更を監視します。 保護する必要がある機密情報が含まれているドキュメントを識別することもできます。

現在、表示されるデータは Azure Information Protection クライアントと Azure Information Protection スキャナーから集計されたものです。

たとえば、次のようなことを確認できます。

- 期間を選択できる**使用状況レポート**からは、次のことが確認できます。
    
    - 適用されているラベル
    
    - ラベル付けされているドキュメントと電子メールの数
    
    - 保護されているドキュメントと電子メールの数
    
    - ドキュメントや電子メールにラベル付けしているユーザーの数とデバイスの数
    
    - ラベル付けに使用されているアプリケーション

- **データ検出**レポートからは、次のことが確認できます。

    - スキャンされたデータ リポジトリにあるファイル
    
    - ラベル付けされ、保護されているファイルと、ラベルごとのファイルの場所
    
    - 既知のカテゴリ (財務データや個人情報など) の機密情報が含まれるファイルと、これらのカテゴリごとのファイルの場所
    
レポートでは [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) を使用して、ユーザーが所有するワークスペースにデータを格納します。 クエリ言語に習熟している場合は、クエリを変更して、新しいレポートや Power BI ダッシュボードを作成できます。 クエリ言語を理解するには、「[Log Analytics のクエリの概要](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal)」のチュートリアルが役立ちます。 

詳細については、ブログ記事「[Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)」 (Microsoft Information Protection を使用して、すべてのデータに対してデータ検出、レポート作成、および分析を行う) を参照してください。

### <a name="information-collected-and-sent-to-microsoft"></a>収集され Microsoft に送信される情報

これらのレポートを生成するため、エンドポイントでは次の種類の情報が Microsoft に送信されます。

- ラベル操作。 ラベルの設定、ラベルの変更、保護の追加または削除、自動ラベルと推奨ラベルなど。

- ラベル操作の前後のラベル名。

- 組織のテナント ID。

- ユーザー ID (電子メール アドレスまたは UPN)。

- ユーザーのデバイスの名前。

- ドキュメントの場合: ラベル付けされているドキュメントのファイル パスとファイル名。

- 電子メールの場合: 電子メールの件名、電子メールの送信者、ラベル付けされた電子メールの受信者。 

- コンテンツ内で検出された機密情報の種類 ([定義済み](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for)およびカスタム)。

- Azure Information Protection クライアントのバージョン。

- クライアント オペレーティング システムのバージョン。

この情報は、自分が所有し、このワークスペースへのアクセス権を持つユーザーが表示できる Azure Log Analytics ワークスペースに格納されます。 ワークスペースに対するアクセスの構成について詳しくは、Azure ドキュメントの「[アカウントとユーザーの管理](/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor#manage-accounts-and-users)」セクションをご覧ください。

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Azure Information Protection 分析の前提条件
Azure Information Protection レポートを表示し、独自のレポートを作成するには、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Log Analytics を含む Azure サブスクリプション|[Azure Log Analytics の価格](https://azure.microsoft.com/pricing/details/log-analytics)ページを参照してください。<br /><br />Azure サブスクリプションをお持ちでない場合、または現在 Azure Log Analytics をご使用でない場合、価格ページには無料試用版へのリンクが含まれます。|
|Azure Information Protection クライアントの現行のプレビュー バージョン。|現行のプレビュー バージョンのクライアントをまだインストールしていない場合は、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードしてインストールできます。|
|**検出とリスク** レポートの場合: <br /><br />- Azure Information Protection スキャナー (現行のプレビュー バージョン) のインスタンスを少なくとも 1 つデプロイしていること|インストール手順については、「[Azure Information Protection スキャナーをデプロイして、ファイルを自動的に分類して保護する](deploy-aip-scanner.md)」を参照してください。 <br /><br />スキャナーの以前のバージョンからアップグレードする場合は、「[Azure Information Protection スキャナーのアップグレード](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を参照してください。|


## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>レポート用に Log Analytics ワークスペースを構成する

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
2. **[管理]** メニュー オプションを探し、**[Configure analytics (Preview)]\(分析の構成 (プレビュー)\)** を選択します。

3. **[Azure Information Protection ログ分析]** ブレードには、テナントによって所有されているすべての Log Analytics ワークスペースの一覧が表示されます。 以下のいずれかを実行します。
    
    - 新しい Log Analytics ワークスペースを作成するには、**[新しいワークスペースの作成]** を選択し、**[Log Analytics ワークスペース]** ブレードで、要求された情報を指定します。
    
    - 既存の Log Analytics ワークスペースを使用するには、一覧からワークスペースを選択します。

Log Analytics ワークスペースの作成に関する情報については、「[Azure ポータルで Log Analytics ワークスペースを作成する](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace)」を参照してください。

ワークスペースが構成されている場合は、レポートを表示する準備ができています。

## <a name="how-to-view-the-reports"></a>レポートの表示方法

[Azure Information Protection] ブレードから **[ダッシュボード]** メニュー オプションを探し、次のいずれかのオプションを選択します。

- **使用状況レポート (プレビュー)**: ラベルがどのように使用されているかを確認するには、このレポートを使用します。 

- **データ検出 (プレビュー)**: スキャナーで検出されたファイルに関する情報を表示するには、このレポートを使用します。

## <a name="how-to-modify-the-reports"></a>レポートを変更する方法

ダッシュボードでクエリ アイコンを選択して、**[ログ検索]** ブレードを開きます。 

![Azure Information Protection のレポートをカスタマイズする [Log Analytics] アイコン](./media/log-analytics-icon.png)


Azure Information Protection のログに記録されたデータは、テーブル **InformationProtectionLogs_CL** に格納されます。

## <a name="next-steps"></a>次の手順
レポートの情報を確認した後で、Azure Information Protection ポリシーを変更することがあります。 手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。