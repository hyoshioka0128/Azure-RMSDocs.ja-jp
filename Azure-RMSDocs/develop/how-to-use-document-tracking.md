---
title: "ドキュメント追跡を使用する方法 | Azure RMS"
description: "ドキュメント追跡機能を使用するには、関連付けられているメタデータの管理とサービスへの登録について理解している必要があります。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ca4982cc86d9c006486540055de7c165adca21da
ms.openlocfilehash: 9872317c2d5f5f56f28ed2683d7ebc9743041a37


---

# 方法: ドキュメント追跡を使用する

ドキュメント追跡機能を使用するには、関連付けられているメタデータの管理とサービスへの登録について理解している必要があります。

## ドキュメント追跡メタデータの管理

ドキュメント追跡をサポートする各オペレーティング システムは、似たような実装を持ちます。 これには、メタデータを表すプロパティのセット、ユーザー ポリシー作成メソッドに追加される新しいパラメーター、ドキュメント追跡サービスで追跡するポリシーを登録するためのメソッドが含まれます。

運用上、ドキュメント追跡に必要なプロパティは、**コンテンツ名**と**通知の種類**のみです。

特定のコンテンツに対してドキュメント追跡をセットアップするための手順を次に示します。

-   **ライセンス メタデータ** オブジェクトを作成します。

    詳細については、[**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) または [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) に関する説明を参照してください。

-   **コンテンツ名**と**通知の種類**を設定します。 必須のプロパティはこれらのプロパティのみです。

    詳細については、プラットフォームの適切なライセンス メタデータ クラスのプロパティ アクセス メソッド ([**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) または [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc)) に関する説明を参照してください。

-   ポリシーの種類 (テンプレートまたはアドホック):

    -   テンプレート ベースのドキュメント追跡の場合は、**ユーザー ポリシー** オブジェクトを作成し、ライセンス メタデータをパラメーターとして渡します。

        詳細については、[**UserPolicy.create**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_class_java) と [**MSUserPolicy.userPolicyWithTemplateDescriptor**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_templatedescriptor_property_objc) に関する説明を参照してください。

    -   アドホック ベースのドキュメントの追跡の場合は、**ライセンス メタデータ** プロパティを**ポリシー記述子**オブジェクトに設定します。

        詳細については、[**PolicyDescriptor.getLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_interface_java)、[**PolicyDescriptor.setLicenseMetadata**](/rights-management/sdk/4.2/api/android/policydescriptor#msipcthin2_policydescriptor_setlicensemetadata_java) および [**MSPolicyDescriptor.licenseMetadata**](/rights-management/sdk/4.2/api/iOS/mspolicydescriptor#msipcthin2_mspolicydescriptor_licensemetadata_property_objc) に関する説明を参照してください。

    **注**: ライセンス メタデータ オブジェクトは、特定のユーザー ポリシーのドキュメント追跡の設定プロセス中に直接アクセスできる唯一のオブジェクトです。 ユーザー ポリシー オブジェクトが作成されると、関連付けられているライセンス メタデータにアクセスできなくなります。つまり、ライセンス メタデータの値を変更しても効果はありません。

     

-   ドキュメント追跡のためのプラットフォーム登録メソッドを呼び出します。

    [**MSUserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) または [**UserPolicy.registerForDocTracking**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_registerfordoctracking_userid_authenticationcallback_completionblock_method_objc) に関する説明を参照してください。

 

 



<!--HONumber=Jun16_HO4-->


