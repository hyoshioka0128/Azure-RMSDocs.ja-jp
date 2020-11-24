---
title: クラス Protection記述子ビルダー
description: 'Microsoft Information Protection (MIP) SDK の protection記述子ビルダー:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 2e5573a896ef0935c33e85a2ed7f73451ced8e7c
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569127"
---
# <a name="class-protectiondescriptorbuilder"></a>クラス Protection記述子ビルダー 
コンテンツの一部に関連付けられている保護を説明する、ProtectionDescriptor を構築します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr\<ProtectionDescriptor\> Build()  |  この ProtectionDescriptorBuilder インスタンスによってアクセス許可が定義される ProtectionDescriptor を作成します。
public void SetName(const std::string& value)  |  保護ポリシー名を設定します。
public void SetDescription(const std::string& value)  |  保護ポリシーの説明を設定します。
public void SetContentValidUntil (const std:: chrono:: time_point \<std::chrono::system_clock\>& 値)  |  保護ポリシーの有効期限を設定します。
public void SetAllowOfflineAccess(bool value)  |  保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
public void SetReferrer(const std::string& uri)  |  保護ポリシーの参照元のアドレスを設定します。
public void SetEncryptedAppData (const std:: map \<std::string, std::string\>& value)  |  暗号化する必要のあるアプリ固有のデータを設定します。
public void SetSignedAppData (const std:: map \<std::string, std::string\>& value)  |  署名する必要があるアプリ固有のデータを設定します。
public void SetDoubleKeyUrl (const std:: string& doubleKeyUrl)  |  カスタム保護に使用する2つのキーの url を設定します。
  
## <a name="members"></a>メンバー
  
### <a name="build-function"></a>ビルド関数
この ProtectionDescriptorBuilder インスタンスによってアクセス許可が定義される ProtectionDescriptor を作成します。

  
**戻り値**: 新しい ProtectionDescriptor インスタンス
  
### <a name="setname-function"></a>SetName 関数
保護ポリシー名を設定します。

パラメーター:  
* **value**: 保護ポリシー名


  
### <a name="setdescription-function"></a>SetDescription 関数
保護ポリシーの説明を設定します。

パラメーター:  
* **値**: ポリシーの説明


  
### <a name="setcontentvaliduntil-function"></a>SetContentValidUntil 関数
保護ポリシーの有効期限を設定します。

パラメーター:  
* **値**: ポリシーの有効期限


  
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
  
### <a name="setdoublekeyurl-function"></a>SetDoubleKeyUrl 関数
カスタム保護に使用する2つのキーの url を設定します。

パラメーター:  
* **値**: 2 つのキーの url

