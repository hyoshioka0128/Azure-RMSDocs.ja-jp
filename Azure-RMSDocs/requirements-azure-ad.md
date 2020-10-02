---
title: Azure AD および Azure Information Protection の追加の前提条件
description: 多要素、または証明書ベースの認証、Office 2010 を使用するコンピューターなど、特定のシナリオでの Azure Information Protection に対する Azure AD の追加要件について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/22/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: 858a2ebb1bbc5040d564d9df05943c10a3f58a4a
ms.sourcegitcommit: 24c97b58849af4322d3211b8d3165734d5ad6c88
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91428357"
---
# <a name="additional-azure-ad-requirements-for-azure-information-protection"></a>Azure Information Protection に対する Azure AD の追加要件

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information protection を使用するには、[Azure AD が必要](requirements.md#azure-active-directory)です。 Azure AD ディレクトリのアカウントを使用して Azure portal にサインインし、Azure Information Protection の設定を構成できます。

Azure Information Protection または Azure Rights Management を含むサブスクリプションをお持ちの場合は、必要に応じて Azure AD ディレクトリが自動的に作成されます。

次のセクションでは、特定のシナリオに関する追加の AIP と Azure AD の要件について説明します。 

## <a name="computers-running-office-2010"></a>Office 2010 を実行しているコンピューター

Azure AD アカウントに加えて Microsoft Office 2010 を実行しているコンピューターでは、Azure Information Protection とそのデータ保護サービス、Azure Rights Management を認証するために [Azure Information Protection 統合ラベル付けクライアント](./rms-client/aip-clientv2.md)または [Azure Information Protection クラシック クライアント](./rms-client/aip-client.md)が必要です。

ユーザー アカウントがフェデレーションされる (たとえば、AD FS を使用する) 場合、これらのコンピューターで Windows 統合認証を使用する必要があります。 このシナリオでのフォーム ベース認証は、Azure Information Protection のユーザー認証に失敗します。

## <a name="support-for-certificate-based-authentication-cba"></a>証明書ベースの認証 (CBA) のサポート

iOS および Android 用の Azure Information Protection アプリでは、証明書ベースの認証をサポートしています。 

詳細については、「[Azure Active Directory の証明書ベースの認証の概要](/azure/active-directory/active-directory-certificate-based-authentication-get-started)」を参照してください。

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多要素認証 (MFA) と Azure Information Protection

Azure Information Protection で多要素認証 (MFA) を使用するには、次のうち 1 つ以上をインストールする必要があります。

- **Microsoft Office** バージョン 2013 以降
- **AIP クライアント**。 必要最小バージョンはありません。 AIP clients for Windows、および iOS と Android 用のビューアー アプリはすべて MFA をサポートしています。
- **Mac コンピューター用の Rights Management 共有アプリケーション**。 Microsoft Rights Management 共有アプリケーションでは、2015 年 9 月のリリース以降、MFA がサポートされています。

> [!NOTE]
> Office 2013 をご使用の場合に Active Directory Authentication Library (ADAL) をサポートするには、[Office 2013 (KB3054853) の 2015 年 6 月 9 日更新](https://support.microsoft.com/kb/3054853)のような追加の更新プログラムのインストールが必要な場合があります。 
>
> 詳細については、Office ブログの「[Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)」(Office 2013 先進認証のパブリック プレビューが発表されました) を参照してください。       

これらの前提条件を確認したら、テナントの構成に応じて、次のいずれかを行います。

- **Azure AD または Microsoft 365 を使用した Microsoft が管理するテナント**。 Azure MFA を構成してユーザー向けに MFA を適用します。 

    詳細については、次を参照してください。 
    - [クラウドでの Azure Multi-Factor Authentication Server の概要](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)
    - [Azure Multi-Factor Authentication とは](/multi-factor-authentication/multi-factor-authentication)

- **フェデレーション サーバーがオンプレミスで実行されているフェデレーション テナント**。 使用しているフェデレーション サーバーを Azure Active Directory または Microsoft 365 向けに構成します。 たとえば AD FS を使用している場合は、「[AD FS の追加の認証方法の構成](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)」を参照してください。 

    このシナリオの詳細については、Office ブログの「[The Works with Microsoft 365 – Identity program now streamlined](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)」(Microsoft 365 の機能 – 合理化された ID プログラム) を参照してください。 

## <a name="rights-management-connector--aip-scanner-requirements"></a>Rights Management コネクタ/AIP スキャナの要件

Rights Management コネクタおよび Azure Information Protection スキャナーでは、MFA はサポートされません。 

コネクタまたはスキャナーをデプロイする場合は、次のアカウントで MFA を要求することはできません。

- コネクタをインストールおよび構成するアカウント。
- コネクタが作成する、Azure AD のサービス プリンシパル アカウント (**Aadrm_S-1-7-0**)。
- スキャナーを実行するサービス アカウント。

## <a name="user-upn-values-dont-match-their-email-addresses"></a>ユーザーの UPN 値がユーザーのメール アドレスと一致しない

ユーザーの UPN 値がユーザーのメール アドレスと一致しない構成は、推奨される構成ではなく、Azure Information Protection のシングル サインオンをサポートしていません。

UPN 値を変更できない場合は、関連するユーザーの代替 ID を構成し、この代替 ID を使用して Office にサインインする方法をユーザーに指示してください。 

詳細については、次を参照してください。

- [代替ログイン ID を構成する](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)
- [Office アプリケーションが SharePoint、OneDrive、Lync Online の資格情報を定期的に要求する](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)。

> [!TIP]
> UPN 値内のドメイン名が、テナントを確認するためのドメインである場合は、ユーザーの UPN 値を別の電子メール アドレスとして Azure AD **proxyAddresses** 属性に追加します。 これにより、使用権限が与えられる時点でユーザーの UPN 値が指定されている場合は、このユーザーの Azure Rights Management が承認されます。 

詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

## <a name="authenticating-on-premises-using-adfs-or-another-authentication-provider"></a>AD FS または別の認証プロバイダーを使用したオンプレミスの認証

AD FS または同等の認証プロバイダーを使用してオンプレミスで認証を行うモバイル デバイスまたは Mac コンピューターを使用している場合は、次のいずれかの構成で AD FS を使用する必要があります。

- **Windows Server 2012 R2** の最小サーバー バージョン
- OAuth 2.0 プロトコルをサポートする代替の認証プロバイダー

## <a name="next-steps"></a>次の手順
その他の要件を確認するには、「[Azure Information Protection の要件](requirements.md)」をご覧ください。
