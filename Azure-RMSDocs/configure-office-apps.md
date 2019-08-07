---
title: AIP から Azure RMS と共に Office アプリを使用するようにクライアントを構成する
description: Azure Information Protection から Azure Rights Management サービスを使用する Office アプリケーションを構成するための、管理者向けの情報と手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 32461a7d3edb53003ea12a7dc26e8b78966e1a4f
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68789252"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office アプリ: Azure Rights Management サービスを使用するようにクライアントを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Information Protection から Office アプリと Azure Rights Management サービスを連動するために必要なことを、この情報を元に決定してください。

## <a name="office365-apps-office-2019-office-2016-and-office-2013"></a>Office 365 アプリ、Office 2019、Office 2016、および Office 2013
これらの最近のバージョンの Office では、Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook on the web などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 すべてのユーザーが Windows 上のこれらのアプリに対して実行する必要があるのは、office 365 資格情報を使用して Office アプリケーションにサインインすることです。 サインイン後、ファイルやメールを保護したり、他のユーザーが保護したファイルやメールを利用したりできます。

### <a name="user-instructions-for-office-for-mac"></a>Office for Mac のユーザー向けの手順

Office for Mac を使用するユーザーは、コンテンツを保護する前に、まず資格情報を確認する必要があります。 例えば:

1. Office 365 の職場または学校のアカウントを使用して、Outlook を開き、プロファイルを作成します。 

2. 新しいメッセージを作成し、 **[オプション]** タブで **[アクセス許可]** を選択し、 **[資格情報の検証]** を選択します。 入力要求が表示されたら、Office 365 の職場または学校のアカウントの詳細をもう一度指定し、 **[サインイン]** を選択します。
    
    この操作により、Azure Rights Management テンプレートがダウンロードされ、**資格情報**が、**制限なし**、**転送不可**、およびに発行されている azure Rights Management テンプレートを含むオプションに置き換えられるようになりました。型. 

3. この新しいメッセージを今すぐ取り消すことができます。

4. 電子メール メッセージやドキュメントを保護するには: **[オプション]** タブで、 **[アクセス許可]** を選択し、電子メールまたはドキュメントを保護するオプションまたはテンプレートを選択します。

## <a name="office2010"></a>Office 2010
クライアントコンピューターが Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアント (クラシック) が必要です。 他の構成は必要ありません。ユーザーが各自の Office 365 資格情報でサインインしさえすれば、ファイルを保護したり、他のユーザーによって保護されたファイルを使用したりできます。

Azure Information Protection クライアント (クラシック) の詳細については、 [「クライアントの Azure Information Protection」を参照してください。クライアントのインストールと構成](configure-client.md)」を参照してください。

