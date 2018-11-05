---
title: class mip ProtectionDescriptor
description: class mip ProtectionDescriptor のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e723041af1eec7be7a839bf36f6d3db67b32447f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446551"
---
# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
コンテンツの一部に関連付けられている保護の説明。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public ProtectionType GetProtectionType() const  |  保護 SDK テンプレートが基になっているかどうかに関係なく、保護の種類を取得します。
 public std::string GetOwner() const  |  保護するために所有者を取得します。
 public std::string GetName() const  |  保護の名前を取得します。
 public std::string GetDescription() const  |  保護の説明を取得します。
 public std::string GetTemplateId() const  |  存在する場合、保護テンプレート ID を取得します。
 public std::string GetLabelId() const  |  存在する場合、ラベル ID を取得します。
public std::vector<UserRights> GetUserRights() const  |  ユーザーから権限へのマッピングのコレクションを取得します。
public std::vector<UserRoles> GetUserRoles() const  |  ユーザーからロールへのマッピングのコレクションを取得します。
public std::chrono::time_point<std::chrono::system_clock> GetContentValidUntil() const  |  保護の有効期限を取得します。
 public bool DoesAllowOfflineAccess() const  |  保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。
 public std::string GetReferrer() const  |  保護の参照元のアドレスを取得します。
public std::map<std::string, std::string> GetEncryptedAppData() const  |  暗号化されたアプリ固有のデータを取得します。
public std::map<std::string, std::string> GetSignedAppData() const  |  署名されたアプリ固有のデータを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="protectiontype"></a>ProtectionType
保護 SDK テンプレートが基になっているかどうかに関係なく、保護の種類を取得します。

  
**戻り値**: 保護の種類
  
### <a name="getowner"></a>GetOwner
保護するために所有者を取得します。

  
**戻り値**: 保護の所有者
  
### <a name="getname"></a>GetName
保護の名前を取得します。

  
**戻り値**: 保護の名前
  
### <a name="getdescription"></a>GetDescription
保護の説明を取得します。

  
**戻り値**: 保護の説明
  
### <a name="gettemplateid"></a>GetTemplateId
存在する場合、保護テンプレート ID を取得します。

  
**戻り値**: テンプレート ID
  
### <a name="getlabelid"></a>GetLabelId
存在する場合、ラベル ID を取得します。

  
**戻り値**: [ラベル](class_mip_label.md) ID このプロパティは、既存の保護されたコンテンツに対して ProtectionDescriptors にのみ設定されます。 これは、保護されたコンテンツが利用される時に、サーバーによって設定されたフィールドです。
  
### <a name="userrights"></a>UserRights
ユーザーから権限へのマッピングのコレクションを取得します。

  
**戻り値**: ユーザーから権限へのマッピングのコレクション。現在のユーザーがこの情報へのアクセス権を持っていない (つまり、ユーザーが所有者ではなく VIEWRIGHTSDATA 権限がない) 場合、[UserRights](class_mip_userrights.md) プロパティの値は空になります。
  
### <a name="userroles"></a>UserRoles
ユーザーからロールへのマッピングのコレクションを取得します。

  
**戻り値**: ユーザーからロールへのマッピングのコレクション
  
### <a name="getcontentvaliduntil"></a>GetContentValidUntil
保護の有効期限を取得します。

  
**戻り値**: 保護の有効期限
  
### <a name="doesallowofflineaccess"></a>DoesAllowOfflineAccess
保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。

  
**戻り値**: 保護がオフライン コンテンツへのアクセスを許可するかどうか (既定値 = true)
  
### <a name="getreferrer"></a>GetReferrer
保護の参照元のアドレスを取得します。

  
**戻り値**: 保護の参照元のアドレス参照元は、コンテンツの保護を解除できない場合、ユーザーに表示可能な URI です。 これには、そのユーザーがコンテンツにアクセスするためのアクセス許可をどのように取得できるかに関する情報が含まれます。
  
### <a name="getencryptedappdata"></a>GetEncryptedAppData
暗号化されたアプリ固有のデータを取得します。

  
**戻り値**: アプリ固有のデータ。[ProtectionHandler](class_mip_protectionhandler.md) では、保護サービスによって暗号化されたアプリ固有のデータのディクショナリを保持する場合があります。 この暗号化データは、[ProtectionDescriptor::GetSignedAppData](class_mip_protectiondescriptor.md#getsignedappdata) を使用してアクセスできる署名済みデータに依存しません
  
### <a name="getsignedappdata"></a>GetSignedAppData
署名されたアプリ固有のデータを取得します。

  
**戻り値**: アプリ固有のデータ。[ProtectionHandler](class_mip_protectionhandler.md) では、保護サービスが署名したアプリ固有のデータのディクショナリを保持する場合があります。 この署名済みデータは、[ProtectionDescriptor::GetEncryptedAppData](class_mip_protectiondescriptor.md#getencryptedappdata) 経由でアクセスできる暗号化データに依存しません