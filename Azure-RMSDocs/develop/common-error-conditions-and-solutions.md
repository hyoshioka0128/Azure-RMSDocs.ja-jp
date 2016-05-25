---
# required metadata

title: 一般的なエラー状況とソリューション |Azure RMS
description: このトピックでは、RMS SDK 2.1 開発者ツールを使用する場合に発生する可能性のある最も一般的なエラー メッセージについて説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: A5B95EB8-3528-4CFF-86FC-166613A5F4A3
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 一般的なエラー状況とソリューション
このトピックでは、Rights Management サービス SDK 2.1 開発者ツールを使用する場合に発生する可能性のある最も一般的なエラー メッセージについて説明します。 また、該当するエラーの修正に推奨される操作も提供します。

**重要**: エラー条件を処理する場合、SDK の API 呼び出しが失敗した直後に常に [IpcGetErrorMessageText](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) を呼び出すと、エラーの性質に関する完全な情報を取得することができます。

 

## エラーとアクション ##
次の一覧には、エラーの定数の一覧、エラーの定数に関連付けられた説明、およびエラー状態への対処に推奨されるアクションが含まれています。

**エラー** - *IPCERROR_DEBUGGER_DETECTED* -RMS SDK 2.1 でデバッガーが検出されました

**アクション** - RMS SDK 2.1 の開発者バージョンは、デバッガーが存在するかどうかはチェックしません。 可能であれば、このバージョンの RMS SDK 2.1 を使用して、アプリケーションをデバッグしてください。
RMS SDK 2.1 の製品版をデバッグする必要がある場合は、次のガイダンスを使用してください。

一部の RMS SDK 2.1 関数は、デバッガーで失敗するように設計されています。
- [IpcGetKey</strong>](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
- [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
- [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)

これらの関数呼び出しの後のコードをデバッグするには、プロセスを中断して、関数の呼び出しが完了した後にデバッガーを添付する必要があります。 これを行う方法の 1 つとして、assert ステートメントを使用したデバッガーの中断があります。 ASSERTE マクロは *Crtdbg.h* ヘッダーに含まれています。
\_ASSERTE の詳細については、「[\_ASSERT、\_ASSERTE マクロ](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)」を参照してください。

**エラー** - *IPCERROR_BROKEN_CERT_CHAIN* - 証明書チェーンが一致しません。

**アクション** - 階層キーに、AD RMS アプリケーション マニフェストへの署名に使用するキーに基づいた適切な値が含まれているかどうかを確認します。
これらは、署名キーおよび関連付けられている値 (階層 **DWORD**) です。
- ISV-1
- 実稼働 - 0 または存在しない

**エラー** - *IPCERROR_MACHINE_CERT_NOT_TRUSTED* - ISV署名キーで署名されたアプリケーションを使用していますが、アプリケーションが本稼働 AD RMS サーバーと通信しようとしているか、またはその逆です。

- AD RMS サーバーの開発者バージョンを使用している場合は、アプリケーションへの署名に ISV の署名キーを使用していることを確認します。
- AD RMS サーバーの運用バージョンを使用している場合は、アプリケーションへの署名に運用署名キーを使用していることを確認します。

**エラー** - *IPCERROR_APPLICATION_AUTH_ERROR_MANIFEST* -アプリケーション マニフェストが無効です。 これは、バイナリ (アプリケーション) が再構築され、マニフェストが再生成されなかったことが原因である可能性があります。

**アクション** - アプリケーションを再構築するたびに、アプリケーション マニフェストを再生成するようにします。

## 関連項目 ##
* [Developer notes (開発者向け注意事項)](developer-notes.md)
* [IpcGetKey](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [IpcGetTemplateList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [IpcGetTemplateIssuerList](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [\_ASSERT、\_ASSERTE マクロ](https://msdn.microsoft.com/en-us/library/ezb1wyez.aspx)
 

 


<!--HONumber=Apr16_HO4-->


