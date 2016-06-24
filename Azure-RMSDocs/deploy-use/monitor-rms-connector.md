---
# required metadata

title: Azure Rights Management コネクタを監視する | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure Rights Management コネクタを監視する

*適用対象: Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

RMS コネクタをインストールして構成した後、以下の方法と情報を使用すると、コネクタと組織の Azure RMS の使用を監視するのに役立ちます。

## アプリケーション イベント ログ エントリ

RMS コネクタは、アプリケーション イベント ログを使用して、**Microsoft RMS コネクタ**のエントリを記録します。 

たとえば、ID 1000 などの情報イベントは、コネクタ サービスが開始したことを示します。ID 1002 はサーバーが正常に RMS コネクタに接続したことを示し、ID 1004 は承認されたアカウントのリスト (各アカウントがリストに含まれる) がコネクタにダウンロードされたことをそのたびに示します。 

HTTPS を使用するようにコネクタを構成していない場合は、クライアントがセキュリティで保護されていない (HTTP) 接続を使用していることを示す警告 ID 2002 が表示されます。

コネクタが Azure RMS への接続に失敗した場合は、通常、エラー 3001 が表示されます。 たとえば、その原因として、DNS の問題や、RMS コネクタを実行している 1 つ以上のサーバーでインターネットにアクセスできないことが考えられます。 

> [!TIP] RMS コネクタ サーバーが Azure RMS に接続できない場合、原因は Web プロキシの構成であることがよくあります。

詳細については、すべてのイベント ログ エントリと同様に、メッセージも詳しく調べてください。

初めてコネクタをデプロイするときは、イベント ログを確認するだけでなく、警告やエラーも継続的に確認してください。 たとえば、当初はコネクタが期待どおりに動作していても、依存する構成を他の管理者が変更してしまう可能性があります。 たとえば、他の管理者が Web プロキシ サーバー構成を変更したために RMS コネクタ サーバーがインターネットにアクセスできなくなったり (エラー 3001)、コネクタの使用を承認されているグループからコンピューター アカウントを削除してしまったりすることがあります (警告 2001)。

## パフォーマンス カウンター

RMS コネクタをインストールすると、**Microsoft Rights Management コネクタ**のパフォーマンス カウンターが自動的に作成されます。これらは、コネクタ経由での Azure RMS の使用のパフォーマンスを監視するために便利です。 

たとえば、ドキュメントや電子メールを保護しているとき、または保護されているドキュメントや電子メールを開いているときに頻繁に遅延が発生する場合は、パフォーマンス カウンターを調べると、遅延の原因がコネクタでの処理時間であるか、Azure RMS での処理時間であるか、ネットワーク遅延であるかを判断できます。 遅延が発生している場所を特定するには、**コネクタの処理時間**、**サービス応答時間**、および**コネクタ応答時間**の平均カウントが含まれているカウンターを調べます。 例: **Licensing Successful Batched Request Average Connector Response Time**。

コネクタを使用する新しいサーバー アカウントを最近追加した場合、確認するとよいカウンターは、**Time since last authorization policy update** です。リストの更新後にコネクタがリストをダウンロードしたことや、もう少し待機する必要があるかどうか (最大 15 分) を確認できます。

## RMS アナライザー

Rights Management サービスのアナライザー ツールを使用すると、コネクタの正常性を監視し、構成の問題を特定できます。

このツールをまだダウンロードしていない場合は、[ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=46437)からダウンロードし、インターネットにアクセスしていて RMS コネクタに接続できる任意のコンピューターにインストールすることができます。 ツールを実行し、**[ようこそ]** ページで **[Azure RMS コネクタ]** オプションを選択します。

その他の情報と手順については、ダウンロード ページの **[詳細]** と **[インストール手順]** を参照してください。

## ログ記録

使用状況ログ記録を使用すると、電子メールやドキュメントが保護および使用された日時を特定できます。 RMS コネクタを使用してこれを実行すると、ログのユーザー ID フィールドには、RMS コネクタのインストール時に自動的に生成されるサービス プリンシパル名が含まれます。

詳細については、「[Azure Rights Management の利用状況をログに記録して分析する](log-analyze-usage.md)」を参照してください。

診断のためにより詳細なログ記録が必要な場合は、Windows Sysinternals の [Debugview](http://go.microsoft.com/fwlink/?LinkID=309277) を使用し、IIS の既定のサイト用の web.config ファイルを変更して RMS コネクタに対するトレースを有効にすることができます。 このためには、次の操作を行います。

1. **%programfiles%\Microsoft Rights Management connector\Web Service** で web.config ファイルを探します。

2. 次の行を探します。

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. 見つかった行を次の行に置き換えます。

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  IIS を停止してから起動し、トレースをアクティブ化します。 

5.  必要なトレースをキャプチャしたら、手順 3. の行を元に戻し、IIS を停止してから再起動します。



<!--HONumber=Jun16_HO2-->


