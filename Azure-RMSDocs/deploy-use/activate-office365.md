---
title: "Office 365 管理センターで Azure RMS をアクティブ化する - AIP"
description: "Office 365 管理センターの新しいバージョンを使用する場合の、Azure Rights Management サービスのアクティブ化手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a2b3e1a2-59a0-4191-bf4c-4485ae7a70a9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ec41508974244a7abe4faf67831d348775cdc73c
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2017
---
# <a name="how-to-activate-azure-rights-management-from-the-office-365-admin-center"></a>Office 365 管理センターから Azure Rights Management をアクティブ化する方法

>*適用対象: Azure Information Protection、Office 365*

Office 365 管理センターから Azure Rights Management サービスにアクセスする場合は、次の手順を使用します。 たとえば、Office 365 E3 または Office 365 E5 のサブスクリプションがあります。

1. Rights Management が含まれている Office 365 プランにサインアップした後、Office 365 のデプロイのグローバル管理者の役割を持つ[職場または学校のアカウントで Office 365 にサインイン](https://portal.office.com/)します。

2. Office 365 管理センターが自動的に表示されない場合は、左上のアプリ ランチャー アイコンを選択し、**[管理]** を選択します。 [ **管理** ] タイルは、Office 365 管理者に対してのみ表示されます。

    > [!TIP]
    > 管理センターのヘルプについては、「[Office 365 管理センターについて](https://support.office.com/article/About-the-Office-365-Admin-Center-758befc4-0888-4009-9f14-0d147402fd23)」を参照してください。

3. **[著作権管理]** ページに移動するか、検索機能を使用します。

    - 移動方法: **[設定]** > **「Services & add-ins」 (サービスとアドイン)** > **[Microsoft Azure Information Protection]** > **「Manage Microsoft Azure Information Protection settings」 (Microsoft Azure Information Protection 設定の管理)**

    - 検索方法: **[ホーム]** ページの検索ボックスで、「**情報保護**」と入力し、検索結果から **[Microsoft Azure Information Protection]**、**「Manage Microsoft Azure Information Protection settings」 (Microsoft Azure Information Protection 設定の管理)** の順にクリックします。 
    
    > [!NOTE]
    >このオプションに移動する場合、ディスプレイによっては、このオプションを表示するのに画面をスクロールする必要がある場合があります。 ただし、このページの一覧に表示されない場合や検索結果が返されない場合は、お客様のサービス プランに Azure Information Protection の Azure Rights Management サービスが含まれていないことが考えられます。
    >
    >Azure Rights Management サービスをアクティブ化するには、[Azure Information Protection Premium プラン](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)を取得するか、[Rights Management を含む Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。 この問題でサポートが必要な場合は、 [askipteam](mailto:askipteam@microsoft.com?subject=I%20cannot%20activate%20RMS)宛てに電子メール メッセージを送信してください。

4. **[RIGHTS MANAGEMENT]** ページで、 **[アクティブ化]**をクリックします。

5. [ **Rights Management をアクティブ化しますか?**] というメッセージが表示されたら、[ **アクティブ化**] をクリックします。

[ **Rights Management はアクティブ化されています** ] というテキストと、非アクティブ化するオプションが表示されます。


## <a name="next-steps"></a>次のステップ
「[Azure Rights Management をアクティブにする](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)」を引き続きお読みください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
