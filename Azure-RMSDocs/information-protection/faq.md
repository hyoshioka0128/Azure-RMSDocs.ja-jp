---
title: "Azure Information Protection プレビューに関してよく寄せられる質問 | Azure Information Protection"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/20/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e60cd910a8e995a2681d7eb87a13f815183d9124
ms.openlocfilehash: 846578a84df383821a64d32ce6dd69290a5fdee9


---

# Azure Information Protection プレビューに関してよく寄せられる質問

*適用対象: Azure Information Protection プレビュー*

Azure Information Protection のプレビュー リリースに関して質問がある場合は、  ここで回答を探してみてください。 

この一覧は、メイン ドキュメントに情報が移動されたり、お客様から寄せられる新しい質問が追加されたりして、頻繁に更新される予定です。 

## Azure Information Protection のプレビュー リリースでは何ができますか、また現在はどのような制限がありますか?

このプレビュー リリースでは、Information Protection バーが Microsoft Office アプリケーションに追加されました。このバーを使うと、データに割り当てられている分類ラベルを表示および変更できます。 分類は、手動、ユーザーへの推奨、または自動で適用されます。 指定する分類により、Azure Rights Management テンプレートを使用してデータを保護できます。  

分類のラベルと動作は、Azure ポータルで構成します。 既定の組み込みポリシーを使用して Azure Information Protection を非常に短時間で評価したり、独自のポリシーを完全にカスタマイズしたりできます。 ユーザーに表示される分類ラベルの色、名称、順序を変更できます。 ツール ヒントおよびヘッダー、フッター、透かしなどの分類のビジュアル マーキングを構成することもできます。

「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」に従えば、わずか数分でこの動作を確認できます。

プレビューでは新しい **Premium P2 サービス プラン**を試せること、および自動ラベル付けや推奨ラベル付けなどの一部の高度な機能は一般公開されている現在のリリースでは使用できない場合があることに注意してください。 各種サービス プラン (Azure Information Protection Premium P1 および Azure Information Protection Premium P2) については、「[Introducing Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/07/introducing-enterprise-mobility-security/)」 (Enterprise Mobility とセキュリティの概要) を参照してください。

このプレビュー リリースには次の制限があります。 追加機能が利用可能になる時期については、[Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)および [Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)での案内に注意してください。

- 分類とラベル付けには集中的なログはありません。

- ラベル名とツール ヒントは英語でのみサポートされます。

- 自動分類の条件は、語句またはパターンでなければなりません。

- Windows エクスプローラーからはファイルを分類できません。

- モバイル デバイス (iOS および Android) および Mac コンピューター用の Office アプリ、および Office Web アプリ (Office Online) は、まだサポートされていません。

- Exchange Online または SharePoint Online とは統合されません。

- パートナー向けおよび開発者向けの SDK はありません。

## Azure Information Protection を試すにはどのようなサブスクリプションが必要ですか?

プレビュー リリースでは、Azure Rights Management を含む任意のサブスクリプションを使用できます。 Azure Information Protection はすべてのリージョンで使用できます。 使用できるサブスクリプション オプションの詳細と無料試用版へのリンクについては、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)」を参照してください。

Azure ポータルで Azure Information Protection のポリシーを構成するには、Azure サブスクリプションが必要です。 組織の Azure サブスクリプションがまだない場合は、無料試用版にサインアップして取得できます。「[Microsoft Azure はじめに](https://account.windowsazure.com/organization)」ページにアクセスし、指示に従ってください。

サブスクリプションの要件が変更される場合は、[Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services)でお知らせします。

## Azure Information Protection が今パブリック プレビューだとしたら、Azure ポータルで見つからないのはなぜですか?

現在、ポータルで Azure Information Protection にアクセスするには、リンク https://portal.azure.com/?Microsoft_Azure_InformationProtection=true を使用する必要があります。

ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「Information Protection」と入力します。 結果から [**Azure Information Protection**] を選択します。

## Azure Information Protection プレビューを試すにはグローバル管理者である必要がありますか?

プレビュー リリースに限り、Azure によって認証されたすべてのユーザーがテナントの Azure Information Protection ポリシーを Azure ポータルで表示および構成できます。

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)をインストールするときにデモ ポリシーをインストールするオプションを選択した場合は、ポータルにサインインしなくてもプレビューを試すことができます。 デモ ポリシーでは Azure Information Protection 用の既定のポリシーがローカルにインストールされるので、ドキュメントと電子メールへのラベル付けを試用できますが、ラベルの変更または新規追加には Azure ポータルにサインインする必要があります。 

