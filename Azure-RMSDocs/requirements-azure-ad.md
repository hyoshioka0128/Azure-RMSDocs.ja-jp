---
title: Azure Information Protection に対する Azure AD の要件 - AIP
description: ユーザーを正常に認証できるように、Azure Information Protection を使用するための Azure AD の要件を特定します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.subservice: prereqs
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6a3ed3272eecd25bd403d6a45a82f937fe26a03a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "72890280"
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Azure Information Protection の Azure Active Directory の要件

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection を使用するには、Azure AD ディレクトリが必要です。 このディレクトリのアカウントを使用して Azure Portal にサインインします。ここでは、たとえば、Azure Information Protection ラベルや Rights Management テンプレートを構成し、管理できます。

Azure Information Protection または Azure Rights Management を含むサブスクリプションをお持ちの場合は、必要に応じて Azure AD ディレクトリが自動的に作成されます。  

Azure AD の詳細については、「[Azure Active Directory とは](/azure/active-directory/fundamentals/active-directory-whatis)」をご覧ください。

Azure AD ディレクトリをオンプレミス AD フォレストと統合するには、「[オンプレミスの Active Directory ドメインと Azure Active Directory を統合する](/azure/architecture/reference-architectures/identity/azure-ad)」をご覧ください。

### <a name="scenarios-that-have-specific-requirements"></a>特定の要件があるシナリオ 

Office 2010 を実行しているコンピューターの場合: 

- これらのコンピューターでは、Azure Information Protection 統合された[ラベル付けクライアント](./rms-client/aip-clientv2.md)または[Azure Information Protection クライアント](./rms-client/aip-client.md)が Azure Information Protection とそのデータ保護サービスである Azure Rights Management に対して認証を行う必要があります。

- ユーザー アカウントがフェデレーションされる (たとえば、AD FS を使用する) 場合、Windows 統合認証を使用する必要があります。 このシナリオでのフォーム ベース認証は、Azure Information Protection のユーザー認証に失敗します。

証明書ベースの認証 (CBA) のサポート:

- iOS および Android 用の Azure Information Protection アプリでは、証明書ベースの認証をサポートしています。 証明書ベースの認証を構成する手順については、[「Azure Active Directory の証明書ベースの認証の概要」](/azure/active-directory/active-directory-certificate-based-authentication-get-started) を参照してください。

ユーザーの UPN 値がユーザーの電子メール アドレスと一致しない：

- これは推奨される構成ではなく、Azure Information Protection のシングルサインオンをサポートしていません。 UPN 値を変更できない場合は、ユーザーの代替ログイン ID を構成し、この代替ログインを使用して Office にサインインする方法をユーザーに指示してください。 詳細については、「[代替ログイン ID を構成する](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id)」と「[Office applications periodically prompt for credentials to SharePoint Online, OneDrive, and Lync Online (Office アプリケーションは SharePoint のオンライン、OneDrive、 Lync オンラインの資格情報を定期的に要求する)](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online)」をご覧ください。
    
    UPN 値内のドメイン名が、テナントを確認するためのドメインである場合は、ユーザーの UPN 値を別の電子メール アドレスとして Azure AD proxyAddresses 属性に追加します。 これにより、使用権限が与えられる時点でユーザーの UPN 値が指定されている場合は、このユーザーの Azure Rights Management が承認されます。 この要件に関する詳細とユーザー アカウントの承認方法については、「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

AD FS または同等の認証プロバイダーを使用してオンプレミスで認証を行うモバイル デバイスまたは Mac コンピューターの場合:

- 最小サーバー バージョンの **Windows Server 2012 R2** で AD FS を使用するか、OAuth 2.0 プロトコルをサポートするその他の認証プロバイダーを使用する必要があります。

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>多要素認証 (MFA) と Azure Information Protection
Azure Information Protection で多要素認証 (MFA) を使用するには、次のうち 1 つ以上が必要です。

-   Office 2013 (最小バージョン):

    -   Office 2013 をご使用の場合に Active Directory Authentication Library (ADAL) をサポートするには、追加の更新プログラムのインストールが必要な場合があります。 たとえば、[Office 2013 用の更新プログラム (KB3054853) (2015 年 6 月 9 日)](https://support.microsoft.com/kb/3054853) です。 この更新プログラムの詳細や、Active Directory 認証ライブラリ (ADAL) を使用した最新の認証による Office 2013 へのサインインの詳細については、Office ブログの「[Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)」(Office 2013 最新認証パブリック プレビューの公開) を参照してください。

- Azure Information Protection クライアント:

    - Windows 用の Azure Information Protection クライアントおよび iOS および Android 用のビューアーアプリでは、常に MFA がサポートされています。最小バージョンは必要ありません。 

-   Mac コンピューター用の Rights Management 共有アプリ:

    -   MFA では、2015 の年 9 月以降にリリースされた RMS 共有アプリがサポートされます。

確認後、MFA ソリューションを構成します。

-   Microsoft が管理するテナント (Azure Active Directory または Office 365) の場合:

    - Azure MFA を構成してユーザー向けに MFA を適用します。 手順については、Multi-Factor Authentication ドキュメントの「[Getting started with Azure Multi-Factor Authentication in the cloud (クラウドでの Azure Multi-Factor Authentication の概要)](/multi-factor-authentication/multi-factor-authentication-get-started-cloud)」を参照してください。

        Azure MFA の詳細については、「[What is Azure Multi-Factor Authentication? (Azure Multi-Factor Authentication とは)](/multi-factor-authentication/multi-factor-authentication)」を参照してください。

- 統合テナント (オンプレミスのフェデレーション サーバー) の場合:

    - 使用しているフェデレーション サーバーを Azure Active Directory または Office 365 向けに構成します。 たとえば、AD FS を使用する場合は、「 [AD FS の追加の認証方法を構成](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)する」を参照してください。

        このシナリオの詳細については、Office ブログの「[The Works with Office 365 – Identity program now streamlined (Office 365 の機能 – 合理化された ID プログラム)](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/)」を参照してください。

Rights Management コネクタおよび Azure Information Protection スキャナーでは、MFA はサポートされません。 コネクタまたはスキャナーをデプロイする場合は、次のアカウントで MFA を要求することはできません。

- コネクタをインストールおよび構成するアカウント。

- コネクタが作成する、Azure AD のサービス プリンシパル アカウント (**Aadrm_S-1-7-0**)。
 
- スキャナーを実行するサービス アカウント。

## <a name="next-steps"></a>次のステップ
その他の要件を確認するには、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

