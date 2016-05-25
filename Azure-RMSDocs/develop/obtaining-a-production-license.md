---
# required metadata

title: 運用環境ライセンスの取得 | Azure RMS
description: RMS SDK 2.1 を使用して開発されたアプリケーションを解放するには、運用環境の使用許諾契約書が必要です。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6749817E-FF34-4384-BF63-39AEA5C372CA
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 運用環境ライセンスの取得

Rights Management サービス SDK 2.1 を使用して開発されたアプリケーションを解放するには、運用環境の使用許諾契約を申請して、運用証明書を取得する必要があります。

> [!IMPORTANT]
> Azure ベースの RMS でクライアント アプリケーションを実行する場合は、Azure RMS テナントを要求する必要があります。 <rmcstbeta@microsoft.com> にテナントを要求する電子メールを送信してください。

Azure RMS での実行に関する詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。


運用証明書と運用前証明書では同様の機能が実行されますが、異なる環境での使用が想定されています。 これらの証明書にはいずれも、信頼のルートに Microsoft の証明機関 (CA) 証明書による証明書チェーンが含まれていますが、運用前証明書は RMS アプリケーションを開発する場合にのみ使用されます。 運用証明書はリリース後の環境で使用されます。 運用証明書および関連付けられている秘密キーは、アプリケーションのプロセス空間に読み込むことができるか、読み込む必要があるファイル、および読み込んではならないファイルを識別するマニフェストの作成と署名に使用されます。

キーに関する詳細については、「[権限保護対応アプリケーションのテスト](running-your-first-application.md)」を参照してください。

運用環境の使用許諾契約書に申請することで、証明書を取得できます。

## 運用環境の使用許諾契約書の要求

-   [RMLA@microsoft.com](mailto:rmla@microsoft.com) に電子メール メッセージを送信 し、次の情報を含めます。

    -   会社の正式名称

    -   会社の住所 (市区町村、都道府県、国またはリージョン、および 郵便番号を含む)
    -   会社の宛先 (市区町村、都道府県、国またはリージョン、および 郵便番号を含む)
    -   会社の電話番号、FAX 番号
    -   会社の URL
    -   法人の国またはリージョン
    -   アプリケーションまたは製品名
    -   要求者の氏名
    -   要求者の役職または職位
    -   要求者の電子メール アドレス

    電子メール アカウントは必須ではありませんが、アプリケーション プロセスの通信は通常、電子メールで行われます。 Microsoft Outlook.com で無料の電子メール アカウントを取得できます。 アカウントがなく、アカウントを必要としていない場合、次のアドレスにタイプ入力した申請書を送信できます。

    `Active Directory Rights Management License Agreements (ADRMLA)`

    `Microsoft Corporation`

    `One Microsoft Way`

    `Redmond, WA 98052-6399`

    契約書を要求するときに、次を実行してください。

    -   契約書に表示されるため、情報は英語で入力してください。
    -   要求されるすべての情報を送信してください。 情報が不足しているか不完全な場合、要求の処理が遅れることがあります。

    Active Directory Rights Management ライセンス契約 (ADRMLA) チームは、電子メールによる要求には 3 営業日以内に応答します。郵送で要求を送信した場合、応答にかかる期間はそれより長くなります。 応答には、使用許諾契約書用紙と詳細な手順が含まれます。 契約書のすべてのページを読み、署名してから ADRMLA チームに返送してください。 使用許諾契約書のフォントを変更したり、段落の書式を変更したりしないでください。

    ADRMLA チームから受信した手順に従ってください。 この手順では、証明書要求を満たすために必要なデジタル情報の項目が一覧表示されます。 この手順に従うことにより、遅延を減らすことができます。

    運用証明書が作成されると、ADRMLA チームによってユーザーに転送されます。 運用証明書は、使用許諾契約書とユーザーが入力したデジタル情報 (公開キーを含む) に基づいて作成されます。 証明書への ADRMLA チームの応答は、電子メールの場合は最大で 15 営業日、郵送の場合はそれより長くかかる場合があることに注意してください。

## 関連項目

* [使用方法](how-to-use-msipc.md)
* [権限保護対応アプリケーションのテスト](running-your-first-application.md)
 

 





<!--HONumber=Apr16_HO4-->


