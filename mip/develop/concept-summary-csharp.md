---
title: Microsoft Information Protection SDK C# ラッパーの概要
description: MIP SDK .NET ラッパーの使用を開始する方法の概要と、.NET ラッパーと C++ SDK の違いについて説明します。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: da563bc385658d716d6813710495d91b42bbcc83
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570038"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Microsoft Information Protection .NET ラッパーを使用したはじめに

Microsoft Information Protection SDK .NET ラッパーを使用すると、開発者は Microsoft Information Protection エクスペリエンスを独自のアプリケーションやサービスに統合できます。 SDK の分類、ラベル付け、保護の機能を使用すると、情報がどこにあるかにかかわらず、分類、ラベル付け、保護を行うことができます。 

マネージラッパーとすべての依存関係は、Visual Studio の NuGet を使用してインストールできます。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

Microsoft Information Protection .NET ラッパーは、次の .NET プラットフォームでサポートされています。

* .NET Standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>パッケージのインストール

Visual Studio 2017 のパッケージマネージャーコンソールから、次を実行してパッケージをインストールします。

`install-package Microsoft.InformationProtection.File`

追加のパッケージは必要ありません。 すべてのサードパーティライブラリが含まれており、ビルド時に出力フォルダーにコピーされます。

## <a name="wrapper-details"></a>ラッパーの詳細

.NET ラッパーは、 [SWIG](https://swig.org/) によって生成されるマネージラッパーです。 ラッパーは、Microsoft Information Protection SDK のコンパイル済み C++ ライブラリを使用します。 これらの Dll は、C++ バージョンの SDK に含まれている Dll と同じ Dll です。

## <a name="concept-overlap"></a>概念の重複

C++ バージョンの SDK とマネージラッパーの間には、いくつかの基本的な違いがあります。

* .NET ラッパーでは、非同期操作にオブザーバーを使用する必要はありません。 非同期操作は、 [タスクベースの非同期パターン](/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)を介して実装されます。
* .NET ラッパーには、C++ SDK: AuthDelegate デリゲートと Conのデリゲートの一部であるデリゲートが必要です。 これらのデリゲートは、インターフェイスを介して実装されます。 `IAuthDelegate``IConsentDelegate`

## <a name="next-steps"></a>次の手順

次に、「 [Microsoft Information Protection (mip) SDK C# のクイックスタート-初期化](quick-app-initialization-csharp.md) 」をレビューして、mip 対応の基本的なコンソールアプリケーションの構築を開始します。