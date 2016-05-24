---
# required metadata

title: SDK の優れている点 | Azure RMS
description: このトピックでは、元の Active Directory Rights Management サービス SDK から RMS SDK 2.1 が大幅に改良された点について説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 622D5C6E-07D5-4C71-A99D-9823C1FE6936
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# SDK の優れている点
このトピックでは、権利保護に対応したアプリケーションの作成に必要な開発者の作業量の観点から、元の [Active Directory Rights Management サービス SDK](https://msdn.microsoft.com/library/Cc530379) と比べて Rights Management Services SDK 2.1 が大幅に改良された点について説明します。

**API サーフェス** - バックエンド実装での数多くの細かな作業を抽象化を通じて解放することで、API サーフェスは大幅に削減されました。 API サーフェスの 84 の RMS SDK 用関数のうち、RMS SDK 2.1 に含まれる API 関数は 20 のみです。 ほとんどのアプリケーションに必要なのは、この API サーフェスのごく一部のみです。

**ランプ アップ時間** -RMS SDK 2.1 では、ステップバイステップ ガイドに従って機密性の高いアプリケーションのリソースを識別し、それらを保護する方法を特定できます。 これは、証明書、形式、トポロジの詳細な知識や、マルチスレッドの複雑なコード記述が必要な RMS SDK とは異なります。

**複数のトポロジのサポート** - RMS SDK 2.1 では、コードの書き直しが最小限で済みます。開発者にとって複雑なトポロジを抽象化し、お使いのアプリケーションがすべてのトポロジで動作するようになります。 一方、RMS SDK では、サポートされているすべてのトポロジを理解し、各トポロジに固有のコードを記述してテストする必要がありました。

**将来性** - RMS SDK 2.1 では、権利保護に対応したコードの書き直しを最小限に抑えます。アプリケーションはすべての RMS 環境で動作し、RMS のコア機能が更新されると新しい機能を自動的に活用できるようになります。 AD RMS SDK では、新しい機能を明示的に活用するには、アプリケーションを更新する必要がありました。

**重要な注意事項**  
MSDN ライブラリの元の「[Active Directory Rights Management サービス SDK](https://msdn.microsoft.com/library/Cc530379)」にある全トピックの冒頭には、現在、次のようなサポート ステートメントが記載されています。

AD RMS SDK は Msdrm.dll でクライアントによって公開される機能を活用し、Windows Server 2008、Windows Vista、Windows Server 2008 R2、Windows 7、Windows Server 2012、Windows 8 で使用できます。 今後のバージョンでは変更されるか、利用できなくなる場合もあります。 代わりに、*Msdrm.dll* でクライアントによって公開される機能を活用する、[Active Directory Rights Management サービス SDK 2.1](microsoft-information-protection-and-control-client-portal.md) を使用してください。

 

## 関連項目 ##
* [概要](ad-rms-overview.md)
* [Active Directory Rights Management サービス SDK](https://msdn.microsoft.com/library/Cc530379)
* [Rights Management サービス SDK 2.1](microsoft-information-protection-and-control-client-portal.md)
 

 


<!--HONumber=Apr16_HO4-->


