---
title: "AIP の Azure Active Directory の要件"
description: "ユーザーを正常に認証できるように、Azure Information Protection を使用するための Azure AD の要件を特定します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/01/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2022f86a32725ef9dfcf5692b1194348f6c39f3b
ms.sourcegitcommit: b471c20eda011a7b75ee801c34081fb4773b64dc
ms.translationtype: HT
ms.contentlocale: ja-JP
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Azure Information Protection の Azure Active Directory の要件

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection を使用するには、Azure AD ディレクトリが必要です。 このディレクトリの組織アカウントを使用して Azure クラシック ポータルにサインインします。ここでは、たとえば、Rights Management テンプレートを構成および管理することができます。

組織の Azure サブスクリプションがまだない場合は、無料試用版にサインアップして取得できます。 「[Azure - はじめに](https://account.windowsazure.com/organization)」ページにアクセスし、指示に従ってください。

詳細については、Azure Active Directory ドキュメントの次のリソースを参照してください。

-   [Azure AD ディレクトリとは](/active-directory/active-directory-whatis)

-   [Azure サブスクリプションを Azure Active Directory に関連付ける方法](/active-directory/active-directory-how-subscriptions-associated-directory)

Azure AD ディレクトリをオンプレミス AD フォレストと統合する場合は、「[Integrating your on-premises identities with Azure Active Directory (オンプレミス ID と Azure Active Directory の統合)](/active-directory/active-directory-aadconnect)」を参照してください。

### <a name="scenarios-that-have-specific-requirements"></a>特定の要件があるシナリオ 

Office 2010 を実行しているコンピューターの場合: 

- Azure Information Protection とそのデータ保護サービスである Azure Rights Management に対して認証を行うには、これらのコンピューターに [Azure Information Protection クライアント](../rms-client/aip-client.md) (推奨) または [Windows 用 Rights Management 共有アプリケーション](../rms-client/sharing-app-windows.md) が必要です。

- ユーザー アカウントがフェデレーションされる (たとえば、AD FS を使用する) 場合、Windows 統合認証を使用する必要があります。 このシナリオでのフォーム ベース認証は、Azure Information Protection のユーザー認証に失敗します。

証明書ベースの認証 (CBA) のサポート: 

- Android 5.0 以上のバージョンをご使用の場合、Android 用 Azure Information Protection アプリは証明書ベースの認証をサポートします。 証明書ベースの認証を構成する手順については、[「Azure Active Directory の証明書ベースの認証の概要」](/azure/active-directory/active-directory-certificate-based-authentication-get-started) を参照してください。

ユーザーの UPN 値がユーザーの電子メール アドレスと一致しない：

- これは、お勧めの構成ではありません。UPN 値を変更できない場合は、ユーザーの代替ログイン ID を構成し、この代替ログインを使用して Office にサインインする方法をユーザーに指示してください。 詳細については、「[代替ログイン ID を構成する](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)」と「[Office applications periodically prompt for credentials to SharePoint Online, OneDrive, and Lync Online (Office アプリケーションは SharePoint のオンライン、OneDrive、 Lync オンラインの資格情報を定期的に要求する)](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)」をご覧ください。
    
    UPN 値内のドメイン名が、テナントを確認するためのドメインである場合は、ユーザーの UPN 値を別の電子メール アドレスとして Azure AD proxyAddresses 属性に追加します。 これにより、使用権限が与えられる時点でユーザーの UPN 値が指定されている場合は、このユーザーの Azure Rights Management が承認されます。 この要件に関する詳細とユーザー アカウントの承認方法については、「[Azure Information Protection 向けのユーザーとグループの準備](../plan-design/prepare.md)」をご覧ください。

AD FS または同等な認証プロバイダーを使用してオンプレミスで認証を行うモバイル デバイスまたは Mac コンピューターの場合:

- 最小サーバー バージョンの **Windows Server 2012 R2** で AD FS を使用するか、OAuth 2.0 プロトコルをサポートするその他の認証プロバイダーを使用する必要があります。

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多要素認証 (MFA) と Azure Information Protection
Azure Information Protection で多要素認証 (MFA) を使用するには、次のうち 1 つ以上が必要です。

-   Office 2013 (最小バージョン):

    -   Office 2013 をご使用の場合に Active Directory Authentication Library (ADAL) をサポートするには、追加の更新プログラムのインストールが必要な場合があります。 たとえば、[Office 2013 用の更新プログラム (KB3054853) (2015 年 6 月 9 日)](https://support.microsoft.com/kb/3054853) です。 この更新プログラムの詳細や、Active Directory 認証ライブラリ (ADAL) を使用した最新の認証による Office 2013 へのサインインの詳細については、Office ブログの「[Office 2013 modern authentication public preview announced (Office 2013 最新認証パブリック プレビューの公開)](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)」を参照してください。

- Azure Information Protection クライアント:

    - Windows、iOS および Android 用の [Azure Information Protection クライアント](../rms-client/aip-client.md)では、常に、MFA がサポートされており、最小バージョンは不要です。 

-   Windows 用 Rights Management 共有アプリケーション:

    -   最小バージョン 1.0.1908.0 がインストールされている必要があります。バージョンはコントロール パネルの [プログラムと機能] で確認できます。 現在、Rights Management 共有アプリケーションは Azure Information Protection クライアントに置き換わっていることに注意してください。 共有アプリケーションの詳細については、[「Windows 用 Rights Management 共有アプリケーション」](../rms-client/sharing-app-windows.md) を参照してください。

-   モバイル デバイス用や Mac コンピューター用の Rights Management 共有アプリ:

    -   最新バージョンがインストールされていることを確認してください。 MFA では、2015 の年 9 月以降にリリースされた RMS 共有アプリがサポートされます。

確認後、MFA ソリューションを構成します。

-   Microsoft が管理するテナント (Azure Active Directory または Office 365) の場合:

    -   Azure MFA を構成してユーザー向けに MFA を適用します。 手順については、Multi-Factor Authentication ドキュメントの「[Getting started with Azure Multi-Factor Authentication in the cloud (クラウドでの Azure Multi-Factor Authentication の概要)](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)」を参照してください。

        Azure MFA の詳細については、「[What is Azure Multi-Factor Authentication? (Azure Multi-Factor Authentication とは)](/multi-factor-authentication/multi-factor-authentication)」を参照してください。

-   統合テナント (オンプレミスのフェデレーション サーバー) の場合:

    -   使用しているフェデレーション サーバーを Azure Active Directory または Office 365 向けに構成します。 たとえば AD FS を使用している場合は、TechNet の記事「[AD FS の追加の認証方法の構成](https://technet.microsoft.com/library/dn758113.aspx)」をご覧ください。

        このシナリオの詳細については、Office ブログの「[The Works with Office 365 – Identity program now streamlined (Office 365 の機能 – 合理化された ID プログラム)](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)」を参照してください。

## <a name="next-steps"></a>次のステップ
その他の要件を確認するには、「[Azure Information Protection の要件](requirements-azure-rms.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
