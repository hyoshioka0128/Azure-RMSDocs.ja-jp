---
# required metadata

title: 個人用 RMS 向けに作成されたアカウントを管理者が制御する方法 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a83880d0-f0f9-4a32-9e00-2f6635d7cc8d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---



# 個人用 RMS 向けに作成されたアカウントを管理者が制御する方法

*適用対象: Azure Rights Management*


組織の個人用 RMS サブスクリプションを有料のサブスクリプションに切り替えない場合でも、組織用に作成された Azure ディレクトリのユーザー アカウントを次の方法で制御できます。

-   Azure Active Directory と Active Directory ドメイン サービス インフラストラクチャに対して、ディレクトリ統合ソリューションを実装します。 アカウントとパスワードを同期することで、ユーザーは Rights Management を使用するために新しいアカウントを作成する必要がなくなり、新しい Azure ユーザー アカウントにオンプレミスのパスワード ポリシーが適用されます。 また、パスワードを同期すると、ユーザーは Rights Management を使用するために別のパスワードを覚えておく必要がなくなります。

-   ユーザーがサインアップして個人用 RMS サブスクリプションで Azure Rights Management を使用するのを防ぐことができます。 通常、この方法には利点がほとんどありません。ユーザーは保護なしでファイルを共有するか (会社に対してリスクが生じる可能性があります)、または IT 部門がデータにアクセスできない別のファイル保護メカニズムを使用するかのいずれかを選択することになるためです。 それでも、ユーザーがサインアップできず個人用 RMS を使用できないようにする場合は、Azure での組織のディレクトリの所有権を取得した後に、次のいずれかの操作を実行してください。

    -   すべてのユーザーが、セルフサービス サブスクリプション (個人用 RMS を含む) にサインアップできないようにします。  現時点で、これをサービス別に設定することはできません。設定はセルフサービス プロセスを使用するすべての Azure サブスクリプションに適用されます。 これを行うには、Azure Active Directory 用 Windows PowerShell モジュールの [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) コマンドレットで **AllowAdHocSubscriptions** パラメーターを false に設定します。 例: **Set-MsolCompanySettings -AllowAdHocSubscriptions $false**

    -   ユーザーが Azure に新しいアカウントを作成できないようにします。つまり、Azure に既にアカウントを持っているユーザーしかセルフサービス サブスクリプション (個人用 RMS を含む) にサインアップできないようにします。  これを行うには、Azure Active Directory 用 Windows PowerShell モジュールの [Set-MsolCompanySettings](http://technet.microsoft.com/library/dn194127.aspx) コマンドレットで **AllowEmailVerifiedUsers** パラメーターを false に設定します。 例: **Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true**

    -   Active Directory ドメイン サービス インフラストラクチャと Azure Active Directory を同期します。 この操作により、ユーザーが個人用 RMS などのセルフサービス サブスクリプションにサインアップしても新しいアカウントが作成されなくなり、Azure ディレクトリに作成済みのアカウントを削除または無効にすることができます。

Azure ディレクトリ内のユーザー アカウントを制御する、またはユーザーによる個人用 RMS へのサインアップを防ぐには、Azure サブスクリプションがあり、ディレクトリを所有している必要があります。 Azure サブスクリプションをまだ持っていない場合は、無料のサブスクリプションを取得できます。 セルフサービス プロセス中にディレクトリが自動作成された場合は、ディレクトリの作成時に使用されたドメインの所有権を取得します。 Azure にディレクトリを既に所有しているが、組織で使用する新しいドメインがユーザーによって指定された場合、そのドメインを既存のディレクトリにマージしてください。 詳細については、「 [Azure のセルフ サービス サインアップについて](https://azure.microsoft.com/documentation/articles/active-directory-self-service-signup/)」の説明をご覧ください。


## 次のステップ

管理者ではないユーザーが個人用 RMS 向けに自分のアカウントを Azure Active Directory に作成できる場合、ユーザーがこの操作を行っているかどうかを確認するには、どうすればよいでしょうか。  「[ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法](rms-for-individuals-identify-sign-up.md)」を参照してください。.


<!--HONumber=Apr16_HO4-->


