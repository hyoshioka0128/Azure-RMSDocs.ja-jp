---
title: class mip::ProtectionDescriptorBuilder
description: Mip::protectiondescriptorbuilder クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: b6ac49c7cb4d6f7592abac041365191d90951b7a
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651292"
---
# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
コンテンツの一部に関連付けられている保護を説明する、[ProtectionDescriptor](class_mip_protectiondescriptor.md) を構築します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr\<ProtectionDescriptor\> Build()  |  この [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) インスタンスによってアクセス許可が定義される [ProtectionDescriptor](class_mip_protectiondescriptor.md) を作成します。
public void SetName(const std::string& value)  |  保護ポリシー名を設定します。
public void SetDescription(const std::string& value)  |  保護ポリシーの説明を設定します。
public void SetContentValidUntil(const std::chrono::time_point\<std::chrono::system_clock\>& value)  |  保護ポリシーの有効期限を設定します。
public void SetAllowOfflineAccess(bool value)  |  保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
public void SetReferrer(const std::string& uri)  |  保護ポリシーの参照元のアドレスを設定します。
public void SetEncryptedAppData(const std::map\<std::string, std::string\>& value)  |  暗号化する必要のあるアプリ固有のデータを設定します。
public void SetSignedAppData(const std::map\<std::string, std::string\>& value)  |  署名する必要があるアプリ固有のデータを設定します。
public virtual ~ProtectionDescriptorBuilder()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="build-function"></a>関数を構築します。
この [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) インスタンスによってアクセス許可が定義される [ProtectionDescriptor](class_mip_protectiondescriptor.md) を作成します。

  
**返します**:新しい[ProtectionDescriptor](class_mip_protectiondescriptor.md)インスタンス
  
### <a name="setname-function"></a>SetName 関数
保護ポリシー名を設定します。

パラメーター:  
* **値**:保護ポリシーの名前


  
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
* **値**:かどうか、ポリシーがオフライン コンテンツへのアクセスを許可する場合


  
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
  
### <a name="protectiondescriptorbuilder-function"></a>~ ProtectionDescriptorBuilder 関数
_まだ文書化されていません。_