分類とラベル付けでドキュメントおよび電子メールを保護してみたくても、Azure Rights Management をまだアクティブ化していない場合、アクティブ化プロセスには特殊な管理者権限が必要です。 詳細については、「[Azure RMS を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?](../get-started/faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators)」を参照してください。


## Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

Azure Information Protection はクラウド ベースのソリューションです。 ハイブリッド シナリオに興味がある場合は、askipteam@microsoft.com 宛てに電子メールを送って Information Protection チームにお問い合わせください。

## Azure Information Protection はどのクライアント プラットフォームとアプリケーションをサポートしますか?

これに関するドキュメントは現在作成中であり、「[Azure Information Protection の要件](requirements-azure-infoprotect.md)」で更新される予定です。


## コンピューターはどのような方法および更新頻度で Azure Information Protection からポリシー情報を取得しますか?

ユーザーが Office アプリケーションを開くたびに、Azure Information Protection クライアントは Azure Information Protection ポリシーの新しいバージョンがあるかどうかを確認します。 新しいバージョンがある場合、クライアントは HTTPS リンクによりデータを保護してポリシーをダウンロードします。 

Azure Information Protection ポリシーが更新されるときにアプリケーションが既に読み込まれていた場合、最新バージョンのポリシーを取得するには、アプリケーションをいったん閉じて開き直す必要があります。

## Azure Information Protection を使用するにはファイルをどこに格納すればよいですか? 

Azure Information Protection はファイルと電子メールに永続的なラベルおよび保護を適用するので、ファイルの保存場所はどこでもかまいません。

## 分類できるのは新しいデータのみですか、既存のデータも分類できますか?

Azure Information Protection ポリシーのアクションは、ドキュメントの保存時および電子メールの送信時に、新規コンテンツおよび既存コンテンツへの変更の両方に対して反映されます。 

分類したいファイルを保存してある場合は、Office アプリケーションで開いて保存するだけです。 

現時点では、スキャンおよび分類の適用を一括して行うことはできず、Office アプリケーションで各ドキュメントを開いて保存する必要があります。 

## Azure Information Protection を分類のみに使用し、暗号化の適用と使用権限の制限が行われないようにすることはできますか?

はい。 ラベルの適用だけを行うように Azure Information Protection ポリシーを構成できます。 実際、このような使い方が、ドキュメントまたは電子メールのサブセットのみを保護する必要がある、特別なデータ管理を必要とするデプロイ ネットワークのほとんどのケースであると思われます。

## 自動分類はどのように行われますか?

Azure ポータルでは、"クレジット カード番号" や "米国社会保障番号" などの定義済みのパターンを使用できます。 または、自動分類の条件として、ユーザー指定の文字列またはパターンを定義することもできます。

この例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」を参照してください。 

