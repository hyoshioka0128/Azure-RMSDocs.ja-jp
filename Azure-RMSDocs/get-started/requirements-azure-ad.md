---
# required metadata

title: Azure RMS の要件&#58; Azure AD ディレクトリ | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure RMS の要件: Azure AD ディレクトリ

*適用対象: Azure Rights Management、Office 365*


Azure Rights Management (Azure RMS) を使用するには、Azure AD ディレクトリが必要です。 このディレクトリの組織アカウントを使用して Azure クラシック ポータルにサインインします。ここでは、たとえば、Rights Management テンプレートを構成および管理することができます。

組織の Azure サブスクリプションがまだない場合は、無料試用版にサインアップして取得できます。[Azure の「はじめに」](https://account.windowsazure.com/organization)ページにアクセスし、指示に従ってください。

詳細については、Azure Active Directory ドキュメントの次のリソースを参照してください。

-   [What is Azure AD Directory? (Azure AD ディレクトリとは)](/active-directory/active-directory-whatis)

-   [How Azure subscriptions are associated with Azure Active Directory (Azure サブスクリプションを Azure Active Directory に関連付ける方法)](/active-directory/active-directory-how-subscriptions-associated-directory)

Azure AD ディレクトリをオンプレミス AD フォレストと統合する場合は、「[Integrating your on-premises identities with Azure Active Directory (オンプレミス ID と Azure Active Directory の統合)](/active-directory/active-directory-aadconnect)」を参照してください。

> [!NOTE] AD FS または同等な認証プロバイダーを使用してオンプレミスで認証を行うモバイル デバイスまたは Mac コンピューターの場合:
> 
> -   最小サーバー バージョンの **Windows Server 2012 R2** で AD FS を使用するか、OAuth 2.0 プロトコルをサポートするその他の認証プロバイダーを使用する必要があります。

## 多要素認証 (MFA) と Azure RMS
Azure RMS で多要素認証 (MFA) を使用するには、次のうち 1 つ以上が必要です。

-   Office 2013 (最小バージョン):

    -   Office 2013 をお持ちの場合、[2015 年 6 月 9 日付 Office 2013 用更新プログラム (KB3054853)](https://support.microsoft.com/kb/3054853) を必ずインストールしてください。 この更新プログラムの詳細や、Active Directory 認証ライブラリ (ADAL) を使用した最新の認証による Office 2013 へのサインインの詳細については、Office ブログの「[Office 2013 modern authentication public preview announced (Office 2013 最新認証パブリック プレビューの公開)](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)」を参照してください。

-   Windows 用 Rights Management 共有アプリケーション:

    -   最小バージョン 1.0.1908.0 がインストールされている必要があります。バージョンはコントロール パネルの [プログラムと機能] で確認できます。 共有アプリケーションの詳細については、「[Windows 用 Rights Management 共有アプリケーション](../rms-client/sharing-app-windows.md)」を参照してください。

-   モバイル デバイス用や Mac コンピューター用の Rights Management 共有アプリ:

    -   最新バージョンがインストールされていることを確認してください。 MFA では、2015 の年 9 月以降にリリースされた RMS 共有アプリがサポートされます。

確認後、MFA ソリューションを構成します。

-   Microsoft が管理するテナント (Azure Active Directory または Office 365) の場合:

    -   Azure MFA を構成してユーザー向けに MFA を適用します。 手順については、Multi-Factor Authentication ドキュメントの「[Getting started with Azure Multi-Factor Authentication in the cloud (クラウドでの Azure Multi-Factor Authentication の概要)](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)」を参照してください。

        Azure MFA の詳細については、「[What is Azure Multi-Factor Authentication? (Azure Multi-Factor Authentication とは)](/multi-factor-authentication/multi-factor-authentication)」を参照してください。

-   統合テナント (オンプレミスのフェデレーション サーバー) の場合:

    -   使用しているフェデレーション サーバーを Azure Active Directory または Office 365 向けに構成します。 たとえば AD FS を使用している場合は、TechNet の記事「[AD FS の追加の認証方法の構成](https://technet.microsoft.com/library/dn758113.aspx)」をご覧ください。

        このシナリオの詳細については、Office ブログの「[The Works with Office 365 – Identity program now streamlined (Office 365 の機能 – 合理化された ID プログラム)](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)」を参照してください。

## 次のステップ
その他の要件を確認するには、「[Azure Rights Management の要件](requirements-azure-rms.md)」を参照してください。



<!--HONumber=May16_HO2-->


