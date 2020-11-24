---
title: 必要な API アクセス許可-Microsoft Information Protection SDK
description: Microsoft Information Protection ソフトウェア開発キットの操作に必要な API のアクセス許可に関する技術的な詳細。
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: ce44c0d8b65f477fdd7b08f34cfe2aacc890d259
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570158"
---
# <a name="api-permissions-for-the-microsoft-information-protection-sdk"></a>Microsoft Information Protection SDK の API アクセス許可

MIP SDK は、ラベル付けと保護に2つのバックエンド Azure サービスを使用します。 [アプリのアクセス許可の Azure Active Directory] ブレードでは、次のサービスがあります。

- Azure Rights Management サービス
- Microsoft Information Protection 同期サービス

アプリケーションのアクセス許可は、MIP SDK を使用してラベル付けと保護を行うときに、1つまたは複数の Api に付与する必要があります。 アプリケーションの認証シナリオによっては、アプリケーションのアクセス許可が異なる場合があります。 アプリケーションの認証シナリオについては、「 [認証のシナリオ](/azure/active-directory/develop/authentication-flows-app-scenarios)」を参照してください。

[AAD ドキュメント](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations)で説明されているように、管理者の同意が必要なアプリケーションのアクセス許可には、テナント全体の管理者の同意を付与する必要があります。

## <a name="application-permissions"></a>アプリケーションのアクセス許可

アプリケーションのアクセス許可により、Azure Active Directory のアプリケーションは、特定のユーザーの代わりにではなく、独自のエンティティとして機能することができます。

| サービス                         | 権限名           | 説明                                  | 管理者の同意が必要です |
| ------------------------------- | ------------------------- | -------------------------------------------- | ---------------------- |
| Azure Rights Management サービス | コンテンツ (スーパーユーザー)         | このテナントのすべての保護されたコンテンツを読み取ります   | はい                    |
| Azure Rights Management サービス | DelegatedReader   | ユーザーの代わりに保護されたコンテンツを読み取る   | はい                    |
| Azure Rights Management サービス | DelegatedWriter   | ユーザーの代わりに保護されたコンテンツを作成する | はい                    |
| Azure Rights Management サービス | Content-type            | 保護されたコンテンツの作成                     | はい                    |
| MIP 同期サービス                | UnifiedPolicy | テナントのすべての統合ポリシーを読み取ります。      | はい                    |

### <a name="contentsuperuser"></a>コンテンツ (スーパーユーザー)

このアクセス許可は、特定のテナントに対して保護されているすべてのコンテンツの暗号化を解除することをアプリケーションに許可する必要がある場合に必要です。 スーパーユーザー権限を必要とするサービスの例としては、データ損失防止やクラウドアクセスセキュリティブローカーサービスがあります。このサービスでは、すべてのコンテンツをプレーンテキストで表示して、データのフローや格納先に関するポリシーの決定を行うことができなければなりません。  

### <a name="contentdelegatedwriter"></a>DelegatedWriter

このアクセス許可は、特定のユーザーによって保護されているコンテンツの暗号化をアプリケーションが許可する必要がある場合に必要です。 委任された書き込み権限を必要とするサービスの例として、ラベルを適用したりコンテンツをネイティブに暗号化したりするために、ユーザーのラベルポリシーに基づいてコンテンツを暗号化する必要がある基幹業務アプリケーションがあります。 このアクセス許可は、ユーザーのコンテキストでコンテンツを暗号化することをアプリケーションに許可します。

### <a name="contentdelegatedreader"></a>DelegatedReader

このアクセス許可は、特定のユーザーに対して保護されているすべてのコンテンツの暗号化を解除することをアプリケーションに許可する必要がある場合に必要です。 委任されたリーダー権限を必要とするサービスの例としては、コンテンツをネイティブに表示するために、ユーザーのラベルポリシーに基づいてコンテンツの暗号化を解除する必要がある基幹業務アプリケーションがあります。 このアクセス許可によって、アプリケーションはユーザーのコンテキストでコンテンツの暗号化を解除して読み取ることができます。

### <a name="contentwriter"></a>Content-type

このアクセス許可は、アプリケーションでコンテンツの暗号化を許可する必要がある場合に必要です。 ライターを必要とするサービスの例としては、エクスポート時に分類ラベルをファイルに適用する基幹業務アプリケーションが挙げられます。 コンテンツライターは、サービスプリンシパル id としてコンテンツを暗号化するため、保護されたファイルの所有者はサービスプリンシパル id になります。

### <a name="unifiedpolicytenantread"></a>UnifiedPolicy

このアクセス許可は、アプリケーションでテナントの統一されたラベル付けポリシーをダウンロードすることを許可する必要がある場合に必要です。 統合ポリシーテナント読み取りを必要とするサービスの例としては、サービスプリンシパル id としてラベルを使用する必要があるアプリケーションがあります。

## <a name="delegated-permissions"></a>委任されたアクセス許可

委任されたアクセス許可により、Azure Active Directory のアプリケーションは、特定のユーザーに代わってアクションを実行できます。

| サービス                         | 権限名         | 説明                                      | 管理者の同意が必要です |
| ------------------------------- | ----------------------- | ------------------------------------------------ | ---------------------- |
| Azure Rights Management サービス | user_impersonation      | ユーザーの保護されたコンテンツを作成してアクセスする | いいえ                     |
| MIP 同期サービス                | UnifiedPolicy | ユーザーがアクセスできるすべての統合ポリシーを読み取ります。   | いいえ                     |

### <a name="user_impersonation"></a>user_impersonation

このアクセス許可は、ユーザーに代わってアプリケーションが Azure Rights Management サービスをユーザーに許可する必要がある場合に必要です。 User_Impersonation 権限を必要とするサービスの例としては、暗号化する必要があるアプリケーションや、ラベルを適用したりコンテンツをネイティブに暗号化したりするためにユーザーのラベルポリシーに基づいてコンテンツにアクセスすることがあります。
  
### <a name="unifiedpolicyuserread"></a>UnifiedPolicy

このアクセス許可は、ユーザーに関連する統一されたラベル付けポリシーの読み取りをアプリケーションが許可する必要がある場合に必要です。 特定のユーザーによって保護されたコンテンツを暗号化します。 委任された書き込み権限を必要とするサービスの例としては、ラベルを適用したりコンテンツをネイティブに暗号化したりするために、ユーザーのラベルポリシーに基づいてコンテンツを暗号化する必要があるアプリケーションがあります。