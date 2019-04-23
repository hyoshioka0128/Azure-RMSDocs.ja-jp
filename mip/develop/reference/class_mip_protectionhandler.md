---
title: class mip::ProtectionHandler
description: Mip::protectionhandler クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 20ac5207e744224d9d8eaef72607708721c55172
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60184469"
---
# <a name="class-mipprotectionhandler"></a>class mip::ProtectionHandler 
特定の保護構成のための保護に関連するアクションを管理します。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<Stream\> CreateProtectedStream (const std::shared_ptr\<Stream\>& backingStream、contentStartPosition の int64_t、int64_t contentSize)  |  コンテンツの暗号化/暗号化解除を可能にする、保護されたストリームを作成します。
public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化します。
public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化解除します。
public int64_t GetProtectedContentLength(int64_t unprotectedLength, bool includesFinalBlock)  |  この [ProtectionHandler](class_mip_protectionhandler.md) を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。
public int64_t GetBlockSize()  |  この [ProtectionHandler](class_mip_protectionhandler.md) で使用される暗号モードのブロック サイズ (バイト) を取得します。
public std::vector\<std::string\> GetRights() const  |  この [ProtectionHandler](class_mip_protectionhandler.md) に関連付けられているユーザー/ID に付与された権限を取得します。
public bool AccessCheck(const std::string& right) const  |  保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。
public const std::string GetIssuedTo()  |  保護ハンドラーに関連付けられているユーザーを取得します。
public const std::string GetOwner()  |  コンテンツ所有者のメール アドレスを取得します。
public bool IsIssuedToOwner()  |  現在のユーザーがコンテンツの所有者かどうかを取得します。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor()  |  保護の詳細を取得します。
public const std::string GetContentId()  |  ドキュメント/コンテンツの一意識別子を取得します。
public bool DoesUseDeprecatedAlgorithms()  |  保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。
public bool IsAuditedExtractAllowed()  |  保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。
public const std::vector\<uint8_t\> GetSerializedPublishingLicense()  |  [ProtectionHandler](class_mip_protectionhandler.md) を発行ライセンス (PL) にシリアル化します
public const std::vector\<uint8_t\> GetSerializedProtectionInfo()  |  保護情報を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="createprotectedstream-function"></a>CreateProtectedStream 関数
コンテンツの暗号化/暗号化解除を可能にする、保護されたストリームを作成します。

パラメーター:  
* **backingStream**:元の読み取り/書き込みストリームをバックアップします。 


* **contentStartPosition**:保護されたコンテンツの開始位置のバッキング ストリーム内の位置 (バイト) 単位の開始 


* **contentSize**:バッキング ストリーム内で保護されたコンテンツのバイト単位でサイズ



  
**返します**:保護されたストリーム
  
### <a name="encryptbuffer-function"></a>EncryptBuffer 関数
バッファーを暗号化します。

パラメーター:  
* **offsetFromStart**:InputBuffer クリア テキスト コンテンツの先頭からの相対位置 


* **inputBuffer**:暗号化するクリア テキスト コンテンツのバッファー 


* **inputBufferSize**:入力バッファーのバイト単位でサイズ 


* **outputBuffer**:暗号化されたコンテンツのコピー先バッファー 


* **outputBufferSize**:出力バッファーのバイト単位でサイズ 


* **最終**:入力バッファーかどうか、クリア テキストの最後のバイトが含まれる場合



  
**返します**:暗号化されたコンテンツの実際のサイズ (単位: バイト)
  
### <a name="decryptbuffer-function"></a>DecryptBuffer 関数
バッファーを暗号化解除します。

パラメーター:  
* **offsetFromStart**:InputBuffer 暗号化されたコンテンツの先頭からの相対位置 


* **inputBuffer**:暗号化が解除される暗号化されたコンテンツのバッファー 


* **inputBufferSize**:入力バッファーのバイト単位でサイズ 


* **outputBuffer**:復号化されたコンテンツのコピー先バッファー 


* **outputBufferSize**:出力バッファーのバイト単位でサイズ 


* **最終**:入力バッファーかどうかの最終的な暗号化されたバイト数を含まれている場合



  
**返します**:復号化されたコンテンツの実際のサイズ (単位: バイト)
  
### <a name="getprotectedcontentlength-function"></a>GetProtectedContentLength function
この [ProtectionHandler](class_mip_protectionhandler.md) を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。

パラメーター:  
* **unprotectedLength**:保護されていないコンテンツのバイト単位でサイズ 


* **includesFinalBlock**:問題のコンテンツ保護されていないにはか、最終ブロックが含まれている場合について説明します。 たとえば、CBC4k 暗号化モードでは、保護される非最終ブロックのサイズは保護されないブロックと同じですが、保護される最終ブロックは対応する保護されないブロックより大きくなります。



  
**返します**:保護されたコンテンツのバイト単位でサイズ
  
### <a name="getblocksize-function"></a>GetBlockSize 関数
この [ProtectionHandler](class_mip_protectionhandler.md) で使用される暗号モードのブロック サイズ (バイト) を取得します。

  
**返します**:ブロック サイズ (バイト単位)
  
### <a name="getrights-function"></a>GetRights 関数
この [ProtectionHandler](class_mip_protectionhandler.md) に関連付けられているユーザー/ID に付与された権限を取得します。

  
**返します**:ユーザーに付与された権限
  
### <a name="accesscheck-function"></a>AccessCheck 関数
保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。

パラメーター:  
* **適切な**:確認します。



  
**返します**:保護のハンドラーは、権利を指定したユーザーのアクセスを付与する場合
  
### <a name="getissuedto-function"></a>GetIssuedTo 関数
保護ハンドラーに関連付けられているユーザーを取得します。

  
**返します**:保護のハンドラーに関連付けられたユーザー
  
### <a name="getowner-function"></a>GetOwner 関数
コンテンツ所有者のメール アドレスを取得します。

  
**返します**:コンテンツ所有者のメール アドレス
  
### <a name="isissuedtoowner-function"></a>IsIssuedToOwner 関数
現在のユーザーがコンテンツの所有者かどうかを取得します。

  
**返します**:現在のユーザーがコンテンツの所有者か場合
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護の詳細を取得します。

  
**返します**:保護の詳細
  
### <a name="getcontentid-function"></a>GetContentId 関数
ドキュメント/コンテンツの一意識別子を取得します。

  
**返します**:一意のコンテンツ識別子
  
### <a name="doesusedeprecatedalgorithms-function"></a>DoesUseDeprecatedAlgorithms 関数
保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。

  
**返します**:保護のハンドラーで使用する場合か暗号アルゴリズムを推奨
  
### <a name="isauditedextractallowed-function"></a>IsAuditedExtractAllowed 関数
保護ハンドラーでユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。

  
**返します**:保護のハンドラーは、'監査済み抽出' 権限かをユーザーに付与する場合
  
### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 関数
[ProtectionHandler](class_mip_protectionhandler.md) を発行ライセンス (PL) にシリアル化します

  
**返します**:シリアル化された発行ライセンス
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo 関数
保護情報を取得します。

  
**返します**:シリアル化された保護情報