---
title: 'クラス mip:: FileInspector'
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileinspector クラスに関するドキュメントを示します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8ae396cc529cbeb17afa8ad0c4617e4bfcfbed3a
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558817"
---
# <a name="class-mipfileinspector"></a>クラス mip:: FileInspector 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public InspectorType GetInspectorType () const  |  ファイルの種類を取得します。
public std:: shared_ptr\<Stream\> GetFileStream () const  |  ファイルストリームを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getinspectortype-function"></a>GetInspectorType 関数
ファイルの種類を取得します。

  
は、InspectorType**を返し**ます。
  
### <a name="getfilestream-function"></a>GetFileStream 関数
ファイルストリームを取得します。

  
は、ファイルストリームへの共有 ptr を**返し**ます。