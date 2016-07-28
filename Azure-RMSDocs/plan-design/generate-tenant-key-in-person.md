---
title: "テナント キーを生成して転送する - 持参 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: 8e77298121a84f6feb16a992da81bd9c3bb7b20b


---

# テナント キーを生成して転送する – 持参

*適用対象: Azure Rights Management、Office 365*


[独自のテナント キーを管理する](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok)ことを選択し、テナント キーをインターネット経由で転送するのではなく、持参する場合は、以下の手順を行います。

## テナント キーの生成
独自のテナント キーを生成するには、次の 3 つの手順を実行します。

-   [手順 1.Thales HSM を設定したワークステーションを準備する](#step-1-prepare-a-workstation-with-thales-hsm)

-   [手順 2:セキュリティ ワールドの作成](#step-2-create-a-security-world)

-   [手順 3:新しいキーの作成](#step-3-create-a-new-key)

### 手順 1.Thales HSM を設定したワークステーションを準備する
Windows コンピューターに nCipher (Thales) サポート ソフトウェアをインストールします。 そのコンピューターに Thales HSM をアタッチします。 Thales ツールがパス上にあるようにします。 詳細については、Thales HSM に付属のユーザー ガイドを参照するか、または Thales 社の Web サイトの Azure RMS に関するページ ( [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud)) にアクセスしてください。

### 手順 2:セキュリティ ワールドの作成
コマンド プロンプトを起動し、Thales 社が提供する new-world プログラムを実行します。

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
このプログラムによって、**セキュリティ ワールド** ファイルが %NFAST_KMDATA%\local\world に作成されます。この場所は、C:\ProgramData\nCipher\Key Management Data\local フォルダーに対応します。 クォーラムに別の値を使用することもできますが、この例では、空のカード 3 枚を挿入し、それぞれの暗証番号 (PIN) を入力するよう求められます。 この場合、任意の 2 枚のカードを使用すると、セキュリティ ワールドへのフル アクセスが可能になります。  これらのカードは、新しいセキュリティ ワールドの **管理者カード セット** になります。

その後、次の手順を実行します。

1.  Thales 社が提供するドキュメントの説明に従って Thales CNG プロバイダーをインストールし、新しいセキュリティ ワールドを使用するように構成します。

2.  セキュリティ ワールド ファイルをバックアップします。 セキュリティ ワールド ファイル、管理者カード、およびカードの暗証番号 (PIN) を安全に保管し、1 人の人物が複数のカードにアクセスできないようにしてください。

RMS テナント キーとなる新しいキーを作成する準備ができました。

### 手順 3:新しいキーの作成
Thales 社が提供する **generatekey** および **cngimport** プログラムを使用して、CNG キーを生成します。

キーを生成するには、次のコマンドを実行します。

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
このコマンドを実行する際は、次の指示に従ってください。

-   ここに示したように、パラメーター **protect** の値は **module** に設定する必要があります。 こうすることで、モジュールで保護されたキーが作成されます。 BYOK ツールセットは、OCS で保護されたキーをサポートしていません。

-   キーのサイズは 2048 を推奨しますが、1024 ビットの RSA キーを保有しており、Azure RMS に移行している既存の AD RMS ユーザーのために 1024 もサポートしています。

-   *ident* および **plainname** の値 **contosokey** は、任意の文字列値に置き換えてください。 管理オーバーヘッドを最小限に抑えて、エラーが発生するリスクを減らすため、ident および plainname の両方に小文字のみを使用した同じ値を指定することを推奨します。

-   pubexp は、この例では空白 (既定値) になっていますが、特定の値を指定することもできます。 詳細については、Thales 社が提供するドキュメントを参照してください。

その後、次のコマンドを実行して、キーを CNG にインポートします。

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
このコマンドを実行する際は、次の指示に従ってください。

-   *contosokey* を手順 1. で指定したのと同じ値に置き換えます。

-   キーがこのシナリオに適したものになるように、**-M** オプションを使用します。 指定しない場合、インポートされたキーは現在のユーザーに固有のキーになります。

このコマンドにより、トークン化されたキー ファイルが %NFAST_KMDATA%\local フォルダーに作成されます。キー ファイル名は **key_caping_`_`** で始まり SID が続きます。 たとえば、**key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb** となります。 このファイルには暗号化されたキーが含まれています。

このトークン化されたキー ファイルは、安全な場所にバックアップしてください。

> [!IMPORTANT]
> 後でキーを Azure RMS に転送する場合、Microsoft はこのキーの復元不可能なコピーを持つことになります。 つまり、Microsoft で HSM からキーを取得することは不可能です。 これにより、テナント キーの排他的制御を維持することができます。 したがって、キーとセキュリティ ワールドのバックアップを安全に行うことがきわめて重要になります。 キーのバックアップに関するガイダンスとベスト プラクティスについては、Thales 社に問い合わせてください。

これで、テナント キーを Azure RMS に転送する準備ができました。

## テナント キーの Azure RMS への転送
独自のキーを生成した後は、使用する前に Azure RMS に転送する必要があります。 最高レベルのセキュリティを保つため、この転送作業では米国ワシントン州レドモンドにある Microsoft のオフィスまで実際に移動していただく必要があります。 このプロセスを完了するには、次の 3 つの手順を実行します。

-   [手順 1.キーを Microsoft に持参する](#step-1-bring-your-key-to-microsoft)

-   [手順 2. キーを Azure RMS セキュリティ ワールドに転送する](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [手順 3:終了手続き](#step-3-closing-procedures)

### 手順 1.キーを Microsoft に持参する

-   Microsoft カスタマーサポート サービス (CSS) に連絡して Azure RMS 用のキーの転送を予約します。 次のものをレドモンドの Microsoft に持参します。

    -   定足数の管理者カード。 前の「[手順 2. セキュリティ ワールドの作成](#step-2-create-a-security-world)」の手順に従った場合、3 枚中任意の 2 枚になります。

    -   管理者カードと PIN を携行する担当者。通常は 2 人 (カードごとに 1 人) です。

    -   USB ドライブ上のセキュリティ ワールド ファイル (%NFAST_KMDATA%\local\world)。

    -   USB ドライブ上のトークン化されたキー ファイル。

### 手順 2. キーを Azure RMS セキュリティ ワールドに転送する

1.  転送するキーが Microsoft に到着してからの手順は次のとおりです。

    -   Microsoft がオフライン ワークステーションを提供します。このワークステーションには Thales HSM がアタッチされていて、Thales ソフトウェアがインストールされ、C:\Temp\Destination フォルダーに Azure RMS セキュリティ ワールドが事前に読み込まれています。

    -   このワークステーションで、持参した USB ドライブのセキュリティ ワールド ファイルとトークン化されたキー ファイルを C:\Temp\Source フォルダーに読み込みます。

    -   Azure RMS オペレーターが Thales ユーティリティを使用して Azure RMS セキュリティ ワールドにキーを安全に転送します。

    このプロセスは次のようになりますが、この例の key-xfer-im の最後のパラメーターは、トークン化されたキー ファイル名に置き換えられます。

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  Mk-reprogram では、お客様と Azure RMS オペレーターに対して、それぞれの管理者カードの挿入と PIN の入力が求められます。 これらのコマンドを実行すると、Azure RMS セキュリティ ワールドにより保護されたキーを含むトークン化されたキー ファイルが C:\Temp\Destination に出力されます。

### 手順 3:終了手続き

-   お客様の立ち会いの下、Azure RMS オペレーターが次のことを行います。

    -   Microsoft が Thales 社と共同で開発したツールを実行して、次の 2 つの権限を削除します:キーを復元する権限、および権限を変更する権限。 これを行うと、キーのコピーは Azure RMS セキュリティ ワールドにロックされます。 Azure RMS オペレーターが管理者カードを持っていても、Thales HSM ではキーのプレーンテキスト コピーを復元できなくなります。

    -   結果のキー ファイルを USB ドライブにコピーし、後で Azure RMS サービスにアップロードします。

    -   HSM を工場出荷時の設定に戻し、ワークステーションをワイプしてクリーンな状態にします。

これで、持参型 BYOK (Bring Your Own Key) に必要な手順が完了しました。次は、組織に戻り、テナント キーを計画および実装する手順に進みます。

> [!div class="button"]
[次の手順 >>](plan-implement-tenant-key.md#next-steps)






<!--HONumber=Jul16_HO3-->


