---
title: "IPCHelloWorld - サンプル アプリケーション | Azure RMS"
description: "このトピックには、権限保護に対応するサンプル アプリケーションを作成する手順が含まれています。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 581451A2-9558-4D0D-9D01-BEAB282C5A83
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ac6afddc2b39d6209ef1b89d8d84011942cdba5a
ms.openlocfilehash: e75ec6c04afd171552697f79deb33ad2cfe2c4e1


---
** この SDK コンテンツは最新のものではありません。 しばらくの間、[最新版](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)の文書は MSDN でご覧ください。 **
# IPCHelloWorld - サンプル アプリケーション

このトピックには、権限保護に対応するサンプル アプリケーションを作成する手順が含まれています。

この IPCHelloWorld というシンプルなアプリケーションは、権限保護対応アプリケーションの基本的な概念とコードの理解に役立ちます。

Microsoft Connect からサンプル アプリケーション [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440) をダウンロードしてください。 このサイトでダウンロードできるその他の項目は、使いやすいようにここでまとめられています。

**注**  Rights Management サービス SDK 2.1 では IPCHelloWorld プロジェクトは既に構成されています。 RMS SDK 2.1 を使用する新しいプロジェクトを構成する方法については、「[Configure Visual Studio (Visual Studio の構成)](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)」を参照してください。

 
以降のセクションでは、アプリケーションの主要な手順と必要な知識について説明します。

## MSIPC.dll の読み込み

RMS SDK 2.1 の関数を呼び出すには、最初に [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) 関数を呼び出して MSIPC.dll を読み込む必要があります。



    hr = IpcInitialize();

    if (FAILED(hr))
    {
      wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
      goto exit;
    }



## テンプレートの列挙

RMS テンプレートでは、データを保護するために使用するポリシー、つまり、データやその権限へのアクセスを許可するユーザーを定義します。 RMS テンプレートは、RMS サーバーにインストールされます。

次のコードでは、既定の RMS サーバーから使用できる RMS テンプレートを列挙します。



    hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

    if (FAILED(hr))
    {
      DisplayError(L"IpcGetTemplateList failed", hr);
      goto exit;
    }



この呼び出しでは、既定のサーバーにインストールされている RMS テンプレートを取得し、結果を *pcTil* 変数によって示される [**IPC\_TIL**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) 構造体に読み込み、読み込んだテンプレートを表示します。



    if (0 == pcTil->cTi)
    {
      wprintf(L"* No templates configured for your RMS server * \n\n");
      wprintf(L"\\------------------------------------------------------\n\n");
      goto exit;
    }

    for (DWORD dw = 0; dw < pcTil->cTi; dw++)
    {
      wprintf(L"Template #%d:\n", dw);
      wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
      wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
      wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
      wprintf(L"\n");
    }



## ライセンスのシリアル化

任意のデータを保護するには、ライセンスをシリアル化し、コンテンツ キーを取得する必要があります。 コンテンツ キーは、機密データの暗号化に使用されます。 通常、シリアル化されたライセンスは、暗号化されたデータにアタッチされ、保護されたデータのコンシューマーに使用されます。 コンシューマーは、コンテンツを解読して、コンテンツに関連付けられたポリシーを取得するためのコンテンツ キーを取得するには、シリアル化されたライセンスを使用して [**IpcGetKey**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey) 関数を呼び出す必要があります。

わかりやすくするために、[**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) によって返される最初の RMS テンプレートを使用してライセンスをシリアル化します。

通常は、ユーザーが目的のテンプレートを選択できるように、ユーザー インターフェイス ダイアログを使用します。



    hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
    0, NULL, &hContentKey, &pSerializedLicense);

    if (FAILED(hr))
    {
      DisplayError(L"IpcSerializeLicense failed", hr);
      goto exit;
    }



これにより、コンテンツ キー *hContentKey* とシリアル化されたライセンス *pSerializedLicense* を取得しました。これらは、保護されたデータにアタッチする必要があります。

## データの保護

[**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) 関数を使用して機密データを暗号化する準備ができました。 最初に、暗号化されたデータがどれぐらいのサイズになるかを **IpcEncrypt** 関数で確認する必要があります。



    cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
    hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
    NULL, 0, &cbEncrypted);

    if (FAILED(hr)) {
      DisplayError(L"IpcEncrypt failed", hr);
      goto exit;
    }



ここでは、保護しようとしているプレーン テキストが *wszText* に含まれています。 [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt) 関数が、暗号化されたデータのサイズを *cbEncrypted* パラメーターに返します。

ここで、暗号化されたデータ用のメモリを割り当てます。



    pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

    if (NULL == pbEncrypted) {
      wprintf(L"Out of memory\n");
      goto exit;
    }


これで、実際の暗号化を行うことができます。



    hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
    pbEncrypted, cbEncrypted, &cbEncrypted);

    if (FAILED(hr)) {
      DisplayError(L"IpcEncrypt failed", hr);
      goto exit;
    }


この手順により、暗号化されたデータ *pbEncrypted* とシリアル化されたライセンス *pSerializedLicense* を取得しました。これらは、データを解読するコンシューマーが使用します。

## エラー処理

このサンプル アプリケーションの全体で、**DisplayError** 関数を使用してエラーを処理しています。



    void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
    {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
    }   


**DisplayError** 関数は、[**IpcGetErrorMessageText**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext) 関数を使用して、対応するエラー コードからエラー メッセージを取得し、標準出力に出力します。

## クリーンアップ

終了する前に、割り当てられているすべてのリソースを解放する必要があります。



    if (NULL != pbEncrypted) {
      LocalFree((HLOCAL)pbEncrypted);
    }

    if (NULL != pSerializedLicense) {
      IpcFreeMemory((LPVOID)pSerializedLicense);
    }

    if (NULL != hContentKey) {
      IpcCloseHandle((IPC_HANDLE)hContentKey);
    }

    if (NULL != pcTil) {
      IpcFreeMemory((LPVOID)pcTil);
    }


## 関連項目

* [Developer notes (開発者向け注意事項)](developer-notes.md)
* [Configure Visual Studio (Visual Studio の構成)](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md)
* [**IpcEncrypt**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcencrypt)
* [**IpcGetErrorMessageText**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgeterrormessagetext)
* [**IpcGetKey**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetkey)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_TIL**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [Webinar\_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
 

 



<!--HONumber=Jun16_HO4-->


