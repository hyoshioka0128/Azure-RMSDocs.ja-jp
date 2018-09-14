---
title: ドキュメント追跡の有効化と取り消しを行う方法 | Azure RMS
description: コンテンツのドキュメント追跡機能を導入する方法の基本的な説明、ならびにメタデータ更新のサンプル コードとアプリの [使用の追跡] ボタンのサンプルコードを紹介します。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 68c7f3c0ca050a13e0e943dc2372267c00f20c48
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44149091"
---
# <a name="how-to-enable-document-tracking-and-revocation"></a>方法: ドキュメント追跡の有効化と取り消し

このトピックでは、コンテンツのドキュメント追跡機能を導入する方法について、その基礎を説明し、また、メタデータ更新のサンプル コードとアプリの **[使用の追跡]** ボタンを作成するためのサンプルコードを紹介します。

## <a name="steps-to-implement-document-tracking"></a>ドキュメント追跡を実装する手順

手順 1 と 2 では、追跡するドキュメントを有効にします。 手順 3 では、保護ドキュメントを追跡するか、取り消す目的で、アプリ ユーザーがドキュメント追跡サイトにアクセスできるようにします。

1. ドキュメント追跡メタデータを追加する
2. RMS サービスでドキュメントを登録する
3. [使用の追跡] ボタンをアプリに追加する

導入の詳しい手順は以下のようになります。

## <a name="1-add-document-tracking-metadata"></a>1.ドキュメント追跡メタデータを追加する

ドキュメント追跡は、Rights Management システムの機能です。 ドキュメントの保護プロセス中に特定のメタデータを追加することにより、追跡用のいくつかのオプションを提供する追跡サービス ポータルにドキュメントを登録できます。

これらの API を使用して、ドキュメント追跡メタデータと共にコンテンツのライセンスを追加または更新します。


運用上、ドキュメント追跡に必要なプロパティは、**コンテンツ名**と**通知の種類**のみです。


- [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
- [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)

  すべてのメタデータ プロパティを設定することをお勧めします。 種類ごとの一覧を以下に示します。

  詳細については、「[License metadata property types (ライセンス メタデータ プロパティの種類)](https://msdn.microsoft.com/library/dn974062.aspx)」を参照してください。

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

- [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)

これらの API から適切なものを使用して、ファイルまたはストリームにメタデータを追加します。

- [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
- [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)

最後に、この API を使用して、追跡対象のドキュメントを追跡システムに登録します。

- [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)


## <a name="2-register-the-document-with-the-rms-service"></a>2.RMS サービスでドキュメントを登録する

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

## <a name="add-a-track-usage-button-to-your-app"></a>**[使用の追跡]** ボタンをアプリに追加する

**[使用の追跡]** UI アイテムをアプリに追加する作業は、次のいずれかの URL 形式の使用と同じように簡単です。

- コンテンツ ID の使用
  - ライセンスがシリアル番号になっており、ライセンス プロパティの **IPC_LI_CONTENT_ID** が使用される場合、[IpcGetLicenseProperty](https://msdn.microsoft.com/library/hh535265.aspx) または [IpcGetSerializedLicenseProperty](https://msdn.microsoft.com/library/hh995038.aspx) を使用してコンテンツ ID を入手します。 詳細については、「[License property types](https://msdn.microsoft.com/library/hh535287.aspx)」 (ライセンスのプロパティの種類) を参照してください。
  - メタデータの **ContentId** と **Issuer** については、次の形式を使用します。`https://track.azurerms.com/#/{ContentId}/{Issuer}`

    例 - `https://track.azurerms.com/#/summary/05405df5-8ad6-4905-9f15-fc2ecbd8d0f7/janedoe@microsoft.com`

- そのメタデータにアクセスできない場合 (すなわち、保護されていないバージョンのドキュメントを調べている)、次の形式で **Content_Name** を使用できます。`https://track.azurerms.com/#/?q={ContentName}`

  例: https://track.azurerms.com/#/?q=Secret!.txt

このクライアントでは、適切な URL でブラウザーを開く必要があります。 RMS ドキュメント追跡ポータルが認証と必要なリダイレクトを処理します。

## <a name="related-topics"></a>関連トピック

* [ライセンス メタデータ プロパティの種類](https://msdn.microsoft.com/library/dn974062.aspx)
* [通知の基本設定](https://msdn.microsoft.com/library/dn974063.aspx)
* [通知の種類](https://msdn.microsoft.com/library/dn974064.aspx)
* [IpcCreateLicenseMetadataHandle](https://msdn.microsoft.com/library/dn974050.aspx)
* [IpcSetLicenseMetadataProperty](https://msdn.microsoft.com/library/dn974059.aspx)
* [IpcSerializeLicenseWithMetadata](https://msdn.microsoft.com/library/dn974058.aspx)
* [IpcfEncryptFileWithMetadata](https://msdn.microsoft.com/library/dn974052.aspx)
* [IpcfEncryptFileStreamWithMetadata](https://msdn.microsoft.com/library/dn974051.aspx)
* [IpcRegisterLicense](https://msdn.microsoft.com/library/dn974057.aspx)

