---
title: "Web Api を Azure Active Directory B2C のクラウド認証"
author: camsoper
description: "ASP.NET Core Web API と Azure Active Directory B2C の認証を設定する方法を検出します。 認証されている web API Postman をテストします。"
ms.author: casoper
manager: wpickett
ms.date: 01/25/2018
ms.topic: tutorial
ms.technology: aspnet
ms.prod: asp.net-core
ms.custom: mvc
uid: security/authentication/azure-ad-b2c-webapi
ms.openlocfilehash: a63bfc26bb6b0f5ea1c64641d6f57a3555d7f401
ms.sourcegitcommit: f2a11a89037471a77ad68a67533754b7bb8303e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="cloud-authentication-in-web-apis-with-azure-active-directory-b2c"></a><span data-ttu-id="dbf7f-104">Web Api を Azure Active Directory B2C のクラウド認証</span><span class="sxs-lookup"><span data-stu-id="dbf7f-104">Cloud authentication in web APIs with Azure Active Directory B2C</span></span>

<span data-ttu-id="dbf7f-105">作成者: [Cam Soper](https://twitter.com/camsoper)</span><span class="sxs-lookup"><span data-stu-id="dbf7f-105">By [Cam Soper](https://twitter.com/camsoper)</span></span>

<span data-ttu-id="dbf7f-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) は、web およびモバイル アプリケーションのクラウド id 管理ソリューションです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-106">[Azure Active Directory B2C](/azure/active-directory-b2c/active-directory-b2c-overview) (Azure AD B2C) is a cloud identity management solution for web and mobile apps.</span></span> <span data-ttu-id="dbf7f-107">サービスは、クラウドとオンプレミスでホストされているアプリの認証を提供します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-107">The service provides authentication for apps hosted in the cloud and on-premises.</span></span> <span data-ttu-id="dbf7f-108">認証の種類には、ソーシャル ネットワーク アカウントでは、個々 のアカウントを含めるし、エンタープライズ アカウントをフェデレーションします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-108">Authentication types include include individual accounts, social network accounts, and federated enterprise accounts.</span></span> <span data-ttu-id="dbf7f-109">また、Azure AD B2C では、最小構成で多要素認証を提供できます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-109">Additionally, Azure AD B2C can provide multi-factor authentication with minimal configuration.</span></span>

> [!TIP]
> <span data-ttu-id="dbf7f-110">Azure Active Directory (Azure AD) の Azure AD B2C の別の製品サービスしています。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-110">Azure Active Directory (Azure AD) Azure AD B2C are separate product offerings.</span></span> <span data-ttu-id="dbf7f-111">Azure AD テナントは、組織を表し、Azure AD B2C テナントは証明書利用者アプリケーションで使用される id のコレクションを表します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-111">An Azure AD tenant represents an organization, while an Azure AD B2C tenant represents a collection of identities to be used with relying party applications.</span></span> <span data-ttu-id="dbf7f-112">詳細については、次を参照してください。 [Azure AD B2C: よく寄せられる質問 (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-112">To learn more, see [Azure AD B2C: Frequently asked questions (FAQ)](/azure/active-directory-b2c/active-directory-b2c-faqs).</span></span>

<span data-ttu-id="dbf7f-113">Web Api には、ユーザー インターフェイスがあるありません、ためにいないユーザーを Azure AD B2C のような場合は、セキュリティ トークン サービスにリダイレクトすることです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-113">Since web APIs have no user interface, they're unable to redirect the user to a secure token service like Azure AD B2C.</span></span> <span data-ttu-id="dbf7f-114">代わりに、この API は、呼び出し元のアプリは、Azure AD B2C を持つユーザーが既に認証からベアラー トークンを渡されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-114">Instead, the API is passed a bearer token from the calling app, which has already authenticated the user with Azure AD B2C.</span></span> <span data-ttu-id="dbf7f-115">API は、ユーザーが直接やり取りせずトークンを検証します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-115">The API then validates the token without direct user interaction.</span></span>

<span data-ttu-id="dbf7f-116">このチュートリアルで学習する方法。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-116">In this tutorial, learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dbf7f-117">Azure Active Directory B2C テナントを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-117">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="dbf7f-118">Azure AD B2C で Web API を登録します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-118">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="dbf7f-119">Visual Studio を使用すると、Azure AD B2C テナント認証を使用するのにように構成、Web API を作成できます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-119">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="dbf7f-120">Azure AD B2C テナントの動作を制御するポリシーを構成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-120">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="dbf7f-121">ログイン ダイアログを表示する web アプリをシミュレートするために使用する Postman は、トークンを取得し、それを使用して、web API に対する要求します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-121">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbf7f-122">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="dbf7f-122">Prerequisites</span></span>

<span data-ttu-id="dbf7f-123">以下は、このチュートリアルで必要です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-123">The following are required for this walkthrough:</span></span>

* [<span data-ttu-id="dbf7f-124">Microsoft Azure サブスクリプション</span><span class="sxs-lookup"><span data-stu-id="dbf7f-124">Microsoft Azure subscription</span></span>](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
* <span data-ttu-id="dbf7f-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (任意のエディション)</span><span class="sxs-lookup"><span data-stu-id="dbf7f-125">[Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) (any edition)</span></span>
* [<span data-ttu-id="dbf7f-126">Postman</span><span class="sxs-lookup"><span data-stu-id="dbf7f-126">Postman</span></span>](https://www.getpostman.com/postman)

## <a name="create-the-azure-active-directory-b2c-tenant"></a><span data-ttu-id="dbf7f-127">Azure Active Directory B2C テナントを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-127">Create the Azure Active Directory B2C tenant</span></span>

<span data-ttu-id="dbf7f-128">Azure AD B2C テナントを作成する[ドキュメント」の説明に従って](/azure/active-directory-b2c/active-directory-b2c-get-started)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-128">Create an Azure AD B2C tenant [as described in the documentation](/azure/active-directory-b2c/active-directory-b2c-get-started).</span></span> <span data-ttu-id="dbf7f-129">メッセージが表示されたら、テナントを Azure サブスクリプションに関連付けるは省略可能なこのチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-129">When prompted, associating the tenant with an Azure subscription is optional for this tutorial.</span></span>

## <a name="configure-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="dbf7f-130">サインアップまたはサインイン ポリシーを構成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-130">Configure a sign-up or sign-in policy</span></span>

<span data-ttu-id="dbf7f-131">Azure AD B2C のドキュメントで手順を使用して[サインアップまたはサインイン ポリシーを作成する](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-131">Use the steps in the Azure AD B2C documentation to [create a sign-up or sign-in policy](/azure/active-directory-b2c/active-directory-b2c-reference-policies#create-a-sign-up-or-sign-in-policy).</span></span> <span data-ttu-id="dbf7f-132">ポリシーに名前**SiUpIn**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-132">Name the policy **SiUpIn**.</span></span>  <span data-ttu-id="dbf7f-133">ドキュメントの例の値を使用して**Id プロバイダー**、**サインアップ属性**、および**アプリケーション要求**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-133">Use the example values provided in the documentation for **Identity providers**, **Sign-up attributes**, and **Application claims**.</span></span> <span data-ttu-id="dbf7f-134">使用して、**を今すぐ実行**ドキュメント」の説明に従って、ポリシーをテストするにはボタンは省略可能です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-134">Using the **Run now** button to test the policy as described in the documentation is optional.</span></span>

## <a name="register-the-api-in-azure-ad-b2c"></a><span data-ttu-id="dbf7f-135">Azure AD B2C の登録 API</span><span class="sxs-lookup"><span data-stu-id="dbf7f-135">Register the API in Azure AD B2C</span></span>

<span data-ttu-id="dbf7f-136">新しく作成された Azure AD B2C テナントの登録 API を使用して、[ドキュメント」の手順](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api)下にある、 **web API を登録**セクションです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-136">In the newly created Azure AD B2C tenant, register your API using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) under the **Register a web API** section.</span></span>

<span data-ttu-id="dbf7f-137">次の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-137">Use the following values:</span></span>

| <span data-ttu-id="dbf7f-138">設定</span><span class="sxs-lookup"><span data-stu-id="dbf7f-138">Setting</span></span>                       | <span data-ttu-id="dbf7f-139">[値]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-139">Value</span></span>               | <span data-ttu-id="dbf7f-140">メモ</span><span class="sxs-lookup"><span data-stu-id="dbf7f-140">Notes</span></span>                                                                                  |
|-------------------------------|---------------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="dbf7f-141">**Name**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-141">**Name**</span></span>                      | <span data-ttu-id="dbf7f-142">*&lt;API 名&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-142">*&lt;API name&gt;*</span></span>  | <span data-ttu-id="dbf7f-143">入力、**名前**コンシューマーにアプリを説明するアプリのです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-143">Enter a **Name** for the app that describes your app to consumers.</span></span>                     |
| <span data-ttu-id="dbf7f-144">**Web アプリは、ロールまたは web API**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-144">**Include web app / web API**</span></span> | <span data-ttu-id="dbf7f-145">[はい]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-145">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="dbf7f-146">**暗黙のフローを許可します。**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-146">**Allow implicit flow**</span></span>       | <span data-ttu-id="dbf7f-147">[はい]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-147">Yes</span></span>                 |                                                                                        |
| <span data-ttu-id="dbf7f-148">**応答 URL**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-148">**Reply URL**</span></span>                 | `https://localhost` | <span data-ttu-id="dbf7f-149">応答 Url は、エンドポイントが Azure AD B2C がアプリを要求するすべてのトークンを返します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-149">Reply URLs are endpoints where Azure AD B2C returns any tokens that your app requests.</span></span> |
| <span data-ttu-id="dbf7f-150">**アプリ ID URI**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-150">**App ID URI**</span></span>                | <span data-ttu-id="dbf7f-151">*api*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-151">*api*</span></span>               | <span data-ttu-id="dbf7f-152">URI は、物理アドレスに解決する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-152">The URI doesn't need to resolve to a physical address.</span></span> <span data-ttu-id="dbf7f-153">のみ一意である必要があります。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-153">It only needs to be unique.</span></span>     |
| <span data-ttu-id="dbf7f-154">**ネイティブ クライアントが含まれます**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-154">**Include native client**</span></span>     | <span data-ttu-id="dbf7f-155">×</span><span class="sxs-lookup"><span data-stu-id="dbf7f-155">No</span></span>                  |                                                                                        |

<span data-ttu-id="dbf7f-156">この API は、登録後、テナントでアプリケーションと Api の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-156">After the API is registered, the list of apps and APIs in the tenant is displayed.</span></span> <span data-ttu-id="dbf7f-157">だけに登録されている API を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-157">Select the API that was just registered.</span></span> <span data-ttu-id="dbf7f-158">選択、**コピー**の右側にあるアイコン、**アプリケーション ID**をクリップボードにコピーするフィールドです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-158">Select the **Copy** icon to the right of the **Application ID** field to copy it to the clipboard.</span></span> <span data-ttu-id="dbf7f-159">選択**スコープをパブリッシュ**既定値を確認してください*user_impersonation*スコープが存在します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-159">Select **Published scopes** and verify the default *user_impersonation* scope is present.</span></span>

## <a name="create-an-aspnet-core-app-in-visual-studio-2017"></a><span data-ttu-id="dbf7f-160">Visual Studio 2017 で ASP.NET Core アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-160">Create an ASP.NET Core app in Visual Studio 2017</span></span>

<span data-ttu-id="dbf7f-161">Visual Studio Web アプリケーション テンプレートは、認証に使用する Azure AD B2C テナント構成されていることができます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-161">The Visual Studio Web Application template can be configured to use the Azure AD B2C tenant for authentication.</span></span>

<span data-ttu-id="dbf7f-162">Visual Studio で。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-162">In Visual Studio:</span></span>

1. <span data-ttu-id="dbf7f-163">新しい ASP.NET Core Web アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-163">Create a new ASP.NET Core Web Application.</span></span> 
2. <span data-ttu-id="dbf7f-164">選択**Web API**テンプレートの一覧からです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-164">Select **Web API** from the list of templates.</span></span>
3. <span data-ttu-id="dbf7f-165">選択、**認証の変更**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-165">Select the **Change Authentication** button.</span></span>
    
    ![変更の認証 ボタン](./azure-ad-b2c-webapi/change-auth-button.png)

4. <span data-ttu-id="dbf7f-167">**認証の変更**ダイアログで、**個々 のユーザー アカウント**、し、 **、クラウド内の既存のユーザー ストアへの接続**ドロップダウン リストにします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-167">In the **Change Authentication** dialog, select **Individual User Accounts**, and then select **Connect to an existing user store in the cloud** in the dropdown.</span></span> 
    
    ![認証の変更 ダイアログ](./azure-ad-b2c-webapi/change-auth-dialog.png)

5. <span data-ttu-id="dbf7f-169">次の値をフォームに入力します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-169">Complete the form with the following values:</span></span>
    
    | <span data-ttu-id="dbf7f-170">設定</span><span class="sxs-lookup"><span data-stu-id="dbf7f-170">Setting</span></span>                       | <span data-ttu-id="dbf7f-171">[値]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-171">Value</span></span>                                                 |
    |-------------------------------|-------------------------------------------------------|
    | <span data-ttu-id="dbf7f-172">**ドメイン名**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-172">**Domain Name**</span></span>               | <span data-ttu-id="dbf7f-173">*&lt;B2C テナントのドメイン名&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-173">*&lt;the domain name of your B2C tenant&gt;*</span></span>          |
    | <span data-ttu-id="dbf7f-174">**アプリケーション ID**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-174">**Application ID**</span></span>            | <span data-ttu-id="dbf7f-175">*&lt;アプリケーション ID をクリップボードから貼り付けます&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-175">*&lt;paste the Application ID from the clipboard&gt;*</span></span> |
    | <span data-ttu-id="dbf7f-176">**サインアップまたはサインイン ポリシー**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-176">**Sign-up or sign-in policy**</span></span> | `B2C_1_SiUpIn`                                        |
    
    <span data-ttu-id="dbf7f-177">選択**OK**を閉じる、**認証の変更**ダイアログ。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-177">Select **OK** to close the **Change Authentication** dialog.</span></span> <span data-ttu-id="dbf7f-178">選択**OK** web アプリを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-178">Select **OK** to create the web app.</span></span>

<span data-ttu-id="dbf7f-179">Visual Studio では、という名前のコント ローラーで、web API を作成*ValuesController.cs* GET 要求に対してハード コーディングされた値を返します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-179">Visual Studio creates the web API with a controller named *ValuesController.cs* that returns hard-coded values for GET requests.</span></span> <span data-ttu-id="dbf7f-180">クラスを装飾、 [Authorize attribute](xref:security/authorization/simple)ので、すべての要求が認証を必要とします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-180">The class is decorated with the [Authorize attribute](xref:security/authorization/simple), so all requests require authentication.</span></span>

## <a name="run-the-web-api"></a><span data-ttu-id="dbf7f-181">Web API を実行します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-181">Run the web API</span></span>

<span data-ttu-id="dbf7f-182">Visual Studio で、API を実行します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-182">In Visual Studio, run the API.</span></span> <span data-ttu-id="dbf7f-183">Visual Studio では、API のルート URL を指すブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-183">Visual Studio launches a browser pointed at the API's root URL.</span></span> <span data-ttu-id="dbf7f-184">アドレス バーの URL をメモして、バック グラウンドで実行されている API のままにします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-184">Note the URL in the address bar, and leave the API running in the background.</span></span>

> [!NOTE]
> <span data-ttu-id="dbf7f-185">ルートの URL に対して定義されているコント ローラーがないため、ブラウザーには、404 (ページが見つかりません) エラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-185">Since there is no controller defined for the root URL, the browser displays a 404 (page not found) error.</span></span> <span data-ttu-id="dbf7f-186">これは通常の動作です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-186">This is expected behavior.</span></span>

## <a name="use-postman-to-get-a-token-and-test-the-api"></a><span data-ttu-id="dbf7f-187">Postman を使用して、トークンを取得および API のテスト</span><span class="sxs-lookup"><span data-stu-id="dbf7f-187">Use Postman to get a token and test the API</span></span>

<span data-ttu-id="dbf7f-188">[Postman](https://getpostman.com/postman)はテスト用ツールの web Api です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-188">[Postman](https://getpostman.com/postman) is a tool for testing web APIs.</span></span> <span data-ttu-id="dbf7f-189">このチュートリアルでは、Postman は、ユーザーの代理で web API にアクセスする web アプリをシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-189">For this tutorial, Postman simulates a web app that accesses the web API on the user's behalf.</span></span>

### <a name="register-postman-as-a-web-app"></a><span data-ttu-id="dbf7f-190">Web アプリとして Postman を登録します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-190">Register Postman as a web app</span></span>

<span data-ttu-id="dbf7f-191">Postman は、Azure AD B2C テナントからトークンを入手できる、web アプリをシミュレート、ので必要があります登録する必要が、テナントで web アプリとします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-191">Since Postman simulates a web app that can obtain tokens from the Azure AD B2C tenant, it must be registered in the tenant as a web app.</span></span> <span data-ttu-id="dbf7f-192">登録を使用して Postman[ドキュメント」の手順](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app)下にある、 **web アプリを登録**セクションです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-192">Register Postman using [the steps in the documentation](/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-app) under the **Register a web app** section.</span></span> <span data-ttu-id="dbf7f-193">停止時刻、 **web アプリ クライアント シークレットの作成**セクションです。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-193">Stop at the **Create a web app client secret** section.</span></span> <span data-ttu-id="dbf7f-194">クライアント シークレットは、このチュートリアルでは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-194">A client secret isn't required for this tutorial.</span></span> 

<span data-ttu-id="dbf7f-195">次の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-195">Use the following values:</span></span>

| <span data-ttu-id="dbf7f-196">設定</span><span class="sxs-lookup"><span data-stu-id="dbf7f-196">Setting</span></span>                       | <span data-ttu-id="dbf7f-197">[値]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-197">Value</span></span>                            | <span data-ttu-id="dbf7f-198">メモ</span><span class="sxs-lookup"><span data-stu-id="dbf7f-198">Notes</span></span>                           |
|-------------------------------|----------------------------------|---------------------------------|
| <span data-ttu-id="dbf7f-199">**Name**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-199">**Name**</span></span>                      | <span data-ttu-id="dbf7f-200">Postman</span><span class="sxs-lookup"><span data-stu-id="dbf7f-200">Postman</span></span>                          |                                 |
| <span data-ttu-id="dbf7f-201">**Web アプリは、ロールまたは web API**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-201">**Include web app / web API**</span></span> | <span data-ttu-id="dbf7f-202">[はい]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-202">Yes</span></span>                              |                                 |
| <span data-ttu-id="dbf7f-203">**暗黙のフローを許可します。**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-203">**Allow implicit flow**</span></span>       | <span data-ttu-id="dbf7f-204">[はい]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-204">Yes</span></span>                              |                                 |
| <span data-ttu-id="dbf7f-205">**応答 URL**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-205">**Reply URL**</span></span>                 | `https://getpostman.com/postman` |                                 |
| <span data-ttu-id="dbf7f-206">**アプリ ID URI**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-206">**App ID URI**</span></span>                | <span data-ttu-id="dbf7f-207">*&lt;空白のままに&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-207">*&lt;leave blank&gt;*</span></span>            | <span data-ttu-id="dbf7f-208">このチュートリアルでは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-208">Not required for this tutorial.</span></span> |
| <span data-ttu-id="dbf7f-209">**ネイティブ クライアントが含まれます**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-209">**Include native client**</span></span>     | <span data-ttu-id="dbf7f-210">×</span><span class="sxs-lookup"><span data-stu-id="dbf7f-210">No</span></span>                               |                                 |

<span data-ttu-id="dbf7f-211">新しく登録されている web アプリでは、ユーザーの代理で web API にアクセスする権限が必要です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-211">The newly registered web app needs permission to access the web API on the user's behalf.</span></span>  

1. <span data-ttu-id="dbf7f-212">選択**Postman**クリックしてアプリの一覧で**API アクセス**左側のメニュー。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-212">Select **Postman** in the list of apps and then select **API access** from the menu on the left.</span></span>
2. <span data-ttu-id="dbf7f-213">選択**+ 追加**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-213">Select **+ Add**.</span></span>
3. <span data-ttu-id="dbf7f-214">**選択 API**ドロップダウン リストで、web API の名前を選択します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-214">In the **Select API** dropdown, select the name of the web API.</span></span>
4. <span data-ttu-id="dbf7f-215">**選択スコープ**ドロップダウン リストで、すべてのスコープが選択されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-215">In the **Select Scopes** dropdown, ensure all scopes are selected.</span></span>
5. <span data-ttu-id="dbf7f-216">選択**Ok**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-216">Select **Ok**.</span></span>

<span data-ttu-id="dbf7f-217">ベアラー トークンを取得するためには、Postman アプリのアプリケーションの ID に注意してください。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-217">Note the Postman app's Application ID, as it's required to obtain a bearer token.</span></span>

### <a name="create-a-postman-request"></a><span data-ttu-id="dbf7f-218">Postman 要求を作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-218">Create a Postman request</span></span>

<span data-ttu-id="dbf7f-219">Postman を起動します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-219">Launch Postman.</span></span> <span data-ttu-id="dbf7f-220">既定では、Postman が表示されます、**新規作成**ダイアログを起動するとします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-220">By default, Postman displays the **Create New** dialog upon launching.</span></span> <span data-ttu-id="dbf7f-221">ダイアログ ボックスが表示されていない場合は、選択、 **+ 新規**左上のボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-221">If the dialog isn't displayed, select the **+ New** button in the upper left.</span></span>

<span data-ttu-id="dbf7f-222">**新規作成** ダイアログ。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-222">From the **Create New** dialog:</span></span>

1. <span data-ttu-id="dbf7f-223">選択**要求**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-223">Select **Request**.</span></span>
    
    ![要求 ボタン](./azure-ad-b2c-webapi/postman-create-new.png)

2. <span data-ttu-id="dbf7f-225">入力*値の取得*で、**要求名**ボックス。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-225">Enter *Get Values* in the **Request name** box.</span></span>
3. <span data-ttu-id="dbf7f-226">選択**+ コレクションの作成**要求を格納するための新しいコレクションを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-226">Select **+ Create Collection** to create a new collection for storing the request.</span></span> <span data-ttu-id="dbf7f-227">コレクションの名前を付けます*ASP.NET Core チュートリアル*し、チェック マークを選択します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-227">Name the collection *ASP.NET Core tutorials* and then select the checkmark.</span></span>
    
    ![新しいコレクションを作成します。](./azure-ad-b2c-webapi/postman-create-collection.png)

4. <span data-ttu-id="dbf7f-229">選択、 **ASP.NET Core チュートリアルへ保存**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-229">Select the **Save to ASP.NET Core tutorials** button.</span></span>

### <a name="test-the-web-api-withoutauthentication"></a><span data-ttu-id="dbf7f-230">Web API withoutauthentication をテストします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-230">Test the web API withoutauthentication</span></span>

<span data-ttu-id="dbf7f-231">Web API に認証が必要であることを確認するには、最初に認証を使用しない要求を作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-231">To verify that the web API requires authentication, first make a request without authentication.</span></span>

1. <span data-ttu-id="dbf7f-232">**要求 URL を入力**ボックスで、URL を入力`ValuesController`です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-232">In the **Enter request URL** box, enter the URL for `ValuesController`.</span></span> <span data-ttu-id="dbf7f-233">URL はブラウザーに表示されるものと同じ**api/値**追加されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-233">The URL is the same as displayed in the browser with **api/values** appended.</span></span> <span data-ttu-id="dbf7f-234">例としては`https://localhost:44375/api/values`します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-234">An example would be `https://localhost:44375/api/values`.</span></span>
2. <span data-ttu-id="dbf7f-235">選択、**送信**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-235">Select the **Send** button.</span></span>
3. <span data-ttu-id="dbf7f-236">応答のステータスは*401 Unauthorized*です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-236">Note the status of the response is *401 Unauthorized*.</span></span>

    ![401 承認されていない応答](./azure-ad-b2c-webapi/postman-401-status.png)

### <a name="obtain-a-bearer-token"></a><span data-ttu-id="dbf7f-238">ベアラー トークンを取得します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-238">Obtain a bearer token</span></span>

<span data-ttu-id="dbf7f-239">Web API に認証された要求にベアラー トークンが必要です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-239">To make an authenticated request to the web API, a bearer token is required.</span></span> <span data-ttu-id="dbf7f-240">Postman 簡単に Azure AD B2C テナントにサインインし、トークンを取得できます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-240">Postman makes it easy to sign in to the Azure AD B2C tenant and obtain a token.</span></span>

1. <span data-ttu-id="dbf7f-241">**承認**] タブで、**型**ドロップダウンで、[ **OAuth 2.0**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-241">On the **Authorization** tab, in the **TYPE** dropdown, select **OAuth 2.0**.</span></span> <span data-ttu-id="dbf7f-242">**承認データを追加して**ドロップダウンで、**要求ヘッダー**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-242">In the **Add authorization data to** dropdown, select **Request Headers**.</span></span> <span data-ttu-id="dbf7f-243">選択**新しいアクセス トークンを取得**です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-243">Select **Get New Access Token**.</span></span>
    
    ![[承認] タブの設定](./azure-ad-b2c-webapi/postman-auth-tab.png)

2. <span data-ttu-id="dbf7f-245">完了、**新しいアクセス トークンの取得**ようダイアログ。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-245">Complete the **GET NEW ACCESS TOKEN** dialog as follows:</span></span>
    
    | <span data-ttu-id="dbf7f-246">設定</span><span class="sxs-lookup"><span data-stu-id="dbf7f-246">Setting</span></span>                   | <span data-ttu-id="dbf7f-247">[値]</span><span class="sxs-lookup"><span data-stu-id="dbf7f-247">Value</span></span>                                                                                         | <span data-ttu-id="dbf7f-248">メモ</span><span class="sxs-lookup"><span data-stu-id="dbf7f-248">Notes</span></span>                                                                                      |
    |---------------------------|-----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
    | <span data-ttu-id="dbf7f-249">**トークン名**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-249">**Token Name**</span></span>            | <span data-ttu-id="dbf7f-250">*&lt;token name&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-250">*&lt;token name&gt;*</span></span>                                                                          | <span data-ttu-id="dbf7f-251">トークンのわかりやすい名前を入力します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-251">Enter a descriptive name for the token.</span></span>                                                    |
    | <span data-ttu-id="dbf7f-252">**付与の種類**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-252">**Grant Type**</span></span>            | <span data-ttu-id="dbf7f-253">暗黙的</span><span class="sxs-lookup"><span data-stu-id="dbf7f-253">Implicit</span></span>                                                                                      |                                                                                            |
    | <span data-ttu-id="dbf7f-254">**コールバック URL**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-254">**Callback URL**</span></span>          | `https://getpostman.com/postman`                                                              |                                                                                            |
    | <span data-ttu-id="dbf7f-255">**Auth URL**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-255">**Auth URL**</span></span>              | `https://login.microsoftonline.com/<tenant domain name>/oauth2/v2.0/authorize?p=B2C_1_SiUpIn` | <span data-ttu-id="dbf7f-256">置き換える*&lt;テナントのドメイン名&gt;*山かっこせず、テナントのドメイン名を使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-256">Replace *&lt;tenant domain name&gt;* with the tenant's domain name without angle brackets.</span></span> |
    | <span data-ttu-id="dbf7f-257">**クライアント ID**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-257">**Client ID**</span></span>             | <span data-ttu-id="dbf7f-258">*&lt;入力 Postman アプリの<b>アプリケーション ID</b>&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-258">*&lt;enter the Postman app's <b>Application ID</b>&gt;*</span></span>                                       |                                                                                            |
    | <span data-ttu-id="dbf7f-259">**クライアント シークレット**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-259">**Client Secret**</span></span>         | <span data-ttu-id="dbf7f-260">*&lt;空白のままに&gt;*</span><span class="sxs-lookup"><span data-stu-id="dbf7f-260">*&lt;leave blank&gt;*</span></span>                                                                         |                                                                                            |
    | <span data-ttu-id="dbf7f-261">**スコープ**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-261">**Scope**</span></span>                 | `https://<tenant domain name>/api/user_impersonation openid offline_access`                   | <span data-ttu-id="dbf7f-262">置き換える*&lt;テナントのドメイン名&gt;*山かっこせず、テナントのドメイン名を使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-262">Replace *&lt;tenant domain name&gt;* with the tenant's domain name without angle brackets.</span></span> |
    | <span data-ttu-id="dbf7f-263">**クライアント認証**</span><span class="sxs-lookup"><span data-stu-id="dbf7f-263">**Client Authentication**</span></span> | <span data-ttu-id="dbf7f-264">本文でクライアントの資格情報を送信します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-264">Send client credentials in body</span></span>                                                               |                                                                                            |
    
3. <span data-ttu-id="dbf7f-265">選択、**トークン要求**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-265">Select the **Request Token** button.</span></span>

4. <span data-ttu-id="dbf7f-266">Postman には、ダイアログ ボックスで、Azure AD B2C テナントの記号を含む新しいウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-266">Postman opens a new window containing the Azure AD B2C tenant's sign in dialog.</span></span> <span data-ttu-id="dbf7f-267">(1 つには、ポリシーのテストが作成された) 場合は、既存のアカウントでサインインまたは選択**今すぐサインアップ**新しいアカウントを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-267">Sign in with an existing account (if one was created testing the policies) or select **Sign up now** to create a new account.</span></span> <span data-ttu-id="dbf7f-268">**パスワードを忘れた場合ですか?**忘れてもパスワードをリセットするリンクを使用します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-268">The **Forgot your password?** link is used to reset a forgotten password.</span></span>

5. <span data-ttu-id="dbf7f-269">正常にサインインした後、ウィンドウが閉じられると、**アクセス トークンの管理**ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-269">After successfully signing in, the window closes and the **MANAGE ACCESS TOKENS** dialog appears.</span></span> <span data-ttu-id="dbf7f-270">クリックし、一番下まで下にスクロール、**使用トークン**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-270">Scroll down to the bottom and select the **Use Token** button.</span></span>
    
    !["使用 Token"ボタンを検索する場所](./azure-ad-b2c-webapi/postman-access-token.png)

### <a name="test-the-web-api-with-authentication"></a><span data-ttu-id="dbf7f-272">認証を使用して、web API をテストします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-272">Test the web API with authentication</span></span>

<span data-ttu-id="dbf7f-273">選択、**送信**をもう一度要求を送信するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-273">Select the **Send** button to send the request again.</span></span> <span data-ttu-id="dbf7f-274">現時点では、応答ステータスが*200 OK* JSON ペイロードが、応答に表示されると**本文** タブ。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-274">This time, the response status is *200 OK* and the JSON payload is visible on the response **Body** tab.</span></span>
    
![ペイロードと成功状態](./azure-ad-b2c-webapi/postman-success.png)

## <a name="next-steps"></a><span data-ttu-id="dbf7f-276">次の手順</span><span class="sxs-lookup"><span data-stu-id="dbf7f-276">Next steps</span></span>

<span data-ttu-id="dbf7f-277">このチュートリアルでは、次の作業を行う方法を学びました。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-277">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dbf7f-278">Azure Active Directory B2C テナントを作成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-278">Create an Azure Active Directory B2C tenant.</span></span>
> * <span data-ttu-id="dbf7f-279">Azure AD B2C で Web API を登録します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-279">Register a Web API in Azure AD B2C.</span></span>
> * <span data-ttu-id="dbf7f-280">Visual Studio を使用すると、Azure AD B2C テナント認証を使用するのにように構成、Web API を作成できます。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-280">Use Visual Studio to create a Web API configured to use the Azure AD B2C tenant for authentication.</span></span>
> * <span data-ttu-id="dbf7f-281">Azure AD B2C テナントの動作を制御するポリシーを構成します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-281">Configure policies controlling the behavior of the Azure AD B2C tenant.</span></span>
> * <span data-ttu-id="dbf7f-282">ログイン ダイアログを表示する web アプリをシミュレートするために使用する Postman は、トークンを取得し、それを使用して、web API に対する要求します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-282">Use Postman to simulate a web app which presents a login dialog, retrieves a token, and uses it to make a request against the web API.</span></span>

<span data-ttu-id="dbf7f-283">学習することにより、API の開発を続行するには。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-283">Continue developing your API by learning to:</span></span>

* <span data-ttu-id="dbf7f-284">[セキュリティで保護された ASP.NET Core web アプリケーションを Azure AD B2C](xref:security/authentication/azure-ad-b2c)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-284">[Secure an ASP.NET Core web app using Azure AD B2C](xref:security/authentication/azure-ad-b2c).</span></span>
* <span data-ttu-id="dbf7f-285">[.NET web API を使用して Azure AD B2C .NET web アプリから呼び出す](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-285">[Call a .NET web API from a .NET web app using Azure AD B2C](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-web-api-dotnet).</span></span>
* <span data-ttu-id="dbf7f-286">[Azure AD B2C ユーザー インターフェイスのカスタマイズ](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-286">[Customize the Azure AD B2C user interface](/azure/active-directory-b2c/active-directory-b2c-reference-ui-customization).</span></span>
* <span data-ttu-id="dbf7f-287">[パスワードの複雑さの要件を構成する](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-287">[Configure password complexity requirements](/azure/active-directory-b2c/active-directory-b2c-reference-password-complexity).</span></span>
* <span data-ttu-id="dbf7f-288">[多要素認証を有効にする](/azure/active-directory-b2c/active-directory-b2c-reference-mfa)です。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-288">[Enable multi-factor authentication](/azure/active-directory-b2c/active-directory-b2c-reference-mfa).</span></span>
* <span data-ttu-id="dbf7f-289">など、追加の id プロバイダーを構成[Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app)、 [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app)、 [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app)、 [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app)、 [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app)、およびその他。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-289">Configure additional identity providers, such as [Microsoft](/azure/active-directory-b2c/active-directory-b2c-setup-msa-app), [Facebook](/azure/active-directory-b2c/active-directory-b2c-setup-fb-app), [Google](/azure/active-directory-b2c/active-directory-b2c-setup-goog-app), [Amazon](/azure/active-directory-b2c/active-directory-b2c-setup-amzn-app), [Twitter](/azure/active-directory-b2c/active-directory-b2c-setup-twitter-app), and others.</span></span>
* <span data-ttu-id="dbf7f-290">[Azure AD Graph API を使用して](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet)Azure AD B2C テナントからグループ メンバーシップなど、追加のユーザー情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="dbf7f-290">[Use the Azure AD Graph API](/azure/active-directory-b2c/active-directory-b2c-devquickstarts-graph-dotnet) to retrieve additional user information, such as group membership, from the Azure AD B2C tenant.</span></span>