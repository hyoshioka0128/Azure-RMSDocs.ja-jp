---
title: Azure AD と Azure Information Protection の追加の前提条件
description: Multi-factor authentication、証明書ベースの認証、Office 2010 を使用するコンピューターなど、特定のシナリオで Azure Information Protection を Azure AD するための追加の前提条件について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/22/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin, has-adal-ref
ms.openlocfilehash: cc58a32da1bca1ce14704e0eb23ebbd0007073f7
ms.sourcegitcommit: 0793013ad733ac2af5de498289849979501b8f6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88788970"
---
# <a name="additional-azure-ad-requirements-for-azure-information-protection"></a>Azure Information Protection に関する追加の Azure AD 要件

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information protection を使用するに [は、Azure AD ディレクトリが必要](requirements.md#azure-active-directory) です。 Azure AD ディレクトリのアカウントを使用して Azure portal にサインインし、Azure Information Protection 設定を構成できます。

Azure Information Protection または Azure Rights Management を含むサブスクリプションをお持ちの場合は、必要に応じて Azure AD ディレクトリが自動的に作成されます。

次のセクションでは、特定のシナリオに関する追加の AIP と Azure AD の要件について説明します。 

## <a name="computers-running-office-2010"></a>Office 2010 を実行しているコンピューター

Microsoft Office 2010 を実行しているコンピューターでは Azure AD アカウントに加えて、Azure Information Protection とそのデータ保護サービスである Azure Rights Management に対して認証を行うために、Azure Information Protection の統一された [ラベル付けクライアント](./rms-client/aip-clientv2.md) または [Azure Information Protection クラシッククライアント](./rms-client/aip-client.md) が必要です。

ユーザーアカウントがフェデレーションされている場合 (たとえば、AD FS を使用する場合)、これらのコンピューターは Windows 統合認証を使用する必要があります。 このシナリオでのフォーム ベース認証は、Azure Information Protection のユーザー認証に失敗します。

## <a name="support-for-certificate-based-authentication-cba"></a>証明書ベースの認証 (CBA) のサポート

iOS および Android 用の Azure Information Protection アプリでは、証明書ベースの認証をサポートしています。 

詳細については、「 [Azure Active Directory で証明書ベースの認証の使用を開始](/azure/active-directory/active-directory-certificate-based-authentication-get-started)する」を参照してください。

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多要素認証 (MFA) と Azure Information Protection

Azure Information Protection で multi-factor authentication (MFA) を使用するには、次のうち少なくとも1つがインストールされている必要があります。

- **Microsoft Office、** バージョン2013以降
- **AIP クライアント**。 最小バージョンは必要ありません。 AIP clients for Windows、および iOS および Android 用のビューアーアプリはすべて MFA をサポートしています。
- **Mac コンピューター用の Rights Management 共有アプリ**。 RMS 共有アプリでは、2015年9月のリリース以降、MFA がサポートされています。

> [!NOTE]
> Office 2013 を使用している場合は、Active Directory 認証ライブラリ (ADAL) をサポートするための追加の更新プログラムをインストールすることが必要になる場合があります。 [たとえば、June 9、2015、update For Office 2013 (KB3054853)](https://support.microsoft.com/kb/3054853)などです。 
>
> 詳細については、Office ブログの「 [office 2013 先進認証のパブリックプレビュー](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) 」を参照してください。       

これらの前提条件を確認したら、テナントの構成に応じて、次のいずれかの操作を行います。

- **Azure AD または Office 365 を使用した Microsoft が管理するテナント**。 Azure MFA を構成してユーザー向けに MFA を適用します。 

    詳細については、次を参照してください: 
    - [クラウドでの Azure Multi-Factor Authentication Server の概要](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)
    - [Azure Multi-Factor Authentication とは](/multi-factor-authentication/multi-factor-authentication)

- フェデレーション**テナント。フェデレーションサーバーはオンプレミスで動作**します。 使用しているフェデレーション サーバーを Azure Active Directory または Office 365 向けに構成します。 たとえば、AD FS を使用する場合は、「 [AD FS の追加の認証方法を構成](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)する」を参照してください。 

    このシナリオの詳細については、Office ブログの「  [Works With office 365 – Identity program が合理化](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) されました。」を参照してください。 

## <a name="rights-management-connector--aip-scanner-requirements"></a>Rights Management connector/AIP スキャナの要件

Rights Management コネクタおよび Azure Information Protection スキャナーでは、MFA はサポートされません。 

コネクタまたはスキャナーをデプロイする場合は、次のアカウントで MFA を要求することはできません。

- コネクタをインストールおよび構成するアカウント。
- コネクタが作成する、Azure AD のサービス プリンシパル アカウント (**Aadrm_S-1-7-0**)。
- スキャナーを実行するサービス アカウント。

## <a name="user-upn-values-dont-match-their-email-addresses"></a>ユーザー UPN の値が電子メールアドレスと一致しません

ユーザーの UPN 値が電子メールアドレスと一致しない構成は、推奨される構成ではなく、Azure Information Protection のシングルサインオンをサポートしていません。

UPN 値を変更できない場合は、関連するユーザーの代替 Id を構成し、この代替 ID を使用して Office にサインインする方法を指示します。 

詳細については、次を参照してください:

- [代替ログイン ID を構成する](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)
- [Office アプリケーションは、SharePoint、OneDrive、および Lync Online の資格情報を定期的に要求](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)します。

> [!TIP]
> UPN 値のドメイン名がテナントに対して検証されたドメインである場合は、ユーザーの UPN 値を別の電子メールアドレスとして Azure AD **proxyAddresses** 属性に追加します。 これにより、使用権限が付与された時点で UPN 値が指定されている場合に、ユーザーに Azure Rights Management の承認を与えることができます。 

詳細については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

## <a name="authenticating-on-premises-using-adfs-or-another-authentication-provider"></a>AD FS または別の認証プロバイダーを使用したオンプレミスの認証

AD FS または同等の認証プロバイダーを使用してオンプレミスで認証を行うモバイルデバイスまたは Mac コンピューターを使用している場合は、次のいずれかの構成で AD FS を使用する必要があります。

- **Windows server 2012 R2**の最小サーバーバージョン
- OAuth 2.0 プロトコルをサポートする代替の認証プロバイダー

## <a name="next-steps"></a>次のステップ
その他の要件を確認するには、「[Azure Information Protection の要件](requirements.md)」をご覧ください。
