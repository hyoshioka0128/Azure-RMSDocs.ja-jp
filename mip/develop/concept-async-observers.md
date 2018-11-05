---
title: 概念 - MIP SDK でのオブザーバー。
description: MIP SDK は、ほぼ完全に非同期になるように設計されています。 この記事は、オブザーバーの実装方法と非同期処理への使用方法を理解するのに役立ちます。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 99f68383a4e697f4f8f04c19523ccb0fb50fa3c0
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445562"
---
# <a name="microsoft-information-protection-sdk---observer-concepts"></a>Microsoft Information Protection SDK - オブザーバーの概念

MIP SDK は、ほぼ完全に非同期になるように設計されています。 たとえば、ネットワークまたはファイルの IO の結果であるすべての操作は非同期に実行されます。 これらの非同期イベントのイベント通知を処理するために、SDK は[オブザーバー パターン](https://wikipedia.org/wiki/Observer_pattern)を使用します。 

## <a name="implementation-overview"></a>実装の概要

非同期操作を実行するオブジェクトを構築する場合、`Observer` クラスを実装する必要があります。 オブザーバーは MIP SDK のさまざまな非同期操作に関連する通知イベントを受け取り、呼び出し元に結果を渡します。

各 `Observer` クラスの関数は、仮想で、優先される非同期パターンでオーバーライドされます。 SDK は、`std::promise` と `std::future` を介してイベント通知オブザーバーのパターンを実装します。

各クラスに固有のオブザーバーには、非同期操作の結果用に一連の success および error/failure 関数があります。 *Success* 関数は、操作と関連するオブジェクトを返します。 *Error*/*Failure* 関数は、操作がなぜ失敗したかの詳細を含む例外を返します。

たとえば、`FileProfile` では次の 2 つの操作をサポートしています。 

- これでは、`FileProfile::AddEngineAsync` を介してプロファイルに新しいエンジンを追加できます。 
- これでは、`FileProfile::UnloadEngineAsync` を使用してプロファイルからエンジンをアンロードできます。

2 つの `Observer` 関数は非同期操作ごとに実装されるので、`FileProfile` には **4 つ**の `Observer` メソッドが関連付けられていると想定できます。 

- `FileProfileObserver::OnAddEngineSuccess()`
- `FileProfileObserver::OnAddEngineError()`
- `FileProfileObserver::OnUnloadEngineSuccess`
- `FileProfileObserver::OnUnloadEngineError()`。 

## <a name="mip-sdk-observer-classes"></a>MIP SDK オブザーバー クラス

MIP SDK ファイル API には、2 つのオブザーバー クラスがあります。

* `mip::FileProfile::Observer`
* `mip::FileHandler::Observer`

MIP SDK ポリシー API には、オブザーバーが 1 つのみあります。

* `mip::Profile::Observer`

MIP SDK 保護 API には、オブザーバーが 3 つあります。

* `mip::ProtectionProfile::Observer`
* `mip::ProtectionEngine::Observer`
* `mip::ProtectionHandler::Observer`

## <a name="next-steps"></a>次の手順

オブザーバーが、さまざまな API によってどのように実装され、使用されるかについて説明しています。

* [ファイル API オブザーバー (C++)](concept-async-observers-file-cpp.md)
* [ポリシー API オブザーバー (C++)](concept-async-observers-policy-cpp.md)
* [保護 API オブザーバー (C++)](concept-async-observers-protection-cpp.md)
