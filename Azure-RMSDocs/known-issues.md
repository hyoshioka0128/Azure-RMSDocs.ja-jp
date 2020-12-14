---
title: 既知の問題 - Azure Information Protection
description: Azure Information Protection の既知の問題と制限を検索して参照します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/15/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ee493790e4997f8be11244490cf6014c17e6c6fd
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384232"
---
# <a name="known-issues---azure-information-protection"></a>既知の問題 - Azure Information Protection

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection の機能に関連する既知の問題と制限事項の詳細については、以下の一覧と表を参照してください。

## <a name="client-support-for-container-files-such-as-zip-files"></a>.Zip ファイルなど、コンテナーファイルのクライアントサポート

コンテナー ファイルは、その他のファイルが含まれるファイルです。典型的な例は、圧縮ファイルが含まれる .zip ファイルです。 その他の例には、.rar、.7z、.msg ファイルや、添付ファイルを含む PDF ドキュメントなどが含まれます。

これらのコンテナー ファイルを分類し、保護できますが、分類と保護はコンテナー内の各ファイルに適用されません。

分類され、保護されているファイルがコンテナー ファイル内にある場合、先にファイルを抽出し、分類または保護設定を変更する必要があります。 ただし、[Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを利用し、サポートされているコンテナー ファイル内の全ファイルの保護を削除できます。

Azure Information Protection ビューアーでは、保護された PDF ドキュメント内の添付ファイルを開くことはできません。 このシナリオでは、ビューアーでドキュメントを開いたときに、添付ファイルは表示されません。

詳細については、「 [管理者ガイド: Azure Information Protection クライアントでサポートされるファイルの種類](rms-client/client-admin-guide-file-types.md)」を参照してください。

## <a name="known-issues-for-aip-and-exploit-protection"></a>AIP と Exploit Protection の既知の問題

Azure Information Protection クライアントは、 [Exploit Protection](/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) が有効になっている、.net 2 または3がインストールされているコンピューターではサポートされていません。これにより、Office アプリがクラッシュします。

ご使用のシステムに必要な .NET 4.x バージョンに加えて .NET バージョン2または3がある場合は、AIP をインストールする前に、Exploit protection を無効にしてください。 

PowerShell を使用して Exploit protection を無効にするには、次のように実行します。

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントの追加の前提条件](rms-client/clientv2-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-unified-labeling-client)」を参照してください。

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの PowerShell のサポート

Azure Information Protection クライアントと共にインストールされる **Azureinformationprotection** PowerShell モジュールの現在のリリースには、次の既知の問題があります。

- **Outlook の個人用フォルダー (*.pst * ファイル) * *。 **Azureinformationprotection** モジュールを使用して、 *.pst* ファイルをネイティブに保護することはできません。

- **Outlook で保護された電子メールメッセージ *(. rpq msg* ファイル)**。 復号化 Outlook で保護された電子メールメッセージは、Outlook の個人用フォルダー *(.pst* ファイル) 内にある場合にのみ、 **azureinformationprotection** モジュールでサポートされます。

    復号化の電子メールメッセージは、 *.pst* ファイルの外部ではサポートされません。

詳細については、「 [管理者ガイド: Azure Information Protection クライアントでの PowerShell の使用](rms-client/client-admin-guide-powershell.md)」を参照してください。

## <a name="aip-known-issues-in-office-applications"></a>Office アプリケーションの AIP に関する既知の問題

