---
title: Azure Information Protection クライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection クライアントのリリースの新機能と変更点、サポートのライフサイクル ポリシーについて説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 02/12/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v1client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: abb96a7d86bddea671230fbd033d9c940cf982a3
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2020
ms.locfileid: "79404744"
---
# <a name="azure-information-protection-client-version-release-history-and-support-policy"></a>Azure Information Protection クライアント: バージョン リリース履歴とサポート ポリシー


>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *手順: [Windows 用の Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*



最新の一般公開リリース バージョンと現在のプレビュー バージョン (利用できる場合) を [Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。 

通常、数週間の遅延が発生すると、最新の一般公開バージョンが Microsoft Update カタログにも含まれます。これには、 **Microsoft Azure Information Protection** > **Microsoft Azure Information Protection クライアント**の製品名と、**更新**の分類が含まれます。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「[Azure Information Protection クライアントのアップグレードと保守](client-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-client)」をご覧ください。

> [!TIP]
> ラベルが Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、または Microsoft 365 コンプライアンスセンターから公開されているため、Azure Information Protection 統合ラベルクライアントの使用に関心がある場合は、 Microsoft ダウンロードセンターから、統合されたラベル付けクライアントをダウンロードしてインストールすると、Azure Information Protection クライアントを、統一された[ラベル付けクライアント](unifiedlabelingclient-version-release-history.md)にアップグレードできます。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection クライアントの各一般公開 (GA) バージョンは、後続の GA バージョンがリリースされた後も最長で 6 か月間はサポートされます。 このセクションを除き、ドキュメントにはサポートされていないバージョンのクライアントに関する情報は含まれていません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアント バージョン|リリース日|
|--------------|-------------|
|1.48.204.0|04/16/2019|
|1.41.51.0|2018 年 11 月 27 日|
|1.37.19.0|2018 年 9 月 17 日|
|1.29.5.0|2018 年 6 月 26 日|
|1.27.48.0|2018 年 5 月 30 日|
|1.26.6.0|04/17/2018|
|1.10.56.0|09/18/2017|
|1.7.210.0|06/06/2017|
|1.4.21.0|03/15/2017|
|1.3.155.2|02/08/2017|
|1.2.4.0.0|10/27/2016|
|1.1.23.0|10/01/2016|

このページで使用される日付形式は、*月/日/年*です。

6/2/2019 以降、Azure Information Protection のラベル付けサービスには、TLS 1.2 を使用する接続が必要です。

1\.4.21.0 リリース03/15/2017 のすべてのクライアントバージョンが TLS 1.2 をサポートしています。 クライアントバージョン**1.3.155.2**、 **1.2.4.0**、および**1.1.23.0**は TLS 1.2 を使用しないため、Azure Information Protection ポリシーをダウンロードできなくなります。

### <a name="release-history"></a>リリース履歴

Windows 用 Azure Information Protection クライアントのサポートされるリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。

> [!NOTE]
> 細かい修正点は記載されていないので、Azure Information Protection クライアントで問題が発生した場合は、最新の GA リリースで問題が修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

## <a name="version-154590"></a>バージョン1.54.59.0

**リリース**日: 12/02/2020

このバージョンには、修正プログラムのみが含まれています。 

**修正内容**:

- 保護が削除された後に、IQP によって保護されているファイルが **回復** オプションまたは 保存 オプションを選択**して**解決される問題。 

- わかりやすく、理解しやすいように、多くの製品機能のツールヒントが改善されました。 

- 保護された PDF ファイルを操作するときに、クライアントの安定性に関連する問題が解決されます。 

- 電子メールの作成プロセス中に電子メールでラベルが削除されると、保護ラベルが期待どおりに削除されるようになりました。 

## <a name="version-154330"></a>バージョン1.54.33.0

**リリース**日: 10/23/2019

08/12/2020 でサポート

このバージョンには、RMS クライアントの MSIPC バージョン1.0.4008.0813 が含まれています。

このリリースには、安定性とパフォーマンスに関する一般的な修正が含まれています。

## <a name="version-153100"></a>バージョン1.53.10.0

**リリース**日: 07/15/2019

04/23/2020 でサポート

このバージョンには、RMS クライアントの MSIPC バージョン1.0.3889.0419 が含まれています。

**新機能:**

- ポリシー設定から Outlook メッセージを除外する新しい高度なクライアント設定**すべてのドキュメントと電子メールにラベルを付ける必要があり**ます。 [詳細情報](client-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)

- 新しい高度なクライアント設定。 Outlook でポップアップメッセージを実装する設定をカスタマイズして、送信される電子メールを警告、ブロック、またはブロックします。 この新しい詳細設定では、添付ファイルのない電子メールメッセージに対して別のアクションを設定できます。 [詳細情報](client-admin-guide-customizations.md#to-specify-a-different-action-for-email-messages-without-attachments)

**修正内容**:

- エクスプローラーを使用する場合、右クリックすると、保護がラベルとは別に適用されているファイルにラベルを付けることができます。 たとえば、ユーザーがファイルにカスタムアクセス許可を適用したとします。

- 電子メールスレッドの [転送不可] オプションを、ユーザー定義のアクセス許可用に構成され、転送しないラベルに置き換えると、元の受信者は引き続き電子メールメッセージを開くことができます。

- 次のシナリオでは、ラベルが自動的に設定されたというラベルのツールヒントにユーザーが表示されなくなりました。ユーザーは、ラベルが付けられていないが自動的に保護されたドキュメントを添付して、保護された電子メールを受け取ります。 差出人と同じ組織のユーザーがドキュメントを開くと、保護設定の対応するラベルがドキュメントに適用されます。

- [Protect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile)コマンドレットを実行するための最小[使用権限](../configure-usage-rights.md#usage-rights-and-descriptions)は、**コピー** (EXTRACT) ではなく **、名前を付けて保存、エクスポート**(エクスポート) されるようになりました。

## <a name="next-steps"></a>次のステップ:

インストールするクライアントが適切かどうかは確認できません。  「 [Windows コンピューターに使用するラベル付けクライアントを選択](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

クライアントのインストールと使用の詳細: 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-client-app.md)

- 管理者向け: [Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)
