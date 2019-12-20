---
title: 概念 - MIP SDK での認証。
description: この記事は、MIP SDK によって認証を実装する方法、およびクライアント アプリケーションで OAuth2 アクセス トークンの取得ロジックを提供するための要件を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: 55bfba6da57fa07614165f4d5fcc5fba226cfca7
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886231"
---
# <a name="microsoft-information-protection-sdk---authentication-concepts"></a>Microsoft Information Protection SDK - 認証の概念

MIP SDK での認証は、クラス `mip::AuthDelegate` を拡張して目的の認証方法を実装することによって実行されます。 `mip::AuthDelegate` には次の項目が含まれています。

- `mip::AuthDelegate::OAuth2Challenge` - OAuth2 権限の情報を管理し、クライアント アプリケーションに提供するクラス。
- `mip::AuthDelegate::OAuth2Token` - (クライアント アプリケーションからの) OAuth2 アクセス トークンの取得、およびトークンの記憶域を管理するクラス。
- `mip::AuthDelegate::AcquireOAuth2Token()` - その実装によってアクセス トークンの取得方法を決定する、純粋仮想関数。 SDK によって呼び出された後、アクセス トークンを取得し、SDK の認証ロジックに提供します。

`mip::AuthDelegate::AcquireOAuth2Token` は、次のパラメーターを受け取り、トークンの取得に成功したかどうかを示すブール値を返します。

- `mip::Identity`: 認証されるユーザーまたはサービスの ID (既知の場合)。
- `mip::AuthDelegate::OAuth2Challenge`: 4 つのパラメーター、**権限**、**リソース**、**要求**、および**スコープ**を受け取ります。 **Authority** は、トークンが生成される対象のサービスです。 **Resource** は、アクセスしようとしている対象のサービスです。 SDK は、呼び出されたときにこれらのパラメーターをデリゲートに渡す処理を行います。 **要求**は、保護サービスに必要なラベル固有の要求です。 **スコープ**は、リソースにアクセスするために必要な Azure AD のアクセス許可スコープです。 
- `mip::AuthDelegate::OAuth2Token`: トークンの結果はこのオブジェクトに書き込まれます。 エンジンが読み込まれるときに SDK によって使用されます。 認証実装の外部では、いずれの場所でもこの値を取得または設定する必要はありません。

**重要:** アプリケーションは `AcquireOAuth2Token` を直接呼び出しません。 必要に応じて SDK がこの関数を呼び出します。

## <a name="consent"></a>同意

Azure AD では、アプリケーションが、セキュリティで保護されたリソース/API にアカウントの ID でアクセスする権限を付与される前に、同意を取得する必要があります。 同意は、特定のアカウント (ユーザーの同意) またはすべてのアカウント (管理者の同意) について、アカウントのテナントでのアクセス許可の永続的な確認として記録されます。 アクセスされる API、アプリケーションが求めるアクセス許可、およびサインインに使用されるアカウントに基づいて、次のさまざまなシナリオで同意が行われます。 

- お客様または管理者が、[アクセス許可の付与] 機能を使用して事前にアクセスに明示的に同意しなかった場合、アプリケーションが登録されている*同じテナント*のアカウント。
- アプリケーションがマルチテナントとして登録されており、テナント管理者が事前にすべてのユーザーに対して同意していない場合、*別のテナント*のアカウント。

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

SDK が同意を必要とする場合、*SDK によって* `GetUserConsent` メソッドが呼び出され、パラメーターとして URL が渡されます。 次のサンプルでは、SDK がその指定された URL に接続し、コマンドラインのオプションをユーザーに提供することがユーザーに通知されます。 ユーザーが選択した内容に基づいて、ユーザーは同意を受け入れたり拒否したりして、SDK に渡されます。 ユーザーが同意を拒否すると、アプリケーションは例外をスローし、保護サービスへの呼び出しは行われません。 

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

テストと開発を目的として、次のような単純な `ConsentDelegate` を実装できます。

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  return Consent::AcceptAlways;
}
```

ただし、運用環境のコードでは、地域または業務上の要件や規制に応じて、ユーザーに同意するかどうかを選択するよう求められる場合があります。 

## <a name="next-steps"></a>次のステップ

わかりやすくするため、デリゲートを示すサンプルで、外部のスクリプトを呼び出すことによってトークンの取得を実装します。 このスクリプトは、他の任意の種類のスクリプト、オープン ソースの OAuth2 ライブラリ、またはカスタムの OAuth2 ライブラリに置き換えられます。

- [PowerShell を使用してアクセス トークンを取得する](concept-authentication-acquire-token-ps.md)
- [Python を使用してアクセス トークンを取得する](concept-authentication-acquire-token-py.md)
