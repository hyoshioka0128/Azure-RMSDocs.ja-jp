---
title: "ドキュメント追跡の有効化と取り消しを行う方法 | Azure RMS"
description: "ドキュメント追跡を実装するための基本的なガイダンス"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: aa4b1b0aee246b32d5214e2587ac5d291a682fe7
ms.openlocfilehash: 61f70a7b4a85c0ab6f0a2732fcf9d314a230e769


---
<<<<<<< 先頭

# コンテンツの追跡
=======
>>>>>>> 81ec5ddf5acf3de78d77c01ed95631e44d37fe6e

# 方法: ドキュメント追跡の有効化と取り消し

このトピックでは、コンテンツのドキュメント追跡機能を導入する方法について、その基礎を説明し、また、メタデータ更新のサンプル コードとアプリの **[使用の追跡]** ボタンを作成するためのサンプルコードを紹介します。

## ドキュメント追跡を実装する手順

手順 1 と 2 では、追跡するドキュメントを有効にします。 手順 3 では、保護ドキュメントを追跡するか、取り消す目的で、アプリ ユーザーがドキュメント追跡サイトにアクセスできるようにします。

1. ドキュメント追跡メタデータを追加する
2. RMS サービスでドキュメントを登録する
3. [使用の追跡] ボタンをアプリに追加する

導入の詳しい手順は以下のようになります。

## 1.ドキュメント追跡メタデータを追加する

ドキュメント追跡は、Rights Management システムの機能です。 ドキュメントの保護プロセス中に特定のメタデータを追加することにより、追跡用のいくつかのオプションを提供する追跡サービス ポータルにドキュメントを登録できます。

これらの API を使用して、ドキュメント追跡メタデータと共にコンテンツのライセンスを追加または更新します。


運用上、ドキュメント追跡に必要なプロパティは、**コンテンツ名**と**通知の種類**のみです。


- [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
- [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

  すべてのメタデータ プロパティを設定することをお勧めします。 種類ごとの一覧を以下に示します。

  詳細については、「[License metadata property types (ライセンス メタデータ プロパティの種類)](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)」を参照してください。

  - **IPC_MD_CONTENT_PATH**

    追跡対象のドキュメントの識別に使用します。 完全パスが使用できない場合は、ファイル名のみを指定します。

  - **IPC_MD_CONTENT_NAME**

    追跡対象のドキュメントの名前の識別に使用します。

  - **IPC_MD_NOTIFICATION_TYPE**

    通知を送信するタイミングの指定に使用します。 詳細については、「Notification type (通知の種類)」を参照してください。

  - **IPC_MD_NOTIFICATION_PREFERENCE**

    通知の種類の指定に使用します。 詳細については、「Notification preference (通知の基本設定)」を参照してください。

  - **IPC_MD_DATE_MODIFIED**

    ユーザーが [保存] をクリックするたびに、この日付を設定することをお勧めします。

  - **IPC_MD_DATE_CREATED**

    ファイルの作成日の設定に使用します。

- [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

これらの API から適切なものを使用して、ファイルまたはストリームにメタデータを追加します。

- [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
- [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

最後に、この API を使用して、追跡対象のドキュメントを追跡システムに登録します。

- [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)


## 2.RMS サービスでドキュメントを登録する

ドキュメント追跡メタデータの設定と追跡システムに登録するための呼び出しの例を表すコード スニペットを次に示します。

      C++
      HRESULT hr = S_OK;
      LPCWSTR wszOutputFile = NULL;
      wstring wszWorkingFile;
      IPC_LICENSE_METADATA md = {0};

      md.cbSize = sizeof(IPC_LICENSE_METADATA);
      md.dwNotificationType = IPCD_CT_NOTIFICATION_TYPE_ENABLED;
      md.dwNotificationPreference = IPCD_CT_NOTIFICATION_PREF_DIGEST;
      //file origination date, current time for this example
      md.ftDateCreated = GetCurrentTime();
      md.ftDateModified = GetCurrentTime();

      LOGSTATUS_EX(L"Encrypt file with official template...");

      hr =IpcfEncryptFileWithMetadata( wszWorkingFile.c_str(),
                               m_wszTestTemplateID.c_str(),
                               IPCF_EF_TEMPLATE_ID,
                               0,
                               NULL,
                               NULL,
                               &md,
                               &wszOutputFile);

     /* This will contain the serialized license */
     PIPC_BUFFER pSerializedLicense;

     /* the context to use for the call */
     PCIPC_PROMPT_CTX pContext;

     wstring wstrContentName(“MyDocument.txt”);
     bool sendLicenseRegistrationNotificationEmail = FALSE;

     hr = IpcRegisterLicense( pSerializedLicense,
                        0,
                        pContext,
                        wstrContentName.c_str(),
                        sendLicenseRegistrationNotificationEmail);

## **[使用の追跡]** ボタンをアプリに追加する

**[使用の追跡]** UI アイテムをアプリに追加する作業は、次のいずれかの URL 形式の使用と同じように簡単です。

- コンテンツ ID の使用
  - ライセンスがシリアル番号になっており、ライセンス プロパティの **IPC_LI_CONTENT_ID** が使用される場合、[IpcGetLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetlicenseproperty) または [IpcGetSerializedLicenseProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgetserializedlicenseproperty) を使用してコンテンツ ID を入手します。 詳細については、「[License property types](/rights-management/sdk/2.1/api/win/constants#msipc_license_property_types)」 (ライセンスのプロパティの種類) を参照してください。
  - メタデータの **ContentId** と **Issuer** については、次の形式を使用します。 `https://track.azurerms.com/#/{ContentId}/{Issuer}`

    例 - `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- そのメタデータにアクセスできない場合 (すなわち、保護されていないバージョンのドキュメントを調べている)、次の形式で **Content_Name** を使用できます。 `https://track.azurerms.com/#/?q={ContentName}`

  例 - https://track.azurerms.com/#/?q=Secret!.txt

このクライアントでは、適切な URL でブラウザーを開く必要があります。 RMS ドキュメント追跡ポータルが認証と必要なリダイレクトを処理します。

## 関連項目

* [ライセンス メタデータ プロパティの種類](/rights-management/sdk/2.1/api/win/constants#msipc_license_metadata_property_types)
* [通知の基本設定](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [通知の種類](/rights-management/sdk/2.1/api/win/constants#msipc_notification_type)
* [IpcCreateLicenseMetadataHandle](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [IpcSetLicenseMetadataProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [IpcSerializeLicenseWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [IpcfEncryptFileWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [IpcfEncryptFileStreamWithMetadata](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [IpcRegisterLicense](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

 



<!--HONumber=Jul16_HO3-->


