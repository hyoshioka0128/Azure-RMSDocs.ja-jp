---
title: 明示的な所有者権限の追加方法 | Azure RMS
description: アプリケーションでは、最初からライセンスを作成するときに、"所有者" 権限を明示的に追加する必要があります。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: EF43FAC4-ABB4-459D-B173-972B5716F816
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 925d1fa7e55e8d58da904e8811f530f2524a1658
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178974"
---
# <a name="how-to-add-explicit-owner-rights"></a>方法: 明示的な所有者権限の追加

アプリケーションでは、[IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) を使って最初からライセンスを作成するときに、"所有者" 権限を明示的に追加する必要があります。

## <a name="prerequisites"></a>前提条件

アプリケーションで [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) を使ってライセンス ハンドルを作成するときは、所有者に完全な権限 (アクセス許可) も明示的に付与する必要があります。

> [!NOTE]
> [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) と **IPC\_LI\_OWNER** プロパティを使ってユーザーを "所有者" として設定しても、所有者に完全なアクセス許可は付与されません。

次のコード例には、特定の権限を作成して特定のライセンスに割り当てるための手順のみが示されています。

## <a name="instructions"></a>手順
 
## <a name="step-1-example-scenario"></a>手順 1:シナリオ例

この例では、[IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) を使って作成したライセンスに必要な権限を追加しています。 この例は、権限の作成のほか、権限リストを使用したライセンスへの権限の割り当てを示しています。

次の 2 つの権限が次のユーザーに追加されます。

- *読み取り*アクセス許可が joe@contoso.com に割り当てられます。
- *完全な*アクセス許可が mary\_kay@contoso.com に割り当てられます。

      // Create User Rights structure
      IPC_USER_RIGHTS ownerRightForOwner = {0};

      // Create rights
      LPCWSTR rgwszOwnerRights[1] = {IPC_GENERIC_ALL};

      // Assign values to members of Rights structure
      ownerRightForOwner.User.dwType = IPC_USER_TYPE_IPC;
      ownerRightForOwner.User.wszID = IPC_USER_ID_OWNER;
      ownerRightForOwner.rgwszRights = rgwszOwnerRights;
      ownerRightForOwner.cRights = 1;

      // Create User Rights structure for Joe with Read permissions
      IPC_USER_RIGHTS joeReadRight = {0};
      LPCWSTR rgwszReadRights[1] = {IPC_GENERIC_READ};

      // Assign values to members of Rights structure for Joe
      joeReadRight.User.dwType = IPC_USER_TYPE_EMAIL;
      joeReadRight.User.wszID = "joe@contoso.com";
      joeReadRight.rgwszRights = rgwszReadRights;
      joeReadRight.cRights = 1;

      // Create User Rights structure for Mary Kay with Full permissions
      IPC_USER_RIGHTS mary_kayFullRight = {0};
      LPCWSTR rgwszFullRights[1] = {IPC_GENERIC_ALL};

      // Assign values to members of Rights structure for Mary Kay
      mary_kayFullRight.User.dwType = IPC_USER_TYPE_EMAIL;
      mary_kayFullRight.User.wszID = L"mary_kay@contoso.com";
      mary_kayFullRight.rgwszRights = rgwszFullRights;
      mary_kayFullRight.cRights = 1;

      // Create User Rights List and assign the above rights
      size_t uNoOfUserRights = 3;
      PIPC_USER_RIGHTS_LIST pUserRightsList = NULL;
      pUserRightsList = reinterpret_cast<PIPC_USER_RIGHTS_LIST>
      (new BYTE[ sizeof(IPC_USER_RIGHTS_LIST) + uNoOfUserRights * sizeof(IPC_USER_RIGHTS)]);

      if(pUserRightsList == NULL)
      {
        // Handle error
      }

      // Assign values to members of Rights List structure for Joe and Mary Kay
      (*pUserRightsList).cbSize = sizeof(IPC_USER_RIGHTS_LIST);
      (*pUserRightsList).cUserRights = uNoOfUserRights;
      (*pUserRightsList).rgUserRights[0] = ownerRightForOwner;
      (*pUserRightsList).rgUserRights[1] = joeReadRight;
      (*pUserRightsList).rgUserRights[2] = mary_kayFullRight;

      // Set the Rights List property on the license via its handle
      // hLicense is a license handle created with IpcCreateLicenseFromScratch
      hr = IpcSetLicenseProperty(hLicense, FALSE, IPC_LI_USER_RIGHTS_LIST, pUserRightsList);

      if(FAILED(hr))
      {
        // Handle the error
      }



## <a name="related-topics"></a>関連トピック

- [開発者向け注意事項](developer-notes.md)
- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
