---
title: "Azure ポータルを使用して RMS 認証用に構成する |Azure RMS"
description: "ADAL での認証プロセスの概要を説明します。"
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3f43f5605b1c341d7be618327038d1a86a305a5b
ms.openlocfilehash: cb82f0333ed17ee2994608baa3bbb50d42f19073


---

# 方法: Azure ポータルを使用して RMS 認証用に構成する

Azure Active Directory Authentication Library (ADAL) を利用し、アプリに対して Azure RMS で認証を実行する。

この方法を使用するには、アプリケーションで独自の OAuth 認証を管理する必要があります。 この方法では、認証が必要なとき、RMS クライアントはアプリケーション定義のコールバックを実行します。

## Azure ポータルによる構成
まず、Azure ポータルで構成するためのガイド「[Configure Azure RMS for ADAL authentication (Azure RMS の ADAL 認証を構成する)](adal-auth.md)」に従ってください。 後で使用するために、このプロセスでの*クライアント ID* と*リダイレクト URI* をコピーして保存しておいてください。

## コード サンプル
Azure ADAL を有効にするモバイル クライアント コード用のサンプルから、コードの一部を以下に示します。 詳細については、[MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp) で完全なサンプルを参照してください。

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## 関連項目

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [Azure RMS の ADAL 認証を構成する](adal-auth.md)



<!--HONumber=Jun16_HO4-->


