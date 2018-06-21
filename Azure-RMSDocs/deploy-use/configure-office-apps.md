---
title: AIP から Azure RMS と共に Office アプリを使用するようにクライアントを構成する
description: Azure Information Protection から Azure Rights Management サービスを使用する Office アプリケーションを構成するための、管理者向けの情報と手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79c3da1d2fcf9405389f5ceba25b81f4808713b8
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
ms.locfileid: "30204692"
---
# <a name="office-apps-configuration-for-clients-to-use-the-azure-rights-management-service"></a>Office アプリ: Azure Rights Management サービスを使用するようにクライアントを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Azure Information Protection から Office アプリと Azure Rights Management サービスを連動するために必要なことを、この情報を元に決定してください。

## <a name="office-2016-and-office-2013"></a>Office 2016 と Office 2013:
これらの最近のバージョンの Office では、Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook on the web などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 ユーザーに求められることは、自分の Office アプリケーションに自分の [!INCLUDE[o365_1](../includes/o365_1_md.md)] 資格情報でサインインすることだけです。 サインイン後、ファイルやメールを保護したり、他のユーザーが保護したファイルやメールを利用したりできます。

ただし、これらのアプリケーションを Azure Information Protection クライアントで補完して、ユーザーが Office アドインを利用し、追加のファイルの種類をサポートできるようにすることをお勧めします。 詳細については、「[Azure Information Protection client: Installation and configuration for clients](configure-client.md)」(Azure Information Protection クライアント: クライアントのインストールと構成) を参照してください。

## <a name="office-2010"></a>Office 2010
クライアント コンピューターの Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアントまたは Windows 用 Rights Management 共有アプリケーションを用意する必要があります。 他の構成は必要ありません。ユーザーが各自の [!INCLUDE[o365_1](../includes/o365_1_md.md)] 資格情報でサインインしさえすれば、ファイルを保護したり、他のユーザーによって保護されたファイルを使用したりできます。

Azure Information Protection クライアントの詳細については、「[Azure Information Protection client: Installation and configuration for clients](configure-client.md)」(Azure Information Protection クライアント: クライアントのインストールと構成) を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
