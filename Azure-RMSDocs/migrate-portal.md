---
title: Azure クラシック ポータルからの移行 - AIP
description: Azure クラシック ポータルで行っていた管理タスクの Azure Portal での操作に関する概要
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5018e69cf1798592d07b053eaeaccef234f71561
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559876"
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Azure クラシック ポータルで行っていたタスク

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Rights Management サービスの管理には Azure クラシック ポータルが利用されていました。Azure Portal への移行でサポートが必要ですか?

Azure クラシック ポータルは、**2018 年 1 月 8 日**をもって廃止されました。 この日付以降は、クラシック ポータルから Azure Rights Management サービスとカスタム テンプレートを管理することができません。 クラシック ポータルにアクセスしようとすると、新しい Azure Portal に移動するためのリンクが表示されます。

クラシック ポータルの廃止については、ブログ投稿でのお知らせ「[Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/)」 (Azure AD 管理は未来に向かいます: Azure クラシック ポータルは使用停止に) を参照してください。 元々の廃止日の一時的な延長については、「[Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/)」 (Azure AD クラシック ポータル エクスペリエンスの廃止と条件付きアクセス ポリシーの移行に関する更新) を参照してください。

## <a name="how-to-do-your-familiar-admin-tasks"></a>使い慣れた管理タスクの実行方法

次の情報を利用して、最新のポータルに短時間で移行できます。

|Azure クラシック ポータル|このタスクを Azure Portal で実行する方法
|-----------|--------------------|
|構成設定に初めてアクセスする|1. [Azure portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。<br /><br />2. [ [Azure Information Protection] ウィンドウに初めてアクセスするに](configure-policy.md#to-access-the-azure-information-protection-pane-for-the-first-time)は、の指示に従います。
|新しいテンプレートを作成する|保護を適用するラベルを作成します。 **[権限の設定]** を利用し、アクセス許可、有効期限、オフライン アクセスを定義します。 <br /><br />その処理の裏では、この構成により、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいカスタム テンプレートが作成されます。<br /><br />詳細については、「[新しいテンプレートを作成するには](configure-policy-templates.md#to-create-a-new-template)」を参照してください。
|テンプレートのプロパティを編集する: <br /><br />- テンプレート名と説明<br /><br />- 使用権限、コンテンツの有効期限、オフライン アクセス設定|まだ行っていない場合、[テンプレートをラベルに変換し](configure-policy-templates.md#to-convert-templates-to-labels)、次の作業を行ってください。<br /><br />1. ラベルの名前と説明を変更します。<br /><br />2. ラベルの保護設定を変更して、アクセス許可、有効期限、およびオフラインアクセスの設定を更新します。<br /><br />詳しくは、[ラベルの保護設定の構成](configure-policy-protection.md#to-configure-a-label-for-protection-settings)に関するページをご覧ください。
|テンプレートをアーカイブに収める|ラベル状態を **[無効]** に設定します。
|スコープ テンプレートを作成する|スコープ テンプレートを作成し、その範囲で保護を適用するラベルを作成します。 <br /><br />詳細については、「[スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法](configure-policy-scope.md)」を参照してください。
|テンプレートをコピーする|Azure Portal では、テンプレートをコピーできません。 2 つのラベルに同じ保護設定を与える場合、ラベルごとにアクセス許可を設定する必要があります。 <br /><br />詳しくは、[ラベルの保護設定の構成](configure-policy-protection.md#to-configure-a-label-for-protection-settings)に関するページをご覧ください。
|テンプレートを削除する|テンプレートを削除するとデータにアクセスできなくなることがあります。そのため、Azure Portal ではテンプレートを削除できないようになっています。 ただし、ラベルを削除してから、PowerShell の[remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)コマンドレットを使用してテンプレートを削除することができます。 <br /><br />詳細については、「[Azure Information Protection のラベルを削除または順序変更する方法](configure-policy-delete-reorder.md)」を参照してください。
|複数言語サポート|**[管理]** メニュー選択から、 **[言語]** を選択すると、テンプレート名と説明が含まれるカスタマイズ可能なフィールドがエクスポートされます。 文字列を変換し、ポータルにインポートします。 <br /><br />詳細については、「[Azure Information Protection で他の言語のラベルとテンプレートを構成する方法](configure-policy-languages.md)」を参照してください。
|Rights Management Web レポート|[Azure Information Protection の中央レポート機能](reports-aip.md)は現在プレビュー段階です。<br /><br />また、PowerShell の[get-help](/powershell/module/aipservice/get-aipserviceuserlog)コマンドレットを使用して、Azure Rights Management サービスの使用状況ログをダウンロードすることもできます。 そのデータを利用し、カスタマイズされたレポートを作成できます。 詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](log-analyze-usage.md)」を参照してください。
|Rights Management サービスを有効/無効化する|**[管理]** メニュー オプションで、 **[保護のアクティブ化]** を選択します。<br /><br />詳細については、「 [Azure portal から Rights Management 保護サービスをアクティブ化する方法](activate-azure.md)」を参照してください。

Azure Portal でテンプレートを編集したり、ラベルに変換したりする前に、「[Azure Portal のテンプレートに関する考慮事項](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal)」を参照してください。


## <a name="what-else-has-changed"></a>その他の変更点

Azure Portal の新機能:

- ユーザーが所属する組織のために[既定のテンプレート](configure-policy-templates.md#default-templates)が自動的に作成されますが、その既定のテンプレートを編集できます。

- テンプレートをラベルに変換できます。結果的に、テンプレートとラベルをそれぞれ管理するのではなく、1 つのオブジェクトを管理することになります。 方法については、「[テンプレートをラベルに変換するには](configure-policy-templates.md#to-convert-templates-to-labels)」を参照してください。

- 他の管理者ロールのサポート: azure Rights Management を構成するには、グローバル管理者として Azure クラシックポータルにサインインする必要がありましたが、他の多くの管理者ロールを使用して Azure Information Protection を管理するために Azure portal にサインインできます。これには、**コンプライアンス管理者**と**コンプライアンスデータ管理者**が含まれます。 サポートされているロールの完全な一覧については、「 [Azure portal へのサインイン](configure-policy.md#signing-in-to-the-azure-portal)」セクションを参照してください。

テンプレートの作成と管理、サービスの有効化と無効化のための PowerShell コマンドレットは、変更なく引き続きサポートされます。

## <a name="see-also"></a>「
詳細については、「[Azure Information Protection ポリシーでテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

