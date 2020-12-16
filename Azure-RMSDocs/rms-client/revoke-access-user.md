---
title: ドキュメントアクセスの取り消し-Azure Information Protection
description: エンドユーザーが AIP クライアントを使用して、保護されているドキュメントのドキュメントへのアクセスを取り消す方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/21/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: abb96719d51658226211653b4ab4d171fcaa6b2e
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/16/2020
ms.locfileid: "97592759"
---
# <a name="user-guide-revoke-document-access-with-azure-information-protection-public-preview"></a>ユーザーガイド: Azure Information Protection を使用したドキュメントアクセスの取り消し (パブリックプレビュー)

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8 *
>
>***関連**: [AIP 統合ラベルクライアントのみ](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 従来のクライアントについては、「 [ユーザーガイド: AIP classic client を使用してドキュメントを追跡および取り消す](client-track-revoke.md)」を参照してください。

この記事では、Microsoft Office から保護したドキュメントへのアクセスを取り消す方法について説明します。

保護されたドキュメントへのアクセスを取り消すと、前にアクセス権を付与した場合でも、他のユーザーがドキュメントにアクセスできなくなります。 詳細については、「 [ユーザーガイド: 分類と保護」を参照して Azure Information Protection 統合ラベルクライアントを](clientv2-classify-protect.md)参照してください。

統一されたラベル付けクライアントの機能の追跡と取り消しは、現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 

## <a name="revoke-access-from-microsoft-office-apps"></a>Microsoft Office アプリからのアクセスを取り消す

Word、Excel、または PowerPoint からのアクセスを取り消すには:

1. アクセスを取り消す保護されたファイルを開きます。 *現在* のユーザーアカウントを使用して、保護を適用したファイルを指定する必要 *があります*。

    > [!TIP]
    > 単にラベルと保護を適用しただけの場合は、同じセッションでアクセスを取り消すことはできません。 アクセスを取り消す必要がある場合は、ドキュメントを再度開きます。

1. [ **ホーム** ] タブで、[ **秘密度** ] ボタンをクリックし、[ **アクセスの取り消し**] を選択します。

    :::image type="content" source="../media/track-revoke-word.png" alt-text="[Microsoft Word からアクセスを取り消す] を選択します。":::

    > [!NOTE]
    > このオプションが表示されない場合は、 詳細については、 [以下](#dont-see-the-revoke-access-option)の考えられるシナリオを参照してください。
    >
 
1. 確認メッセージが表示されたら、[ **はい** ] をクリックして続行します。

アクセスが取り消され、他のユーザーがドキュメントにアクセスできなくなります。

### <a name="dont-see-the-revoke-access-option"></a>Revoke アクセスオプションが表示されない場合は、

[**感度**] メニューで **アクセスを取り消す** オプションが表示されない場合は、次のいずれかのシナリオが考えられます。

- このセッションでは、保護を適用したばかりの可能性があります。 この場合は、ドキュメントを閉じて再度開き、もう一度やり直してください。

- 保護されていないドキュメントを表示している可能性があります。 アクセスの取り消しは、保護されたドキュメントにのみ関連します。

- 最新の AIP のラベル付けクライアントバージョンがインストールされていないか、インストール後に Office アプリまたはコンピューターの再起動が必要になる可能性があります。 

    詳細については、「 [ユーザーガイド: Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

## <a name="revoking-access-where-the-document-protection-has-been-changed-on-a-copy"></a>コピーでドキュメント保護が変更されたアクセス権を取り消す

別のユーザーがドキュメントのコピーのラベルまたは保護を変更した場合、そのドキュメントのコピーのアクセスは *取り消されません* 。 

これは、アクセスの追跡と取り消しは一意の ContentID 値を使用して行われるため、保護が変更されるたびに変更されます。

> [!IMPORTANT]
> ユーザーがドキュメントのラベルまたは保護レベルを変更し、アクセスを取り消す必要があると思われる場合は、システム管理者に連絡して、ドキュメントのそのコピーに対するアクセスを取り消すことができます。
> 
## <a name="next-steps"></a>次のステップ

詳細については、次を参照してください。

- [AIP 統合ラベルクライアントユーザーガイド](clientv2-user-guide.md)
- [AIP 統一されたラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)
- [ドキュメントアクセスの追跡と取り消しに関する既知の問題](../known-issues.md#tracking-and-revoking-document-access-public-preview)