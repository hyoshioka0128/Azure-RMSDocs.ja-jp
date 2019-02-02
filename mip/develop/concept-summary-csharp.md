---
title: Microsoft Information Protection SDKC#ラッパーの概要
description: MIP SDK .NET ラッパー、および .NET ラッパーと C++ SDK の違いを開始する方法の概要。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/04/2019
ms.author: tommos
ms.openlocfilehash: ec1d2083449f1cb4ffccb086f71a7085a9251604
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651981"
---
# <a name="getting-started-with-the-microsoft-information-protection-net-wrapper"></a>Microsoft の情報保護の .NET ラッパーの概要

Microsoft の情報保護 SDK .NET ラッパーでは、独自のアプリケーションとサービスで、Microsoft Information Protection エクスペリエンスを統合することができます。 SDK の分類、ラベル付け、および保護機能のヘルプ情報がされていることを確認するというラベルが付いたし、場所をたどる際に関係なく保護します。 

Visual Studio で NuGet を使用してマネージ ラッパーとすべての依存関係をインストールすることができます。

## <a name="supported-platforms"></a>サポートされるプラットフォーム

Microsoft の情報保護の .NET ラッパーは、次の .NET プラットフォームでサポートされます。

* .NET standard 2.0
* .NET 4.0

## <a name="installing-the-package"></a>パッケージをインストールします。

Visual Studio 2017 でのパッケージ マネージャー コンソールから実行して、パッケージをインストールします。

`install-package Microsoft.InformationProtection.File`

その他のパッケージは必要ありません。 すべてのサード パーティ製のライブラリが含まれ、ビルドの出力フォルダーにコピーされます。

## <a name="wrapper-details"></a>ラッパーの詳細

.NET ラッパーが、 [SWIG](https://swig.org/)マネージ ラッパーを生成します。 ラッパーは、Microsoft Information Protection の SDK からコンパイル済みの C++ ライブラリを使用します。 これらの Dll は、C++ のバージョンの SDK に含まれている同じ Dll です。

## <a name="concept-overlap"></a>概念の重複

C++ のバージョンの SDK とマネージ ラッパーの間のいくつかの基本的な違いがあります。

* .NET ラッパーは、非同期操作のオブザーバーの使用を必要としません。 使用してすべての非同期操作が実装されている、[タスクベースの非同期パターン](https://docs.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap)します。
* .NET ラッパーは、デリゲートは C++ SDK の一部である必要があります。Authdelegate: ConsentDelegate. これらのデリゲートが、インターフェイスを使用して実装されている`IAuthDelegate`と `IConsentDelegate`

## <a name="next-steps"></a>次の手順

次に、確認[クイック スタート - Microsoft Information Protection (MIP) SDK の初期化C# ](quick-app-initialization-csharp.md) MIP 対応の基本的なコンソール アプリケーションの構築を開始します。
