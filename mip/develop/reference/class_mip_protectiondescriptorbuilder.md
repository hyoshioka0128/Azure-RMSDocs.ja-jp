---
title: class mip::ProtectionDescriptorBuilder
description: Microsoft Information Protection (MIP) SDK の mip::p rotectiondescriptorbuilder クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: cf3007c7d75b669de3f9952223f4f3920489251e
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070588"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
コンテンツの一部に関連付けられている保護を説明する、[ProtectionDescriptor](class_mip_protectiondescriptor.md) を構築します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public MIP_API std:: shared_ptr\<protectiondescriptor\> Build ()  |  この [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) インスタンスによってアクセス許可が定義される [ProtectionDescriptor](class_mip_protectiondescriptor.md) を作成します。
public void SetName(const std::string& value)  |  保護ポリシー名を設定します。
public void SetDescription(const std::string& value)  |  保護ポリシーの説明を設定します。
public void SetContentValidUntil(const std::chrono::time_point\<std::chrono::system_clock\>& value)  |  保護ポリシーの有効期限を設定します。
public void SetAllowOfflineAccess(bool value)  |  保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
public void SetReferrer(const std::string& uri)  |  保護ポリシーの参照元のアドレスを設定します。
public void SetEncryptedAppData(const std::map\<std::string, std::string\>& value)  |  暗号化する必要のあるアプリ固有のデータを設定します。
public void setsignedappdata (const std:: map\<std:: string, std:: string\>& value)  |  署名する必要があるアプリ固有のデータを設定します。
public virtual ~ProtectionDescriptorBuilder()  | _まだ文書化されていません。_
public static MIP_API std:: shared_ptr&lt;protection記述子ビルダー&gt; MIP::P rotectiondescriptorbuilder:: createfromuserrights | ユーザーと権限によって定義されるアクセス権限を持つ Protection記述子ビルダーを作成します。
public static MIP_API std:: shared_ptr&lt;protection記述子ビルダー&gt; MIP::P rotectiondescriptorbuilder:: createfromuserroles | ユーザーおよびロールによってアクセス許可が定義されている Protection記述子ビルダーを作成します。
public static MIP_API std:: shared_ptr&lt;protection記述子ビルダー&gt; MIP::P rotectiondescriptorbuilder:: CreateFromTemplate | 保護テンプレートによって定義されたアクセス許可を持つ Protection記述子ビルダーを作成します。 


## <a name="members"></a>メンバー
  
### <a name="build-function"></a>ビルド関数
この [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) インスタンスによってアクセス許可が定義される [ProtectionDescriptor](class_mip_protectiondescriptor.md) を作成します。

  
次の**値を返し**ます。新しい[Protectiondescriptor](class_mip_protectiondescriptor.md)インスタンス
  
### <a name="setname-function"></a>SetName 関数
保護ポリシー名を設定します。

パラメーター:  
* **値**:保護ポリシー名


  
### <a name="setdescription-function"></a>SetDescription 関数
保護ポリシーの説明を設定します。

パラメーター:  
* **値**:ポリシーの説明

### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil 関数
保護ポリシーの有効期限を設定します。

パラメーター:  
* **値**:ポリシーの有効期限


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess 関数
保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。

パラメーター:  
* **値**:ポリシーでオフラインコンテンツへのアクセスが許可されているかどうか

### <a name="setreferrer-function"></a>SetReferrer 関数
保護ポリシーの参照元のアドレスを設定します。

パラメーター:  
* **uri**:ポリシーの参照元アドレス


参照元は、保護ポリシーの取得に失敗したときにユーザーが表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法に関する情報が含まれます。
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData 関数
暗号化する必要のあるアプリ固有のデータを設定します。

パラメーター:  
* **値**:アプリ固有のデータ


アプリケーションでは、保護サービスによって暗号化されるアプリ固有のデータのディクショナリを指定できます。 この暗号化データは、SetSignedAppData によって設定される署名済みデータに依存しません。
  
### <a name="setsignedappdata-function"></a>SetSignedAppData 関数
署名する必要があるアプリ固有のデータを設定します。

パラメーター:  
* **値**:アプリ固有のデータ


アプリケーションでは、保護サービスによって署名されるアプリ固有のデータのディクショナリを指定できます。 この署名済みデータは、SetEncryptedAppData によって設定される暗号化データに依存しません。
  
### <a name="protectiondescriptorbuilder-function"></a>~ Protection記述子ビルダー関数
_まだ文書化されていません。_

### <a name="createfromuserrights-function"></a>CreateFromUserRights 関数
ユーザーと権限によって定義されるアクセス権限を持つ Protection記述子ビルダーを作成します。

パラメーター:
* **usersAndRights**:ユーザーから権限へのマッピングのコレクション。

次の**値を返し**ます。新しい[Protectiondescriptor](class_mip_protectiondescriptor.md)インスタンス 

### <a name="createfromuserroles-function"></a>CreateFromUserRoles 関数
ユーザーおよびロールによってアクセス許可が定義されている Protection記述子ビルダーを作成します。

パラメーター:
* **usersAndRoles**:ユーザーからロールへのマッピングのコレクション。

次の**値を返し**ます。ユーザーおよびロールによってアクセス許可が定義されている[Protectiondescriptor](class_mip_protectiondescriptor.md)を作成します。

### <a name="createfromtemplate-function"></a>CreateFromTemplate 関数
保護テンプレートによって定義されたアクセス許可を持つ Protection記述子ビルダーを作成します。 

パラメーター:
* **templateId**:保護テンプレート ID。

次の**値を返し**ます。新しい[Protectiondescriptor](class_mip_protectiondescriptor.md)インスタンス。



