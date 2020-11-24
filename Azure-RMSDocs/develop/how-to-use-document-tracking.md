---
title: ドキュメント追跡を使用する方法 | Azure RMS
description: ドキュメント追跡機能を使用するには、関連付けられているメタデータの管理とサービスへの登録について理解している必要があります。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 70E10936-7953-49B0-B0DC-A5E7C4772E60
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: dfcb4c616be2f5891b242a918a06abf2708c12cc
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570519"
---
# <a name="how-to-use-document-tracking"></a>方法: ドキュメント追跡を使用する

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

ドキュメント追跡機能を使用するには、関連付けられているメタデータの管理とサービスへの登録について理解している必要があります。

## <a name="managing-document-tracking-metadata"></a>ドキュメント追跡メタデータの管理

ドキュメント追跡をサポートする各オペレーティング システムは、似たような実装を持ちます。 これには、メタデータを表すプロパティのセット、ユーザー ポリシー作成メソッドに追加される新しいパラメーター、ドキュメント追跡サービスで追跡するポリシーを登録するためのメソッドが含まれます。

運用上、ドキュメント追跡に必要なプロパティは、**コンテンツ名** と **通知の種類** のみです。

特定のコンテンツに対してドキュメント追跡をセットアップするための手順を次に示します。

- **ライセンス メタデータ** オブジェクトを作成してから、**コンテンツ名** と **通知タイプ** を設定します。 必須のプロパティはこれらのプロパティのみです。
  - Android - [LicenseMetadata](/previous-versions/windows/desktop/msipcthin2/licensemetadata-interface-java)
  -  iOS - [MSLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/mslicensemetadata-class-objc)

ポリシーの種類 (テンプレートまたはアドホック) を選択します。
- テンプレート ベースのドキュメント追跡の場合は、**ユーザー ポリシー** オブジェクトを作成し、ライセンス メタデータをパラメーターとして渡します。
  - Android - [UserPolicy.create](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-templatedescriptor-property-objc)

- アドホック ベースのドキュメントの追跡の場合は、**ライセンス メタデータ** プロパティを **ポリシー記述子** オブジェクトに設定します。
  - Android - [PolicyDescriptor.setLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/policydescriptor-setlicensemetadata-java)
  - iOS -  [MSPolicyDescriptor.licenseMetadata](/previous-versions/windows/desktop/msipcthin2/mspolicydescriptor-licensemetadata-property-objc)

    **メモ**   ライセンスメタデータオブジェクトには、指定されたユーザーポリシーのドキュメント追跡を設定するプロセス中にのみ直接アクセスできます。 ユーザー ポリシー オブジェクトが作成されると、関連付けられているライセンス メタデータにアクセスできなくなります。つまり、ライセンス メタデータの値を変更しても効果はありません。

     

- 最後に、ドキュメント追跡のためのプラットフォーム登録メソッドを呼び出します。
  - Android - [UserPolicy.registerForDocTracking asynchronous](/previous-versions/windows/desktop/msipcthin2/userpolicy-registerfordoctracking-boolean--sting--authenticationcallback--creationcallback--java) または [UserPolicy.registerForDocTracking synchronous](/previous-versions/windows/desktop/msipcthin2/userpolicy-registerfordoctracking-synchronous-method-java)
  - iOS - [MSUserPolicy.registerForDocTracking](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-registerfordoctracking-userid-authenticationcallback-completionblock-method-objc)