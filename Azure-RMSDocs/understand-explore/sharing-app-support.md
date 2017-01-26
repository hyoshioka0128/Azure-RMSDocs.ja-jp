---
title: "Windows およびモバイル プラットフォーム用の RMS 共有アプリケーション | Azure Information Protection"
description: "Office 2010 のサポートには必須の、Windows コンピューター、Mac コンピューター、モバイル デバイスにも推奨される、無料でダウンロードできるアプリケーションとして RMS 共有アプリケーションが Azure RMS をサポートする方法について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/03/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1da6e372-2b3f-4af7-80f7-6b9073dff7f5
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c8ffebad1130c8ba084c0feb83aa3ec54692ad54
ms.openlocfilehash: 5b438ed97df754b88b0d654439153dea03c8250c


---


# <a name="rms-sharing-application-for-windows-and-mobile-platforms"></a>Windows およびモバイル プラットフォーム用の RMS 共有アプリケーション

>*適用対象: Azure Information Protection、Office 365*

RMS 共有アプリケーションは、無料でダウンロードできるアプリケーションであり、Office 2010 のサポートには必須で、Windows コンピューター、Mac コンピューター、モバイル デバイスにも推奨されます。 利点の&1; つとして、Azure Rights Management サービスをネイティブでサポートしないアプリケーションやファイルの一般的な保護を適用できることが挙げられます。つまり、すべてのファイルを保護できます。 各種の保護レベルの詳細については、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide-technical.md#levels-of-protection--native-and-generic)」の「[保護のレベル – ネイティブと汎用](../rms-client/sharing-app-admin-guide.md)」セクションを参照してください。

ユーザーが RMS 共有アプリケーションを使用してファイルを保護すると、ユーザーが保護したドキュメントを追跡したり、必要に応じてそれらへのアクセスを取り消したりすることもできます。 これを行うには、 [ドキュメント追跡サイト](http://go.microsoft.com/fwlink/?LinkId=529562)を使用します。

Windows コンピューターの場合、RMS 共有アプリケーションは、ユーザーが既に使用しているアプリケーションに既に統合されていて機能を拡張しています。

-   Word、Excel、PowerPoint、および Outlook 用の Office アドインのインストール。 このアドオンにより、**[Share Protected]** (保護ファイルの共有) ボタンがリボンに表示され、このボタンをクリックすると、電子メールで送信されるファイルの保護の設定に最もよく使用される、使いやすいダイアログ ボックスが開きます。 また、このボタンを利用するとドキュメント追跡サイトに簡単にアクセスできます。

-   エクスプローラーの新しい右クリック オプション。 このオプションにより、**[Protect in-place]** (保護済み) オプションが表示され、このボタンをクリックすると、ディスクに保存されているファイルの保護の設定に最もよく使用される、使いやすいダイアログ ボックスが開きます。

-   Azure Rights Management サービスによって保護されているファイルを開くビューアー。 このビューアーは、保護されたファイルを開くことができるアプリケーションが他にインストールされていない場合に自動的に起動します。

-   Office 2010 のバックエンド構成により、このスイートの Word、Excel、PowerPoint、および Outlook が Azure Rights Management サービスとシームレスに連携できるようになります。

Windows 用の RMS 共有アプリケーションは、 [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970)ページを使用して&1; つのコンピューターにダウンロードしてインストールできますが、サイレント インストールおよびカスタム構成のためのエンタープライズ デプロイもサポートされています。 詳細については、次のリソースを参照してください。

-   [Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)

-   [Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)

モバイル デバイス用の RMS 共有アプリケーションは、iPad、iPhone、Android、Windows Phone、Windows RT などの最も一般的に使用されているモバイル デバイスをサポートします。 ユーザーは、関連するストアからこのアプリをダウンロードできます。 [Microsoft Rights Management ページ](http://go.microsoft.com/fwlink/?LinkId=303970)には、それらのリンクがあります。

**Microsoft Intune がある場合**: RMS 共有アプリには Microsoft Intune アプリ ソフトウェア開発キットが含まれているため、次のオプションを使用できます。

-   Intune で登録されている iOS および Android デバイス用のアプリをデプロイおよび管理する。

-   Intune で登録されていない Android デバイス用のアプリを管理する。


## <a name="next-steps"></a>次のステップ
他のアプリケーションおよびサービスで Azure Information Protection からの Azure Rights Management サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Jan17_HO4-->


