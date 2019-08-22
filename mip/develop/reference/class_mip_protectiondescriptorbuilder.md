---
title: class mip::ProtectionDescriptorBuilder
description: Microsoft Information Protection (MIP) SDK の mip::p rotectiondescriptorbuilder クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 5985aad4f4cb9b8276ca855026119507febc9445
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885122"
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
