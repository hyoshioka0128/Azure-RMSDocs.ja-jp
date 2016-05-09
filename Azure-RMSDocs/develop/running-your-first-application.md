---
# required metadata

title: 権限保護対応アプリケーションのテスト | Azure RMS
description: RMS SDK 2.1 の権限保護対応アプリケーションのテストを実行するために必要な手順について説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 43b611a8-2cc0-49a8-9db9-e81321c38f7a

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 権限保護対応アプリケーションのテスト

このトピックでは、Rights Management サービス SDK 2.1 の権限保護対応アプリケーションのテストを実行するために必要な手順について説明します。

Rights Management Services (RMS) アプリケーションは、保護されたコンテンツを発行および消費するために、最終的に Microsoft の証明機関に到達する証明書チェーンを構成するさまざまな種類の証明書やライセンスを使用します。 マイクロソフトでは、次の階層構造を提供します。

-   アプリケーションの開発およびテストに使用できる運用前階層。
-   リリースされたアプリケーションで使用する必要がある運用階層。

アプリケーションの開発段階では、運用前階層を使用することをお勧めします。 これにより、マイクロソフトと Production License Agreement を契約しなくても作業できます。

> [!IMPORTANT]
> ベスト プラクティスとして、はじめに RMS サーバーに対して RMS 運用前環境で RMS SDK 2.1 アプリケーションをテストすることをお勧めします。 その後で、顧客に Azure RMS サービスでのアプリケーションの使用を勧める場合は、その環境でのテストに移行します。 詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

 

### 必要条件

-   RMS SDK 2.1 開発環境のセットアップ。 詳細については、「[Setting up the pre-production development environment](how-to-set-up-the-pre-production-development-environment.md)」 (運用前開発環境をセットアップする) を参照してください。
-   サンプル アプリケーションについては、「[IPCHelloWorld - an example application](how-to-build-your-first-application.md)」 (IPCHelloWorld - サンプル アプリケーション) を参照してください。

手順

### 手順 1.

権限保護対応アプリケーションを作成してビルドします。 オプションについては、前述の「必要条件」を参照してください。

### 手順 2. 運用前証明書チェーンを使用してアプリケーション マニフェストを生成します。

アプリケーションを実行する前に、マニフェストを生成する必要があります。

**注**  アプリケーションをサーバー API モード (**IPC\_API\_MODE\_SERVER**) で実行する場合、アプリケーション マニフェストを使用する必要はありません。 運用 AD RMS サーバーに対してアプリケーションをテストすることができ、運用環境に切り替えるときに運用のライセンスを取得する必要はありません。 サーバー モード アプリケーションの詳細については、「[アプリケーションの種類](application-types.md)」を参照してください。

 

このプロセスは、アプリケーションへの署名とも呼ばれます。 運用証明書チェーンまたは SDK と共にインストールされている運用前証明書チェーンのいずれかを使用してマニフェストを生成することができます。 開発中は、運用前証明書チェーンを使用することをお勧めします。

キーおよび証明書チェーンの詳細については、「[Understanding certificate chains](understanding-certificate-chains.md)」 (証明書チェーンについて) を参照してください。

運用証明書チェーンでアプリケーションに署名する方法については、「[Switching to the production environment](switching-to-the-production-environment.md)」 (運用環境への切り替え) を参照してください。

運用前証明書チェーンを使用してアプリケーション マニフェストを生成するには、開発用コンピューターで次の手順を実行します。

1.  インストール ディレクトリから、アプリケーションと同じフォルダーに次のファイルをコピーします。

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\YourAppName.isv.mcf

2.  アプリケーション フォルダーで、マニフェスト構成ファイル YourAppName.isv.mcf の名前を、使用するアプリケーションの名前に変更し、.mcf ファイル名拡張子を追加 します。 たとえば、アプリケーション名が MyApp.exe である場合、YourAppName.isv.mcf の名前を MyApp.exe.mcf に変更します。

3.  テキスト エディターを使用して、アプリケーションをマニフェスト構成ファイルに追加します。 これを行うには、.mcf ファイル内のモジュール一覧で &lt;YourAppName&gt;.exe のプレース ホルダー テキストをアプリケーション名、たとえば MyApp.exe に置き換えます。

    .mcf ファイルを変更せずに使用すると、署名プロセスでエラーが発生します。

4.  アプリケーション マニフェストを生成する Genmanifest.exe を実行します。 この操作は、アプリケーションへの署名とも呼ばれます。 この操作を実行すると、.man ファイルが出力されます。 たとえば、アプリケーション名が MyApp.exe で、マニフェスト構成ファイル名が MyApp.exe.mcf の場合は、次のコマンドを実行します。

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MyApp.exe.mcf MyApp.exe.man**

### 手順 3. アプリケーションを実行します。

任意のディレクトリからアプリケーションを実行することができますが、アプリケーション マニフェスト (MyApp.exe.man) は、実行可能ファイル (MyApp.exe) と同じディレクトリにある必要があります。

-   **RMS 1 ボックス環境を使用する場合**

    RMS 1 ボックス環境を使用してアプリケーションをテストする場合、アプリケーションの実行可能ファイルとアプリケーション マニフェストを 1 ボックス環境の任意のディレクトリにコピーし、アプリケーションを実行します。

    RMS 1 ボックス環境については、「[テスト環境のセットアップ](how-to-set-up-your-test-environment.md)」を参照してください。

-   **運用前サーバー構成を使用する場合**

    運用前の構成になっている RMS サーバーに対してアプリケーションをテストする場合、アプリケーションを実行するコンピューター、たとえば、開発用コンピューターに Active Directory Rights Management Services Client 2.1 が構成されていること確認します。 アプリケーションの実行可能ファイルとアプリケーション マニフェストの両方がそのコンピューター上の同じディレクトリにあることを確認し、アプリケーションを実行します。

    コンピューターにクライアントを構成する方法については、「[Configure the client](how-to-configure-the-ad-rms-client-2-0.md)」 (クライアントの構成) を参照してください。 RMS サーバーのインストールについては、「[サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md)」を参照してください。

### 関連項目

* [How-to use (使用方法)](how-to-use-msipc.md)
* [クライアントの構成](how-to-configure-the-ad-rms-client-2-0.md)
* [サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - サンプル アプリケーション](how-to-build-your-first-application.md)
* [Setting up the pre-production development environment (運用前開発環境のセットアップ)](how-to-set-up-the-pre-production-development-environment.md)
* [Switching to the production environment (運用環境への切り替え)](switching-to-the-production-environment.md)
* [テスト環境のセットアップ](how-to-set-up-your-test-environment.md)
* [Understanding certificate chains (証明書チェーンについて)](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO3-->


