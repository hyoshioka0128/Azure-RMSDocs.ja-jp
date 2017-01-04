---
title: "Azure Information Protection を使用してファイルや電子メールを分類して保護する | Azure Information Protection"
description: "ドキュメントや電子メールを分類して保護する方法の手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e6d4cc50259b9d9bb73a75c648f9e6915562accf
ms.openlocfilehash: e1d61fbe1d74a4a57d9a1fdf518aeb0242d0f7ad


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Azure Information Protection を使用してファイルや電子メールを分類して保護する

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

**[このバージョンのクライアントはプレビュー段階にあり、変更される可能性があります。]**

Office のデスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) でドキュメントや電子メールを作成したり編集すると、分類と保護が簡単になります。 

ただし、**エクスプローラー**を使用してファイルの分類と保護を行うこともできます。エクスプローラーは、その他のファイルの種類をサポートし、複数のファイルを一度に分類して保護するための便利な方法です。

## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類して保護する

Azure Information Protection バーを使用して、構成されているラベルを 1 つ選択します。 たとえば、

![Azure Information Protection バーの例](../media/info-protect-bar-not-set-callout.png)


## <a name="using-file-explorer-to-classify-and-protect-files"></a>エクスプローラーを使用してファイルを分類および保護する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類して保護することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類および保護のオプションで自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、設定されたオプションで自動的に構成されません。

ファイルの分類と保護にエクスプローラーを使用すると、ラベルが常に使用できるわけではないことに気付くことがあります。 これは、選択したファイルが分類をサポートしていない場合に起こります。 このようなファイルについては、管理者によってラベルが保護を適用するように構成された場合にのみ、ラベルを選択できます。 または、独自の保護設定を指定することができます。 

エクスプローラーでサポートされているファイルの種類の一覧は、このページの「[分類と保護がサポートされているファイルの種類](#file-types-supported-for-classification-and-protection)」を参照してください。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類および保護するには

1.  エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[Classify and protect (プレビュー)]**(分類と保護 (プレビュー)) を選択します。 

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類と保護を設定します。 ラベルが (使用できず) 選択できない場合は、選択されたファイルで分類はサポートされませんが、ファイルを保護することはできます。

3. ファイルを保護するには、管理者の定義した保護設定の中から選択したラベルに使用する設定 (**選択された分類レベルに基づく自動設定**) を選択するか、または独自の設定 (**カスタムのアクセス許可による上書き**) を指定します。
    
    上書きオプションでは、選択したラベルには管理者が定義したいずれの保護設定も使用されず、 代わりに独自の保護設定を指定します。 

4. 上書きオプションを選択した場合は、次の項目を指定します。

    - **アクセス許可の選択**: 選択したファイルを保護する場合のユーザーのアクセス レベルを選択します。
    
    - **ユーザーの選択**: ファイルに対して選択したアクセス許可を持つユーザーを指定します。 組織内のユーザーやグループについては、アドレス帳を使用して検索と選択ができます。 別の組織のユーザーについては、完全なメール アドレスを指定する必要があります。 個人用のメールアドレスは現在サポートされていないため、仕事用のメール アドレスを使用してください。
        
    - **アクセスの有効期限**: ファイルの期間が限定されていて、指定された日付を過ぎた後は指定されたユーザーがファイルを開けないようにする場合にのみ、このオプションを選択します。 自分は元のファイルを引き続き開くことができますが、(使用中のタイム ゾーンで) 選択した日付の深夜を過ぎた後は、他のユーザーはファイルを開くことができなくなります。

5. **[適用]**、**[閉じる]** の順にクリックします。

選択されたファイルは、指定した設定に従って分類および保護されます。 場合によっては (保護の追加によってファイル名の拡張子が変更される場合)、エクスプローラーの元のファイルが Azure Information Protection のロック アイコンの付いた新しいファイルに置き換えられます。 たとえば、

![Azure Information Protection のロック アイコンが付いた保護されたファイル](../media/Pfile.png)

分類と保護について考えが変わったり、後で設定を変更する必要がある場合は、新しい設定でこのプロセスを繰り返すだけです。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類と保護はファイルに設定されたままです。 ファイルを保護した場合は、ユーザーによる保護されたファイルの使用状況を追跡し、必要に応じてファイルへのアクセスを取り消すことができます。 詳細については、「[Azure Information Protection を使用して保護されたドキュメントを追跡および取り消す](client-track-revoke.md)」を参照してください。 

#### <a name="file-types-supported-for-classification-and-protection"></a>分類と保護がサポートされているファイルの種類

次のファイルの種類では分類のみがサポートされています。 ほかのファイルの種類では、保護されている場合に分類がサポートされます。

- **Microsoft Visio**: .vsdx、.vsdm、.vssx、.vssm、.vsd、.vdw、.vst

- **Microsoft Project**: .mpp、.mpt

- **Microsoft Publisher**: .pub

- **Microsoft Office 97、Office 2010、Office 2003**: .xls、.xlt、.doc、.dot、.ppt、.pps、.pot

- **Microsoft XPS**: .xps、.oxps

- **イメージ**: .jpg、.jpe、.jpeg、.jif、.jfif、.jfi.png、.tif、.tiff

- **SolidWorks**: .sldprt、.slddrw、.sldasm

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng


Rights Management サービスを使用した保護は、「[ファイル API の構成](../develop/file-api-configuration.md)」に記載されたファイルの種類でサポートされています。 管理者によって構成されたラベルを選択した場合は、この保護が自動的に適用されます。または[アクセス許可レベル](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)を使って、独自の保護設定を指定することができます。 


## <a name="other-instructions"></a>その他の手順
操作方法に関する手順については、「Azure Information Protection ユーザー ガイド」の次のセクションを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)




<!--HONumber=Dec16_HO1-->


