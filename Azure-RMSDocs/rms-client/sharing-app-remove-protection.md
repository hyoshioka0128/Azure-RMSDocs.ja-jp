---
# required metadata

title: Rights Management 共有アプリケーションの使用によるファイルからの保護の削除 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rights Management 共有アプリケーションの使用によるファイルからの保護の削除

*適用対象: Active Directory Rights Management サービス、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

RMS 共有アプリケーションを使用して、保護されていたファイルから保護を削除する (つまり、ファイルの保護を解除する) には、エクスプローラーの [ **保護の削除** ] を使用します。

> [!IMPORTANT]
> 保護を削除するには、ファイルの所有者である必要があります。

## ファイルから保護を削除するには

1.  エクスプローラーで、ファイル (たとえば、Sample.ptxt) を右クリックし、**[RMS による保護]** を選択して、**[Protect in-place]** (保護済み) をクリックしてから、**[保護の解除]** をクリックします。

    ![RMS 共有アプリケーションの [保護の解除] メニュー オプション](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    資格情報が要求される場合があります。

注: これらのオプションが表示されない場合は、RMS 共有アプリケーションがコンピューターにインストールされていない、最新バージョンがインストールされていない、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 共有アプリケーションをインストールする方法の詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](install-sharing-app.md)」を参照してください。.

元の保護されたファイル (たとえば、Sample.ptxt) が削除され、同じ名前を持つが、保護されていないファイル名拡張子 (たとえば、Sample.txt) のファイルで置き換えられます。

## 例とその他の説明
Rights Management 共有アプリケーションの使用方法の例と操作手順については、Rights Management 共有アプリケーション ユーザー ガイドの次のセクションをご覧ください。

-   [RMS 共有アプリケーションの使用例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [作業内容](sharing-app-user-guide.md#what-do-you-want-to-do-)

## 参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)


<!--HONumber=May16_HO2-->


