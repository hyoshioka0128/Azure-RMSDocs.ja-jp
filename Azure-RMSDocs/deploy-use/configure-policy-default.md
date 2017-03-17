---
title: "Azure Information Protection の既定のポリシー"
description: "Azure Information Protection の既定のポリシーの構成方法について説明します。 既定のポリシーを変更した場合、これらの値を参照して、ポリシーを既定値に戻すことができます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
ms.openlocfilehash: 3a2c5af41023021893f0eb751321e798ea523e8c
ms.sourcegitcommit: d5ce1bce5e63b3e510033ff9d4d246dd3511ed7c
translationtype: HT
---
# <a name="the-default-azure-information-protection-policy"></a>Azure Information Protection の既定のポリシー

>*適用対象: Azure Information Protection*

以下では、Azure Information Protection の既定のポリシーの構成方法を説明します。 既定のポリシーを変更した場合、これらの値を参照して、ポリシーを既定値に戻すことができます。


## <a name="information-protection-bar"></a>Information Protection バー

|Setting|値|
|-------------------------------|---------------------------|
|タイトル|検出感度|
|ツールヒント|情報の秘密度は&4; つの異なるレベル (パブリック、内部、機密、秘密) で構成され、これによってユーザーは、社内または社外の承認されていないユーザーに対する情報漏えいのリスクを識別できます。|

## <a name="labels"></a>ラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|個人用|個人用としてのみ使用します。 このデータは組織によって監視されることはありません。 個人用の情報にビジネスに関連するデータを含めないでください。|**有効**: オン <br /><br />**色**: 明るい緑<br /><br />**視覚的なマーキング**: オフ <br /><br />**条件**: なし<br /><br />**保護**: なし|
|パブリック|これは内部情報であり、社内および社外のだれもが使用できます。|**有効**: オン <br /><br />**色**: 緑<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|内部|この情報には、すべての従業員が使用でき、承認された顧客およびビジネス パートナーと共有できる、幅広い内部ビジネス データが含まれます。 内部情報の例として、会社のポリシーや、ほとんどの内部通信が挙げられます。|**有効**: オン <br /><br />**色**: 青 <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />**条件**: なし<br /><br />**保護**: なし|
|社外秘|このデータには機密性の高いビジネス情報が含まれます。 承認されていないユーザーにこのデータを公開すると、組織に損害が生じる可能性があります。 機密情報の例には、従業員情報、個々の顧客のプロジェクトまたは契約書、販売取引データなどがあります。|**有効**: オン <br /><br />**色**: オレンジ<br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />**条件**: なし<br /><br />**保護**: なし|
|秘密|このデータには、保護する必要がある機密性の高いビジネス情報が含まれます。 承認されていないユーザーに秘密データを公開すると、組織に深刻な損害が生じる可能性があります。 秘密情報の例には、個人識別情報、顧客レコード、ソース コード、発表前の財務レポートなどがあります。|**有効**: オン <br /><br />**色**: 赤<br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />**条件**: なし<br /><br />**保護**: なし|

## <a name="sub-labels"></a>サブラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|秘密 \ 会社全体|このデータには、すべての会社の従業員に対して許可される機密性のあるビジネス情報が含まれます。|**有効**: オン <br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|秘密 \ マイ グループ|このデータには、従業員グループに対してのみ許可される機密性のあるビジネス情報が含まれます。|**有効**: オン <br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|

## <a name="global-settings"></a>グローバル設定

|Setting|値|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) (すべてのドキュメントと電子メールにラベルを設定する必要があります (自動設定またはユーザーが設定))|オフ|
|Select the default label (既定のラベルを選択する)|None|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります)|オフ|


## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]