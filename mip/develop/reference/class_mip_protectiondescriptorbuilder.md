---
title: class mip::ProtectionDescriptorBuilder
description: Microsoft Information Protection (MIP) SDK の mip::p rotectiondescriptorbuilder クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: ed9d7085f7406e5c921843d32069f2f6af9f5807
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489692"
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
public virtual ~ProtectionDescriptorBuilder()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="build-function"></a>ビルド関数
この ProtectionDescriptor ビルダーインスタンスによってアクセス許可が定義されている ProtectionDescriptor を作成します。

  
**戻り値**: 新しい protectiondescriptor インスタンス
  
### <a name="setname-function"></a>SetName 関数
保護ポリシー名を設定します。

パラメータ:  
* **value**: 保護ポリシー名


  
### <a name="setdescription-function"></a>SetDescription 関数
保護ポリシーの説明を設定します。

パラメータ:  
* **value**: ポリシーの説明


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil 関数
保護ポリシーの有効期限を設定します。

パラメータ:  
* **value**: ポリシーの有効期限


  
### <a name="setallowofflineaccess-function"></a>SetAllowOfflineAccess 関数
保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。

パラメータ:  
* **value**: ポリシーがオフライン コンテンツへのアクセスを許可するかどうか


  
### <a name="setreferrer-function"></a>SetReferrer 関数
保護ポリシーの参照元のアドレスを設定します。

パラメータ:  
* **uri**: ポリシーの参照元のアドレス


参照元は、保護ポリシーの取得に失敗したときにユーザーが表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法に関する情報が含まれます。
  
### <a name="setencryptedappdata-function"></a>SetEncryptedAppData 関数
暗号化する必要のあるアプリ固有のデータを設定します。

パラメータ:  
* **value**: アプリ固有のデータ


アプリケーションでは、保護サービスによって暗号化されるアプリ固有のデータのディクショナリを指定できます。 この暗号化データは、SetSignedAppData によって設定される署名済みデータに依存しません。
  
### <a name="setsignedappdata-function"></a>SetSignedAppData 関数
署名する必要があるアプリ固有のデータを設定します。

パラメータ:  
* **value**: アプリ固有のデータ


アプリケーションでは、保護サービスによって署名されるアプリ固有のデータのディクショナリを指定できます。 この署名済みデータは、SetEncryptedAppData によって設定される暗号化データに依存しません。
  
### <a name="protectiondescriptorbuilder-function"></a>~ Protection記述子ビルダー関数
_まだ文書化されていません。_
