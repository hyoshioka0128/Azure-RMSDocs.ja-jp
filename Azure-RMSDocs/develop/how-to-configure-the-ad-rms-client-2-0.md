---
# required metadata

title: クライアントの構成 | Azure RMS
description: Active Directory Rights Management サービス クライアント 2.1 を構成する手順を説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 58051d42-5a0a-4b65-9e02-bcdbf17d3262

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
# クライアントの構成

このトピックでは、Active Directory Rights Management サービス クライアント 2.1 を構成する方法を説明します。

**重要**  アプリケーションを 1-box RMS ISV 環境で実行してテストする場合は、AD RMS クライアント 2.1 を構成する必要はありません。 詳細については、「[権限保護対応アプリケーションのテスト](running-your-first-application.md)」を参照してください。

 

### 必要条件

-   AD RMS クライアント 2.1 がアプリケーションのテストを実行するコンピューターにインストールされている必要があります。

    -   開発コンピューターでアプリケーションをテストする場合は、Rights Management サービス SDK 2.1 を既にインストールしています。 この時点で、AD RMS クライアント 2.1 がサイレント インストールされています。

        RMS SDK 2.1 のインストール方法については、「[SDK のインストール](create-your-first-rights-aware-application.md)」を参照してください。

    -   開発コンピューター以外のコンピューターでアプリケーションをテストする場合は、[AD RMS クライアント 2.1 ダウンロード ページ](http://www.microsoft.com/en-us/download/details.aspx?id=38396)からそのコンピューターに AD RMS クライアント 2.1 をインストールできます。
        **注**  アプリケーションをサーバー API モード (**IPC\_API\_MODE\_SERVER**) で実行する場合、アプリケーション マニフェストを使用する必要はありません。 運用 RMS サーバーに対してアプリケーションをテストすることができ、運用環境に切り替えるときに運用のライセンスを取得する必要はありません。 サーバー モード アプリケーションの詳細については、「[アプリケーションの種類](application-types.md)」を参照してください。

         

-   運用前環境での操作用に RMS サーバーがインストールされ、構成されている必要があります。 詳細については、「[サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md)」を参照してください。

手順

### 手順 1: 運用前証明書の階層用に RMS クライアント 2.1 をセットアップする方法

次の手順では、開発者向けランタイムをインストールし、クライアントを ISV 証明書 (運用前) 階層を使用するように構成し、クライアントにサービス検出をセットアップする方法を説明します。

1.  開発者向けランタイム、Ipcsecproc\_isv.dll を %MSIPCSDKDIR%\\bin\\x86 (32 ビット バージョンの Windows 向け) または %MSIPCSDKDIR\\bin\\x64 (64 ビット バージョンの Windows 向け) から C:\\Program Files\\Active Directory Rights Management Services Client 2.1 にコピーします。

    **重要**  64 ビット バージョンの Windows で 32 ビット アプリケーションを実行する場合は、Ipcsecproc\_isv.dll を %MSIPCSDKDIR%\\bin\\x86 から C:\\Program Files(x86)\\Active Directory Rights Management Services Client 2.1 にコピーする必要があります。

     

2.  AD RMS クライアント 2.1 を ISV 証明書 (運用前) 階層を使用するように構成します。このためには、**階層**レジストリ キーの値を 1 に設定します。

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    **注**  **階層**値がレジストリにないということは、機能的にその値が0 (ゼロ) に設定されていることと同じであり、RMS SDK 2.1 は運用モードで動作します。 キーおよび証明書チェーンの詳細については、「[Understanding certificate chains](understanding-certificate-chains.md)」 (証明書チェーンについて) を参照してください。

    **重要**  
    64 ビット バージョンの Windows で 32 ビット アプリケーションを実行する場合は、**階層**値を次のキーの場所に設定する必要があります。

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  サーバー側の検出またはクライアント側の検出を、AD RMS クライアント 2.1 で運用前 RMS サーバーとの通信を検出し、確立できるように構成します。

    -   サーバー側の検出では、管理者が Active Directory により運用前 RMS ルート クラスターに対してサービス接続ポイント (SCP) を登録すると、クライアントは Active Directory にクエリを実行して SCP を検出し、サーバーとの接続を確立します。
    -   クライアント側の検出では、AD RMS クライアント 2.1 が実行されるコンピューター上のレジストリに RMS サービス検出の設定を構成します。 これにより、AD RMS クライアント 2.1 が RMS サーバーを使用するように設定されます。 これらの設定がある場合、サーバー側の検出は実行されません。

    クライアント側の検出を構成する場合、次のレジストリ キーを運用前 RMS サーバーをポイントするように設定できます。 サービス側の検出を構成する方法については、「[RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)」 (RMS クライアント 2.0 のデプロイに関する注意事項) を参照してください。

|キー|値|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|(既定):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Certification**|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|(既定):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Licensing**|


**注**  既定では、これらのキーはレジストリに存在しないため、作成する必要があります。
     
**重要**  
    64 ビット バージョンの Windows で 32 ビット アプリケーションを実行する場合は、これらのキーを次のキーの場所に設定する必要があります。


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### 解説

このトピックのガイダンスは包括的なものではありません。 AD RMS クライアント 2.1 の構成方法について詳しくは、「[RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)」 (RMS クライアント 2.0 のデプロイに関する注意事項) をご覧ください。

### 関連項目


* [How-to use (使用方法)](how-to-use-msipc.md)
* [RMS Client 2.0 Deployment Notes (RMS クライアント 2.0 のデプロイに関する注意事項)](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [SDK のインストール](create-your-first-rights-aware-application.md)
* [サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md)
* [権限保護対応アプリケーションのテスト](running-your-first-application.md)
* [Understanding certificate chains (証明書チェーンについて)](understanding-certificate-chains.md)
 

 


<!--HONumber=Apr16_HO3-->


