---
title: AIP から Azure RMS と共に Office アプリを使用するようにクライアントを構成する
description: Azure Information Protection から Azure Rights Management サービスを使用する Office アプリケーションを構成するための、管理者向けの情報と手順です。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7746a412225248808e02731433133fc4182874a9
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136259"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office アプリ: Azure Rights Management サービスを使用するようにクライアントを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Information Protection から Office アプリと Azure Rights Management サービスを連動するために必要なことを、この情報を元に決定してください。

## <a name="office365-apps-office-2019-office-2016-and-office-2013"></a>Office 365 アプリ、Office 2019、Office 2016、および Office 2013
これらの最近のバージョンの Office では、Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook on the web などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 すべてのユーザーが Windows 上のこれらのアプリに対して実行する必要があるのは、office 365 資格情報を使用して Office アプリケーションにサインインすることです。 サインイン後、ファイルやメールを保護したり、他のユーザーが保護したファイルやメールを利用したりできます。

### <a name="user-instructions-for-office-for-mac"></a>Office for Mac のユーザー向けの手順

Office for Mac を使用するユーザーは、コンテンツを保護する前に、まず資格情報を確認する必要があります。 次に例を示します。

1. Office 365 の職場または学校アカウントを使用して、Outlook を開き、プロファイルを作成します。 

2. 新しいメッセージを作成し、[**オプション**] タブで [**アクセス許可**] を選択し、[**資格情報の検証**] を選択します。 入力要求が表示されたら、Office 365 の職場または学校アカウントの詳細をもう一度指定し、**[サインイン]** を選択します。
    
    この操作により、Azure Rights Management テンプレートがダウンロードされ、**資格情報**が、**制限なし**、**転送不可**、およびテナントに発行されている Azure Rights Management テンプレートを含むオプションに置き換えられるようになりました。 

3. この新しいメッセージは、ここで取り消すことができます。

4. 電子メールメッセージまたはドキュメントを保護するには、[**オプション**] タブで [**アクセス許可**] を選択し、電子メールまたはドキュメントを保護するオプションまたはテンプレートを選択します。

## <a name="office2010"></a>Office 2010
クライアントコンピューターが Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアント (クラシック) が必要です。 他の構成は必要ありません。ユーザーが各自の Office 365 資格情報でサインインしさえすれば、ファイルを保護したり、他のユーザーによって保護されたファイルを使用したりできます。

Azure Information Protection クライアント (クラシック) の詳細については、「クライアント[のインストールと構成](configure-client.md)」を参照して Azure Information Protection ください。

