---
title: "Office アプリ: クライアントの構成 - AIP"
description: "Azure Information Protection から Azure Rights Management サービスを使用する Office アプリケーションを構成するための、管理者向けの情報と手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ec269afe-4e87-4cc1-9144-5fbb594b412e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 37521bad9e6e1cfb9db9741ba3c8495460a20da6
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="office-apps-configuration-for-clients"></a>Office アプリ: クライアントの構成

>*適用対象: Azure Information Protection、Office 365*


この情報を使用して、エンド ユーザーが使用する Office アプリを Azure Information Protection からの Azure Rights Management サービスに対応させるために行う必要があることを確認してください。

## <a name="office-2016-and-office-2013"></a>Office 2016 と Office 2013:
これらの最近のバージョンの Office では、Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook Web App などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 すべてのユーザーは、各自の [!INCLUDE[o365_1](../includes/o365_1_md.md)] 資格情報を使用して Office アプリケーションにサインインするだけで、ファイルや電子メールを保護したり、他のユーザーが保護しているファイルや電子メールを使用することができます。

ただし、これらのアプリケーションを Azure Information Protection クライアントで補完して、ユーザーが Office アドインを利用し、追加のファイルの種類をサポートできるようにすることをお勧めします。 詳細については、「[Azure Information Protection client: Installation and configuration for clients](configure-client.md)」(Azure Information Protection クライアント: クライアントのインストールと構成) を参照してください。

## <a name="office-2010"></a>Office 2010
クライアント コンピューターの Office 2010 で Azure Rights Management サービスを使用するには、Azure Information Protection クライアントまたは Windows 用 Rights Management 共有アプリケーションをインストールしている必要があります。 他の構成は必要ありません。ユーザーが各自の [!INCLUDE[o365_1](../includes/o365_1_md.md)] 資格情報でサインインしさえすれば、ファイルを保護したり、他のユーザーによって保護されたファイルを使用したりできます。

Azure Information Protection クライアントの詳細については、「[Azure Information Protection client: Installation and configuration for clients](configure-client.md)」(Azure Information Protection クライアント: クライアントのインストールと構成) を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
