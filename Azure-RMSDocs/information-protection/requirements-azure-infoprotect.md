---
title: "Azure Information Protection の要件 | Azure Information Protection"
description: "Azure Information Protection のプレビュー リリースを評価するために必要な前提条件を確認してください。"
author: cabailey
manager: mbaldwin
ms.date: 08/29/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: aa4353e5-c5b0-47f6-a6f9-87d13e8f075f
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: b9bb97e075e569e54e535c921c5d1db77200b20c


---

# Azure Information Protection の要件

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

Azure Information Protection のプレビュー リリースを評価するには、次の前提条件が満たされていることを確認してください。 

|要件|詳細情報|
|---------------|--------------------|
|Azure Rights Management を含む Office 365 のサブスクリプション|たとえば、Office 365 E3、E4、または E5 のサブスクリプションです。<br /><br />使用できるサブスクリプション オプションの詳細と無料試用版へのリンクについては、Azure RMS の要件に関するドキュメントの「[Office 365 サブスクリプション](../get-started/requirements-subscriptions.md#office-365-subscription)」セクションを参照してください。|
|Azure AD ディレクトリ|組織には Azure RMS および Azure Information Protection のユーザー認証をサポートするための Azure AD ディレクトリが必要です。 また、オンプレミスのディレクトリ (AD DS) のユーザー アカウントを使用する場合は、ディレクトリ統合も構成する必要があります。<br /><br />必要なクライアント ソフトウェアと正しく構成された MFA サポート インフラストラクチャがある場合は、Azure RMS で Multi-Factor Authentication (MFA) がサポートされます。<br /><br />詳細については、「[Azure AD ディレクトリ](../get-started/requirements-azure-ad.md)」を参照してください。Azure RMS についての情報は Azure Information Protection にも当てはまります。|
|クライアント デバイス|このプレビューでは、次のクライアント デバイスがサポートされます。<br /><br />- Windows 10 (x86、x64)<br /><br />- Windows 8.1 (x86、x64)<br /><br />- Windows 8 (x86、x64)<br /><br />- Windows 7 Service Pack 1 (x86、x64)<br /><br />データを保護する場合、Azure Rights Management をサポートする同じデバイス (Windows、Mac、iOS、Android) でデータを使用できます。 デバイスおよびサポートされるバージョンの詳細は、「[Azure RMS の要件: Azure RMS をサポートするクライアント デバイス](../get-started/requirements-client-devices.md)」を参照してください。|
|アプリケーション|プレビュー リリースおよび一般公開 (GA) では、Azure Information Protection は次の Office スイートの Office アプリケーション **Word**、**Excel**、**PowerPoint**、**Outlook** で作成されたファイルと電子メールのラベル付けと保護をサポートします。<br /><br />- Office Professional Plus 2016<br /><br />- Office Professional Plus 2013 Service Pack 1<br /><br />- Office Professional Plus 2010<br /><br />一般公開の後、PDF、オーディオ、ビデオ、画像などの他のファイル タイプを Azure Information Protection がサポートするようになる時期については、[Enterprise Mobility and Security のブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)で確認してください。|
|インターネットと依存クラウド サービスへの接続をサポートするインフラストラクチャ|特定の接続を許可するように構成する必要があるファイアウォールまたは同様の介在するネットワーク デバイスがある場合は、Office 記事「[Office 365 URL および IP アドレス範囲](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)」の「[Office 365 ポータルと共有](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#BKMK_Portal-identity)」セクションで **Azure Rights Management (RMS)** に関する情報を参照してください。<br /><br />さらに<br /><br />- **api.informationprotection.azure.com** TCP 443 の HTTPS トラフィックを許可します。<br /><br />- TLS クライアント/サービス間接続を終了しないでください (たとえばパケット レベルの検査を行うために)。 <br /><br />- 認証が必要な Web プロキシを使用している場合には、ユーザーの Active Directory ログオン資格情報による統合 Windows 認証を使用するようにプロキシを構成する必要があります。|

## 次のステップ

これらの要件が満たされたなら、自習デモ「[Quick start tutorial for Azure Information Protection](infoprotect-quick-start-tutorial.md)」 (Azure Information Protection クイック スタート チュートリアル) を参考にして Azure Information Protection を構成し、使ってみてください。




<!--HONumber=Sep16_HO1-->


