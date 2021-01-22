---
title: Rights Management コネクタを監視する - AIP
description: Azure Information Protection からコネクタと組織の Azure Rights Management サービスの使用を監視するのに役立つ情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/20/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 49b74533f745906ee919173884c8bc4bafdb52fa
ms.sourcegitcommit: ee20112ada09165b185d9c0c9e7f1179fc39e7cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/21/2021
ms.locfileid: "98659104"
---
# <a name="monitor-the-azure-rights-management-connector"></a>Azure Rights Management コネクタを監視する

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>***関連する内容**:[AIP の統合ラベル付けクライアントとクラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

RMS コネクタのインストールと構成を行うと、以下の方法と情報を使用することで、コネクタと組織の Azure Rights Management サービスの使用状況を Azure Information Protection から監視できます。

## <a name="application-event-log-entries"></a>アプリケーション イベント ログ エントリ

RMS コネクタは、アプリケーション イベント ログを使用して、**Microsoft RMS コネクタ** のエントリを記録します。 

たとえば、次のような情報イベントです。

- ID 1000、コネクタ サービスが開始されたことを確認

- ID 1002、サーバーが RMS コネクタに正常に接続したとき

- ID 1004、承認済みアカウントの一覧 (各アカウントの一覧) がコネクタにダウンロードされるとき 

HTTPS を使用するようにコネクタを構成していない場合は、クライアントがセキュリティで保護されていない (HTTP) 接続を使用していることを示す警告 ID 2002 が表示されます。

コネクタが Azure Rights Management サービスへの接続に失敗した場合は、通常、エラー 3001 が表示されます。 たとえば、この接続エラーは、DNS の問題や、RMS コネクタを実行している1つ以上のサーバーでインターネットにアクセスできないことが原因である可能性があります。 

> [!TIP]
> RMS コネクタ サーバーが Azure Rights Management サービスに接続できない場合、その理由の多くが Web プロキシの構成によるものです。

詳細については、すべてのイベント ログ エントリと同様に、メッセージも詳しく調べてください。

初めてコネクタをデプロイするときは、イベント ログを確認するだけでなく、警告やエラーも継続的に確認してください。 当初はコネクタが期待どおりに動作していても、依存する構成を他の管理者が変更してしまう可能性があります。 たとえば、別の管理者が web プロキシサーバーの構成を変更して、RMS コネクタサーバーがインターネットにアクセスできないようにする (エラー 3001) か、コネクタを使用する権限が指定されているグループからコンピューターアカウントを削除します (警告 2001)。

### <a name="event-log-ids-and-descriptions"></a>イベント ログ ID と説明

次のセクションでは、可能性のあるイベント ID、説明、およびその他の情報を特定できます。

-----

情報 **1000**

**Microsoft RMS コネクタの Web サービスが開始しました。**

このイベントは、RMS コネクタが最初に起動しようとしたときに記録されます。

----

情報 **1001**

**Microsoft RMS コネクタ Web サービスが停止しました。**

このイベントは、通常の操作の結果として、RMS コネクタが停止したときに記録されます。 たとえば、IIS が再起動したか、コンピューターがシャットダウンされた場合などです。 

----

情報 **1002**

**承認されたサーバーのみが Microsoft RMS コネクタにアクセスできます。**

このイベントは、オンプレミス サーバーのアカウントが RMS コネクタの管理者ツールで Azure RMS 管理者によって承認された後、初めて RMS コネクタに接続されたときに記録されます。 SID、アカウント名、接続を行っているコンピューターの名前がイベント メッセージに含まれます。

----

情報 **1003**

**以下に示すクライアントからの接続が、セキュリティで保護されていない (HTTP) 接続から、セキュリティで保護された (HTTPS) 接続に切り替わりました。**

このイベントは、オンプレミス サーバーから RMS コネクタへの接続が HTTP (安全性が低い) から HTTPS (安全性が高い) に変更されたときに記録されます。 SID、アカウント名、接続を行っているコンピューターの名前がイベント メッセージに含まれます。

----

情報 **1004**

**承認されたアカウントの一覧が更新されました。**

このイベントは、RMS コネクタの使用が承認されているアカウントの最新の一覧 (既存のアカウントとすべての変更) を RMS コネクタがダウンロードしたときに記録されます。 RMS コネクタが Azure Rights Management サービスと通信できる場合、この一覧は 15 分ごとにダウンロードされます。

----

警告 **2000**

**HTTP コンテキストにユーザー プリンシパルがないか、無効です。Microsoft RMS コネクタ Web サイトで、IIS の匿名認証が無効にされ、Windows 認証だけが有効にされていることを確認してください。**

このイベントは、RMS コネクタに接続しようとしているアカウントを RMS コネクタが一意に識別できないときに記録されます。 これは、IIS の匿名認証が正しく構成されていないか、アカウントが信頼されていないフォレストのものであることが原因である可能性があります。

----

警告 **2001**

**Microsoft RMS コネクタへの承認されていないアクセス試行です。**

このイベントは、アカウントが RMS コネクタに接続しようとして失敗したときに記録されます。 この警告の最も一般的な理由は、RMS コネクタが Azure Rights Management サービスからダウンロードを行う、承認済みアカウントの一覧に、接続を行うアカウントが含まれていないことです。 たとえば、最新の一覧がまだダウンロードされていない (このイベントは 15 分ごとに発生します) か、アカウントが一覧に含まれていません。 

RMS コネクタを使用するように構成されているサーバーと同じサーバーにそのコネクタをインストールしたことが原因である場合もあります。 たとえば、Exchange Server を実行するサーバーに RMS コネクタをインストールして、Exchange アカウントにそのコネクタを使用することを承認したとします。 しかし、この構成はサポートされません。RMS コネクタが接続を試みてもアカウントを正しく識別できないためです。

イベント メッセージには、RMS コネクタに接続しようとしているアカウントとコンピューターに関する情報が含まれています。

- RMS コネクタに接続しようとしているアカウントが有効なアカウントである場合は、RMS コネクタ管理者ツールを使用して、承認されたアカウントの一覧にそのアカウントを追加します。 承認が必要なアカウントの詳細については、「[許可されたサーバーの一覧へのサーバーの追加](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers)」を参照してください。 

- RMS コネクタに接続しようとしているアカウントが RMS コネクタのサーバーと同じコンピューターのものである場合は、コネクタを別のサーバーにインストールします。 コネクタの前提条件の詳細については、「[RMS コネクタの前提条件]( deploy-rms-connector.md#prerequisites-for-the-rms-connector)」を参照してください。

----

警告 **2002**

**次の一覧に示すクライアントからの接続で、セキュリティで保護されていない (HTTP) 接続が使用されています。**

このイベントは、オンプレミスのサーバーが RMS コネクタに接続できるものの、その接続で HTTPS (安全性が高い) ではなく HTTP (安全性が低い) を使用しているときに記録されます。 接続ごとではなく、アカウントごとに 1 つのイベントが記録されます。 このイベントは、アカウントが HTTPS を使用するように切り替えられたものの、HTTP に戻った場合、再度トリガーされます。

イベント メッセージには、アカウントの SID、アカウント名、RMS コネクタへの接続を行うコンピューターの名前が含まれています。

HTTPS 接続用の RMS コネクタを構成する方法については、「[HTTPS を使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)」を参照してください。

----

警告 **2003**

**承認の一覧が空です。このサービスは、コネクタに対して承認されたユーザーとグループの一覧が作成されるまで使用できません。**

このイベントは、承認されたアカウントの一覧が RMS コネクタに含まれていないため、オンプレミスのサーバーが接続できないときに記録されます。 RMS コネクタは、Azure RMS から一覧を 15 分ごとにダウンロードします。 

アカウントを指定するには、RMS コネクタ管理者ツールを使用します。 詳細については、「[RMS コネクタを使用するサーバーの承認]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)」を参照してください。 

----

エラー **3000**

**Microsoft RMS コネクタで未処理の例外が発生しました。**

このイベントは、RMS コネクタで予期しないエラーが発生するたびに記録されます。エラーの詳細はイベント メッセージに含まれています。

イベント メッセージ内に **「空の応答によってリクエストが失敗しました」** というテキストがあるかどうかを確認することで、考えられる原因の 1 つを特定できます。 このテキストが見つかった場合、オン プレミス サーバーと RMS コネクタ サーバー間に、パケットの SSL 検査を実行しているネットワーク デバイスが存在する可能性あります。 Azure Rights Management サービスはこの構成をサポートしていないため、通信は失敗し、このイベント ログ メッセージが出力されます。

----

エラー **3001**

**認証情報のダウンロード中に例外が発生しました。**

このイベントは、RMS コネクタの使用が承認されているアカウントの最新の一覧を、RMS コネクタがダウンロードできない場合に記録されます。 エラーの詳細はイベント メッセージに含まれています。



----

## <a name="performance-counters"></a>パフォーマンス カウンター

RMS コネクタをインストールすると、**Microsoft Rights Management コネクタ** のパフォーマンス カウンターが自動的に作成されます。これによって、Azure Rights Management サービスの使用に関するパフォーマンスを監視や改善することができ、役に立ちます。 

たとえば、ドキュメントまたは電子メールが保護されている場合は、定期的に遅延が発生します。 あるいは、保護されているドキュメントまたは電子メールが開かれるとき、遅延が発生します。 このような場合は、パフォーマンス カウンターによって、遅延の原因がコネクタの処理時間や Azure Rights Management サービスの処理時間なのか、それともネットワークの遅延なのかを判断できます。 

遅延が発生している場所を特定するには、**コネクタの処理時間**、**サービス応答時間**、および **コネクタ応答時間** の平均カウントが含まれているカウンターを調べます。 例: **Licensing Successful Batched Request Average Connector Response Time**。

コネクタを使用する新しいサーバー アカウントを最近追加した場合、確認するとよいカウンターは、**Time since last authorization policy update** です。リストの更新後にコネクタがリストをダウンロードしたことや、もう少し待機する必要があるかどうか (最大 15 分) を確認できます。

## <a name="logging"></a>ログ記録

使用状況ログ記録を使用すると、電子メールやドキュメントが保護および使用された日時を特定できます。 RMS コネクタを使用してコンテンツを保護および使用する際、ログ内のユーザー ID フィールドには **Aadrm_S-1-7-0** のサービス プリンシパル名が含まれます。 この名前は、RMS コネクタ用に自動的に作成されます。

使用状況ログの詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](log-analyze-usage.md)」を参照してください。

診断のためにより詳細なログ記録が必要な場合は、Windows Sysinternals の [Debugview](/sysinternals/downloads/debugview) を使用して、ログをデバッグパイプに出力します。 

1. 管理者として debugview を起動し、 **[capture**  >  **capture Global Win32**] を選択します。

1. IIS で既定のサイトの **web.config** ファイルを変更して、RMS コネクタのトレースを有効にします。

    1. **%Programfiles%\Microsoft Rights Management Connector\Web Service** フォルダーで、 **web.config** ファイルを見つけます。

    1. 次の行を見つけます。

        ```sh
        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>
        ```

    1. その行を次のテキストに置き換えます。
        ```sh
        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>
        ```

1.  IIS を停止してから起動し、トレースをアクティブ化します。 

1.  DebugView で必要なトレースをキャプチャしたら、手順 3. の行を元に戻し、IIS を停止してから再度起動します。