---
title: 'クラス mip:: HttpOperation'
description: 'Microsoft Information Protection (MIP) SDK の mip:: httpoperation クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d0f72a60233b05eab2c9e4b9e9cec2bf8bcda495
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056029"
---
# <a name="class-miphttpoperation"></a>クラス mip:: HttpOperation 
[Httpdelegate](class_mip_httpdelegate.md)をオーバーライドするときにクライアントアプリによって実装される、単一の HTTP 操作を記述するインターフェイス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetId() const  |  操作 ID を取得します。
public std:: shared_ptr\<httpresponse.cache\> GetResponse ()  |  応答を取得します (存在する場合)。
public bool IsCancelled ()  |  操作のキャンセルステータスを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getid-function"></a>GetId 関数
操作 ID を取得します。

  
次の**値を返し**ます。操作 ID 対応する HttpRequest と Httpresponse.cache の ID は同じになります
  
### <a name="getresponse-function"></a>GetResponse 関数
応答を取得します (存在する場合)。

  
次の**値を返し**ます。応答
  
### <a name="iscancelled-function"></a>IsCancelled 関数
操作のキャンセルステータスを取得します。

  
次の**値を返し**ます。キャンセルの状態