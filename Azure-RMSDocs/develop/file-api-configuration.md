---
title: ファイル API の構成 | Azure RMS
description: ファイルの API の動作は、レジストリの設定を使用して構成できます。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 10/11/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 84b0f1ec7e5ef647161c5e44059140ea59ffab77
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2018
ms.locfileid: "27765801"
---
# <a name="file-api-configuration"></a>ファイル API の構成


ファイルの API の動作は、レジストリの設定を使用して構成できます。

ファイル API は、2 種類の保護 (ネイティブ保護と PFile 保護) を提供します。

-   **ネイティブ保護** - ファイルの MIME の種類 (ファイル名拡張子) を基に、AD RMS 形式に対してファイルが保護されます。
-   **PFile 保護** - AD RMS で保護されたファイル (PFile) 形式に対してファイルが保護されます。

サポートされているファイル形式について詳しくは、この記事の「**ファイル API - ファイルのサポートの詳細**」をご覧ください。

## <a name="keykey-value-types-and-descriptions"></a>キー、キーの値、種類、および説明

以降のセクションでは、暗号化を制御するキーおよびキーの値について説明します。

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection`

**種類**: キー

**説明**: ファイル API の一般的な構成が含まれています。

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>`

**種類**: キー

**説明**: 特定のファイル拡張子 (TXT、JPG など) の構成情報を指定します。

- ワイルドカード文字 "*" を使用できます。ただし、特定の拡張子の設定は、ワイルドカードの設定よりも優先されます。 ワイルドカード文字は、Microsoft Office ファイルの設定には影響しません。これらは、ファイルの種類ごとに明示的に無効する必要があります。
- 拡張子がないファイルを指定するには、"." を使用します。
- 特定のファイル拡張子のキーを指定する場合は、"." 文字を指定しないでください。たとえば、.txt ファイルの設定を指定するには、`HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` を使用します。 (`HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT` を使用しないでください)。

保護動作を指定するには、キーに **Encryption** 値を設定します。 **Encryption** 値が設定されていない場合は、ファイルの種類の既定の動作が実行されます。


### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>\Encryption*`

**種類**: REG_SZ

**説明**: 次の 3 つの値のいずれかが含まれています。

- **Off**: 暗号化が無効です。

> [!Note]
> この設定は、解読には影響しません。 ユーザーが **EXTRACT** 権限を持っている限り、ネイティブ保護と PFile 保護のどちらを使用して暗号化されたファイルでも解読できます。

- **Native**: ネイティブ暗号化が使用されます。 Office ファイルの場合、暗号化されたファイルの拡張子は元のファイルと同じです。 たとえば、.docx ファイルの拡張子は、暗号化しても .docx のままです。 ネイティブ保護を適用できるその他のファイルの場合、暗号化されたファイルの拡張子の形式は p*zzz* になります。*zzz* は元のファイル拡張子です。 たとえば、.txt ファイルを暗号化すると、ファイル拡張子は .ptxt になります。 ネイティブ保護を適用できるファイル拡張子の一覧を以下に示します。

- **Pfile**: PFile 暗号化が使用されます。 暗号化されたファイルでは、元の拡張子に .pfile が追加されます。 たとえば、.txt ファイルを暗号化すると、拡張子は .txt.pfile になります。


> [!Note]
> この設定は、Office ファイル形式には影響しません。 たとえば、`HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` 値が &quot;Pfile" に設定されている場合、.docx ファイルはネイティブ保護を使用して暗号化され、暗号化されたファイルの拡張子は .docx のままです。

その他の値を設定する場合や、値を設定しない場合は、既定の動作が実行されます。

## <a name="default-behavior-for-different-file-formats"></a>各ファイル形式の既定の動作

-   **Office ファイル** ネイティブ暗号化が有効になります。
-   **txt、xml、jpg、jpeg、pdf、png、tiff、bmp、gif、giff、jpe、jfif、jif ファイル** ネイティブ暗号化が有効になります (xxx は pxxx になります)。
-   **その他のすべてのファイル** 暗号化は保護されたファイル (pfile) に対応します (xxx は xxx.pfile になります)。

暗号化を試行したファイルの種類がブロックされている場合は、[IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx) エラーが発生します。

### <a name="file-api---file-support-details"></a>ファイル API - ファイルのサポートの詳細

すべてのファイルの種類 (拡張子) に対してネイティブ サポートを追加できます。 たとえば、拡張子 &lt;ext&gt; (Office 以外) では、その拡張子の管理者の構成が "NATIVE" の場合、\*.p&lt;ext&gt; が使用されます。

**Office ファイル**

-   ファイル拡張子: doc、dot、xla、xls、xlt、pps、ppt、docm、docx、dotm、dotx、xlam、xlsb、xlsm、xlsx、xltm、xltx、xps、potm、potx、ppsx、ppsm、pptm、pptx、thmx、vsdx、vsdm、vssx、vssm、vstx、vstm。 
-   保護の種類 = ネイティブ (既定): sample.docx を暗号化すると、sample.docx のままです。
-   保護の種類 = Pfile: Office ファイルの場合は、ネイティブと同じ結果になります。
-   Off: 暗号化を無効にします。

**PDF ファイル**

-   保護の種類 = ネイティブ: sample.pdf を暗号化すると、sample.ppdf という名前になります。
-   保護の種類 = Pfile: sample.pdf を暗号化すると、sample.pdf.pfile という名前になります。
-   Off: 暗号化を無効にします。

**その他のすべてのファイル形式**

-   保護の種類 = Pfile: sample.*zzz* を暗号化すると、sample.*zzz*.pfile という名前になります。*zzz* は元のファイル拡張子です。
-   Off: 暗号化を無効にします。

### <a name="examples"></a>例

次の設定は、txt ファイルの PFile 暗号化を有効にします。 Office ファイルには (既定で) ネイティブ保護が適用され、txt ファイルには PFile 保護が適用され、その他のすべてのファイルの保護は (既定で) ブロックされます。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

次の設定は、Office 以外のすべてのファイル (txt ファイルを除く) の PFile 暗号化を有効にします。 Office ファイルには (既定で) ネイティブ保護が適用され、txt ファイルの保護はブロックされ、その他のすべてのファイルには PFile 保護が適用されます。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

次の設定は、docx ファイルのネイティブ暗号化を無効にします。 Office ファイル (docx ファイルを除く) には (既定で) ネイティブ保護が適用され、その他のすべてのファイルの保護は (既定で) ブロックされます。

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## <a name="related-articles"></a>関連記事

- [開発者向け注意事項](developer-notes.md)
- [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]