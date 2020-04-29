---
title: Httpresponse.cache クラス
description: 'Microsoft Information Protection (MIP) SDK の httpresponse.cache:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 6e37613adce0397ed543c4df793a59e74795fb26
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762465"
---
# <a name="class-httpresponse"></a>Httpresponse.cache クラス 
HttpDelegate をオーバーライドするときに、クライアント アプリによって実装される 1 つの HTTP 要求を表すインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  応答 ID を取得します。
public int32_t GetStatusCode() const  |  応答の状態コードを取得します。
public const std:: vector\<Uint8_t\>& getbody () const  |  要求本文を取得します。
public const std:: map\<std:: string、std:: String、CaseInsensitiveComparator\>& GetHeaders () const  |  要求ヘッダーを取得します。
  
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