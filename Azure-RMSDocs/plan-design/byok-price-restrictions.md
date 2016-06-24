---
# required metadata

title: BYOK の料金と制限事項 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# BYOK の料金と制限事項

*適用対象: Azure Rights Management、Office 365*


IT 部門が管理する Azure サブスクリプションを持つ組織は無料で BYOK を使用でき、その使用状況をログに記録できます。 個人用 RMS を使用する組織は BYOK やログを構成するテナント管理者がいないので、これらの機能を使用できません。


> [!NOTE]
> 個人用 RMS の詳細については、「[個人向け RMS と Microsoft Azure Rights Management](../understand-explore/rms-for-individuals.md)」を参照してください。.

![BYOK は Exchange Online をサポートしていません](../media/RMS_BYOK_noExchange.png)

BYOK とログは、Azure RMS と統合されたすべてのアプリケーションでシームレスに動作します。 これには SharePoint Online などのクラウド サービス、Exchange や SharePoint を実行し、RMS コネクタを使用して Azure RMS と連携するオンプレミス サーバー、Office 2013 などのクライアント アプリケーションが含まれます。 どのアプリケーションが Azure RMS のリクエストを作成するかにかかわらず、キー利用状況ログを取得できます。

例外が 1 つあります。現時点では、 **Azure RMS BYOK には Exchange Online との互換性がありません**。  Exchange Online を使用する場合、Azure RMS のデプロイは既定のキー管理モードのままにして、キーの作成と管理をマイクロソフトで行うことをお勧めします。 こうすれば、たとえば Exchange Online が Azure RMS BYOK をサポートする場合など、後で BYOK に変更できます。 ただし、すぐに必要な場合は、Azure RMS を BYOK でデプロイして、Exchange Online 用の RMS 機能を制限付きで使用することもできます (保護されていない電子メールと保護されていない添付ファイルは引き続き完全に機能します)。

-   Outlook Web Access の保護された電子メールや保護された添付ファイルは表示できません。

-   Exchange ActiveSync IRM を使用するモバイル デバイス上の保護された電子メールは表示できません。

-   トランスポート復号化 (たとえば、マルウェアのスキャンなど)、およびジャーナルの復号化を行うことはできません。そのため、保護された電子メールと保護された添付ファイルはスキップされます。

-   IRM ポリシーを適用するトランスポート保護ルールとデータ損失防止 (DLP) を使用することはできません。そのため、これらの方法を使用して RMS 保護を適用することはできません。

-   サーバーベースで保護された電子メールが検索されます。そのため、保護された電子メールはスキップされます。

Exchange Online 用に制限された RMS 機能を使用して Azure RMS BYOK を使用する場合、RMS は Windows の Outlook および Mac の電子メール クライアント、および Exchange ActiveSync IRM を使用していないその他の電子メール クライアントで動作します。

AD RMS から Azure RMS に移行している場合は、信頼された発行ドメイン (TPD) として (これは Exchange 用語での BYOK で、Azure RMS BYOK とは別のものです)、キーを Exchange Online にインポートしています。 この場合、Exchange Online から TPD を削除して、テンプレートとポリシーの競合を防ぐ必要があります。 詳細については、Exchange Online コマンドレット ライブラリの「[Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx)」を参照してください。

場合によっては、Exchange Online の Azure RMS BYOK の例外は、実際には問題にならないこともあります。 たとえば、BYOK とログ作成を必要とする組織は、データ アプリケーション (Exchange、SharePoint、Office) をオンプレミスで実行し、Azure RMS を使用するのは、オンプレミス AD RMS では簡単に使用できない機能 (他社とのコラボレーションやモバイル クライアントからのアクセスなど) を使用するためです。 BYOK とログ作成はこのシナリオで問題なく動作し、組織は Azure RMS サブスクリプションを完全に制御できます。

## 次のステップ

独自のキーを管理する場合は、「[Azure Rights Management テナント キーの実装](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key)」を参照してください。.

テナント キーを Microsoft が管理する既定の構成を使用する場合は、「Azure Rights Management テナント キーを計画して実装する」の「[次のステップ](plan-implement-tenant-key.md#next-steps)」セクションを参照してください。



<!--HONumber=Apr16_HO4-->


