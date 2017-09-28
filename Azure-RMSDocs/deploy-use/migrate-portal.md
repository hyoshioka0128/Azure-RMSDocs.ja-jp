---
title: "Azure クラシック ポータルからの移行 - AIP"
description: "Azure クラシック ポータルで行っていた管理タスクの Azure Portal での操作に関する概要"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/19/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 8462a0c351ef8a75a7cd31bae923fd5ec3b8999f
ms.sourcegitcommit: f7ef0f040ae4af4bf1283ebcb0750b65b6939313
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2017
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Azure クラシック ポータルで行っていたタスク

>*適用対象: Azure Information Protection、Office 365*

Azure Rights Management サービスの管理には Azure クラシック ポータルが利用されていました。Azure Portal への移行でサポートが必要ですか? 

> [!NOTE]
> Azure クラシック ポータルは **2017 年 11 月 30 日**をもって使用停止となります。 詳細については、ブログ投稿でのお知らせ「[Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://blogs.technet.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/)」 (Azure AD 管理は未来に向かいます: Azure クラシック ポータルは使用停止に) を参照してください。

## <a name="how-to-do-your-familiar-admin-tasks"></a>使い慣れた管理タスクの実行方法

次の情報を利用して、新しいポータルに短時間で移行できます。

|Azure クラシック ポータル|このタスクを Azure Portal で実行する方法
|-----------|--------------------|
|構成設定に初めてアクセスする|1.テナントの全体管理者またはセキュリティ管理者として Azure Portal にサインインします。<br /><br />2.ハブ メニューで、**[新規]** をクリックし、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。<br /><br />3.**[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選びます。 次に、**[Azure Information Protection]** ブレードで **[作成]** をクリックします。<br /><br />**[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。
|新しいテンプレートを作成する|保護を適用するラベルを作成します。**[権限の設定]** を利用し、アクセス許可、有効期限、オフライン アクセスを定義します。 <br /><br />その処理の裏では、この構成により、Rights Management テンプレートと統合されるサービスとアプリケーションが次からアクセスできるようになる新しいカスタム テンプレートが作成されます。<br /><br />詳細については、「[新しいテンプレートを作成するには](configure-policy-templates.md#to-create-a-new-template)」を参照してください。
|テンプレートのプロパティを編集する: <br /><br />- テンプレート名と説明<br /><br />- 使用権限、コンテンツの有効期限、オフライン アクセス設定|まだ行っていない場合、[テンプレートをラベルに変換し](configure-policy-templates.md#to-convert-templates-to-labels)、次の作業を行ってください。<br /><br />1.ラベル名と説明を変更します。<br /><br />2.ラベルの保護設定を変更し、アクセス許可、有効期限、オフライン アクセス設定を更新します。<br /><br />詳しくは、「[Rights Management による保護にラベルを構成するには](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection)」を参照してください。
|テンプレートをアーカイブに収める|ラベル状態を **[無効]** に設定します。
|スコープ テンプレートを作成する|スコープ テンプレートを作成し、その範囲で保護を適用するラベルを作成します。 <br /><br />詳細については、「[スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法](configure-policy-scope.md)」を参照してください。
|テンプレートをコピーする|Azure Portal では、テンプレートをコピーできません。 2 つのラベルに同じ保護設定を与える場合、ラベルごとにアクセス許可を設定する必要があります。 <br /><br />詳しくは、「[Rights Management による保護にラベルを構成するには](configure-policy-protection.md#to-configure-a-label-for-rights-management-protection)」を参照してください。
|テンプレートを削除する|テンプレートを削除するとデータにアクセスできなくなることがあります。そのため、Azure Portal ではテンプレートを削除できないようになっています。 ただし、ラベルを削除し、PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) コマンドレットを実行すれば、テンプレートを削除できます。 <br /><br />詳細については、「[Azure Information Protection のラベルを削除または順序変更する方法](configure-policy-delete-reorder.md)」を参照してください。
|複数言語サポート|**[管理]** メニュー選択から、**[言語 (プレビュー)]** を選択すると、テンプレート名と説明が含まれるカスタマイズ可能なフィールドがエクスポートされます。 文字列を変換し、ポータルにインポートします。 <br /><br />詳細については、「[Azure Information Protection で他の言語のラベルとテンプレートを構成する方法](configure-policy-languages.md)」を参照してください。
|Rights Management Web レポート|PowerShell [Get-AadrmUsageLog](/powershell/module/aadrm/Get-AadrmUsageLog) コマンドレットを使用し、Azure Rights Management サービスの使用状況ログをダウンロードします。 そのデータを利用し、カスタマイズされたレポートを作成できます。 <br /><br />詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](log-analyze-usage.md)」を参照してください。<br /><br />ヒント: [Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)で、Azure Information Protection のための新しい集中レポート ソリューションの告知にご注目ください。 
|Rights Management サービスを有効/無効化する|**[管理]** メニュー オプションから、**[RMS の設定]** または **[Protection activation]\(保護のアクティブ化\)** を選択します。 このオプションの名前は、変更される予定です。<br /><br />詳細については、「[Azure Portal から Azure Rights Management をアクティブ化する方法](activate-azure.md)」を参照してください。

Azure Portal でテンプレートを編集したり、ラベルに変換したりする前に、「[Azure Portal のテンプレートに関する考慮事項](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal)」を参照してください。


## <a name="what-else-has-changed"></a>その他の変更点

Azure Portal の新機能:

- ユーザーが所属する組織のために[既定のテンプレート](configure-policy-templates.md#default-templates)が自動的に作成されますが、その既定のテンプレートを編集できます。

- テンプレートをラベルに変換できます。結果的に、テンプレートとラベルをそれぞれ管理するのではなく、1 つのオブジェクトを管理することになります。 方法については、「[テンプレートをラベルに変換するには](configure-policy-templates.md#to-convert-templates-to-labels)」を参照してください。

セキュリティ管理者ロールのサポート: Azure Rights Management を構成するためにグローバル管理者として Azure クラシック ポータルにサインインする必要がありましたが、Azure Information Protection を構成する目的で Azure Portal にサインインするときは、グローバル管理者ロールかセキュリティ管理者ロールが与えられたアカウントを利用できます。 

テンプレートの作成と管理、サービスの有効化と無効化のための PowerShell コマンドレットは、変更なく引き続きサポートされます。


## <a name="see-also"></a>関連項目
詳細については、「[Azure Information Protection ポリシーでテンプレートを構成して管理する](../deploy-use/configure-policy-templates.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]