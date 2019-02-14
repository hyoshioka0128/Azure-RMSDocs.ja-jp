---
title: class mip::ProtectionDescriptor
description: Mip::protectiondescriptor クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: d04d1fe3c3d59592084a60b68d50d74ae10291c0
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259628"
---
# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
コンテンツの一部に関連付けられている保護の説明。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  保護 SDK テンプレートが基になっているかどうかに関係なく、保護の種類を取得します。
public std::string GetOwner() const  |  保護するために所有者を取得します。
public std::string GetName() const  |  保護の名前を取得します。
public std::string GetDescription() const  |  保護の説明を取得します。
public std::string GetTemplateId() const  |  存在する場合、保護テンプレート ID を取得します。
public std::string GetLabelId() const  |  存在する場合、ラベル ID を取得します。
public std::vector\<UserRights\> GetUserRights() 定数  |  ユーザーから権限へのマッピングのコレクションを取得します。
public std::vector\<UserRoles\> GetUserRoles() 定数  |  ユーザーからロールへのマッピングのコレクションを取得します。
public bool DoesContentExpire() const  |  かどうかコンテンツ有効期限かどうかを確認します。
public std::chrono::time_point\<std::chrono::system_clock\> GetContentValidUntil() const  |  保護の有効期限を取得します。
public bool DoesAllowOfflineAccess() const  |  保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。
public std::string GetReferrer() const  |  保護の参照元のアドレスを取得します。
public std::map\<std::string, std::string\> GetEncryptedAppData() const  |  暗号化されたアプリ固有のデータを取得します。
public std::map\<std::string, std::string\> GetSignedAppData() const  |  署名されたアプリ固有のデータを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getprotectiontype-function"></a>GetProtectionType 関数
保護 SDK テンプレートが基になっているかどうかに関係なく、保護の種類を取得します。

  
**返します**:保護の種類
  
### <a name="getowner-function"></a>GetOwner 関数
保護するために所有者を取得します。

  
**返します**:保護の所有者
  
### <a name="getname-function"></a>GetName 関数
保護の名前を取得します。

  
**返します**:保護名
  
### <a name="getdescription-function"></a>GetDescription 関数
保護の説明を取得します。

  
**返します**:保護の説明
  
### <a name="gettemplateid-function"></a>GetTemplateId 関数
存在する場合、保護テンプレート ID を取得します。

  
**返します**:テンプレート ID
  
### <a name="getlabelid-function"></a>GetLabelId 関数
存在する場合、ラベル ID を取得します。

  
**返します**:[ラベル](class_mip_label.md)ID の既存の ProtectionDescriptors でこのプロパティが入力のみが保護されたコンテンツ。 これは、保護されたコンテンツが利用される時に、サーバーによって設定されたフィールドです。
  
### <a name="getuserrights-function"></a>GetUserRights 関数
ユーザーから権限へのマッピングのコレクションを取得します。

  
**返します**:ユーザーから権限へのマッピングのコレクションの値、 [UserRights](class_mip_userrights.md)プロパティは (つまり場合、ユーザーが所有者ではないと、VIEWRIGHTSDATA 権限がありません)、現在のユーザーはこの情報へのアクセスを持っていない場合は空になります。
  
### <a name="getuserroles-function"></a>GetUserRoles 関数
ユーザーからロールへのマッピングのコレクションを取得します。

  
**返します**:ユーザーからロールへのマッピングのコレクション
  
### <a name="doescontentexpire-function"></a>DoesContentExpire 関数
かどうかコンテンツ有効期限かどうかを確認します。

  
**返します**:コンテンツは有効期限、偽の場合は true。
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil 関数
保護の有効期限を取得します。

  
**返します**:保護の有効期限
  
### <a name="doesallowofflineaccess-function"></a>DoesAllowOfflineAccess 関数
保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。

  
**返します**:保護がない、またはオフライン コンテンツへのアクセスを許可する場合 (既定値 = true)
  
### <a name="getreferrer-function"></a>GetReferrer 関数
保護の参照元のアドレスを取得します。

  
**返します**:保護参照元アドレス。 参照元は、コンテンツ保護の解除できない場合、ユーザーに表示可能なである URI です。 これには、そのユーザーがコンテンツにアクセスするためのアクセス許可をどのように取得できるかに関する情報が含まれます。
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData 関数
暗号化されたアプリ固有のデータを取得します。

  
**返します**:アプリ固有のデータ。 [ProtectionHandler](class_mip_protectionhandler.md) protection サービスによって暗号化されたアプリ固有のデータのディクショナリを保持する可能性があります。 この暗号化データは、[ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getappsigneddata-function) を使用してアクセスできる署名済みデータに依存しません
  
### <a name="getsignedappdata-function"></a>GetSignedAppData 関数
署名されたアプリ固有のデータを取得します。

  
**返します**:アプリ固有のデータ。 [ProtectionHandler](class_mip_protectionhandler.md) protection サービスによって署名されたアプリ固有のデータのディクショナリを保持する可能性があります。 この署名済みデータは、[ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata-function) 経由でアクセスできる暗号化データに依存しません
