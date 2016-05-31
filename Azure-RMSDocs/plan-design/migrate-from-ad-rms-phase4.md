---
# required metadata

title: AD RMS から Azure Rights Management への移行 - フェーズ 4 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 移行フェーズ 4 - 移行後のタスク

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*


AD RMS から Azure Rights Management (Azure RMS) への移行フェーズ 4 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Rights Management への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 8. から手順 9. を説明します。.


## 手順 8. AD RMS の使用を停止する

省略可能: サービス接続ポイント (SCP) を Active Directory から削除し、コンピューターがオンプレミス Rights Management インフラストラクチャを検出しないようにします。 これは、レジストリに (たとえば、移行スクリプトを実行して) 構成したリダイレクトのため省略可能です。 サービス接続ポイントを削除するには、[Rights Management Services Administration Toolkit](http://www.microsoft.com/download/details.aspx?id=1479) の AD SCP Register ツールを使用します。.

たとえば、[システム正常性レポートの要求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest テーブル](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)、[保護されたコンテンツへのユーザー アクセスの監査](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)などを調べることによって、AD RMS サーバーのアクティビティを監視します。 RMS クライアントがこれらのサーバーと通信していないこと、およびクライアントが Azure RMS を正常に使用していることを確認できたら、これらのサーバーから AD RMS サーバーの役割を削除できます。 専用のサーバーを使用している場合は、クライアントが Azure RMS を使用しない理由を調査するときにサービスの継続性を確保するように、サーバーの再起動が必要となる報告された問題がないことを確認するあめに、最初にサーバーのシャットダウン期間に警告手順を使用してもかまいません。

AD RMS サーバーの使用を停止した後、Azure クラシック ポータルでテンプレートをレビューして統合しユーザーの選択肢を減らしたり、再構成したり、新しいテンプレートを追加したりできます。 これは、既定のテンプレートを発行する絶好のタイミングでもあります。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。.

## 手順 9.  Azure RMS テナント キーを更新する
これは、AD RMS デプロイで RMS Cryptographic Mode 1 を使用していた場合、移行が完了したときに必要な手順です。キーの更新により RMS Cryptographic Mode 2 を使用する新しいテナント キーが作成されるためです。 Cryptographic Mode 1 での Azure RMS の使用は、移行プロセス中にのみサポートされます。

この手順は省略可能ですが、移行が完了したとき、RMS Cryptographic Mode 2 で実行していた場合でも推奨されます。AD RMS キーに対する潜在的なセキュリティ侵害から Azure RMS テナント キーをセキュリティで保護するのに役立ちます。 Azure RMS テナント キーを更新すると ("キーのローリング" とも呼ばれます)、新しいキーが作成され、元のキーがアーカイブされます。 ただし、キーの移動には数週間かかりすぐには完了しないので、元のキーの侵害が疑われるまで待たず、移行が完了したらすぐに RMS テナント キーを更新してください。

Azure RMS テナント キーを更新するには:

-   RMS テナント キーがマイクロソフト管理の場合:マイクロソフト カスタマー サポート サービス (CSS) を呼び出し、RMS テナント管理者であることを証明します。

-   RMS テナント キーが顧客管理 (BYOK) である場合:BYOK 手順を繰り返して、インターネット経由または手動で新しいキーを生成および作成します。

RMS テナント キーの管理の詳細については、「[Azure Rights Management テナント キーに対する操作](../deploy-use/operations-tenant-key.md)」を参照してください。.

## 次のステップ

移行が完了した後は、[デプロイ ロードマップ](deployment-roadmap.md)を参照して、必要になる可能性があるその他のデプロイ タスクを確認します。



<!--HONumber=Apr16_HO4-->


