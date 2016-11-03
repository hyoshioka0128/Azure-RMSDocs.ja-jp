---
title: "iOS 用および Android 用の Azure Information Protection アプリに関する FAQ | Azure Information Protection"
description: 
keywords: "iOS 用および Android 用の Azure Information Protection アプリの使用に役立つよく寄せられる質問"
author: cabailey
manager: mbaldwin
ms.date: 10/14/2016
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 539b4ff8-5d3b-4c4d-9c84-c14da83ff76d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c03bcfc5590035ab0d51cb3b4f2b7196db458ea3
ms.openlocfilehash: 1829557b41d2c49ac661cbde96f69dda2ccc5b19


---

# iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ

*適用対象: Active Directory Rights Management サービス、Azure Information Protection*

このページでは、iOS 用および Android 用の Azure Information Protection アプリの使用に役立つよく寄せられる質問への回答を示します。

## Azure Information Protection アプリを使ってできる操作

お使いの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合、このアプリを使うと、権利が保護された電子メール メッセージ (.rpmsg ファイル) を表示できます。 このアプリでは、権利で保護された PDF ファイル、画像、テキスト ファイルを表示することもできます。 現時点では、このアプリを使用して、保護されたメール メッセージを新規作成したり、メール メッセージに返信したり、保護されたファイルを作成または編集したりすることはできません。

## SharePoint の保護されているライブラリと OneDrive For Business にある PDF ファイルを開くことはできますか。

はい。SharePoint と OneDrive for Business によって、他のユーザーがお客様と共有している保護された PDF ファイルを開くことができます。 リンクをタップし、このアプリを選択してファイルを自分用に開きます。 

## ビューアー アプリを開始するにはどうすればよいですか。

モバイル デバイスで、アプリがビューアーでの表示をサポートするファイルのいずれかにアクセスする必要があります。 次に例を示します。

- **.rpmsg ファイル**: モバイル デバイスの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合に、電子メール メッセージの添付ファイルとして表示する、権利が保護された電子メール メッセージ。 
    
    別のデバイスを使用して、モバイル デバイスからアクセスできる権利が保護された電子メール メッセージを自分自身に送信します。 たとえば、Windows コンピューターから Outlook を使用します。 Rights Management をネイティブにサポートする電子メール クライアントの一覧については、「[Azure Rights Management データ保護をサポートするアプリケーション](../get-started/requirements-applications.md)」ページの「電子メール」列を参照してください。

- **権利が保護された PDF ファイル**: Windows コンピューターの Rights Management 共有アプリケーションまたは Rights Management をネイティブにサポートする PDF アプリケーションを使用して、権利が保護された PDF ファイルを電子メールの添付ファイルとして自分自身に送信します。 または、自分の電子メール アドレスを使用し、SharePoint で保護されたライブラリに PDF ファイルをアップロードして共有します。

- **.ptxt、.pjpg、.ppng**: Windows コンピューターの Rights Management 共有アプリケーションと [[保護ファイルの共有]](sharing-app-protect-by-email.md) オプションを使用して、保護されたファイルを電子メールの添付ファイルとして自分自身に送信します。 テストのために使用できるすべてのファイルの種類の一覧については、Rights Management 共有アプリケーション管理者ガイドの「[サポートされているファイルの種類とファイル名拡張子](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)」セクションの最初の表を参照してください。 

これらのファイルを Azure Information Protection ビューアー アプリで表示するには、電子メールの添付ファイルまたはリンクをタップします。 ファイルを開くアプリの選択を求められたら、**[AIP Viewer]** (AIP ビューアー) アプリを選択します。 職場または学校アカウントでサインインするように求められます。 正常に認証されると、Azure Information Protection アプリで電子メールまたはファイルが表示されて読めるようになります。

## このアプリにサインインするにはどのような資格情報を使用する必要がありますか?

組織が既に (モバイル デバイス拡張機能と共に) オンプレミスの AD RMS を所有している、または Azure Rights Management サービスを使用している場合は、自分の資格情報を使用してサインインできます。 それ以外の場合は、[Azure Rights Management ページ](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload) を使用して、無料の新しいアカウントにサインアップできます。

## Hotmail または Gmail アカウントなど、個人の電子メール アドレスで無料アカウントにサインアップできますか?

まだできません。 現在、勤務先の電子メール アドレス (職場または学校のアカウント) でのみサインアップできます。 個人の電子メール アドレスのサポートに取り組んでおり、利用可能になった場合はこのエントリを更新します。

## このアプリで開くことができるファイル拡張子

.rpmsg、.pdf、.ppdf、.pjpg、.ptxt、およびその他のいくつかのテキストと画像ファイル形式を開くことができます。

##  このアプリに関するフィードバックを提供する方法

アプリで、**[設定]** > **[フィードバックの送信]** に移動します。


## 自分の質問が回答されていません。どうすればよいですか。

質問を [Yammer サイト](http://www.yammer.com/AskIPTeam) に投稿するか、または [情報保護チームに電子メールを送信](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app)してください。



<!--HONumber=Oct16_HO2-->


