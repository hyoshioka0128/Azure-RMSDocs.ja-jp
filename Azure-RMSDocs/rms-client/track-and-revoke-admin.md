---
title: アクセスの追跡と取り消し-Azure Information Protection
description: 管理者が保護されたドキュメントのドキュメントアクセスを追跡し、必要に応じてアクセスを取り消す方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 12/08/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: ac4e506d3c3a6f582975a435a7e9f1e327068ac2
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/16/2020
ms.locfileid: "97592766"
---
# <a name="administrator-guide-track-and-revoke-document-access-with-azure-information-protection-public-preview"></a>管理者ガイド: Azure Information Protection を使用したドキュメントアクセスの追跡と取り消し (パブリックプレビュー)

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8 *
>
>***関連**: [AIP 統合ラベルクライアントのみ](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 従来のクライアントについては、「 [管理者ガイド: AIP でのドキュメント追跡の構成と使用](client-admin-guide-document-tracking.md)」を参照してください。

[バージョン 2.9.109.0](unifiedlabelingclient-version-release-history.md#version-291090-public-preview)以降にアップグレードした場合、追跡用にまだ登録されていない保護されたドキュメントは、AIP 統合ラベルクライアントを使用して次回開いたときに自動的に登録されます。

ドキュメントを追跡対象として登録すると、AIP のグローバル管理者は、成功したアクセスイベントや拒否された試行など、アクセスの詳細を追跡し、必要に応じてアクセスを取り消すことができます。 

統一されたラベル付けクライアントの機能の追跡と取り消しは、現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 

## <a name="track-document-access"></a>ドキュメントのアクセスの追跡

管理者は、登録時に保護されたドキュメント用に生成された ContentID を使用して、保護されたドキュメントへのアクセスを PowerShell で追跡できます。

**ドキュメントのアクセスの詳細を表示するに** は:

追跡するドキュメントの詳細を検索するには、次のコマンドレットを使用します。

1. 追跡するドキュメントの **ContentID** 値を検索します。
    
    [Get-AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog)を使用して、保護を適用したユーザーのファイル名や電子メールアドレスを使用してドキュメントを検索します。
    
    次に例を示します。
        
    ```PowerShell
    PS C:\>Get-AipServiceDocumentLog -ContentName "test.docx" -OwnerEmail “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```
 
    このコマンドは、追跡用に登録されている、すべての一致する保護されたドキュメントの **ContentID** を返します。

    > [!NOTE]
    > 保護されたドキュメントは、統合されたラベル付けクライアントがインストールされているコンピューターで最初に開かれたときに、追跡用に登録されます。 このコマンドによって保護されたファイルの ContentID が返されない場合は、ドキュメントを追跡するために登録するために、統合されたラベル付けクライアントがインストールされているコンピューターで開きます。

1. ドキュメントの **ContentID** と共に [Get AipServiceTrackingLog](/powershell/module/aipservice/get-aipservicetrackinglog)コマンドレットを使用して、追跡データを返します。

    次に例を示します。
    
    ```PowerShell
    PS C:\>Get-Get-AipServiceTrackingLog -ContentId c03bf90c-6e40-4f3f-9ba0-2bcd77524b87
    ```

    アクセスを試行したユーザーの電子メール、アクセスが許可または拒否されたかどうか、試行の日時、およびアクセス試行が発生したドメインと場所を含む、追跡データが返されます。

## <a name="revoke-document-access-from-powershell"></a>PowerShell からドキュメントへのアクセスを取り消す

管理者は、 [Set-AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) コマンドレットを使用して、ローカルのコンテンツ共有に格納されている保護されたドキュメントのアクセスを取り消すことができます。 

1. アクセスを取り消すドキュメントの ContentID 値を検索します。
    
    [Get-AipServiceDocumentLog](/powershell/module/aipservice/get-aipservicedocumentlog)を使用して、保護を適用したユーザーのファイル名や電子メールアドレスを使用してドキュメントを検索します。
    
    次に例を示します。
        
    ```PowerShell
    PS C:\>Get-AipServiceDocumentLog -ContentName "test.docx" -OwnerEmail “alice@contoso.com” -FromTime "12/01/2020 00:00:00" -ToTime "12/31/2020 23:59:59"
    ```

    返されるデータには、ドキュメントの ContentID 値が含まれます。

    > [!TIP]
    > ContentID 値を持つのは、保護され、追跡のために登録されているドキュメントだけです。 
    >
    > ドキュメントに ContentID がない場合は、統一されたラベル付けクライアントがインストールされているコンピューターで開き、追跡用にファイルを登録します。

1. ドキュメントの ContentID によって設定された [AIPServiceDocumentRevoked](/powershell/module/aipservice/set-aipservicedocumentrevoked) を使用して、アクセスを取り消します。

    次に例を示します。

    ```PowerShell
    Set-AipServiceDocumentRevoked -ContentId 0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
    ```

> [!TIP]
> ユーザーは、Office アプリの [ **秘密度** ] メニューから直接保護を適用したドキュメントのアクセスを取り消すこともできます。 詳細については、「[ユーザーガイド: Azure Information Protection によるドキュメントアクセスの取り消し](revoke-access-user.md)」を参照してください。

### <a name="un-revoke-access"></a>アクセスの取り消し

特定のドキュメントへのアクセスが誤って取り消された場合は、 [Clear-AipServiceDocumentRevoke](/powershell/module/aipservice/clear-aipservicedocumentrevoke)コマンドレットで同じ **ContentID** 値を使用して、アクセスの取り消しを解除します。 

次に例を示します。 

```PowerShell
Clear-AipServiceDocumentRevoke -ContentId   0e421e6d-ea17-4fdb-8f01-93a3e71333b8 -IssuerName testIssuer
```

"発行先 **" パラメーターで** 定義したユーザーにドキュメントアクセスが付与されます。

## <a name="next-steps"></a>次のステップ

詳細については、次を参照してください。

- [AIP 統合ラベルクライアントユーザーガイド](clientv2-user-guide.md)
- [AIP 統一されたラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)
- [ドキュメントアクセスの追跡と取り消しに関する既知の問題](../known-issues.md#tracking-and-revoking-document-access-public-preview)