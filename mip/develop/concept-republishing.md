---
title: MIP SDK での再パブリッシュ
description: この記事は、シナリオの再発行に保護ハンドラーを再利用する方法のシナリオを理解するうえで役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 05/01/2020
ms.author: mbaldwin
ms.openlocfilehash: 79fd94614fd19a3cc93c59736931495c9019e2d8
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864976"
---
# <a name="republishing-c"></a>再パブリッシュ (C++)

## <a name="overview"></a>概要

この概要では、mipmap SDK での再パブリッシュに焦点を当てています。アプリケーションでユーザーにファイルの編集を許可する必要があり、所有者、権限、コンテンツキーなどに関する元の [発行ライセンス](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/licenses-and-certificates-and-how-ad-rms-protects-and-consumes/ba-p/247309) 情報を保持する必要がある場合に発生する特定のシナリオです。

パターンは次のようになります。

- ユーザーは、保護されたドキュメントを編集用に開きます。
- ユーザーは、適切な権限が付与されている場合にのみ、ファイルの編集を許可する必要があります。
- ユーザーは、ドキュメントを編集して保存します。

このタスクを実行するための MIP SDK 擬似コードは、次のようになります。

- `mip::FileHandler`ターゲットファイルを指すを作成します。
- `mip::ProtectionHandler`のメソッドによって公開されるを格納し `mip::FileHandler` `GetProtection()` ます。
- メソッドを呼び出して、ユーザーが **編集** 権限を持っていることを確認 `AccessCheck()` します。
- のまたはを使用して `mip::FileHandler` `GetDecryptedTemporaryFileAsync()` `GetDecryptedTemporaryStreamAsync()` 、暗号化解除された一時的な出力を取得します。
- 一時ファイルまたはストリームの内容を編集して保存します。
- `mip::FileHandler`一時ファイルを指す新しいインスタンスを作成し、メソッドを使用し `SetProtection()` `mip::ProtectionHandler` て、パラメーターとして格納されているを指定します。
- 変更をコミットします。

元のファイルのを使用して、 `mip::ProtectionHandler` 編集されたドキュメントに所有者、コンテンツ ID、コンテンツキーなどを保持します。 この再パブリッシュのシナリオでは、アプリケーションが元のへの参照を保持している必要があり `mip::ProtectionHandler` ます。

## <a name="implementation"></a>実装

前に説明したように、 `mip::FileHandler` クラスは、ラベルと保護情報の両方を読み取り、書き込み、および削除するメソッドを公開します。 サポートされている操作の完全な一覧については、 [API リファレンス](./reference/class_mip_filehandler.md#summary)を確認してください。

このシナリオでは、の次のメソッドを使用し `mip::FileHandler` ます。

- `GetProtection()`
- `CommitAsync()`
- `GetDecryptedTemporaryFileAsync()`
- `SetProtection()`

このシナリオでは `mip::ProtectionHandler` 、を使用して、保護されたストリームとバッファーの暗号化と復号化、アクセスチェックの実行、発行ライセンスの取得、および保護された情報からの属性の取得を行う関数を公開します。 メソッドは、 `AccessCheck()` ユーザーがファイルを編集する権限を持っていることを検証するために使用されます。

この再保護シナリオを正常に完了するには、[次のステップ] でクイックスタートを確認し、アプリケーションがビルドされ、ラベルが正常に表示されることを確認します。

## <a name="create-a-protection-handler-from-the-file-and-decrypt-the-file"></a>ファイルから保護ハンドラーを作成し、ファイルの暗号化を解除します。

`mip::ProtectionHandler` 保護されたストリームとバッファーの暗号化と復号化、アクセスチェックの実行、発行ライセンスの取得、および保護された情報からの属性の取得を行うための関数を公開します。 `mip::ProtectionHandler` オブジェクトは、ProtectionDescriptor またはシリアル化された公開ライセンスを提供することによって構築されます。 このユースケースでは、既に保護されているコンテンツを復号化する場合、またはライセンスが既に構築されているコンテンツを保護する場合に、発行ライセンスを暗黙的に使用します。

`mip::FileHandler``GetProtection()`に関連付けられているファイルからを取得するという名前のメソッドを公開 `mip::ProtectionHandler` `mip::FileHandler` します。 オブジェクトを取得したら、同じを使用して、 `mip::ProtectionHandler` ファイルのユーザーのアクセスレベルを検証し、ファイルを復号化した後、ファイルを編集した後で暗号化します。

`mip::ProtectionHandler``AccessCheck()`は、ユーザーがファイルに対して特定の権限を持っていることを検証し、結果に応じてブール型の応答を返すために使用されます。 たとえば、ユーザーが編集権限を持っていることを確認するには、メソッドを呼び出して、値 "EDIT" を渡します。 結果が *true* の場合は、ユーザーにファイルの編集を許可します。 **編集** 権限が検証されたら、を使用し `mip::FileHandler` て、暗号化解除され `GetDecryptedTemporaryFileAsync()` た一時ファイルを取得します。

さまざまなユーザー権利の詳細については、「 [Azure Information Protection のユーザー権利](/azure/information-protection/configure-usage-rights)」を参照してください。

 > [!IMPORTANT]
 > アクセスの確認と強制は、純粋にアプリケーション開発者に対して行われます。 表示権限を持つユーザーは、保護された情報を復号化することができます。 アプリケーションでは、ユーザーに付与された権限のセットを検証し、コピー、編集、スクリーンショットの作成などの情報保護コントロールを使用して権限を適用します。 保護制御を正しく実装できないと、機密情報が公開される可能性があります。

## <a name="save-and-publish-the-edited-file-by-applying-protection"></a>保護を適用して、編集したファイルを保存して発行する

ファイルの暗号化が解除された後、ファイルを編集できます。 編集操作が完了すると、変更をコミットできます。 `IFileHandler`上記の一時ファイルを使用して、コミットされたファイルを処理するオブジェクトを作成します。 一時ファイルは、元のファイルから取得したオブジェクトを使用して保護することができ `IProtectionHandler` ます。

## <a name="next-steps"></a>次の手順

- [C++ の再パブリッシュのクイックスタートを確認する](quick-file-republishing-cpp.md)
- [C の再パブリッシュのクイックスタートを確認する#](quick-file-republishing-csharp.md)