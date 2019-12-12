---
title: class mip::ProtectionDescriptor
description: Microsoft Information Protection (MIP) SDK の mip::p rotectiondescriptor クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 34acc6109a5d3dfcbbaec37e81f3215dd30f5018
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73557733"
---
# <a name="class-mipprotectiondescriptor"></a>class mip::ProtectionDescriptor 
コンテンツの一部に関連付けられている保護の説明。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public ProtectionType GetProtectionType() const  |  保護 SDK テンプレートが基になっているかどうかに関係なく、保護の種類を取得します。
public std::string GetOwner() const  |  保護するために所有者を取得します。
public std::string GetName() const  |  保護の名前を取得します。
public std::string GetDescription() const  |  保護の説明を取得します。
public std::string GetTemplateId() const  |  存在する場合、保護テンプレート ID を取得します。
public std::string GetLabelId() const  |  存在する場合、ラベル ID を取得します。
public std::string GetContentId() const  |  コンテンツ ID (存在する場合) を取得します。
public std:: vector\<UserRights\> GetUserRights () const  |  ユーザーから権限へのマッピングのコレクションを取得します。
public std:: vector\<UserRoles\> GetUserRoles () const  |  ユーザーからロールへのマッピングのコレクションを取得します。
public bool DoesContentExpire() const  |  コンテンツの有効期限が切れているかどうかを確認します。
public std::chrono::time_point\<std::chrono::system_clock\> GetContentValidUntil() const  |  保護の有効期限を取得します。
public bool DoesAllowOfflineAccess() const  |  保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。
public std::string GetReferrer() const  |  保護の参照元のアドレスを取得します。
public std::map\<std::string, std::string\> GetEncryptedAppData() const  |  暗号化されたアプリ固有のデータを取得します。
public std:: map\<std:: string、std:: string\> GetSignedAppData () const  |  署名されたアプリ固有のデータを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getprotectiontype-function"></a>GetProtectionType 関数
保護 SDK テンプレートが基になっているかどうかに関係なく、保護の種類を取得します。

  
**戻り値**: 保護の種類
  
### <a name="getowner-function"></a>GetOwner 関数
保護するために所有者を取得します。

  
**戻り値**: 保護の所有者
  
### <a name="getname-function"></a>GetName 関数
保護の名前を取得します。

  
**戻り値**: 保護の名前
  
### <a name="getdescription-function"></a>GetDescription 関数
保護の説明を取得します。

  
**戻り値**: 保護の説明
  
### <a name="gettemplateid-function"></a>GetTemplateId 関数
存在する場合、保護テンプレート ID を取得します。

  
**戻り値**: テンプレート ID
  
### <a name="getlabelid-function"></a>Getlabが d 関数
存在する場合、ラベル ID を取得します。

  
**戻り値**: ラベル ID このプロパティは、保護された既存のコンテンツの protectiondescriptors にのみ設定されます。 これは、保護されたコンテンツが利用される時に、サーバーによって設定されたフィールドです。
  
### <a name="getcontentid-function"></a>GetContentId 関数
コンテンツ ID (存在する場合) を取得します。

  
**戻り値**: コンテンツ ID
  
### <a name="getuserrights-function"></a>GetUserRights 関数
ユーザーから権限へのマッピングのコレクションを取得します。

  
**戻り**値: ユーザーから権限へのマッピングのコレクション。現在のユーザーがこの情報へのアクセス権を持っていない場合 (つまり、ユーザーが所有者ではなく、VIEWRIGHT .sdata 権限を持っていない場合)、userrights プロパティの値は空になります。
  
### <a name="getuserroles-function"></a>GetUserRoles 関数
ユーザーからロールへのマッピングのコレクションを取得します。

  
**戻り値**: ユーザーからロールへのマッピングのコレクション
  
### <a name="doescontentexpire-function"></a>@ Content有効期限関数
コンテンツの有効期限が切れているかどうかを確認します。

  
は、コンテンツの有効期限が切れる場合は True、それ以外の場合は false**を返し**ます。
  
### <a name="getcontentvaliduntil-function"></a>GetContentValidUntil 関数
保護の有効期限を取得します。

  
**戻り値**: 保護の有効期限
  
### <a name="doesallowofflineaccess-function"></a>アクセス関数
保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。

  
**戻り値**: 保護がオフライン コンテンツへのアクセスを許可するかどうか (既定値 = true)
  
### <a name="getreferrer-function"></a>GetReferrer 元関数
保護の参照元のアドレスを取得します。

  
**戻り値**: 保護の参照元のアドレス参照元は、コンテンツの保護を解除できない場合、ユーザーに表示可能な URI です。 これには、そのユーザーがコンテンツにアクセスするためのアクセス許可をどのように取得できるかに関する情報が含まれます。
  
### <a name="getencryptedappdata-function"></a>GetEncryptedAppData 関数
暗号化されたアプリ固有のデータを取得します。

  
が**返さ**れます: アプリ固有のデータ保護サービスによって暗号化されたアプリ固有のデータの辞書を保持することができます。 この暗号化されたデータは、ProtectionDescriptor:: GetSignedAppData を使用してアクセスできる署名済みデータに依存しません。
  
### <a name="getsignedappdata-function"></a>GetSignedAppData 関数
署名されたアプリ固有のデータを取得します。

  
が**返さ**れます: アプリ固有のデータ保護サービスによって署名されたアプリ固有のデータの辞書を保持することができます。 この署名付きデータは、ProtectionDescriptor:: GetEncryptedAppData を使用してアクセスできる暗号化されたデータに依存しません。