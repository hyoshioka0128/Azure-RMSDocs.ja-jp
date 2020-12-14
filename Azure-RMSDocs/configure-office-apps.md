---
title: AIP から Azure RMS と共に Office アプリを使用するようにクライアントを構成する
description: Azure Information Protection から Azure Rights Management サービスを使用する Office アプリケーションを構成するための、管理者向けの情報と手順です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ea6b8afa02b9555924bcd1df5dfae1b7b37a217a
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383535"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office アプリ: Azure Rights Management サービスを使用するようにクライアントを構成する

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*


Azure Information Protection から Office アプリと Azure Rights Management サービスを連動するために必要なことを、この情報を元に決定してください。

## <a name="office-365-apps-office-2019-office-2016-and-office-2013"></a>Office 365 アプリ、Office 2019、Office 2016、および Office 2013

これらの新しいバージョンの Office では、Azure Rights Management サービスのサポートが組み込まれているため、web 上の Word、Excel、PowerPoint、Outlook、Outlook などのアプリケーションで information Rights Management (IRM) 機能をサポートするために、クライアントコンピューターを構成する必要はありません。 

すべてのユーザーが Windows 上のこれらのアプリに対して行う必要があるのは、Microsoft 365 資格情報を使用して Office アプリケーションにサインインすることです。 サインイン後、ファイルやメールを保護したり、他のユーザーが保護したファイルやメールを利用したりできます。

### <a name="user-instructions-for-office-for-mac"></a>Office for Mac のユーザー向けの手順

Office for Mac を使用するユーザーは、コンテンツを保護する前に、まず資格情報を確認する必要があります。 次に例を示します。

1. Outlook を開き、Microsoft 365 職場または学校アカウントを使用してプロファイルを作成します。 

2. 新しいメッセージを作成し、[ **オプション** ] タブで [ **アクセス許可**] を選択し、[ **資格情報の検証**] を選択します。 メッセージが表示されたら、Microsoft 365 職場または学校アカウントの詳細をもう一度指定し、[ **サインイン**] を選択します。
    
    この操作により、Azure Rights Management テンプレートがダウンロードされ、 **資格情報** が、 **制限なし**、 **転送不可**、およびテナントに発行されている Azure Rights Management テンプレートを含むオプションに置き換えられるようになりました。 

3. この新しいメッセージは、ここで取り消すことができます。

4. 電子メールメッセージまたはドキュメントを保護するには、[ **オプション** ] タブで [ **アクセス許可** ] を選択し、電子メールまたはドキュメントを保護するオプションまたはテンプレートを選択します。

## <a name="office-2010"></a>Office 2010

クライアント コンピューターの Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアントを用意する必要があります。 ユーザーが Microsoft 365 資格情報でサインインする必要がある以外に、他の構成は必要ありません。その後、ファイルを保護し、他のユーザーによって保護されているファイルを使用することができます。

詳細については、「[Azure Information Protection クライアント: クライアントのインストールと構成](configure-client.md)」を参照してください。

