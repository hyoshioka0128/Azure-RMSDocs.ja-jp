---
title: RMS 共有アプリケーションを使用して実行するタスク - AIP
description: RMS 共有アプリケーションから Azure Information Protection クライアントにアップグレードしたユーザー向けの手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/29/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: d7bc2478-c22f-4e19-9992-012658362b25
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 796676d4fe4d612476b8ecda48b78acbe0a00120
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44148944"
---
# <a name="user-guide-tasks-that-you-used-to-do-with-the-rms-sharing-application"></a>ユーザー ガイド: RMS 共有アプリケーションを使用して実行するタスク

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

ここでは、最近、Rights Management 共有アプリケーション (単に "RMS 共有アプリ" ともいう) から Azure Information Protection クライアントにアップグレードした場合に役立つ情報を提供します。 

以下の情報を利用すれば、すばやく作業を開始することができます。

|RMS 共有アプリ|Azure Information Protection クライアントでの作業方法
|-----------|--------------------|
|デバイス上のファイルを保護する <br /><br />"インプレースで保護" ともいう|Office アプリの場合、必要な保護を適用するラベルを選択するか、カスタム アクセス許可を設定します。<br /><br />他のファイルの場合、エクスプローラーのメニュー オプション **[分類して保護する]** を使用して、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスを開きます。 次に、必要な保護を適用するラベルを選択するか、独自のカスタム アクセス許可を指定します。 <br /><br />詳細については、「[ファイルや電子メールを分類して保護する](client-classify-protect.md)」を参照してください。
|電子メールで共有するファイルを保護する <br /><br />"保護ファイルの共有" ともいう|Outlook を使用する場合は、電子メール メッセージに必要な保護を適用したラベルを適用するか、Outlook の **[転送不可]** オプションを選択します。 保護されていない添付ファイルでも[ファイルの種類がサポートされている](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)場合、その添付ファイルは自動的に保護されます。<br /><br />注: 電子メールで送信する保護されたドキュメントを追跡するには、まず、それを保護してから電子メール メッセージに添付します。<br /><br />詳細については、「[ファイルや電子メールを分類して保護する](client-classify-protect.md)」を参照してください。
|保護されたファイルに対するアクセス許可を変更する <br /><br />"再保護” ともいう|Azure Information Protection のバーを表示する Office アプリの場合: 必要な保護を適用するラベルを選択します。<br /><br />その他のファイルの場合、および Azure Information Protection クライアントが[保護のみモード](client-protection-only-mode.md)になっている場合: エクスプローラーのメニュー オプション **[分類して保護する]** を使用して、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスを開きます。 次に、必要な保護を適用するラベルを選択するか、独自のカスタム アクセス許可を指定します。<br /><br />詳細については、「[ファイルや電子メールを分類して保護する](client-classify-protect.md)」を参照してください。
|ドキュメントを追跡して取り消す|Word、Excel、PowerPoint からの場合: ドキュメントを開き、**[ホーム]** タブ、**[保護]** グループ、**[保護]** > **[追跡と取り消し]** の順に移動します。<br /><br />エクスプローラーから: ファイルまたはフォルダーを右クリックし、**[分類して保護する]** をクリックします。 次に、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[追跡と取り消し]** をクリックします。 <br /><br />詳細については、「[ドキュメントを追跡して取り消す](client-track-revoke.md)」を参照してください。
|保護されているファイルの表示と使用|保護されている Office ドキュメントの場合は、Office をインストールする必要があります。 Azure Information Protection ビューアーで、他の多くの保護されているファイルを開いて読み取ることができます。また、印刷と保存操作のアクセス許可がある場合は、保護されているファイルを印刷して保存することもできます。 このビューアーはクライアントと共に自動的にインストールされますが、個別にインストールすることもできます。<br /><br />詳細については、「[保護されているファイルを開く](client-view-use-files.md)」を参照してください。
|ファイルからの保護の削除|エクスプローラーのメニュー オプション **[分類して保護する]** を使用して、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスを開きます。 <br /><br />次に、1 つのファイルの場合は、**[Protect with custom permissions]** (カスタム アクセス許可で保護) オプションをオフにします。 複数のファイル、またはフォルダーの場合は、**[Remove custom permissions]** (カスタム アクセス許可の削除) をクリックします。<br /><br />詳細については、[ファイルや電子メールからのラベルと保護の削除](client-remove-label-protection.md)に関するページを参照してください。|

## <a name="cant-find-the-option-youre-looking-for"></a>お探しのオプションは見つかりましたか?

RMS 共有アプリケーションで選択していた特定のオプションをお探しの場合は、以下の表を確認してください。

|RMS 共有アプリのオプション|説明
|-----------|--------------------|
|**保護ファイルの共有**|このオプションは、Office リボンで使用できなくなりました。 Office アプリケーション内から直接共有する代わりに、エクスプローラーの右クリック オプション **[分類して保護する]** を使用して、カスタム アクセス許可でドキュメントのコピーを保護し、選択した電子メール クライアントを使用するか、共有場所を使用してファイルを共有します。 <br /><br /> 保護した電子メールに、保護されていない Office ドキュメントを添付することもでき、そのドキュメントは、同じ制限で自動的に保護されます。 ただし、このドキュメントを追跡したり、取り消したりすることはできません。
|**他のユーザーがこのドキュメントを開こうとしたら電子メールで通知する**|ドキュメント追跡サイトを使用して、優先する電子メール通知設定を構成します。その場合、共有した保護ドキュメントを見つけ、**[設定]** > **[メール通知]** の順に移動します。
|**これらのドキュメントへのアクセスをすぐに取り消せるようにする**|このオプションは利用できなくなりました。 オフライン アクセスを許可しない管理者定義の保護設定を使用します。 また、管理者は、[Set-AadrmMaxUseLicenseValidityTime](/powershell/aadrm/vlatest/set-aadrmmaxuselicensevaliditytime) を実行することで、テナントの使用ライセンスの有効期間を短縮できます。
|Outlook での**使用の追跡**|Outlook からドキュメント追跡サイトにアクセスする機能は使用できなくなりました。 代わりに、Word、PowerPoint、Excel、エクスプローラーから **[追跡と取り消し]** オプションを使用します。 または、ブラウザーを使用して[ドキュメント追跡サイト](https://go.microsoft.com/fwlink/?LinkId=529562)に直接移動できます。

## <a name="next-steps"></a>次の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [作業内容](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
「[Azure Information Protection クライアント管理者ガイド](client-admin-guide.md)」をご覧ください。

  
