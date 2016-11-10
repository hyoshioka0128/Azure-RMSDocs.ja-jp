---
title: "HYOK の制限事項 | Azure Information Protection"
description: Identify the limitations, prerequisites, and recommendations if you select AD RMS protection with Azure Information Protection. This solution is sometimes referred to as "hold your own key" (HYOK).
manager: mbaldwin
ms.date: 10/10/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
translationtype: Human Translation
ms.sourcegitcommit: 821f4c0bfbad4c88bea0fbe26807f8e50677069b
ms.openlocfilehash: 44a7dc786b678844e58f2a60204853d86c8750a7


---

# AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項

>*適用対象: Azure Information Protection*

**[ この機能はまだ暫定的で、情報は変更される可能性があります。 ]**

最も機密性の高いドキュメントや電子メールを保護する場合、通常、次のような利点がある Azure Rights Management 保護を適用します。

- サーバー インフラストラクチャが不要で、問題の解決が迅速になり、オンプレミス ソリューションよりもデプロイと保守のコスト効率が高くなる。

- クラウドベースの認証を使用して、他の組織のパートナーやユーザーと簡単に共有することができる。

- 検索、Web ビューアー、ピボット ビュー、マルウェア対策、電子情報開示、Delve などの、Office 365 サービスと密接に統合されている。

- 共有した機密ドキュメントの追跡、取り消し、電子メール通知機能を使用できる。

