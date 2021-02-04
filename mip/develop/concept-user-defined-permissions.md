---
title: 概念-MIP SDK-ユーザー定義のアクセス許可の主要な概念。
description: この記事は、ユーザー定義のアクセス許可と呼ばれる主要な SDK の概念を理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/02/2021
ms.author: tommos
ms.openlocfilehash: 27d17b14ed34ae72fafdf1084d277d3389a1790c
ms.sourcegitcommit: 314f8109920a706bd1000dd4e63ba9cdd12cd671
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/04/2021
ms.locfileid: "99554193"
---
# <a name="microsoft-information-protection-sdk---user-defined-permissions"></a>Microsoft Information Protection SDK-ユーザー定義のアクセス許可

Microsoft Information Protection SDK では、テンプレートベースのアクセス許可とユーザー定義の2種類のラベルに基づくアクセス許可がサポートされています。

- **テンプレートベースのアクセス許可:** これらの権限は、セキュリティとコンプライアンスセンターのラベル管理者によって定義されます。 これらのラベルは一元的に管理され、構成の変更は、既にファイルのコピーを持っているユーザーに影響します。 たとえば、管理者が承認されたユーザーの一覧からユーザーを削除した場合、そのユーザーは次にライセンスを取得しようとしたときに保護されたデータにアクセスできなくなります。

- **ユーザー定義のアクセス許可**: これらの権限は、エンドユーザーまたはアプリケーションによって **ラベル付けされるときに** 定義されます。 アクセス許可は、ユーザーからロールまたはユーザーと権限のマッピングのコレクションの形式で MIP SDK に渡されます。 これらの権限は、保護されたドキュメントの公開ライセンスに書き込まれます。テンプレートベースのアクセス許可とは異なり、直接アクセスしてドキュメントを変更しなくても、共有後に一元的に管理または変更することはできません。

## <a name="users-rights-and-roles"></a>ユーザー、権限、およびロール

ラベル付け時にユーザーによって権限が定義されることが予想されるため、アプリケーションは、ユーザーまたはサービスがユーザーの電子メールアドレスと権限またはロールに対する入力を提供できるようにするためのインターフェイスを提供する必要があります。 この構成は、オブジェクトまたはオブジェクトのコレクションを渡すことによって実現され `UserRoles` `UserRights` ます。具体的には、ドキュメントへのアクセスレベルをどのユーザーに与えるかを定義します。

```csharp
// Create a List<string> of the first set of permissions. 
List<string> users = new List<string>()
{
    "alice@contoso.com",
    "bob@contoso.com"
};

// Create a List<string> of the Rights the above users should have. 
List<string> rights = new List<string>()
{
    Rights.View,
    Rights.Edit                
};

// Create a UserRights object containing the defined users and rights.
UserRights userRights = new UserRights(users, rights);

// Add them to a new List<UserRights>
List<UserRights> userRightsList = new List<UserRights>()
{
    userRights
};
```

結果として、 `List<UserRights>` Alice と Bob の両方が保護されたファイルで表示および編集できることを指定するコレクションが作成されます。 *別* のアクセス許可セットを持つユーザーをさらに追加するには、プロセスを繰り返して2番目のオブジェクトを作成し `UserRights` 、新しいユーザーとアクセス許可を渡して、を `List<UserRights>` 呼び出してコレクションに追加し `userRightsList.Add(userRights2)` ます。

このパターンは、にも当てはまり `UserRoles` 、 **権限** を **ロール** に置き換えてコレクションを作成するだけで実装でき `List<UserRoles>` ます。

### <a name="apply-protection"></a>保護の適用

保護の設定は、 `ProtectionDescriptor` オブジェクトまたはオブジェクトからを作成してからに渡すことによって実現でき `List<UserRights>` `List<UserRoles>` `FileHandler.SetProtection()` ます。 最後に、ファイルに対する変更をコミットして、新しいファイルを書き込みます。 

### <a name="when-to-apply-protection-to-files"></a>ファイルに保護を適用する場合

MIP SDK を使用してラベルを設定すると、 `FileHandler.SetLabel()` すべての操作を実行し、保護を適用する必要があります。 ラベルがユーザー定義のアクセス許可 (UDP) 用に構成されている場合、アプリケーションでは、ラベルが UDP ラベルであることを事前に把握することはできません。 MIP SDK は、型の例外をスローすることによってこの情報をサーフェイスし `Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException` ます。 `FileHandler`コードでこの例外をキャッチし、ユーザーまたはサービスインターフェイスをトリガーしてカスタムアクセス許可を定義する必要があります。 完了すると、保護を設定できるようになります。 次の例は、エンドツーエンドのパターンを示していますが、オブジェクトをビルドする関数が既に実装されていることを前提としてい `List<UserRights>` ます。

```csharp
try
{
    // Attempt to set the label. If it's a UDP label, this will throw. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());
}

catch (Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException)
{
    // Assumes you've create a function that returns the List<UserRights> as previously detailed. 
    List<UserRights> userRightsList = GetUserRights();

    // Create a ProtectionDescriptor using the set of UserRights.
    ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(userRightsList);
    
    // Apply protection to the file using the new ProtectionDescriptor. 
    handler.SetProtection(protectionDescriptor, new ProtectionSettings());

    // Set the label. This will now succeed as protection has been defined. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());

    // Commit the change. 
    var result = Task.Run(async () => await handler.CommitAsync("myFileOutput.xlsx")).Result;
}
```

## <a name="custom-protection"></a>カスタム保護

このプロセスを使用すると、保護を設定し、手順をスキップして保護のみを設定することもでき `SetLabel()` ます。 アプリケーションでラベルを適用する必要がない場合は、例外ハンドラーは不要であり、このパターンに従って保護を設定でき `ProtectionDescriptor`  ->  `SetProtection()`  ->  `CommitAsync()` ます。

## <a name="next-steps"></a>次の手順

- [Microsoft 365 のドキュメントで、ラベル暗号化の構成を確認します。](https://docs.microsoft.com/en-us/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide#understand-how-the-encryption-works)
