---
title: Httpresponse.cache クラス
description: 'Microsoft Information Protection (MIP) SDK の httpresponse.cache:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 0a08b2bea4834375a01897b3d657772112463b89
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566874"
---
# <a name="class-httpresponse"></a>Httpresponse.cache クラス 
HttpDelegate をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  応答 ID を取得します。
public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
public const std:: vector \<uint8_t\>& getbody () const  |  要求本文を取得します。
public const std:: map \<std::string, std::string, CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
応答 ID を取得します。

  
**戻り値**: 対応する HTTPREQUEST の id が同じである応答 id
  
### <a name="getstatuscode-function"></a>GetStatusCode 関数
応答の状態コードを取得します。

  
**戻り値**: 状態コード
  
### <a name="getbody-function"></a>GetBody 関数
要求本文を取得します。

  
**戻り値**: 要求本文
  
### <a name="getheaders-function"></a>GetHeaders 関数
要求ヘッダーを取得します。

  
**戻り値**: 要求ヘッダー