Azure RMS は、Microsoft または自社 ("Bring Your Own Key" (BYOK) シナリオ) が管理する組織の秘密キーを使用して組織のドキュメントと電子メールを保護します。 Azure RMS で保護されている情報はクラウドに送信されません。保護対象のドキュメントと電子メールは、Azure に保存するように明示的に指定した場合や、Azure に保存する別のクラウド サービスを使用している場合を除き、Azure には保存されません。 テナント キー オプションの詳細については、「[Azure Information Protection テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。 

一方、オンプレミスにホストされているキーを使用して、一部のドキュメントと電子メールを保護する場合があります。 たとえば、規制や準拠のために必要な場合があります。 

この構成は、"Hold Your Own Key" (HYOK) とも呼ばれ、有効な Active Directory Rights Management サービス (AD RMS) デプロイがある場合に Azure Information Protection でサポートされます。次のセクションでは、その要件について説明します。 この機能はまだプレビュー段階です。

この HYOK シナリオでは、権利ポリシーとそのポリシーを保護する組織の秘密キーの管理と保存はオンプレミスで行われますが、ラベル付けと分類の Azure Information Protection ポリシーの管理と保存は Azure で行われます。 Azure RMS の保護と同様に、AD RMS で保護する情報は、クラウドに送信されません。

> [!NOTE]
> この構成は、必要な場合にのみ、必要なドキュメントと電子メールにのみ使用します。 AD RMS の保護には、Azure RMS の保護の場合ほど多くの利点はありません。AD RMS の目的は、"是が非でもデータの不透明度を高くすること" です。

ラベルに AD RMS の保護を使用する場合、Azure RMS の保護よりも、ユーザーに認識されにくくなります。 AD RMS の保護には制限事項があるため、AD RMS の保護を適用するラベルをユーザーが選択する場合の明確な指針を示すようにしてください。

## HYOK を使用するときの制限事項

Azure RMS による保護を使うときの利点は得られないことに加えて、AD RMS による保護を Azure Information Protection とともに使う場合は次のような制限が課せられます。

- Office 2010 や Office 2007 はサポートされません。

- Azure RMS による保護も使用する場合: Azure RMS による保護のためのラベルを構成するときに**転送不可**オプションを使用しないでください。 ユーザーにも、このオプションを Outlook で手動選択しないよう指示する必要があります。 

    "転送不可" オプションがラベルによって、またはユーザーの手動設定によって適用されている場合に、このオプションを Azure Rights Management サービスによって適用するつもりであっても、AD RMS デプロイによって適用される可能性があります。 このシナリオでは、外部の共有相手は "転送不可" オプションが指定されたメール メッセージを開くことができなくなります。

## HYOK の要件

Azure Information Protection に AD RMS の保護を適用する場合、AD RMS のデプロイが次の要件を満たしていることを確認してください。

- AD RMS の構成:
    
    - Windows Server 2012 R2 の最小バージョン: 運用環境では必須ですが、テストまたは評価を目的とする場合は、Windows Server 2008 R2 Service Pack 1 の最小バージョンを使用できます。
    
    - 単一の AD RMS ルート クラスター。
    
    - [暗号化モード 2](https://technet.microsoft.com/library/hh867439.aspx): AD RMS クラスターの暗号化モードのバージョンと、その全体的な正常性を確認するには、[RMS アナライザー ツール](https://www.microsoft.com/en-us/download/details.aspx?id=46437)を使用します。   
    
    - 接続先のクライアントによって信頼されている有効な x.509 証明書で SSL/TLS を使用するように AD RMS サーバーが構成されている: 運用環境では必須ですが、テストまたは評価目的の場合は必須ではありません。
    
    - 構成済みの権利テンプレート。

- オンプレミス Active Directory と Azure Active Directory 間にディレクトリ同期が構成され、AD RMS の保護を使用するユーザーのシングル サインオンが構成されている。

- AD RMS で保護されているドキュメントまたは電子メールを組織以外の相手と共有する場合: AD RMS は、信頼されたユーザー ドメイン (TUD)、または Active Directory Federation Services (AD FS) を使用して作成されたまたはフェデレーションによる信頼を使用して、他の組織との直接的なポイント間の関係に明示的に定義した信頼向けに構成されている。

- ユーザーは、Windows 7 Service Pack 1 以降で実行されている Office 2013 Pro Plus Service 1 または Office 2016 Pro Plus のバージョンの Office を持っている (このシナリオでは、Office 2010 と Office 2007 は、サポートされません)。

> [!IMPORTANT]
> このシナリオが提供する高い確実性を実現するために、AD RMS サーバーは DMZ に配置せず、適切に管理されているコンピューター (たとえば、モバイル デバイスやワークグループ コンピューター以外のコンピューター) からのみ使用することをお勧めします。 
> 
> また、AD RMS クラスターでハードウェア セキュリティ モジュール (HSM) を使用することをお勧めします。これを使用すれば、AD RMS のデプロイが侵入または侵害されても、サーバー ライセンサー証明書 (SLC) の秘密キーが公開または盗難されることはありません。 

AD RMS のデプロイの情報と手順については、Windows Server ライブラリの「[Active Directory Rights Management Services の概要](https://technet.microsoft.com/library/hh831364.aspx)」を参照してください。 


## Azure Information Protection ラベルによる AD RMS の保護を指定する情報の確認

AD RMS の保護のラベルを構成する場合、AD RMS クラスターのテンプレート GUID とライセンス URL を指定する必要があります。 これらの情報は、いずれも Active Directory Rights Management サービス コンソールから確認することができます。

- テンプレート GUID を確認するには: クラスターを展開し、**[権利ポリシー テンプレート]** をクリックします。 **[配布権利ポリシー テンプレート]** の情報から、使用するテンプレートの GUID をコピーできます。 例: 82bf3474-6efe-4fa1-8827-d1bd93339119

- ライセンス URL を確認するには: クラスター名をクリックします。 **[クラスターの詳細]** の情報から、**[ライセンス]** 値の **/_wmcs/licensing** 文字列以外をコピーします。 例: https://rmscluster.contoso.com 
    
    エクストラネット ライセンス値とイントラネット ライセンス値があり、異なる値の場合: 明示的なポイント間の信頼で定義したパートナーとの間で、保護されたドキュメントを共有する場合にのみ、エクストラネット値を指定します。 それ以外の場合、イントラネット値を使用し、Azure Information Protection 接続で AD RMS の保護を使用するすべてのクライアント コンピューターが、イントラネット接続を使用して接続するようにします (たとえば、リモート コンピューターは VPN 接続を使用する)。

## 次のステップ

このプレビュー機能の詳細については、ブログ投稿のお知らせ「[Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/)」(HYOK (Hold Your Own Key) による Azure Information Protection) を参照してください。

AD RMS の保護のラベルを構成するには、「[Rights Management による保護を適用するためのラベルを構成する方法](../deploy-use/configure-policy-protection.md)」を参照してください。 



<!--HONumber=Oct16_HO2-->

