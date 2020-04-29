---
title: クラス ProtectionHandler
description: 'Microsoft Information Protection (MIP) SDK の protectionhandler:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 948db155cbeca6c36c10bac76f26d42952e11e90
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764490"
---
# <a name="class-protectionhandler"></a>クラス ProtectionHandler 
特定の保護構成のための保護に関連するアクションを管理します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<stream\> CreateProtectedStream (const std:: Shared_ptr\<stream\>& Backingstream、int64_t contentStartPosition、int64_t contentsize)  |  コンテンツの暗号化/暗号化解除を可能にする、保護されたストリームを作成します。
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化します。
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化解除します。
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  この ProtectionHandler を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。
public int64_t GetBlockSize()  |  この ProtectionHandler で使用される暗号モードのブロック サイズ (バイト) を取得します。
public std:: vector\<std:: string\> getrights () const  |  この ProtectionHandler に関連付けられているユーザー/ID に付与された権限を取得します。
public bool AccessCheck(const std::string& right) const  |  保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。
public const std::string GetIssuedTo()  |  保護ハンドラーに関連付けられているユーザーを取得します。
public const std::string GetOwner()  |  コンテンツ所有者のメール アドレスを取得します。
public bool IsIssuedToOwner()  |  現在のユーザーがコンテンツの所有者かどうかを取得します。
public std:: shared_ptr\<protectiondescriptor\> getprotectiondescriptor ()  |  保護の詳細を取得します。
public const std::string GetContentId()  |  ドキュメント/コンテンツの一意識別子を取得します。
public bool DoesUseDeprecatedAlgorithms()  |  保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。
public bool IsAuditedExtractAllowed()  |  保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。
public const std:: vector\<Uint8_t\>& GetSerializedPublishingLicense () const  |  ProtectionHandler を発行ライセンス (PL) にシリアル化します
public const std:: vector\<Uint8_t\>& GetSerializedPreLicense (prelicenseformat format) const  |  ライセンスを取得します。
enum PreLicenseFormat  |  ライセンス前の形式。
  
## <a name="members"></a>メンバー
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream 関数
コンテンツの暗号化/暗号化解除を可能にする、保護されたストリームを作成します。

パラメーター:  
* **backingStream**: 読み取り/書き込みを行うバッキング ストリーム 


* **contentStartPosition**: 保護されたコンテンツが始まる、バッキング ストリーム内の開始位置 (バイト) 


* **contentSize**: バッキング ストリーム内の保護されたコンテンツのサイズ (バイト)



  
**戻り値**: 保護されたストリーム
  
### <a name="encryptbuffer-function"></a>EncryptBuffer 関数
バッファーを暗号化します。

パラメーター:  
* **offsetFromStart**: クリア テキスト コンテンツの先頭からの、inputBuffer の相対位置 


* **inputBuffer**: 暗号化されるクリア テキスト コンテンツのバッファー 


* **inputBufferSize**: 入力バッファーのサイズ (バイト) 


* **outputBuffer**: 暗号化されたコンテンツがコピーされるバッファー 


* **outputBufferSize**: 出力バッファーのサイズ (バイト) 


* **isFinal**: 入力バッファーにクリア テキストの最終バイトが含まれているかどうか



  
**戻り値**: 暗号化されたコンテンツの実際のサイズ (バイト)
  
### <a name="decryptbuffer-function"></a>DecryptBuffer 関数
バッファーを暗号化解除します。

パラメーター:  
* **offsetFromStart**: 暗号化されたコンテンツの先頭からの、inputBuffer の相対位置 


* **inputBuffer**: 暗号化解除する、暗号化されたコンテンツのバッファー 


* **inputBufferSize**: 入力バッファーのサイズ (バイト) 


* **outputBuffer**: 暗号化解除されたコンテンツがコピーされるバッファー 


* **outputBufferSize**: 出力バッファーのサイズ (バイト) 


* **isFinal**: 入力バッファーに暗号化された最終バイトが含まれているかどうか



  
**戻り値**: 暗号化解除されたコンテンツの実際のサイズ (バイト)
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength 関数
この ProtectionHandler を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。

パラメーター:  
* **unprotectedLength**: 保護されないコンテンツのサイズ (バイト単位) 


* **includesFinalBlock**: 対象の保護されないコンテンツに最終ブロックが含まれているかどうかを説明します。 たとえば、CBC4k 暗号化モードでは、保護される非最終ブロックのサイズは保護されないブロックと同じですが、保護される最終ブロックは対応する保護されないブロックより大きくなります。



  
**戻り値**: 保護されたコンテンツのサイズ (バイト)
  
### <a name="getblocksize-function"></a>GetBlockSize 関数
この ProtectionHandler で使用される暗号モードのブロック サイズ (バイト) を取得します。

  
**戻り値**: ブロック サイズ (バイト)
  
### <a name="getrights-function"></a>GetRights 関数
この ProtectionHandler に関連付けられているユーザー/ID に付与された権限を取得します。

  
**戻り値**: ユーザーに付与された権限
  
### <a name="accesscheck-function"></a>AccessCheck 関数
保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。

パラメーター:  
* **right**: 確認する権限



  
**戻り値**: 保護ハンドラーで、指定された権限へのアクセス権がユーザーに付与されるかどうか
  
### <a name="getissuedto-function"></a>GetIssuedTo 関数
保護ハンドラーに関連付けられているユーザーを取得します。

  
**戻り値**: 保護ハンドラーに関連付けられているユーザー
  
### <a name="getowner-function"></a>GetOwner 関数
コンテンツ所有者のメール アドレスを取得します。

  
**戻り値**: コンテンツ所有者のメール アドレス
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner 関数
現在のユーザーがコンテンツの所有者かどうかを取得します。

  
**戻り値**: 現在のユーザーがコンテンツの所有者かどうか
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護の詳細を取得します。

  
**戻り値**: 保護の詳細
  
### <a name="getcontentid-function"></a>GetContentId 関数
ドキュメント/コンテンツの一意識別子を取得します。

  
**戻り値**: 一意のコンテンツ識別子
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms 関数
保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。

  
**戻り値**: 保護ハンドラーで非推奨の暗号アルゴリズムを使用するかどうか
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed 関数
保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。

  
**戻り値**: 保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうか
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 関数
ProtectionHandler を発行ライセンス (PL) にシリアル化します

  
**戻り値**: シリアル化された発行ライセンス
  
### <a name="getserializedprelicense-function"></a>GetSerializedPreLicense 関数
ライセンスを取得します。

パラメーター:  
* **形式**: ライセンス前の形式



  
は、シリアル化されたライセンスの事前ライセンスを**取得**します。これにより、ユーザーは追加の HTTP 呼び出しを行うことなく、すぐにコンテンツを使用できます。 ProtectionHandler [::P ublishingsettings:: SetPreLicenseUserEmail](class_mip_protectionhandler_publishingsettings.md)値を使用して作成されている必要があります。そうしないと、空のベクターが返されます。
  
### <a name="prelicenseformat-enum"></a>PreLicenseFormat 列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
xml            | MSIPC で使用されるレガシ XML/SOAP 形式
Json            | MIP SDK および RMS SDK で使用される JSON/REST 形式
ライセンス前の形式。