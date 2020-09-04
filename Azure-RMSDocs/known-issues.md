---
title: 既知の問題-Azure Information Protection
description: Azure Information Protection の既知の問題と制限を検索して参照します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9a6d2ae357490b57b71b52e33ffef9827ecdceac
ms.sourcegitcommit: 9600ae255e7ccc8eeb49c50727a26e4666415fe2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2020
ms.locfileid: "89447040"
---
# <a name="known-issues---azure-information-protection"></a>既知の問題-Azure Information Protection

Azure Information Protection の機能に関連する既知の問題と制限事項の詳細については、以下の一覧と表を参照してください。

> [!NOTE]
> この記事では、クラシックと統合されたラベル付けクライアントの両方の既知の問題について説明します。 これらのクライアントの違いがわからない場合は、 [Faq](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)を参照してください。

## <a name="client-support-for-container-files-such-as-zip-files"></a>.Zip ファイルなど、コンテナーファイルのクライアントサポート

コンテナー ファイルは、その他のファイルが含まれるファイルです。典型的な例は、圧縮ファイルが含まれる .zip ファイルです。 その他の例には、.rar、.7z、.msg ファイルや、添付ファイルを含む PDF ドキュメントなどが含まれます。

これらのコンテナー ファイルを分類し、保護できますが、分類と保護はコンテナー内の各ファイルに適用されません。