|機能  |既知の問題  |
|---------|---------|
|**複数のバージョンの Office**    | Azure Information Protection クライアントでは、クラシックでも統合ラベル付けでも、同じコンピューター上で複数のバージョンの Office を使用したり、Office のユーザー アカウントを切り替えたりすることはサポートされていません。       |
|**複数のディスプレイ** |複数の表示を使用していて、Office アプリケーションを開いている場合は、次のようになります。 <br><br>-Office アプリでパフォーマンスの問題が発生する可能性があります。<br>-Azure Information Protection バーが、1つまたは両方の画面で、Office 画面の中央にフローティングするように見える場合があります。 <br><br>一貫したパフォーマンスを確保し、バーが正しい場所にあることを確認するには、Office アプリケーションの [**オプション**] ダイアログを開き、[**全般**] で、[**最適化**] ではなく [**互換性のために最適化**] を選択します。    |
|**Office 2016 での IRM のサポート**| Office 2016 でメタデータの暗号化を制御する [Drmencryptproperty](/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) レジストリ設定は、Azure Information Protection ラベルではサポートされていません。|
|**Word のコンテンツのマーキング**    | Microsoft Word のヘッダーまたはフッター内の AIP [コンテンツのマーキング](configure-policy-markings.md) は、オフセットされているか、正しく配置されていないか、同じヘッダーまたはフッターにテーブルが含まれていると、完全に隠れている可能性があります。<br><br>詳細については、「 [視覚的なマーキングが適用されるタイミング](configure-policy-markings.md#when-visual-markings-are-applied)」を参照してください。 |
|**電子メールに添付されたファイル** |Windows の最新の更新プログラムの制限により、 [Microsoft Outlook が Azure Rights Management によって保護](office-apps-services-support.md)されている場合、電子メールに添付されたファイルは、ファイルを開いた後にロックされる可能性があります。 |
|**差し込み印刷**    |  Office の[差し込み印刷](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705)機能は、どの Azure Information Protection 機能でもサポートされていません。       |
| **S/MIME メール** | Outlook の閲覧ウィンドウで S/MIME メールを開くと、パフォーマンスの問題が発生する可能性があります。 <br><br>S/MIME 電子メールのパフォーマンスの問題を回避するには、 [**OutlookSkipSmimeOnReadingPaneEnabled**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) advanced プロパティを有効にします。 <br><br>**注**: このプロパティを有効にすると、Outlook の閲覧ウィンドウに AIP バーまたは電子メール分類が表示されなくなります。 |
|**[ファイルエクスプローラーに送信] オプション** |エクスプローラーでファイルを右クリックして [ **> メール受信者に送信**] を選択した場合は、添付ファイルが添付されている Outlook メッセージに AIP ツールバーが表示されないことがあります。 <br><br>このエラーが発生し、AIP ツールバーオプションを使用する必要がある場合は、Outlook 内から電子メールを開始し、送信するファイルを参照して添付します。|
| | |

## <a name="known-issues-in-policies"></a>ポリシーに関する既知の問題

発行ポリシーには最大24時間かかることがあります。

## <a name="known-issues-in-the-aip-client"></a>AIP クライアントの既知の問題

- **ファイルの最大サイズ。** 2 GB を超える場合、保護はサポートされますが、暗号化解除はサポートされません。

- **AIP ビューアー。** AIP ビューアーでは画像が縦モードで表示され、ワイドビューの画像によっては拡大表示されることがあります。

    たとえば、元のイメージは左側に下に表示されます。右側の AIP ビューアーには、拡大した縦のバージョンが表示されます。 
    
    :::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="クライアントビューアーで拡大されるイメージ":::
    
    詳細については、次を参照してください。

    - [統一された **ラベル付けクライアント**: Azure Information Protection ビューアーで保護されたファイルを表示する](rms-client/clientv2-view-use-files.md)
    - [**従来のクライアント**: Azure Information Protection ビューアーで保護されたファイルを表示する](rms-client/client-view-use-files.md)


## <a name="aip-for-windows-and-office-versions-in-extended-support"></a>AIP for Windows および Office バージョンの拡張サポート

- [**Windows 7 の拡張サポートは、2020年1月14日に終了しまし**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)た。 

    Windows 10 の新しいバージョンにアップグレードすることを強くお勧めします。 ただし、強化されたセキュリティ更新プログラム (ESU) とサポート契約を締結している場合は、引き続き Windows 7 システムのセキュリティを維持するために AIP サポートを利用できます。

    詳細については、サポート担当者にお問い合わせください。

- [**Office 2010 は現在拡張サポートされ**](https://support.microsoft.com/lifecycle/search?alpha=office%202010)ています。 

    このサポートは、2020年10月13日に終了し、拡張されません。 また、ESU は Office 2010 向けに提供されないため、新しいバージョンの Office 365 にアップグレードすることを強くお勧めします。 
    
    拡張サポートで Office 2010 を現在実行しているお客様の場合、AIP サポートは2020年10月13日まで利用できます。 

    詳細については、サポート担当者にお問い合わせください。

## <a name="aip-based-conditional-access-policies"></a>AIP ベースの条件付きアクセスポリシー

[条件付きアクセスポリシー](/azure/active-directory/conditional-access/concept-conditional-access-policy-common)によって保護されたコンテンツを受信する外部ユーザーは、コンテンツを表示するために、Azure Active Directory (Azure AD) 企業間 (B2B) コラボレーションのゲストユーザーアカウントを持っている必要があります。

外部ユーザーを招待して、ゲストユーザーアカウントを認証し、条件付きアクセス要件を渡すことができますが、必要なすべての外部ユーザーに対してこの問題が発生していることを確認することは困難な場合があります。

内部ユーザーのみに対して AIP ベースの条件付きアクセスポリシーを有効にすることをお勧めします。

**AIP の条件付きアクセスポリシーを内部ユーザーのみに有効に** します。

1.  Azure portal で、[ **条件付きアクセス** ] ブレードに移動し、変更する条件付きアクセスポリシーを選択します。 
2.  [ **割り当て**] で [ **ユーザーとグループ**] を選択し、[ **すべてのユーザー**] を選択します。 [ **すべてのゲストと外部ユーザー** ] オプションが選択されて *いない* ことを確認します。
3.  変更内容を保存します。 
 
また、この潜在的な問題を回避するために、組織で機能が必要でない場合は Azure Information Protection 内で CA を完全に無効にすることもできます。 

詳細については、 [条件付きアクセスのドキュメント](/azure/active-directory/conditional-access/concept-conditional-access-users-groups)を参照してください。

## <a name="more-information"></a>説明

次の記事は、Azure Information Protection の既知の問題に関する質問に回答する際に役立つ場合があります。

- [Azure Information Protection に関してよく寄せられる質問](faqs.md)
- [Azure Information Protection のデータ保護に関してよく寄せられる質問](faqs-rms.md)
- [Azure Information Protection の分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)
- [iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](rms-client/mobile-app-faq.md)