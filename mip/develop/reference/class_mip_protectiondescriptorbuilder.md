---
title: class mip::ProtectionDescriptorBuilder
description: Microsoft Information Protection (MIP) SDK の mip::p rotectiondescriptorbuilder クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: cdc72fd45a4b82611aa02d0a9182cd829b6d8a9e
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560772"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
コンテンツの一部に関連付けられた保護を記述する ProtectionDescriptor を構築します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public MIP_API std:: shared_ptr\<ProtectionDescriptor\> Build ()  |  この ProtectionDescriptor ビルダーインスタンスによってアクセス許可が定義されている ProtectionDescriptor を作成します。
public void SetName(const std::string& value)  |  保護ポリシー名を設定します。
public void SetDescription(const std::string& value)  |  保護ポリシーの説明を設定します。
public void SetContentValidUntil (const std:: chrono:: time_point\<std:: chrono:: system_clock\>& 値)  |  保護ポリシーの有効期限を設定します。
public void SetAllowOfflineAccess(bool value)  |  保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
public void SetReferrer(const std::string& uri)  |  保護ポリシーの参照元のアドレスを設定します。
public void SetEncryptedAppData (const std:: map\<std:: string、std:: string\>& 値)  |  暗号化する必要のあるアプリ固有のデータを設定します。
public void SetSignedAppData (const std:: map\<std:: string、std:: string\>& 値)  |  署名する必要があるアプリ固有のデータを設定します。
public virtual ~ProtectionDescriptorBuilder()  | まだ文書化されていません。
public static MIP_API std:: shared_ptr&lt;Protection記述子ビルダー&gt; MIP::P rotectionDescriptorBuilder:: CreateFromUserRights | ユーザーと権限によって定義されるアクセス権限を持つ Protection記述子ビルダーを作成します。
public static MIP_API std:: shared_ptr&lt;Protection記述子ビルダー&gt; MIP::P rotectionDescriptorBuilder:: CreateFromUserRoles | ユーザーおよびロールによってアクセス許可が定義されている Protection記述子ビルダーを作成します。
public static MIP_API std:: shared_ptr&lt;Protection記述子ビルダー&gt; MIP::P rotectionDescriptorBuilder:: CreateFromTemplate | 保護テンプレートによって定義されたアクセス許可を持つ Protection記述子ビルダーを作成します。 

## <a name="members"></a>メンバー
  
### <a name="build-function"></a>ビルド関数
この ProtectionDescriptor ビルダーインスタンスによってアクセス許可が定義されている ProtectionDescriptor を作成します。

  
**戻り値**: 新しい protectiondescriptor インスタンス
  
### <a name="setname-function"></a>SetName 関数
保護ポリシー名を設定します。

パラメーター:  
* **value**: 保護ポリシー名


  
### <a name="setdescription-function"></a>SetDescription 関数
保護ポリシーの説明を設定します。

パラメーター:  
* **value**: ポリシーの説明


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil 関数
保護ポリシーの有効期限を設定します。

パラメーター:  
* **value**: ポリシーの有効期限


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess 関数
保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。

パラメーター:  
* **value**: ポリシーがオフライン コンテンツへのアクセスを許可するかどうか


  
### <a name="setreferrer-function"></a>SetReferrer 関数
保護ポリシーの参照元のアドレスを設定します。

パラメーター:  
* **uri**: ポリシーの参照元のアドレス


参照元は、保護ポリシーの取得に失敗したときにユーザーが表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法に関する情報が含まれます。
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData 関数
暗号化する必要のあるアプリ固有のデータを設定します。

パラメーター:  
* **value**: アプリ固有のデータ


アプリケーションでは、保護サービスによって暗号化されるアプリ固有のデータのディクショナリを指定できます。 この暗号化データは、SetSignedAppData によって設定される署名済みデータに依存しません。
  
### <a name="setsignedappdata-function"></a>SetSignedAppData 関数
署名する必要があるアプリ固有のデータを設定します。

パラメーター:  
* **value**: アプリ固有のデータ


アプリケーションでは、保護サービスによって署名されるアプリ固有のデータのディクショナリを指定できます。 この署名済みデータは、SetEncryptedAppData によって設定される暗号化データに依存しません。
  
### <a name="protectiondescriptorbuilder-function"></a>~ Protection記述子ビルダー関数
_まだ文書化されていません。_

### <a name="createfromuserrights-function"></a>CreateFromUserRights 関数
ユーザーと権限によって定義されるアクセス権限を持つ Protection記述子ビルダーを作成します。

パラメーター:
* **usersAndRights**: ユーザーから権限へのマッピングのコレクション。

**戻り値**: 新しい [ProtectionDescriptor](class_mip_protectiondescriptor.md) インスタンス 

### <a name="createfromuserroles-function"></a>CreateFromUserRoles 関数
ユーザーおよびロールによってアクセス許可が定義されている Protection記述子ビルダーを作成します。

パラメーター:
* **usersAndRoles**: ユーザーからロールへのマッピングのコレクション。

**を返し**ます。ユーザーとロールによってアクセス許可が定義されている[protectiondescriptor](class_mip_protectiondescriptor.md)を作成します。

### <a name="createfromtemplate-function"></a>CreateFromTemplate 関数
保護テンプレートによって定義されたアクセス許可を持つ Protection記述子ビルダーを作成します。 

パラメーター:
* **templateId**: 保護テンプレート ID。

**戻り値**: 新しい[protectiondescriptor](class_mip_protectiondescriptor.md)インスタンス。