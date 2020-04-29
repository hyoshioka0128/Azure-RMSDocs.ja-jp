---
title: 概念-MIP SDK の同意。
description: この記事では、MIP SDK が RMS サービスへの接続に同意するためにユーザーに同意フローを実装する方法を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 7025e042d0ded7164b26efbe9b453b4546c5ca05
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81766543"
---
# <a name="microsoft-information-protection-sdk---consent"></a>Microsoft Information Protection SDK-同意

`mip::Consent` 列挙型クラスは、アプリケーション開発者が、SDK によってアクセスされるエンドポイントに基づいてカスタムの同意エクスペリエンスを提供できる、使いやすいアプローチを実装します。 通知により、収集されるデータのユーザー、データを削除する方法、または法律またはコンプライアンス ポリシーで要求されるその他の情報を通知できます。 ユーザーが同意すると、アプリケーションが続行できます。 

### <a name="implementation"></a>実装

`mip::Consent` 基本クラスを拡張し、いずれかの `mip::Consent` 列挙値を返すように `GetUserConsent` を実装することで、同意が実装されます。 

`mip::Consent` から派生したオブジェクトが、`mip::FileProfile::Settings` または `mip::ProtectionProfile::Settings` コンストラクターに渡されます。

同意を与える必要のある操作をユーザーが実行すると、SDK が `GetUserConsent` メソッドを呼び出し、パラメーターとして宛先 URL を渡します。 このメソッドには、必要な情報をユーザーに表示する動作が実装されており、ユーザーはサービスの使用に同意するかどうかを決定できます。 

### <a name="consent-options"></a>同意オプション

- **AcceptAlways**: 同意し、決定事項を保存します。
- **Accept**: 一度同意します。
- **Reject**: 同意しません。

このメソッドを使用して SDK でユーザーの同意が求められる場合、クライアント アプリケーションではユーザーに URL を提示する必要があります。 クライアント アプリケーションでは、ユーザーの同意を取得するための手段を提供し、ユーザーの決定に対応する適切な Consent 列挙型を返す必要があります。

### <a name="sample-implementation"></a>実装例

#### <a name="consent_delegate_implh"></a>consent_delegate_impl.h

```cpp
class ConsentDelegateImpl final : public mip::ConsentDelegate {
public:
  ConsentDelegateImpl() = default;
  
  virtual mip::Consent GetUserConsent(const std::string& url) override;

};
```

#### <a name="consent_delegate_implcpp"></a>consent_delegate_impl.cpp

SDK が同意を必要とする場合、*SDK によって*`GetUserConsent` メソッドが呼び出され、パラメーターとして URL が渡されます。 次のサンプルでは、SDK がその指定された URL に接続し、コマンドラインのオプションをユーザーに提供することがユーザーに通知されます。 ユーザーが選択した内容に基づいて、ユーザーは同意を受け入れたり拒否したりして、SDK に渡されます。 ユーザーが同意を拒否すると、アプリケーションは例外をスローし、保護サービスへの呼び出しは行われません。 

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  //Print the consent URL, ask user to choose
  std::cout << "SDK will connect to: " << url << std::endl;

  std::cout << "1) Accept Always" << std::endl;
  std::cout << "2) Accept" << std::endl;
  std::cout << "3) Reject" << std::endl;
  std::cout << "Select an option: ";
  char input;
  std::cin >> input;

  switch (input)
  {
  case '1':
    return Consent::AcceptAlways;
    break;
  case '2':
    return Consent::Accept;
    break;
  case '3':
    return Consent::Reject;
    break;
  default:
    return Consent::Reject;
  }  
}
```

テストと開発を目的として`ConsentDelegate` 、次のような単純なを実装できます。

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

ただし、運用環境のコードでは、地域または業務上の要件や規制に応じて、ユーザーに同意するかどうかを選択するよう求められる場合があります。 