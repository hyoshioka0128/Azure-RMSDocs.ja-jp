---
title: Azure RMS および FCI のための PowerShell スクリプト - AIP
description: Windows Server ファイル分類インフラストラクチャでの RMS の保護に関するページで説明されている、コピーして編集するためのサンプル スクリプトです。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ae6d8d0f-4ebc-43fe-a1f6-26b690fd83d0
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 22db2bd08d97b13ad69d9805a39c174698561eef
ms.sourcegitcommit: 1e25e7a32cc0b2a3a6c9b80575927009d8a96838
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71689990"
---
# <a name="windows-powershell-script-for-azure-rms-protection-by-using-file-server-resource-manager-fci"></a>ファイル サーバー リソース マネージャー FCI を使用する Azure RMS 保護のための Windows PowerShell スクリプト

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

このページには、[Windows Server ファイル分類インフラストラクチャでの RMS の保護](configure-fci.md)に関するページに説明されているサンプル スクリプトが含まれています。このスクリプトをコピーし、編集してください。

このスクリプトでは、AzureInformationProtection モジュールに **1.3.155.2** という最小バージョンを使用しています。 次のコマンドを実行してバージョンを確認してください。`(Get-Module AzureInformationProtection -ListAvailable).Version` 

*&#42;&#42;免責事項&#42;&#42;: このサンプルスクリプトは、Microsoft の標準サポートプログラムまたはサービスではサポートされていません。このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。*

```
<#
.SYNOPSIS 
     Helper script to protect all file types using the Azure Rights Management service and FCI.
.DESCRIPTION
     Protect files with the Azure Rights Management service and Windows Server FCI, using an RMS template ID and AzureInformationProtection module minimum version 1.3.155.2.   
#>
param(
            [Parameter(Mandatory = $false)]
            [ValidateScript({ If($_ -eq "") {$true} else { if (Test-Path -Path $_ -PathType Leaf) {$true} else {throw "Can't find file specified"} } })]
            [string]$File,

            [Parameter(Mandatory = $false)]
            [string]$TemplateID,

            [Parameter(Mandatory = $false)]
            [string]$OwnerMail,

            [Parameter(Mandatory = $false)]
            [string]$AppPrincipalId = "<enter your AppPrincipalId here>",

            [Parameter(Mandatory = $false)]
            [string]$SymmetricKey = "<enter your key here>",

            [Parameter(Mandatory = $false)]
            [string]$BposTenantId = "<enter your BposTenantId here>"
) 

# script information
[String] $Script:Version = 'version 3.4' 
[String] $Script:Name = "RMS-Protect-FCI.ps1"

#global working variables
[switch] $Script:isScriptProcess = $False # Controls the script process. If false, the script gracefully stops running.

#**Functions (general helper)***************************************
function Get-ScriptName(){ 

    return $MyInvocation.ScriptName.Substring($MyInvocation.ScriptName.LastIndexOf('\') + 1, $MyInvocation.ScriptName.LastIndexOf('.') - $MyInvocation.ScriptName.LastIndexOf('\') - 1)
}

#**Functions (script specific)**************************************

function Check-Module{

    param ([String]$Module = $(Throw "Module name not specified"))

    [bool]$isResult = $False

    #try to load the module
    if ((get-module -list -name $Module) -ne $nil)
        {

            $isResult = $True
        } else 
        
        {
            $isResult = $False
        } 

    return $isResult
}

function Protect-File ($ffile, $ftemplateId, $fownermail) {

    [bool] $returnValue = $false
    try {
        If ($OwnerMail -eq $null -or $OwnerMail -eq "") {
            $protectReturn = Protect-RMSFile -File $ffile -InPlace -DoNotPersistEncryptionKey All -TemplateID $ftemplateId
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId")
        } else {
            $protectReturn = Protect-RMSFile -File $ffile -InPlace -DoNotPersistEncryptionKey All -TemplateID $ftemplateId -OwnerEmail $fownermail
            $returnValue = $true
            Write-Host ( "Information: " + "Protected File: $ffile with Template: $ftemplateId, set Owner: $fownermail")
        }
    } catch {
        Write-Host ( "ERROR" + "During protection of file: $ffile with Template: $ftemplateId")
            }
    return $returnValue
}

function Set-RMSConnection ($fappId, $fkey, $fbposId) {

    [bool] $returnValue = $false
    try {
               Set-RMSServerAuthentication -AppPrincipalId $fappId -Key $fkey -BposTenantId $fbposId
        Write-Host ("Information: " + "Connected to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")
#       Get-RMSTemplate -Force
        $returnValue = $true
    } catch {
        Write-Host ("ERROR" + "During connection to Azure RMS Service with BposTenantId: $fbposId using AppPrincipalId: $fappId")

    }
    return $returnValue
}

#**Main Script (Script)*********************************************
Write-Host ("-== " + $Script:Name + " " + $Version + " ==-")

$Script:isScriptProcess = $True

# Validate Azure RMS connection by checking the module and then connection
if ($Script:isScriptProcess) {
        if (Check-Module -Module AzureInformationProtection){
        $Script:isScriptProcess = $True
    } else {

        Write-Host ("The AzureInformationProtection module is not loaded") -foregroundcolor "yellow" -backgroundcolor "black"           
        $Script:isScriptProcess = $False
    }
}

if ($Script:isScriptProcess) {
    #Write-Host ("Try to connect to Azure RMS with AppId: $AppPrincipalId and BPOSID: $BposTenantId" )  
    if (Set-RMSConnection $AppPrincipalId $SymmetricKey $BposTenantId) {
        Write-Host ("Connected to Azure RMS")

    } else {
        Write-Host ("Couldn't connect to Azure RMS") -foregroundcolor "yellow" -backgroundcolor "black"
        $Script:isScriptProcess = $False
    }
}

#  Start working loop
if ($Script:isScriptProcess) {
    if ( !(($File -eq $null) -or ($File -eq "")) ) {
        if (!(Protect-File -ffile $File -ftemplateId $TemplateID -fownermail $OwnerMail)) {
            $Script:isScriptProcess = $False           
        }
    }
}

# Closing
if (!$Script:isScriptProcess) { Write-Host "ERROR occurred during script process" -foregroundcolor "red" -backgroundcolor "black"}
write-host ("-== " + $Script:Name + " " + $Version + "  ==-")
if (!$Script:isScriptProcess) { exit(-1) } else {exit(0)}
```

---

「[Windows Server ファイル分類インフラストラクチャでの RMS の保護](configure-fci.md)」に戻ります。
