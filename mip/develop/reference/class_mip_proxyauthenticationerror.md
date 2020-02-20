---
title: クラス mip::P roxyAuthenticationError
description: Microsoft Information Protection (MIP) SDK の mip::p roxyauthenticationerror クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c0289f9b2f2a8a1163e62e6c6a96e3023f297194
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489624"
---
# <a name="class-mipproxyauthenticationerror"></a>クラス mip::P roxyAuthenticationError 
プロキシ認証エラーです。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Category GetCategory () const  |  ネットワークエラーのカテゴリを取得します。
パブリック int32_t GetResponseStatusCode () const  |  HTTP 応答のステータスコードを取得します。
列挙型のカテゴリ  |  ネットワークエラーのカテゴリ。
  
## <a name="members"></a>メンバー
  
### <a name="getcategory-function"></a>GetCategory 関数
ネットワークエラーのカテゴリを取得します。

  
**戻り値**: ネットワークエラーのカテゴリ
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode 関数
HTTP 応答のステータスコードを取得します。

  
**戻り値**: HTTP 応答の状態コード、0の場合は0
  
### <a name="category-enum"></a>カテゴリの列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
不明            | 不明なネットワークエラー
FailureResponseCode            | HTTP 応答コードがエラーを示す
BadResponse            | HTTP 応答を読み取れませんでした
UnexpectedResponse            | HTTP 応答が完了しましたが、予期しないデータが含まれました
NoConnection            | 接続を確立できませんでした
Proxy            | プロキシエラー
SSL            | SSL エラー
タイムアウト            | 接続がタイムアウトしました
オフライン            | 操作にはネットワーク接続が必要です
Throttled            | サーバートラフィックの調整により HTTP 操作に失敗しました
取り消し済み            | HTTP 操作はアプリケーションによって取り消されました
ネットワークエラーのカテゴリ。