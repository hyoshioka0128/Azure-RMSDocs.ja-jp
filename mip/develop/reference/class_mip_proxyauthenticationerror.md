---
title: クラス ProxyAuthenticationError
description: 'Microsoft Information Protection (MIP) SDK の proxyauthenticationerror:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 04915e74cc09f271a2ca3bb256b906bc442bb3fd
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214305"
---
# <a name="class-proxyauthenticationerror"></a>クラス ProxyAuthenticationError 
プロキシ認証エラーです。
  
## <a name="summary"></a>まとめ
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

ネットワークエラーのカテゴリ。

 値                         | 説明                                
--------------------------------|---------------------------------------------
Unknown            | 不明なネットワークエラー
FailureResponseCode            | HTTP 応答コードがエラーを示す
BadResponse            | HTTP 応答を読み取れませんでした
UnexpectedResponse            | HTTP 応答が完了しましたが、予期しないデータが含まれました
NoConnection            | 接続を確立できませんでした。
プロキシ            | プロキシエラー
SSL            | SSL エラー
タイムアウト            | 接続がタイムアウトしました
オフライン            | 操作にはネットワーク接続が必要です
Throttled            | サーバートラフィックの調整により HTTP 操作に失敗しました
キャンセル            | HTTP 操作はアプリケーションによって取り消されました
