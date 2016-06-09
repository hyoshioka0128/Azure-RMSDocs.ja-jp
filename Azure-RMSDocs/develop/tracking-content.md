---
# required metadata

title: コンテンツの追跡 | Azure RMS
description: ドキュメント追跡を実装するための基本的なガイダンス
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5089765-9D94-452B-85E0-00D22675D847
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** この SDK コンテンツは最新のものではありません。 しばらくの間、[最新版](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)の文書は MSDN でご覧ください。 **
# コンテンツの追跡

このトピックでは、Rights Management サービス SDK 2.1 で保護されたコンテンツのドキュメント追跡を実装するための基本的なガイダンスを提供します。

ドキュメント追跡は、Rights Management システムの機能です。 ドキュメントの保護プロセス中に特定のメタデータを追加することにより、追跡用のいくつかのオプションを提供する追跡サービス ポータルにドキュメントを登録できます。

これらの API を使用して、ドキュメント追跡メタデータと共にコンテンツのライセンスを追加または更新します。

-   [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
-   [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)

    すべてのメタデータ プロパティを設定することをお勧めします。 種類ごとの一覧を以下に示します。

    詳細については、「[**License metadata property types (ライセンス メタデータ プロパティの種類)**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)」を参照してください。

    -   **IPC\_MD\_CONTENT\_PATH**

        追跡対象のドキュメントの識別に使用します。 完全パスが使用できない場合は、ファイル名のみを指定します。

    -   **IPC\_MD\_CONTENT\_NAME**

        追跡対象のドキュメント名の識別に使用します。

    -   **IPC\_MD\_NOTIFICATION\_TYPE**

        通知を送信するタイミングの指定に使用します。 詳細については、「[**Notification type (通知の種類)**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)」を参照してください。

    -   **IPC\_MD\_NOTIFICATION\_PREFERENCE**

        通知の種類の指定に使用します。 詳細については、「[**Notification preference (通知の基本設定)**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)」を参照してください。

    -   **IPC\_MD\_DATE\_MODIFIED**

        ユーザーが **[保存]** をクリックするたびに、この日付を設定することをお勧めします。

    -   **IPC\_MD\_DATE\_CREATED**

        ファイルの作成日です。

-   [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)

これらの API から適切なものを使用して、ファイルまたはストリームにメタデータを追加します。

-   [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
-   [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)

最後に、この API を使用して、追跡対象のドキュメントを追跡システムに登録します。

-   [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)

ドキュメント追跡メタデータの設定と追跡システムに登録するための呼び出しの例を表すコード スニペットを次に示します。



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

    LOGSTATUS_EX(L&quot;Encrypt file with official template...&quot;);

    hr =IpcfEncryptFileWithMetadata(  wszWorkingFile.c_str(),
                                       m_wszTestTemplateID.c_str(),
                                       IPCF_EF_TEMPLATE_ID,
                                       0,
                                       NULL,
                                       NULL,
                                       &amp;md,
                                       &amp;wszOutputFile);

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


## 関連項目


* [**ライセンス メタデータ プロパティの種類**](/rights-management/sdk/2.1/api/win/license%20metadata%20property%20types#msipc_license_metadata_property_types)
* [**通知の基本設定**](/rights-management/sdk/2.1/api/win/constants#msipc_notification_preference)
* [**通知の種類**](/rights-management/sdk/2.1/api/win/notification%20type#msipc_notification_type)
* [**IpcCreateLicenseMetadataHandle**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensemetadatahandle)
* [**IpcSetLicenseMetadataProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicensemetadataproperty)
* [**IpcSerializeLicenseWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcserializelicensemetadata)
* [**IpcfEncryptFileWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilewithmetadata)
* [**IpcfEncryptFileStreamWithMetadata**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfilestreamwithmetadata)
* [**IpcRegisterLicense**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcregisterlicense)
 

 


<!--HONumber=Jun16_HO1-->