分類され、保護されているファイルがコンテナー ファイル内にある場合、先にファイルを抽出し、分類または保護設定を変更する必要があります。 ただし、[Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを利用し、サポートされているコンテナー ファイル内の全ファイルの保護を削除できます。

Azure Information Protection ビューアーでは、保護された PDF ドキュメント内の添付ファイルを開くことはできません。 このシナリオでは、ビューアーでドキュメントを開いたときに、添付ファイルは表示されません。

詳細については、「 [管理者ガイド: Azure Information Protection クライアントでサポートされるファイルの種類](rms-client/client-admin-guide-file-types.md)」を参照してください。

## <a name="known-issues-for-installing-the-aip-client"></a>AIP クライアントのインストールに関する既知の問題

Azure Information Protection クライアントは、 [Exploit Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/enable-exploit-protection) が有効になっているコンピューターではサポートされていません。

AIP をインストールする前に、Exploit protection を無効にしてください。 

PowerShell を使用して Exploit protection を無効にするには、次のように実行します。

```PowerShell
Set-ProcessMitigation -Name "OUTLOOK.EXE" -Disable EnableExportAddressFilterPlus, EnableExportAddressFilter, EnableImportAddressFilter
```

詳細については、「 [Azure Information Protection の要件](requirements.md)」を参照してください。

## <a name="powershell-support-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの PowerShell のサポート

Azure Information Protection クライアントと共にインストールされる **Azureinformationprotection** PowerShell モジュールの現在のリリースには、次の既知の問題があります。

- **Outlook の個人用フォルダー (*.pst * ファイル) * *。 **Azureinformationprotection**モジュールを使用して、 *.pst*ファイルをネイティブに保護することはできません。

- **Outlook で保護された電子メールメッセージ *(. rpq msg* ファイル)**。 復号化 Outlook で保護された電子メールメッセージは、Outlook の個人用フォルダー *(.pst*ファイル) 内にある場合にのみ、 **azureinformationprotection**モジュールでサポートされます。

    復号化の電子メールメッセージは、 *.pst* ファイルの外部ではサポートされません。

詳細については、「 [管理者ガイド: Azure Information Protection クライアントでの PowerShell の使用](rms-client/client-admin-guide-powershell.md)」を参照してください。

## <a name="aip-known-issues-in-office-applications"></a>Office アプリケーションの AIP に関する既知の問題

|特徴量  |既知の問題  |
|---------|---------|
|**複数のバージョンの Office**    | Azure Information Protection クライアントは、従来のラベル付けと統一されたラベル付けの両方を含み、同じコンピューターで複数のバージョンの Office をサポートしたり、Office のユーザーアカウントを切り替えたりすることはできません。       |
|**複数のディスプレイ** |複数の表示を使用していて、Office アプリケーションを開いている場合は、次のようになります。 </br></br>-Office アプリでパフォーマンスの問題が発生する可能性があります。</br>-Azure Information Protection バーが、1つまたは両方の画面で、Office 画面の中央にフローティングするように見える場合があります。 </br></br>一貫したパフォーマンスを確保し、バーが正しい場所にあることを確認するには、Office アプリケーションの [ **オプション** ] ダイアログを開き、[全般] で **、** [最適化] ではなく [ **互換性のために最適化** ] を選択し **ます。**    |
|**Office 2016 での IRM のサポート**| Office 2016 でメタデータの暗号化を制御する [Drmencryptproperty](https://docs.microsoft.com/deployoffice/security/protect-sensitive-messages-and-documents-by-using-irm-in-office#office-2016-irm-registry-key-options) レジストリ設定は、Azure Information Protection ラベルではサポートされていません。|
|**Word のコンテンツのマーキング**    | フッターにテーブルが含まれている場合、Microsoft Word のフッターで Azure Information Protection コンテンツの [マーキング](configure-policy-markings.md) が非表示になることがあります。 詳細については、「 [視覚的なマーキングが適用されるタイミング](configure-policy-markings.md#when-visual-markings-are-applied)」を参照してください。 |
|**電子メールに添付されたファイル** |Windows の最新の更新プログラムの制限により、 [Microsoft Outlook が Azure Rights Management によって保護](office-apps-services-support.md)されている場合、電子メールに添付されたファイルは、ファイルを開いた後にロックされる可能性があります。 |
|**差し込み印刷**    |  Office [メールのマージ](https://support.office.com/article/use-mail-merge-for-bulk-email-letters-labels-and-envelopes-f488ed5b-b849-4c11-9cff-932c49474705) 機能は、Azure Information Protection 機能ではサポートされていません。       |
| **S/MIME メール** | Outlook の閲覧ウィンドウで S/MIME メールを開くと、パフォーマンスの問題が発生する可能性があります。 </br></br>S/MIME 電子メールのパフォーマンスの問題を回避するには、 [**OutlookSkipSmimeOnReadingPaneProperty**](rms-client/clientv2-admin-guide-customizations.md#prevent-outlook-performance-issues-with-smime-emails) advanced プロパティを有効にします。 </br></br>**注:** このプロパティを有効にすると、Outlook の閲覧ウィンドウに AIP バーまたは電子メール分類が表示されなくなります。 |
| | |

## <a name="known-issues-in-policies"></a>ポリシーに関する既知の問題

発行ポリシーには最大24時間かかることがあります。

## <a name="known-issues-in-the-aip-client"></a>AIP クライアントの既知の問題

- **ファイルの最大サイズ。** 2 GB を超えるファイルは保護がサポートされますが、暗号化解除はサポートされていません。

- **AIP ビューアー。** AIP ビューアーでは画像が縦モードで表示され、ワイドビューの画像によっては拡大表示されることがあります。

    たとえば、元のイメージは左側に下に表示されます。右側の AIP ビューアーには、拡大した縦のバージョンが表示されます。 
    
    :::image type="content" source="media/client-viewer-stretched-images.PNG" alt-text="クライアントビューアーで拡大されるイメージ":::
    
    詳細については、次を参照してください。

    - [**従来のクライアント**: Azure Information Protection ビューアーで保護されたファイルを表示する](rms-client/client-view-use-files.md)
    - [統一された**ラベル付けクライアント**: Azure Information Protection ビューアーで保護されたファイルを表示する](rms-client/clientv2-view-use-files.md)

## <a name="aip-for-windows-and-office-versions-in-extended-support"></a>AIP for Windows および Office バージョンの拡張サポート

- [**Windows 7 の拡張サポートは、2020年1月14日に終了しまし**](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)た。 

    Windows 10 の新しいバージョンにアップグレードすることを強くお勧めします。 ただし、強化されたセキュリティ更新プログラム (ESU) とサポート契約を締結している場合は、引き続き Windows 7 システムのセキュリティを維持するために AIP サポートを利用できます。

    詳細については、サポート担当者にお問い合わせください。

- [**Office 2010 は現在拡張サポートされ**](https://support.microsoft.com/lifecycle/search?alpha=office%202010)ています。 

    このサポートは、2020年10月13日に終了し、拡張されません。 また、ESU は Office 2010 向けに提供されないため、新しいバージョンの Office 365 にアップグレードすることを強くお勧めします。 
    
    拡張サポートで Office 2010 を現在実行しているお客様の場合、AIP サポートは2020年10月13日まで利用できます。 

    詳細については、サポート担当者にお問い合わせください。


## <a name="more-information"></a>詳細情報

次の記事は、Azure Information Protection の既知の問題に関する質問に回答する際に役立つ場合があります。

- [Azure Information Protection に関してよく寄せられる質問](faqs.md)
- [Azure Information Protection のデータ保護に関してよく寄せられる質問](faqs-rms.md)
- [Azure Information Protection の分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)
- [iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](rms-client/mobile-app-faq.md)

