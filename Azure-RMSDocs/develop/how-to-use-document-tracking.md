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
ms.openlocfilehash: 334b4aed3e24a64e553429587eea4b0bf4c7948a
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178371"
---
# <a name="how-to-use-document-tracking"></a>方法: ドキュメント追跡を使用する

ドキュメント追跡機能を使用するには、関連付けられているメタデータの管理とサービスへの登録について理解している必要があります。

## <a name="managing-document-tracking-metadata"></a>ドキュメント追跡メタデータの管理

ドキュメント追跡をサポートする各オペレーティング システムは、似たような実装を持ちます。 これには、メタデータを表すプロパティのセット、ユーザー ポリシー作成メソッドに追加される新しいパラメーター、ドキュメント追跡サービスで追跡するポリシーを登録するためのメソッドが含まれます。

運用上、ドキュメント追跡に必要なプロパティは、**コンテンツ名**と**通知の種類**のみです。

特定のコンテンツに対してドキュメント追跡をセットアップするための手順を次に示します。

- **ライセンス メタデータ** オブジェクトを作成してから、**コンテンツ名**と**通知タイプ**を設定します。 必須のプロパティはこれらのプロパティのみです。
  - Android - [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx)
  -  iOS - [MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx)

ポリシーの種類 (テンプレートまたはアドホック) を選択します。
- テンプレート ベースのドキュメント追跡の場合は、**ユーザー ポリシー** オブジェクトを作成し、ライセンス メタデータをパラメーターとして渡します。
  - Android - [UserPolicy.create](https://msdn.microsoft.com/library/dn790887.aspx)
  - iOS - [MSUserPolicy.userPolicyWithTemplateDescriptor](https://msdn.microsoft.com/library/dn790808.aspx)

- アドホック ベースのドキュメントの追跡の場合は、**ライセンス メタデータ** プロパティを**ポリシー記述子**オブジェクトに設定します。
  - Android - [PolicyDescriptor.setLicenseMetadata](https://msdn.microsoft.com/library/mt573698.aspx)
  - iOS -  [MSPolicyDescriptor.licenseMetadata](https://msdn.microsoft.com/library/mt573693.aspx)

    **注**:  ライセンス メタデータ オブジェクトは、特定のユーザー ポリシーのドキュメント追跡の設定プロセス中に直接アクセスできる唯一のオブジェクトです。 ユーザー ポリシー オブジェクトが作成されると、関連付けられているライセンス メタデータにアクセスできなくなります。つまり、ライセンス メタデータの値を変更しても効果はありません。

     

- 最後に、ドキュメント追跡のためのプラットフォーム登録メソッドを呼び出します。
  - Android - [UserPolicy.registerForDocTracking asynchronous](https://msdn.microsoft.com/library/mt573699.aspx) または [UserPolicy.registerForDocTracking synchronous](https://msdn.microsoft.com/library/mt631387.aspx)
  - iOS - [MSUserPolicy.registerForDocTracking](https://msdn.microsoft.com/library/mt573694.aspx)
