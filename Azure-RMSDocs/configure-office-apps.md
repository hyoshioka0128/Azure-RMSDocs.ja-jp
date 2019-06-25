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
ms.suite: ems
ms.openlocfilehash: 09f7eaaaafb6c1ecbce584876a7e8bf254e0c0d5
ms.sourcegitcommit: 2af2297319265c1f91aa76eb227c6f4d316df42a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67348807"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office アプリ: Azure Rights Management サービスを使用するようにクライアントを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Information Protection から Office アプリと Azure Rights Management サービスを連動するために必要なことを、この情報を元に決定してください。

## <a name="office365-apps-office-2019-office-2016-and-office-2013"></a>Office 365 アプリ、Office 2019、Office 2016、および Office 2013
これらの最近のバージョンの Office では、Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook on the web などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 すべてのユーザーは、これらのアプリの Windows で行う必要があるは、Office 365 の資格情報を使用して Office アプリケーションにサインインします。 サインイン後、ファイルやメールを保護したり、他のユーザーが保護したファイルやメールを利用したりできます。

### <a name="user-instructions-for-office-for-mac"></a>For Office for Mac のユーザーの手順

コンテンツを保護する前に、Office for Mac を持つユーザーは自分の資格情報を確認しなければなりません。 以下に例を示します。

1. Office 365 の職場または学校のアカウントを使用して、Outlook を開き、プロファイルを作成します。 

2. 新しいメッセージを作成し、**オプション** タブで **権限**、し、**資格情報の確認**します。 入力要求が表示されたら、Office 365 の職場または学校のアカウントの詳細をもう一度指定し、 **[サインイン]** を選択します。
    
    このアクションは、Azure Rights Management テンプレートをダウンロードし、**資格情報の確認**を含むオプションで置き換えられました**無制限**、**不可**とテナント用にパブリッシュされた任意の Azure Rights Management テンプレート。 

3. この新しいメッセージを今すぐ取り消すことができます。

4. 電子メール メッセージやドキュメントを保護するには: **オプション**] タブで [**権限**オプションまたは、電子メールやドキュメントを保護するテンプレートを選択します。

## <a name="office2010"></a>Office 2010
クライアント コンピュータが Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアント (クラシック) が必要です。 他の構成は必要ありません。ユーザーが各自の Office 365 資格情報でサインインしさえすれば、ファイルを保護したり、他のユーザーによって保護されたファイルを使用したりできます。

Azure Information Protection クライアント (クラシック) の詳細については、次を参照してください。 [Azure Information Protection クライアント。クライアントのインストールと構成](configure-client.md)」を参照してください。

