---
title: class mip::ProtectionHandler
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionhandler クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 306748121e34122a5623aea3e1d7ff4ba7f14787
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883421"
---
# <a name="class-mipprotectionhandler"></a>class mip::ProtectionHandler 
特定の保護構成のための保護に関連するアクションを管理します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ストリーム\> CreateProtectedStream (const std:: shared_ptr\<ストリーム\>& backingstream、int64_t contentStartPosition、int64_t contentsize)  |  コンテンツの暗号化/暗号化解除を可能にする、保護されたストリームを作成します。
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化します。
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化解除します。
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  この [ProtectionHandler](class_mip_protectionhandler.md) を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。
public int64_t GetBlockSize()  |  この [ProtectionHandler](class_mip_protectionhandler.md) で使用される暗号モードのブロック サイズ (バイト) を取得します。
public std:: vector\<std:: string\> getrights () const  |  この [ProtectionHandler](class_mip_protectionhandler.md) に関連付けられているユーザー/ID に付与された権限を取得します。
public bool AccessCheck(const std::string& right) const  |  保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。
public const std::string GetIssuedTo()  |  保護ハンドラーに関連付けられているユーザーを取得します。
public const std::string GetOwner()  |  コンテンツ所有者のメール アドレスを取得します。
public bool IsIssuedToOwner()  |  現在のユーザーがコンテンツの所有者かどうかを取得します。
public std:: shared_ptr\<protectiondescriptor\> getprotectiondescriptor ()  |  保護の詳細を取得します。
public const std::string GetContentId()  |  ドキュメント/コンテンツの一意識別子を取得します。
public bool DoesUseDeprecatedAlgorithms()  |  保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。
public bool IsAuditedExtractAllowed()  |  保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。
public const std:: vector\<uint8_t\> GetSerializedPublishingLicense ()  |  [ProtectionHandler](class_mip_protectionhandler.md) を発行ライセンス (PL) にシリアル化します
  
## <a name="members"></a>メンバー
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream 関数
コンテンツの暗号化/暗号化解除を可能にする、保護されたストリームを作成します。

パラメーター:  
* **Backingstream**:読み取り/書き込みの対象となるバッキングストリーム 


* **contentStartPosition**:保護されたコンテンツを開始するバッキングストリーム内の開始位置 (バイト単位) 


* **Contentsize**:バッキングストリーム内の保護されたコンテンツのサイズ (バイト単位)



  
次の**値を返し**ます。保護されたストリーム
  
### <a name="encryptbuffer-function"></a>EncryptBuffer 関数
バッファーを暗号化します。

パラメーター:  
* **offsetFromStart**:クリアテキストコンテンツの先頭からの inputBuffer の相対位置 


* **inputBuffer**:暗号化されるクリアテキストのコンテンツのバッファー 


* **Inputbuffersize**:入力バッファーのサイズ (バイト単位) 


* **Outputbuffer**:暗号化されたコンテンツがコピーされるバッファー 


* **Outputbuffersize**:出力バッファーのサイズ (バイト単位) 


* **Isfinal**:入力バッファーに最終的なクリアテキストバイトが含まれているかどうか



  
次の**値を返し**ます。暗号化されたコンテンツの実際のサイズ (バイト単位)
  
### <a name="decryptbuffer-function"></a>DecryptBuffer 関数
バッファーを暗号化解除します。

パラメーター:  
* **offsetFromStart**:暗号化されたコンテンツの先頭からの inputBuffer の相対位置 


* **inputBuffer**:復号化される暗号化されたコンテンツのバッファー 


* **Inputbuffersize**:入力バッファーのサイズ (バイト単位) 


* **Outputbuffer**:復号化されたコンテンツのコピー先のバッファー 


* **Outputbuffersize**:出力バッファーのサイズ (バイト単位) 


* **Isfinal**:入力バッファーに最後の暗号化されたバイトが含まれているかどうか



  
次の**値を返し**ます。復号化されたコンテンツの実際のサイズ (バイト単位)
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength 関数
この [ProtectionHandler](class_mip_protectionhandler.md) を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。

パラメーター:  
* **unprotectedLength**:保護されていないコンテンツのサイズ (バイト単位) 


* すべての**Finalblock**:対象の保護されていないコンテンツに最後のブロックが含まれているかどうかを示します。 たとえば、CBC4k 暗号化モードでは、保護される非最終ブロックのサイズは保護されないブロックと同じですが、保護される最終ブロックは対応する保護されないブロックより大きくなります。



  
次の**値を返し**ます。保護されたコンテンツのサイズ (バイト単位)
  
### <a name="getblocksize-function"></a>GetBlockSize 関数
この [ProtectionHandler](class_mip_protectionhandler.md) で使用される暗号モードのブロック サイズ (バイト) を取得します。

  
次の**値を返し**ます。ブロックサイズ (バイト単位)
  
### <a name="getrights-function"></a>GetRights 関数
この [ProtectionHandler](class_mip_protectionhandler.md) に関連付けられているユーザー/ID に付与された権限を取得します。

  
次の**値を返し**ます。ユーザーに付与された権限
  
### <a name="accesscheck-function"></a>AccessCheck 関数
保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。

パラメーター:  
* **right**:確認する権限



  
次の**値を返し**ます。保護ハンドラーが、指定された権限に対するユーザーアクセス権を付与する場合
  
### <a name="getissuedto-function"></a>GetIssuedTo 関数
保護ハンドラーに関連付けられているユーザーを取得します。

  
次の**値を返し**ます。保護ハンドラーに関連付けられているユーザー
  
### <a name="getowner-function"></a>GetOwner 関数
コンテンツ所有者のメール アドレスを取得します。

  
次の**値を返し**ます。コンテンツ所有者のメール アドレス
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner 関数
現在のユーザーがコンテンツの所有者かどうかを取得します。

  
次の**値を返し**ます。現在のユーザーがコンテンツの所有者であるかどうか
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護の詳細を取得します。

  
次の**値を返し**ます。保護の詳細
  
### <a name="getcontentid-function"></a>GetContentId 関数
ドキュメント/コンテンツの一意識別子を取得します。

  
次の**値を返し**ます。一意のコンテンツ識別子
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms 関数
保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。

  
次の**値を返し**ます。保護ハンドラーが非推奨の暗号アルゴリズムを使用する場合
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed 関数
保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。

  
次の**値を返し**ます。保護ハンドラーがユーザーの ' 監査済み抽出 ' 権限を付与する場合
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 関数
[ProtectionHandler](class_mip_protectionhandler.md) を発行ライセンス (PL) にシリアル化します

  
次の**値を返し**ます。シリアル化された公開ライセンス