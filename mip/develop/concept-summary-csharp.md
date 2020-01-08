---
title: Microsoft Information Protection SDK C#ラッパーの概要
description: MIP SDK .NET ラッパーの使用を開始する方法の概要と、.NET ラッパーとC++ SDK の違いについて説明します。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: 21fc590388615b2917ca62fdd848b3a63ce26912
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556114"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Microsoft Information Protection .NET ラッパーを使用したはじめに

Microsoft Information Protection SDK .NET ラッパーを使用すると、開発者は Microsoft Information Protection エクスペリエンスを独自のアプリケーションやサービスに統合できます。 SDK の分類、ラベル付け、保護の機能を使用すると、情報がどこにあるかにかかわらず、分類、ラベル付け、保護を行うことができます。 

マネージラッパーとすべての依存関係は、Visual Studio の NuGet を使用してインストールできます。

## <a name="supported-platforms"></a>［サポートされているプラットフォーム］

Microsoft Information Protection .NET ラッパーは、次の .NET プラットフォームでサポートされています。

* .NET Standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>パッケージのインストール

Visual Studio 2017 のパッケージマネージャーコンソールから、次を実行してパッケージをインストールします。

`install-package Microsoft.InformationProtection.File`

追加のパッケージは必要ありません。 すべてのサードパーティライブラリが含まれており、ビルド時に出力フォルダーにコピーされます。

## <a name="wrapper-details"></a>ラッパーの詳細

.NET ラッパーは、 [SWIG](https://swig.org/)によって生成されるマネージラッパーです。 ラッパーは、Microsoft C++ Information Protection SDK のコンパイル済みライブラリを使用します。 これらの Dll は、 C++バージョンの SDK に含まれている dll と同じです。

## <a name="concept-overlap"></a>概念の重複

SDK とマネージラッパーのバージョンにC++は、いくつかの基本的な違いがあります。

* .NET ラッパーでは、非同期操作にオブザーバーを使用する必要はありません。 非同期操作は、[タスクベースの非同期パターン](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)を介して実装されます。
* .NET ラッパーには、 C++ SDK: authdelegate デリゲートと conのデリゲートの一部であるデリゲートが必要です。 これらのデリゲートは、インターフェイス `IAuthDelegate` および `IConsentDelegate` を介して実装されています。

## <a name="next-steps"></a>次のステップ

次に、「 [Microsoft Information Protection (mip) SDK C#のクイックスタート-初期化](quick-app-initialization-csharp.md)」を確認して、mip 対応の基本的なコンソールアプリケーションの構築を開始します。
