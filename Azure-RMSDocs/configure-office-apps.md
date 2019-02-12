---
title: AIP から Azure RMS と共に Office アプリを使用するようにクライアントを構成する
description: Azure Information Protection から Azure Rights Management サービスを使用する Office アプリケーションを構成するための、管理者向けの情報と手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/01/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7896e1c8a342ce8a430d9133950a2fe47a7de602
ms.sourcegitcommit: 8558af7116f62414054feffa346aba197a1250d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2019
ms.locfileid: "55559769"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office アプリ: Azure Rights Management サービスを使用するようにクライアントを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Information Protection から Office アプリと Azure Rights Management サービスを連動するために必要なことを、この情報を元に決定してください。

## <a name="office2016-and-office-2013"></a>Office 2016 と Office 2013
これらの最近のバージョンの Office では、Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook on the web などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 ユーザーに求められることは、自分の Office アプリケーションに自分の Office 365 資格情報でサインインすることだけです。 サインイン後、ファイルやメールを保護したり、他のユーザーが保護したファイルやメールを利用したりできます。

ただし、これらのアプリケーションを Azure Information Protection クライアントで補完して、ユーザーが Office アドインを利用し、追加のファイルの種類をサポートできるようにすることをお勧めします。 詳細については、「[Azure Information Protection クライアント:クライアントのインストールと構成](configure-client.md)」を参照してください。

## <a name="office2010"></a>Office 2010
クライアント コンピューターの Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアントを用意する必要があります。 他の構成は必要ありません。ユーザーが各自の Office 365 資格情報でサインインしさえすれば、ファイルを保護したり、他のユーザーによって保護されたファイルを使用したりできます。

Azure Information Protection クライアントの詳細については、「[Azure Information Protection クライアント: クライアントのインストールと構成](configure-client.md)」を参照してください。

