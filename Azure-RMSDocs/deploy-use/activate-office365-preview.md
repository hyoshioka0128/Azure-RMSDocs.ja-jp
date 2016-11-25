---
title: "Office 365 管理センター プレビューから Azure Rights Management をアクティブ化する方法 | Azure Information Protection"
description: "Office 365 管理センターの新しいプレビュー バージョン (Office 365 管理センター プレビュー) にアクセスできる場合の、Azure Rights Management サービス向けのアクティブ化手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a2b3e1a2-59a0-4191-bf4c-4485ae7a70a9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 986cb20b1cf4ecebb08e5f651bbc3af9e28d884b


---

# <a name="how-to-activate-azure-rights-management-from-the-office-365-admin-center-preview"></a>Office 365 管理センター プレビューから Azure Rights Management をアクティブ化する方法

>*適用対象: Azure Information Protection、Office 365*


Office 365 管理センターの新しいプレビュー バージョン (**Office 365 管理センター プレビュー**) を使用している場合にのみ、次の手順を使用します。

このバージョンの管理センターはプレビュー段階であり、Azure Rights Management の Azure Information Protection への再ブランド化が進行中であるため、このバージョンの管理センターの手順は、従来のバージョンの管理センターの手順を使用するよりも信頼性が低いことに注意してください。 このバージョンの管理センターを使用する場合は、顧客によって異なったオプションが表示される可能性があります。

1. Rights Management が含まれている Office 365 プランにサインアップした後、Office 365 のデプロイのグローバル管理者である[職場または学校のアカウントで Office 365 にサインイン](https://portal.office.com/)します。

2. Office 365 管理センターが自動的に表示されない場合は、左上のアプリ ランチャー アイコンを選択し、**[管理]** を選択します。 [ **管理** ] タイルは、Office 365 管理者に対してのみ表示されます。

    > [!TIP]
    > 管理センターのヘルプについては、「 [Office 365 管理センターについて - 管理者向けヘルプ](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)」を参照してください。

3. **[著作権管理]** ページに移動するか、検索機能を使用します。

    プレビュー バージョンの使用が初めてで、関連する構成オプションも見たいという場合はナビゲーションがお勧めです。プレビュー バージョンに慣れていて、Azure Rights Management の起動を即座に行いたい場合は、検索機能の使用がお勧めです。 ナビゲーション指示と表示内容が一致しない場合は、管理センターのプレビュー バージョンを使用中に、検索オプションを使用する必要が生じる場合もあります。

    - 移動方法: **[設定]** > **[Services & add-ins] (サービスとアドイン)** > **[Microsoft Azure Information Protection]** > **[Manage Microsoft Azure Information Protection settings] (Microsoft Azure Information Protection 設定の管理)**

    - 検索方法: **[ホーム]** ページの検索ボックスで、「**情報保護**」と入力し、検索結果から **[Microsoft Azure Information Protection]**、**[Manage Microsoft Azure Information Protection settings] (Microsoft Azure Information Protection 設定の管理)** の順にクリックします。 検索結果が返されない場合は、「**著作権管理**」と入力し、検索結果から **[Microsoft Azure rights management settings]** をクリックします。

        > [!NOTE]
        >このオプションに移動する場合、ディスプレイによっては、このオプションを表示するのに画面をスクロールする必要がある場合があります。 ただし、このページの一覧に表示されない場合や検索結果が返されない場合は、お客様のサービス プランに Azure Information Protection の Azure Rights Management サービスが含まれていないことが考えられます。
        >
        >Azure Rights Management サービスをアクティブ化するには、[Azure Information Protection Premium プラン](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)を取得するか、[Rights Management を含む Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。 この問題でサポートが必要な場合は、 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)宛てに電子メール メッセージを送信してください。

4. **[RIGHTS MANAGEMENT]** ページで、 **[アクティブ化]**をクリックします。

5. [ **Rights Management をアクティブ化しますか?**] というメッセージが表示されたら、[ **アクティブ化**] をクリックします。

[ **Rights Management はアクティブ化されています** ] というテキストと、非アクティブ化するオプションが表示されます。


## <a name="next-steps"></a>次のステップ
「[Azure Rights Management をアクティブにする](activate-service.md)」に戻ります。




<!--HONumber=Nov16_HO2-->


