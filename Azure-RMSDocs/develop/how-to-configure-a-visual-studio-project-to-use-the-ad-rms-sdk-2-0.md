---
title: "Visual Studio の構成 | Azure RMS"
description: "RMS SDK 2.1 を使用するように Visual Studio プロジェクトを構成する手順。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 872bb0c20db2ef8d661d321598a2b1fe61d69316
ms.openlocfilehash: 9747c39742c66735b9619036cb77a914563ecf29


---

# Visual Studio の構成

このトピックでは、Rights Management サービス SDK 2.1 を使用するように Visual Studio プロジェクトを構成する方法について説明します。

## 必要条件

-   [SDK のインストール](install-the-rms-sdk.md)

**手順**

### 手順 1. RMS SDK 2.1 を使用するように Visual Studio プロジェクトを構成する

ここでは、Microsoft Visual Studio 2010 に固有の手順を紹介します。 Microsoft Visual Studio の別のバージョンを使用している場合、設定ダイアログ ボックスが多少異なる場合があります。

次の手順は、ネイティブ 32 ビット アプリケーションのビルドに適用されます。

1.  RMS SDK 2.1 インクルード ディレクトリを Visual Studio 2010 プロジェクトに追加します。

    **[構成プロパティ]** で、**[VC++ ディレクトリ]** を選択し、RMS SDK 2.1 インクルード ディレクトリ **$(MSIPCSDKDIR)\\inc** を **[インクルード ディレクトリ]** フィールドに追加します。

    ![[構成プロパティ] の [インクルード ディレクトリ] フィールド](../media/include_directories.png)

2.  RMS SDK 2.1 ライブラリ ディレクトリを Visual Studio 2010 プロジェクトに追加します。

    **[構成プロパティ]** で、**[VC++ ディレクトリ]** を選択し、使用しているプラットフォームの RMS SDK 2.1 ライブラリ ディレクトリを **[ライブラリ ディレクトリ]** フィールドに追加します。

    -   Win32 の場合は、**$(MSIPCSDKDIR)\\lib** を使用します。
    -   x64 の場合は、**$(MSIPCSDKDIR)\\lib\\x64** を使用します。

    ![[構成プロパティ] の [ライブラリ ディレクトリ] フィールド](../media/library_directories.png)

3.  RMS SDK 2.1 ライブラリ ファイルを Visual Studio 2010 の依存関係として追加します。

    **[リンカー]** で、**[入力]** を選択し、RMS SDK 2.1 ライブラリ ファイル **Msipc.lib** および **Msipc\_s.lib** を **[追加の依存ファイル]** フィールドに追加します。

    ![[リンカー] のライブラリの依存ファイル フィールド](../media/additional_dependencies.png)

4.  RMS SDK 2.1 ダイナミック リンク ライブラリ (DLL) を遅延読み込み DLL として追加します。

    **[リンカー]** で、**[入力]** を選択し、RMS SDK 2.1 DLL ファイル **Msipc.dll** を **[DLL の遅延読み込み]** フィールドに追加します。

    ![[リンカー] の [DLL の遅延読み込み] フィールド](../media/delay_loaded.png)

5.  結果のバイナリのバージョン情報を作成します。

    **[ソリューション エクスプローラー]** で、**[リソース ファイル]** を選択し、目的のバイナリ名を **[OriginalFileName]** フィールドに追加します。

    ![[ソリューション エクスプローラー] の [リソース ファイル] フィールド](../media/original_file_name.png)

## 関連項目

* [SDK のインストール](install-the-rms-sdk.md)
 

 



<!--HONumber=Jun16_HO4-->


