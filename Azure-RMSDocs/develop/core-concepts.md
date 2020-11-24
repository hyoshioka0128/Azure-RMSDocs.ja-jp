---
title: Azure Information Protection SDK 4.2 開発者ガイド |Microsoft Docs
description: Microsoft Rights Management SDK 4.2 では、Active Directory 適切な管理サービス (AD RMS) を活用する AD RMS 対応アプリケーションを構築する方法について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 01/23/2017
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae67523a-c094-44da-86b8-739bedba7111
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 957f347381b4de8abe4f828d4fd7903c0a0e62f3
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "95569583"
---
# <a name="rights-management-sdk42-developer-guidance"></a>Rights Management SDK 4.2 開発者ガイド

Microsoft Rights Management SDK 4.2 では、Active Directory Rights Management サービス (AD RMS) を利用する AD RMS 対応アプリケーションを可能な限りシンプルに構築できるようにすることに重点が置かれています。

RMS 対応アプリケーションを開発するためのデザイン プロセスについては、次のトピックが参考になります。

- [Azure AD でアプリの登録と RMS の有効化を行う方法](authentication-integration.md) - RMS 対応アプリのユーザー認証の基本について説明します。
- [エラーとパフォーマンスのログを有効にする方法](enabling-logging.md) - RMS SDK 4.2 では、診断ログとパフォーマンス ログのアップロードを 1 つのデバイス プロパティで管理します。
- [組み込み権限を使用する方法](built-in-rights-usage-restriction-reference.md) - RMS SDK 4.2 の組み込み権限と、その制限に従うことでアプリケーションによって適用される使用制限について説明します。
- [ドキュメント追跡を使用する方法](how-to-use-document-tracking.md) - ドキュメント追跡機能を使用するには、関連付けられているメタデータの管理とサービスへの登録について理解している必要があります。
