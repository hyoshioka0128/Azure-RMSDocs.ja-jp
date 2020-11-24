---
title: クラス ProtectionDescriptor
description: 'Microsoft Information Protection (MIP) SDK の protectiondescriptor:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 16095a9183fb0dd89306a4769cd21499afc09d55
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569134"
---
# <a name="class-protectiondescriptor"></a>クラス ProtectionDescriptor 
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
public std:: string GetContentId () const  |  コンテンツ ID (存在する場合) を取得します。
public std::vector\<UserRights\> GetUserRights() const  |  ユーザーから権限へのマッピングのコレクションを取得します。
public std::vector\<UserRoles\> GetUserRoles() const  |  ユーザーからロールへのマッピングのコレクションを取得します。
public bool の有効期限 () const  |  コンテンツの有効期限が切れているかどうかを確認します。
public std:: chrono:: time_point \<std::chrono::system_clock\> getcontentvaliduntil () const  |  保護の有効期限を取得します。
public bool DoesAllowOfflineAccess() const  |  保護がオフライン コンテンツへのアクセスを許可するかどうかを取得します。
public std::string GetReferrer() const  |  保護の参照元のアドレスを取得します。
public std:: map \<std::string, std::string\> getencryptedappdata () const  |  暗号化されたアプリ固有のデータを取得します。
public std:: map \<std::string, std::string\> getsignedappdata () const  |  署名されたアプリ固有のデータを取得します。
public std:: string GetDoubleKeyUrl () const  |  カスタム保護に使用する2つのキーの url を取得します。
  
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

  
**戻り値**: ユーザーから権限へのマッピングのコレクション。現在のユーザーがこの情報へのアクセス権を持っていない (つまり、ユーザーが所有者ではなく VIEWRIGHTSDATA 権限がない) 場合、UserRights プロパティの値は空になります。
  
### <a name="getuserroles-function"></a>GetUserRoles 関数
ユーザーからロールへのマッピングのコレクションを取得します。

  
**戻り値**: ユーザーからロールへのマッピングのコレクション
  
### <a name="doescontentexpire-function"></a>@ Content有効期限関数
コンテンツの有効期限が切れているかどうかを確認します。

  
は、コンテンツの有効期限が切れる場合は True、それ以外の場合は false **を返し** ます。
  
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

  
**戻り値**: アプリ固有のデータ。ProtectionHandler では、保護サービスによって暗号化されたアプリ固有のデータのディクショナリを保持する場合があります。 この暗号化データは、ProtectionDescriptor::GetSignedAppData を使用してアクセスできる署名済みデータに依存しません
  
### <a name="getsignedappdata-function"></a>GetSignedAppData 関数
署名されたアプリ固有のデータを取得します。

  
**戻り値**: アプリ固有のデータ。ProtectionHandler では、保護サービスが署名したアプリ固有のデータのディクショナリを保持する場合があります。 この署名済みデータは、ProtectionDescriptor::GetEncryptedAppData 経由でアクセスできる暗号化データに依存しません
  
### <a name="getdoublekeyurl-function"></a>GetDoubleKeyUrl 関数
カスタム保護に使用する2つのキーの url を取得します。

  
**返される値**: 2 番目のキーで情報を保護するためにカスタム要求で使用される2つのキーの url。