分類の精度は、条件に基づく分類ルールの構成方法によって異なります。 現時点では、条件はテキスト パターンと正規表現をサポートしています。 プレビュー中に使用できる各オプションの説明と、テスト用に推奨されるいくつかの例については、Yammer の投稿「[Description of content matching for our pre-define Information types](https://www.yammer.com/askipteam/#/Threads/show?threadId=737163344)」 (定義済みの情報の種類に対するコンテンツの一致の例) を参照してください。 検出は、ドキュメントの保存時または電子メールの送信時に実行されます。

最適なユーザー エクスペリエンスおよびビジネス継続性の確保のためには、完全自動アクションではなく、ユーザー推奨アクションで始めることをお勧めします。 このようにすると、ユーザーは、ラベル付けまたは保護のアクションを受け入れることも、これらの推奨アクションをオーバーライドすることもできます。   

## Azure Information Protection では、自動分類を使用するのではなく、自分でファイルを分類するようにユーザーに要求できますか? 

はい。 Azure ポータルで自動分類または推奨のどちらを使うかを構成できます。**[Select how this label is applied: automatically or recommended to user]** (このラベルの適用方法を選択: 自動または推奨) オプションを **[Recommended]** (推奨) に設定すると、ユーザーに対して推奨が行われます。

この例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」を参照してください。

## 強制的にすべてのドキュメントを分類できますか?

はい。 ユーザーに保存するすべてのファイルを分類するよう要求するには、Azure ポータルで、**[All documents and emails must have a label]** (すべてのドキュメントとメールにラベルが必要) オプションを **[On]** (オン) に設定します。 

## ファイルから分類を削除できますか?

はい。 ファイルから分類を削除するには、Office アプリケーションでファイルを開き、Information Protection バーの **[ラベルの編集]** アイコンをクリックして、**[ラベルの削除]** アイコンの順にクリックし、**[OK]** をクリックしてアクションを確認します。 


## ユーザーに分類レベルを変更する理由の説明を求めることはできますか?

はい。 ユーザーに分類を変更する理由の説明を求めるには、Azure ポータルで **[Users must provide justification when lowering the sensitivity level]** (秘密度レベルを下げるときは妥当性を示す必要があります) オプションを **[On]** (オン) に設定します。 このように設定すると、ユーザーのアクションと理由が、ローカル Windows イベント ログの **[アプリケーション]**  >  **[Microsoft Azure Information Protection]** に記録されます。

## 分類された後のコンテンツを自動的に保護するにはどうすればよいですか?

Azure ポータルで Azure Rights Management テンプレートを選択することにより、指定した分類レベルに従ってコンテンツを自動的に保護できます。

この例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」を参照してください。

## 1 つのファイルを 2 つの異なる分類に分類できますか?

必要な場合は、サブラベルを作成して、特定の秘密度ラベルのサブカテゴリを適切に記述できます。 たとえば、主ラベル [**Secret**] (社内秘) に対して、[**Secret – Legal**] (社内秘 - 法務) や [**Secret – Finance**] (社内秘 -財務) などのサブラベルを作成できます。 その後、異なるサブラベルに対し、異なる分類ビジュアル マーキングと異なる Rights Management テンプレートを適用できます。

現在はビジュアル マーキング、保護、条件を両方のレベルで設定できますが、サブレベルを使用するときは、これらの設定をサブレベルのみで構成します。 親ラベルとそのサブレベルで同じ設定を構成した場合は、サブレベルの設定が優先されます。

## DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 ファイルでは、このメタデータはカスタム プロパティに格納されます。電子メールでは、この情報は電子メールのヘッダーに含まれます。

## Azure Information Protection では、ドキュメントの追跡と失効はどのように行われますか?

Azure Information Protection を使用して分類および保護されたファイルのドキュメントの追跡は、現在の Azure Rights Management の場合と同じように行われます。 詳細については、「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](../rms-client/sharing-app-track-revoke.md)」を参照してください。

## ユーザーが構成したポリシーを Azure Information Protection はどのように適用しますか?

ドキュメントが Azure Rights Management テンプレートを使用して保護されている場合、最初にユーザーがドキュメントに対する権限を持つことを認証された後、使用権利ポリシーがアプリケーションによって適用されます。 

## Azure Information Protection は Azure Active Directory をどのように使用しますか?

Azure Information Protection は Azure Active Directory をユーザー認証に使用します。

## Azure Information Protection を使用してコンテンツを分類および保護できるユーザーを制御できますか?

Azure Information Protection クライアントの配布を制御することで、データを分類および保護するユーザーを制限できます。 

Azure Information Protection によって分類されたファイルおよび電子メールは、Azure Information Protection クライアントのインストールの有無に関係なく、すべてのユーザーが使用または編集できます。 

## このプレビューの問題を報告またはフィードバックを送信するにはどうすればよいですか?

プレビュー リリースの使用中に問題が見つかった場合は、Office アプリケーションの **[ホーム]** タブの **[Protection]** (保護) グループで **[Protect]** (保護) をクリックし、**[Help and feedback]** (ヘルプとフィードバック) をクリックします。 **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[フィードバックの送信]** をクリックします。 これにより、Information Protection チームに電子メールが送信され、問題の診断に役立つ PC のログ ファイルが自動的に添付されます。 

質問やご意見がある場合は、[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)を使用してください。 

## 質問がここに含まれていない場合は、どうすればよいですか

最初に、Enterprise Mobility and Security ブログの [Azure Information Protection プレビューに関する発表](https://blogs.technet.microsoft.com/enterprisemobility/2016/07/12/azure-information-protection-public-preview-available-now/)に質問が含まれていないことを確認します。

次に、[Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)にアクセスして、他のユーザーが同じ質問を既にしているかどうかを確認します。 ない場合は、質問を投稿してください。







<!--HONumber=Jul16_HO3-->


