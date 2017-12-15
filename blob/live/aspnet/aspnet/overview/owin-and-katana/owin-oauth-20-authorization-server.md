---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: "OWIN OAuth 2.0 承認サーバー |Microsoft ドキュメント"
author: hongyes
description: "このチュートリアルでは、OAuth の OWIN ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について説明します。 これは高度なチュートリアル、その唯一の outlin しています."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/20/2014
ms.topic: article
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 8842f57df84d841df77b34e9645dbf4909f82d85
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2017
---
<a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="bf7cf-104">OWIN OAuth 2.0 承認サーバー</span><span class="sxs-lookup"><span data-stu-id="bf7cf-104">OWIN OAuth 2.0 Authorization Server</span></span>
====================
<span data-ttu-id="bf7cf-105">によって[Hongye Sun](https://github.com/hongyes)、 [Praburaj Thiagarajan](https://github.com/Praburaj)、 [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="bf7cf-105">by [Hongye Sun](https://github.com/hongyes), [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="bf7cf-106">このチュートリアルでは、OAuth の OWIN ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-106">This tutorial will guide you on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span> <span data-ttu-id="bf7cf-107">これは、のみ OWIN OAuth 2.0 承認サーバーを作成する手順が説明されている高度なチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-107">This is an advanced tutorial that only outlines the steps to create an OWIN OAuth 2.0 Authorization Server.</span></span> <span data-ttu-id="bf7cf-108">これは、ステップ バイ ステップ チュートリアルではありません。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-108">This is not a step by step tutorial.</span></span> <span data-ttu-id="bf7cf-109">[サンプル コードをダウンロード](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip)です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-109">[Download the sample code](https://code.msdn.microsoft.com/OWIN-OAuth-20-Authorization-ba2b8783/file/114932/1/AuthorizationServer.zip).</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="bf7cf-110">このアウトラインは、セキュリティで保護された実稼働アプリケーションの作成に使用するものでありません必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-110">This outline should not be intended to be used for creating a secure production app.</span></span> <span data-ttu-id="bf7cf-111">このチュートリアルは、OAuth の OWIN ミドルウェアを使用して OAuth 2.0 承認サーバーを実装する方法について概要を提供するためのものです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-111">This tutorial is intended to provide only an outline on how to implement an OAuth 2.0 Authorization Server using OWIN OAuth middleware.</span></span>
> 
> 
> ## <a name="software-versions"></a><span data-ttu-id="bf7cf-112">ソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="bf7cf-112">Software versions</span></span>
> 
> | <span data-ttu-id="bf7cf-113">**このチュートリアルで示す**</span><span class="sxs-lookup"><span data-stu-id="bf7cf-113">**Shown in the tutorial**</span></span> | <span data-ttu-id="bf7cf-114">**でも動作します。**</span><span class="sxs-lookup"><span data-stu-id="bf7cf-114">**Also works with**</span></span> |
> | --- | --- |
> | <span data-ttu-id="bf7cf-115">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="bf7cf-115">Windows 8.1</span></span> | <span data-ttu-id="bf7cf-116">Windows 8、Windows 7</span><span class="sxs-lookup"><span data-stu-id="bf7cf-116">Windows 8, Windows 7</span></span> |
> | [<span data-ttu-id="bf7cf-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="bf7cf-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads) | <span data-ttu-id="bf7cf-118">[デスクトップの visual Studio 2013 Express](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express)です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-118">[Visual Studio 2013 Express for Desktop](https://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express).</span></span> <span data-ttu-id="bf7cf-119">Visual Studio 2012 と最新の更新プログラムの作業する必要がありますが、チュートリアルはこれを使ってテストされていないおよび一部のメニューやダイアログ ボックスが異なる。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-119">Visual Studio 2012 with the latest update should work, but the tutorial has not been tested with it, and some menu selections and dialog boxes are different.</span></span> |
> | <span data-ttu-id="bf7cf-120">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="bf7cf-120">.NET 4.5</span></span> |  |
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="bf7cf-121">質問やコメント</span><span class="sxs-lookup"><span data-stu-id="bf7cf-121">Questions and Comments</span></span>
> 
> <span data-ttu-id="bf7cf-122">チュートリアルに直接関連付けられていない質問がある場合でそれらを投稿[GitHub の Katana プロジェクト](https://github.com/aspnet/AspNetKatana/)です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-122">If you have questions that are not directly related to the tutorial, you can post them at [Katana Project on GitHub](https://github.com/aspnet/AspNetKatana/).</span></span> <span data-ttu-id="bf7cf-123">に関する質問やコメント自体、チュートリアル、ページの下部にあるコメント セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-123">For questions and comments regarding the tutorial itself, see the comments section at the bottom of the page.</span></span>


<span data-ttu-id="bf7cf-124">[OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) HTTP サービスへのアクセス制限を取得するサード パーティ製アプリを有効にします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-124">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="bf7cf-125">保護されたリソースにアクセスするリソース所有者の資格情報を使用する代わりに、クライアントはアクセス トークンを取得 (文字列は、特定のスコープ、有効期間、およびその他のアクセス属性を示す) です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-125">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="bf7cf-126">アクセス トークンは、リソースの所有者の承認をサード パーティ製のクライアントに、承認サーバーによって発行されます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-126">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="bf7cf-127">このチュートリアルを取り上げます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-127">This tutorial will cover:</span></span>

- <span data-ttu-id="bf7cf-128">次の 4 つの承認をサポートする承認サーバーを作成する方法は、付与タイプと更新トークン。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-128">How to create an authorization server to support four authorization grant types and refresh tokens:</span></span>
    - <span data-ttu-id="bf7cf-129">認証コード付与</span><span class="sxs-lookup"><span data-stu-id="bf7cf-129">Authorization code grant</span></span>
    - <span data-ttu-id="bf7cf-130">Implicit Grant</span><span class="sxs-lookup"><span data-stu-id="bf7cf-130">Implicit Grant</span></span>
    - <span data-ttu-id="bf7cf-131">リソース所有者のパスワード資格情報が付与</span><span class="sxs-lookup"><span data-stu-id="bf7cf-131">Resource Owner Password Credentials Grant</span></span>
    - <span data-ttu-id="bf7cf-132">クライアント資格情報が付与</span><span class="sxs-lookup"><span data-stu-id="bf7cf-132">Client Credentials Grant</span></span>
- <span data-ttu-id="bf7cf-133">アクセス トークンによって保護されているリソース サーバーを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-133">Creating a resource server which is protected by an access token.</span></span>
- <span data-ttu-id="bf7cf-134">OAuth 2.0 クライアントを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-134">Creating OAuth 2.0 clients.</span></span>

<a id="prerequisites"></a>
## <a name="prerequisites"></a><span data-ttu-id="bf7cf-135">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="bf7cf-135">Prerequisites</span></span>

- <span data-ttu-id="bf7cf-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) 、無料または[Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express)に示されているように、**ソフトウェア バージョン**ページの上部にあります。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-136">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-editions) or the free [Visual Studio Express 2013](https://www.microsoft.com/visualstudio/eng/downloads#d-2013-express), as indicated in **Software Versions** at the top of the page.</span></span>
- <span data-ttu-id="bf7cf-137">OWIN 熟知します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-137">Familiarity with OWIN.</span></span> <span data-ttu-id="bf7cf-138">参照してください[Katana プロジェクトの使用を開始する](https://msdn.microsoft.com/en-us/magazine/dn451439.aspx)と[OWIN および Katana 新](index.md)です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-138">See [Getting Started with the Katana Project](https://msdn.microsoft.com/en-us/magazine/dn451439.aspx) and [What's new in OWIN and Katana](index.md).</span></span>
- <span data-ttu-id="bf7cf-139">十分に理解[OAuth](http://tools.ietf.org/html/rfc6749)用語では、含む[ロール](http://tools.ietf.org/html/rfc6749#section-1.1)、[プロトコル フロー](http://tools.ietf.org/html/rfc6749#section-1.2)、および[Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3)です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-139">Familiarity with [OAuth](http://tools.ietf.org/html/rfc6749) terminology, including [Roles](http://tools.ietf.org/html/rfc6749#section-1.1), [Protocol Flow](http://tools.ietf.org/html/rfc6749#section-1.2), and [Authorization Grant](http://tools.ietf.org/html/rfc6749#section-1.3).</span></span> <span data-ttu-id="bf7cf-140">[OAuth 2.0 の概要](http://tools.ietf.org/html/rfc6749#section-1)の概要を提供します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-140">[OAuth 2.0 introduction](http://tools.ietf.org/html/rfc6749#section-1) provides a good introduction.</span></span>

## <a name="create-an-authorization-server"></a><span data-ttu-id="bf7cf-141">承認サーバーを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-141">Create an Authorization Server</span></span>

<span data-ttu-id="bf7cf-142">このチュートリアルではおはほぼスケッチを使用する方法を[OWIN](https://msdn.microsoft.com/en-us/magazine/dn451439.aspx)と ASP.NET MVC を承認サーバーを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-142">In this tutorial, we will roughly sketch out how to use [OWIN](https://msdn.microsoft.com/en-us/magazine/dn451439.aspx) and ASP.NET MVC to create an authorization server.</span></span> <span data-ttu-id="bf7cf-143">このチュートリアルでは、各手順は含まれません、すぐに、完成したサンプルのダウンロードを提供する予定です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-143">We hope to soon provide a download for the completed sample, as this tutorial does not include each step.</span></span> <span data-ttu-id="bf7cf-144">という名前の空の web アプリを最初に、作成*AuthorizationServer*し、次のパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-144">First, create an empty web app named *AuthorizationServer* and install the following packages:</span></span>

- <span data-ttu-id="bf7cf-145">Microsoft.AspNet.Mvc</span><span class="sxs-lookup"><span data-stu-id="bf7cf-145">Microsoft.AspNet.Mvc</span></span>
- <span data-ttu-id="bf7cf-146">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="bf7cf-146">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="bf7cf-147">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="bf7cf-147">Microsoft.Owin.Security.OAuth</span></span>
- <span data-ttu-id="bf7cf-148">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="bf7cf-148">Microsoft.Owin.Security.Cookies</span></span>
- <span data-ttu-id="bf7cf-149">Microsoft.Owin.Security.Google (その他のソーシャル ログインのパッケージまたは Microsoft.Owin.Security.Facebook など)</span><span class="sxs-lookup"><span data-stu-id="bf7cf-149">Microsoft.Owin.Security.Google (Or any other social login package such as Microsoft.Owin.Security.Facebook)</span></span>

<span data-ttu-id="bf7cf-150">追加、 [OWIN スタートアップ クラス](owin-startup-class-detection.md)という名前のプロジェクト ルート フォルダーの下にある*スタートアップ*です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-150">Add an [OWIN Startup class](owin-startup-class-detection.md) under the project root folder named *Startup*.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample1.cs?highlight=8)]

<span data-ttu-id="bf7cf-151">作成、*アプリ\_開始*フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-151">Create an *App\_Start* folder.</span></span> <span data-ttu-id="bf7cf-152">選択、*アプリ\_開始*フォルダーと、ダウンロードしたバージョンを追加するには Shift + Alt + A を使用して、 *AuthorizationServer\App\_Start\Startup.Auth.cs*ファイル。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-152">Select the *App\_Start* folder and use Shift+Alt+A to add the downloaded version of the *AuthorizationServer\App\_Start\Startup.Auth.cs* file.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample2.cs)]

<span data-ttu-id="bf7cf-153">上記のコードは、アプリケーション/外部サインインは cookie と Google の認証、承認サーバー自体によってアカウントを管理するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-153">The code above enables application/external sign in cookies and Google authentication, which are used by authorization server itself to manage accounts.</span></span>

<span data-ttu-id="bf7cf-154">`UseOAuthAuthorizationServer`拡張メソッドは、承認サーバーをセットアップします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-154">The `UseOAuthAuthorizationServer` extension method is to setup the authorization server.</span></span> <span data-ttu-id="bf7cf-155">セットアップのオプションは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-155">The setup options are:</span></span>

- <span data-ttu-id="bf7cf-156">`AuthorizeEndpointPath`: クライアント アプリケーションがユーザーを取得するために、ユーザー エージェントをリダイレクト場所の要求パス トークンまたはコードを発行することに同意します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-156">`AuthorizeEndpointPath`: The request path where client applications will redirect the user-agent in order to obtain the users consent to issue a token or code.</span></span> <span data-ttu-id="bf7cf-157">たとえば、先頭のスラッシュで始める必要があります"`/Authorize`"です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-157">It must begin with a leading slash, for example, "`/Authorize`".</span></span>
- <span data-ttu-id="bf7cf-158">`TokenEndpointPath`要求パスのクライアント アプリケーションは、アクセス トークンを取得する直接通信します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-158">`TokenEndpointPath`: The request path client applications directly communicate to obtain the access token.</span></span> <span data-ttu-id="bf7cf-159">これは、"/token"のように、先頭にスラッシュで始めなければなりません。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-159">It must begin with a leading slash, like "/Token".</span></span> <span data-ttu-id="bf7cf-160">クライアントが発行された場合は、[クライアント\_シークレット](http://tools.ietf.org/html/rfc6749#appendix-A.2)、このエンドポイントを指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-160">If the client is issued a [client\_secret](http://tools.ietf.org/html/rfc6749#appendix-A.2), it must be provided to this endpoint.</span></span>
- <span data-ttu-id="bf7cf-161">`ApplicationCanDisplayErrors`: に設定します。 `true` web アプリケーションが上のクライアント検証エラーのカスタム エラー ページを生成する場合は`/Authorize`エンドポイント。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-161">`ApplicationCanDisplayErrors`: Set to `true` if the web application wants to generate a custom error page for the client validation errors on `/Authorize` endpoint.</span></span> <span data-ttu-id="bf7cf-162">たとえばバックアップ、クライアント アプリケーションに、ブラウザーがリダイレクトでない場合にのみ必要です、ときに、`client_id`または`redirect_uri`が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-162">This is only needed for cases where the browser is not redirected back to the client application, for example, when the `client_id` or `redirect_uri` are incorrect.</span></span> <span data-ttu-id="bf7cf-163">`/Authorize`エンドポイントはず"oauth です。エラー"、"oauth です。ErrorDescription"、および"oauth です。ErrorUri"プロパティは、OWIN 環境に追加されます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-163">The `/Authorize` endpoint should expect to see the "oauth.Error", "oauth.ErrorDescription", and "oauth.ErrorUri" properties are added to the OWIN environment.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="bf7cf-164">以外の場合は true、承認サーバーは返しますエラーの詳細に既定のエラー ページ。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-164">If not true, the authorization server will return a default error page with the error details.</span></span>
- <span data-ttu-id="bf7cf-165">`AllowInsecureHttp`: True を承認し、HTTP URI アドレスに到着して、受信を許可するトークンが要求を許可する`redirect_uri`HTTP URI アドレスを持つ要求パラメーターを承認します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-165">`AllowInsecureHttp`: True to allow authorize and token requests to arrive on HTTP URI addresses, and to allow incoming `redirect_uri` authorize request parameters to have HTTP URI addresses.</span></span> 

    > [!WARNING]
    > <span data-ttu-id="bf7cf-166">セキュリティ - これは開発専用です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-166">Security - This is for development only.</span></span>
- <span data-ttu-id="bf7cf-167">`Provider`: 認証サーバー ミドルウェアによって発生したイベントを処理するアプリケーションによって提供されるオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-167">`Provider`: The object provided by the application to process events raised by the Authorization Server middleware.</span></span> <span data-ttu-id="bf7cf-168">アプリケーションが完全に実装するインターフェイス、またはのインスタンスを作成することがあります、 `OAuthAuthorizationServerProvider` OAuth フローがこのサーバーをサポートしているために必要なデリゲートを割り当てます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-168">The application may implement the interface fully, or it may create an instance of `OAuthAuthorizationServerProvider` and assign delegates necessary for the OAuth flows this server supports.</span></span>
- <span data-ttu-id="bf7cf-169">`AuthorizationCodeProvider`: クライアント アプリケーションに戻るには 1 回だけ認証コードを生成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-169">`AuthorizationCodeProvider`: Produces a single-use authorization code to return to the client application.</span></span> <span data-ttu-id="bf7cf-170">OAuth するサーバーには、アプリケーションをセキュリティで保護**必要があります**のインスタンスを提供`AuthorizationCodeProvider`によってトークンが生成される、`OnCreate/OnCreateAsync`イベントは 1 つだけの呼び出しの有効と見なされます`OnReceive/OnReceiveAsync`です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-170">For the OAuth server to be secure the application **MUST** provide an instance for `AuthorizationCodeProvider` where the token produced by the `OnCreate/OnCreateAsync` event is considered valid for only one call to `OnReceive/OnReceiveAsync`.</span></span>
- <span data-ttu-id="bf7cf-171">`RefreshTokenProvider`: 必要なときに、新しいアクセス トークンを生成するために使用できる更新トークンを生成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-171">`RefreshTokenProvider`: Produces a refresh token which may be used to produce a new access token when needed.</span></span> <span data-ttu-id="bf7cf-172">かどうかは指定されていない、承認サーバーは返されませんから更新トークン、`/Token`エンドポイント。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-172">If not provided the authorization server will not return refresh tokens from the `/Token` endpoint.</span></span>

## <a name="account-management"></a><span data-ttu-id="bf7cf-173">アカウント管理</span><span class="sxs-lookup"><span data-stu-id="bf7cf-173">Account Management</span></span>

<span data-ttu-id="bf7cf-174">OAuth はしないユーザー アカウント情報を管理する方法や場所を注意してください。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-174">OAuth doesn't care where or how you manage your user account information.</span></span> <span data-ttu-id="bf7cf-175">[ASP.NET Identity](../../../identity/index.md)はそれを担当します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-175">It's [ASP.NET Identity](../../../identity/index.md) which is responsible for it.</span></span> <span data-ttu-id="bf7cf-176">このチュートリアルではおをアカウント管理のコードを簡略化し、ユーザーがログインできる cookie の OWIN ミドルウェアを使用することを確認しておいてください。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-176">In this tutorial, we will simplify the account management code and just make sure that user can login using OWIN cookie middleware.</span></span> <span data-ttu-id="bf7cf-177">簡単なサンプル コードをここでは、 `AccountController`:</span><span class="sxs-lookup"><span data-stu-id="bf7cf-177">Here is the simplified sample code for the `AccountController`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample3.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample4.cs?highlight=1)]

<span data-ttu-id="bf7cf-178">`ValidateClientRedirectUri`登録されたリダイレクト URL を使用してクライアントの検証に使用されます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-178">`ValidateClientRedirectUri` is used to validate the client with its registered redirect URL.</span></span> <span data-ttu-id="bf7cf-179">`ValidateClientAuthentication`基本的なスキームのヘッダーとクライアントの資格情報を取得するフォームの本文を確認します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-179">`ValidateClientAuthentication` checks the basic scheme header and form body to get the client's credentials.</span></span>

<span data-ttu-id="bf7cf-180">ログイン ページは、次に示します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-180">The login page is shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image1.png)

<span data-ttu-id="bf7cf-181">確認、IETF の OAuth 2[認証コード付与](http://tools.ietf.org/html/rfc6749#section-4.1)セクションのようになりました。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-181">Review the IETF's OAuth 2 [Authorization Code Grant](http://tools.ietf.org/html/rfc6749#section-4.1) section now.</span></span> 

<span data-ttu-id="bf7cf-182">**プロバイダー** (次の表では) は[OAuthAuthorizationServerOptions](https://msdn.microsoft.com/en-us/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx)です。型プロバイダー `OAuthAuthorizationServerProvider`、OAuth サーバーのすべてのイベントが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-182">**Provider** (in the table below) is [OAuthAuthorizationServerOptions](https://msdn.microsoft.com/en-us/library/microsoft.owin.security.oauth.oauthauthorizationserveroptions(v=vs.111).aspx).Provider, which is of type `OAuthAuthorizationServerProvider`, which contains all OAuth server events.</span></span> 

| <span data-ttu-id="bf7cf-183">認証コード付与セクションからフロー手順</span><span class="sxs-lookup"><span data-stu-id="bf7cf-183">Flow steps from Authorization Code Grant section</span></span> | <span data-ttu-id="bf7cf-184">ダウンロードしたサンプルで上記の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-184">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="bf7cf-185">(A)、クライアントは、リソースの所有者のユーザー エージェントを承認エンドポイントにダイレクトすることで、フローを開始します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-185">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="bf7cf-186">クライアントには、クライアント識別子、要求のスコープ、ローカルの状態、および承認サーバーが送信するユーザー エージェント アクセスを許可 (または拒否) 後のリダイレクト URI が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-186">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="bf7cf-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="bf7cf-187">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-188">(B)、承認サーバーは、(ユーザー エージェント) 経由でリソースの所有者を認証し、リソースの所有者が許可されたり、クライアントのアクセス要求を拒否するかどうかを確立します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-188">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="bf7cf-189">**&lt;ユーザー アクセスを許可する場合&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="bf7cf-189">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-190">(承認サーバーは、リダイレクト URI を使用して、クライアントにユーザー エージェントをリダイレクト、アクセスを許可 C) リソースの所有者と仮定した場合 (要求またはクライアントの登録中に) 以前です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-190">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="bf7cf-191">...</span><span class="sxs-lookup"><span data-stu-id="bf7cf-191">...</span></span> |  |
|  |  |
| <span data-ttu-id="bf7cf-192">(D)、クライアントは、前の手順で受信した認証コードを含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-192">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="bf7cf-193">要求を行うときに、クライアントは承認サーバーに対して認証します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-193">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="bf7cf-194">クライアントには、URI 検証のための認証コードを取得するために使用するリダイレクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-194">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> | <span data-ttu-id="bf7cf-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsyncRefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="bf7cf-195">Provider.MatchEndpoint Provider.ValidateClientAuthentication AuthorizationCodeProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantAuthorizationCode Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |

<span data-ttu-id="bf7cf-196">実装サンプル`AuthorizationCodeProvider.CreateAsync`と`ReceiveAsync`を作成し、認証コードの検証の制御を次に示します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-196">A sample implementation for `AuthorizationCodeProvider.CreateAsync` and `ReceiveAsync` to control the creation and validation of authorization code is shown below.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample5.cs)]

<span data-ttu-id="bf7cf-197">上記のコードは、コードと id のチケットを格納およびコードが表示されたら、id を復元するメモリ内の同時実行ディクショナリを使用します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-197">The code above uses an in-memory concurrent dictionary to store the code and identity ticket and restore the identity after receiving the code.</span></span> <span data-ttu-id="bf7cf-198">実際のアプリケーションで、永続的なデータ ストアで置き換えられますなります。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-198">In a real application, it would be replaced by a persistent data store.</span></span> <span data-ttu-id="bf7cf-199">承認エンドポイントでは、クライアントへのアクセス許可をリソース所有者のです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-199">The authorization endpoint is for the resource owner to grant access to the client.</span></span> <span data-ttu-id="bf7cf-200">通常、ユーザーがボタンをクリックし、許可を確認できるようにするユーザー インターフェイスが必要です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-200">Usually, it needs a user interface to allow the user to click a button and confirm the grant.</span></span> <span data-ttu-id="bf7cf-201">OAuth の OWIN ミドルウェアは、承認エンドポイントを処理するアプリケーション コードを許可します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-201">OWIN OAuth middleware allows application code to handle the authorization endpoint.</span></span> <span data-ttu-id="bf7cf-202">呼ばれる MVC コント ローラーを使用するアプリでは、サンプル、お`OAuthController`それを処理します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-202">In our sample app, we use an MVC controller called `OAuthController` to handle it.</span></span> <span data-ttu-id="bf7cf-203">次に、サンプルの実装を示します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-203">Here is the sample implementation:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample6.cs?highlight=15)]

<span data-ttu-id="bf7cf-204">`Authorize`アクションのかどうか、ユーザーがログイン承認サーバーはまずチェックします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-204">The `Authorize` action will first check if the user has logged in to the authorization server.</span></span> <span data-ttu-id="bf7cf-205">ない場合、認証ミドルウェアが"Application"の cookie を使用して認証を呼び出し元の課題をし、ログイン ページにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-205">If not, the authentication middleware challenges the caller to authenticate using the "Application" cookie and redirects to the login page.</span></span> <span data-ttu-id="bf7cf-206">(上記の強調表示されたコードを参照してください)。ユーザー ログインしている場合は、次のように、Authorize ビューを表示します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-206">(See highlighted code above.) If user has logged in, it will render the Authorize view, as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image2.png)

<span data-ttu-id="bf7cf-207">場合、 **Grant**ボタンが選択されている、`Authorize`アクションは、新しい"Bearer"の id とそれを使用してサインインを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-207">If the **Grant** button is selected, the `Authorize` action will create a new "Bearer" identity and sign in with it.</span></span> <span data-ttu-id="bf7cf-208">ベアラー トークンを生成し、JSON ペイロードでクライアントに送信する承認サーバーがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-208">It will trigger the authorization server to generate a bearer token and send it back to the client with JSON payload.</span></span> 

### <a name="implicit-grant"></a><span data-ttu-id="bf7cf-209">Implicit Grant</span><span class="sxs-lookup"><span data-stu-id="bf7cf-209">Implicit Grant</span></span>

<span data-ttu-id="bf7cf-210">IETF の OAuth 2 を参照してください[Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2)セクションのようになりました。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-210">Refer to the IETF's OAuth 2 [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) section now.</span></span>

 <span data-ttu-id="bf7cf-211">[Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2)図 4 に示すフローは次のフローとマッピングする OWIN OAuth ミドルウェアに依存します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-211">The [Implicit Grant](http://tools.ietf.org/html/rfc6749#section-4.2) flow shown in Figure 4 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="bf7cf-212">Implicit Grant セクションからフロー手順</span><span class="sxs-lookup"><span data-stu-id="bf7cf-212">Flow steps from Implicit Grant section</span></span> | <span data-ttu-id="bf7cf-213">ダウンロードしたサンプルで上記の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-213">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="bf7cf-214">(A)、クライアントは、リソースの所有者のユーザー エージェントを承認エンドポイントにダイレクトすることで、フローを開始します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-214">(A) The client initiates the flow by directing the resource owner's user-agent to the authorization endpoint.</span></span> <span data-ttu-id="bf7cf-215">クライアントには、クライアント識別子、要求のスコープ、ローカルの状態、および承認サーバーが送信するユーザー エージェント アクセスを許可 (または拒否) 後のリダイレクト URI が含まれています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-215">The client includes its client identifier, requested scope, local state, and a redirection URI to which the authorization server will send the user-agent back once access is granted (or denied).</span></span> | <span data-ttu-id="bf7cf-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span><span class="sxs-lookup"><span data-stu-id="bf7cf-216">Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-217">(B)、承認サーバーは、(ユーザー エージェント) 経由でリソースの所有者を認証し、リソースの所有者が許可されたり、クライアントのアクセス要求を拒否するかどうかを確立します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-217">(B) The authorization server authenticates the resource owner (via the user-agent) and establishes whether the resource owner grants or denies the client's access request.</span></span> | <span data-ttu-id="bf7cf-218">**&lt;ユーザー アクセスを許可する場合&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="bf7cf-218">**&lt;If user grants access&gt;** Provider.MatchEndpoint Provider.ValidateClientRedirectUri Provider.ValidateAuthorizeRequest Provider.AuthorizeEndpoint AuthorizationCodeProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-219">(承認サーバーは、リダイレクト URI を使用して、クライアントにユーザー エージェントをリダイレクト、アクセスを許可 C) リソースの所有者と仮定した場合 (要求またはクライアントの登録中に) 以前です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-219">(C) Assuming the resource owner grants access, the authorization server redirects the user-agent back to the client using the redirection URI provided earlier (in the request or during client registration).</span></span> <span data-ttu-id="bf7cf-220">...</span><span class="sxs-lookup"><span data-stu-id="bf7cf-220">...</span></span> |  |
|  |  |
| <span data-ttu-id="bf7cf-221">(D)、クライアントは、前の手順で受信した認証コードを含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-221">(D) The client requests an access token from the authorization server's token endpoint by including the authorization code received in the previous step.</span></span> <span data-ttu-id="bf7cf-222">要求を行うときに、クライアントは承認サーバーに対して認証します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-222">When making the request, the client authenticates with the authorization server.</span></span> <span data-ttu-id="bf7cf-223">クライアントには、URI 検証のための認証コードを取得するために使用するリダイレクトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-223">The client includes the redirection URI used to obtain the authorization code for verification.</span></span> |  |

<span data-ttu-id="bf7cf-224">承認エンドポイントは既に実装されているため (`OAuthController.Authorize`アクション) の認証コード付与が自動的に有効に暗黙のフローもです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-224">Since we already implemented the authorization endpoint (`OAuthController.Authorize` action) for authorization code grant, it automatically enables implicit flow as well.</span></span> <span data-ttu-id="bf7cf-225">注: `Provider.ValidateClientRedirectUri` 、リダイレクト URL は、送信、アクセス トークンを悪意のあるクライアントからの暗黙的な付与フローを保護すると、クライアント ID の検証に使用されます ([仲介で攻撃](https://www.owasp.org/index.php/Man-in-the-middle_attack))。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-225">Note: `Provider.ValidateClientRedirectUri` is used to validate the client ID with its redirection URL, which protects the implicit grant flow from sending the access token to malicious clients ([Man-in-the-middle attack](https://www.owasp.org/index.php/Man-in-the-middle_attack)).</span></span>

### <a name="resource-owner-password-credentials-grant"></a><span data-ttu-id="bf7cf-226">リソース所有者のパスワード資格情報が付与</span><span class="sxs-lookup"><span data-stu-id="bf7cf-226">Resource Owner Password Credentials Grant</span></span>

<span data-ttu-id="bf7cf-227">IETF の OAuth 2 を参照してください[リソース所有者のパスワード資格情報の付与](http://tools.ietf.org/html/rfc6749#section-4.3)セクションのようになりました。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-227">Refer to the IETF's OAuth 2 [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) section now.</span></span>

 <span data-ttu-id="bf7cf-228">[リソース所有者のパスワード資格情報の付与](http://tools.ietf.org/html/rfc6749#section-4.3)フロー図 5 に示すように、フローは、ミドルウェアに依存する OWIN OAuth をマッピングします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-228">The [Resource Owner Password Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.3) flow shown in Figure 5 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="bf7cf-229">リソース所有者のパスワード資格情報の付与 セクションからフロー手順</span><span class="sxs-lookup"><span data-stu-id="bf7cf-229">Flow steps from Resource Owner Password Credentials Grant section</span></span> | <span data-ttu-id="bf7cf-230">ダウンロードしたサンプルで上記の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-230">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="bf7cf-231">(A) リソースの所有者のユーザー名とパスワードをクライアントに提供します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-231">(A) The resource owner provides the client with its username and password.</span></span> |  |
|  |  |
| <span data-ttu-id="bf7cf-232">(B)、クライアントは、リソースの所有者から受信した資格情報を含めることによって、承認サーバーのトークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-232">(B) The client requests an access token from the authorization server's token endpoint by including the credentials received from the resource owner.</span></span> <span data-ttu-id="bf7cf-233">要求を行うときに、クライアントは承認サーバーに対して認証します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-233">When making the request, the client authenticates with the authorization server.</span></span> | <span data-ttu-id="bf7cf-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="bf7cf-234">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantResourceOwnerCredentials Provider.TokenEndpoint AccessToken Provider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-235">(C)、承認サーバーは、クライアントを認証およびリソース所有者の資格情報を検証し、有効な場合は、アクセス トークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-235">(C) The authorization server authenticates the client and validates the resource owner credentials, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="bf7cf-236">実装のサンプルを次に示します`Provider.GrantResourceOwnerCredentials`:</span><span class="sxs-lookup"><span data-stu-id="bf7cf-236">Here is the sample implementation for `Provider.GrantResourceOwnerCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample7.cs)]

> [!NOTE]
> <span data-ttu-id="bf7cf-237">上記のコードは、チュートリアルのこのセクションで説明するためのものし、安全では使用できませんまたは運用アプリ。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-237">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="bf7cf-238">リソース所有者の資格情報はチェックされません。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-238">It does not check the resource owners credentials.</span></span> <span data-ttu-id="bf7cf-239">すべての資格情報は有効であり、そのため、新しい id の作成と見なします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-239">It assumes every credential is valid and creates a new identity for it.</span></span> <span data-ttu-id="bf7cf-240">新しい id がアクセス トークンを生成し、更新トークンに使用されます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-240">The new identity will be used to generate the access token and refresh token.</span></span> <span data-ttu-id="bf7cf-241">セキュリティで保護されたアカウント管理コードには、コードに置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-241">Please replace the code with your own secure account management code.</span></span>


### <a name="client-credentials-grant"></a><span data-ttu-id="bf7cf-242">クライアント資格情報が付与</span><span class="sxs-lookup"><span data-stu-id="bf7cf-242">Client Credentials Grant</span></span>

<span data-ttu-id="bf7cf-243">IETF の OAuth 2 を参照してください[Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4)セクションのようになりました。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-243">Refer to the IETF's OAuth 2 [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) section now.</span></span>

 <span data-ttu-id="bf7cf-244">[Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4)フロー図 6 に示すように、フローは、OWIN OAuth をマッピングするミドルウェアに依存します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-244">The [Client Credentials Grant](http://tools.ietf.org/html/rfc6749#section-4.4) flow shown in Figure 6 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="bf7cf-245">クライアント資格情報の付与 セクションからフロー手順</span><span class="sxs-lookup"><span data-stu-id="bf7cf-245">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="bf7cf-246">ダウンロードしたサンプルで上記の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-246">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="bf7cf-247">(A)、クライアントは承認サーバーに対して認証し、トークン エンドポイントからアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-247">(A) The client authenticates with the authorization server and requests an access token from the token endpoint.</span></span> | <span data-ttu-id="bf7cf-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="bf7cf-248">Provider.MatchEndpoint Provider.ValidateClientAuthentication Provider.ValidateTokenRequest Provider.GrantClientCredentials Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-249">(B)、承認サーバーは、クライアントを認証し、有効な場合は、アクセス トークンを発行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-249">(B) The authorization server authenticates the client, and if valid, issues an access token.</span></span> |  |

<span data-ttu-id="bf7cf-250">実装のサンプルを次に示します`Provider.GrantClientCredentials`:</span><span class="sxs-lookup"><span data-stu-id="bf7cf-250">Here is the sample implementation for `Provider.GrantClientCredentials`:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="bf7cf-251">上記のコードは、チュートリアルのこのセクションで説明するためのものし、安全では使用できませんまたは運用アプリ。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-251">The code above is intended to explain this section of the tutorial and should not be used in secure or production apps.</span></span> <span data-ttu-id="bf7cf-252">セキュリティで保護されたクライアント管理コードには、コードに置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-252">Please replace the code with your own secure client management code.</span></span>


### <a name="refresh-token"></a><span data-ttu-id="bf7cf-253">更新トークン</span><span class="sxs-lookup"><span data-stu-id="bf7cf-253">Refresh Token</span></span>

<span data-ttu-id="bf7cf-254">IETF の OAuth 2 を参照してください[更新トークン](http://tools.ietf.org/html/rfc6749#section-1.5)セクションのようになりました。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-254">Refer to the IETF's OAuth 2 [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) section now.</span></span>

 <span data-ttu-id="bf7cf-255">[更新トークン](http://tools.ietf.org/html/rfc6749#section-1.5)フロー図 2 に示すように、フローは、OWIN OAuth をマッピングするミドルウェアに依存します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-255">The [Refresh Token](http://tools.ietf.org/html/rfc6749#section-1.5) flow shown in Figure 2 is the flow and mapping which the OWIN OAuth middleware follows.</span></span>  

| <span data-ttu-id="bf7cf-256">クライアント資格情報の付与 セクションからフロー手順</span><span class="sxs-lookup"><span data-stu-id="bf7cf-256">Flow steps from Client Credentials Grant section</span></span> | <span data-ttu-id="bf7cf-257">ダウンロードしたサンプルで上記の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-257">Sample download performs these steps with:</span></span> |
| --- | --- |
|  |  |
| <span data-ttu-id="bf7cf-258">(G)、クライアントは、承認サーバーによる認証方法と更新トークンを提示して、新しいアクセス トークンを要求します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-258">(G) The client requests a new access token by authenticating with the authorization server and presenting the refresh token.</span></span> <span data-ttu-id="bf7cf-259">クライアントの認証要件は、サーバーの承認ポリシーとクライアントの種類に基づいています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-259">The client authentication requirements are based on the client type and on the authorization server policies.</span></span> | <span data-ttu-id="bf7cf-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsyncRefreshTokenProvider.CreateAsync</span><span class="sxs-lookup"><span data-stu-id="bf7cf-260">Provider.MatchEndpoint Provider.ValidateClientAuthentication RefreshTokenProvider.ReceiveAsync Provider.ValidateTokenRequest Provider.GrantRefreshToken Provider.TokenEndpoint AccessTokenProvider.CreateAsync RefreshTokenProvider.CreateAsync</span></span> |
|  |  |
| <span data-ttu-id="bf7cf-261">(H)、承認サーバーは、クライアントを認証し更新トークンを検証し、有効な場合が、新しいアクセス トークン (および、必要に応じて、新しい更新トークン) を発行します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-261">(H) The authorization server authenticates the client and validates the refresh token, and if valid, issues a new access token (and, optionally, a new refresh token).</span></span> |  |

<span data-ttu-id="bf7cf-262">実装のサンプルを次に示します`Provider.GrantRefreshToken`:</span><span class="sxs-lookup"><span data-stu-id="bf7cf-262">Here is the sample implementation for `Provider.GrantRefreshToken`:</span></span> 

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample9.cs)]

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample10.cs)]

## <a name="create-a-resource-server-which-is-protected-by-access-token"></a><span data-ttu-id="bf7cf-263">アクセス トークンで保護されているリソース サーバーを作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-263">Create a Resource Server which is protected by Access Token</span></span>

<span data-ttu-id="bf7cf-264">空の web アプリ プロジェクトを作成し、次のプロジェクト内のパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-264">Create an empty web app project and install following packages in the project:</span></span>

- <span data-ttu-id="bf7cf-265">Microsoft.AspNet.WebApi.Owin</span><span class="sxs-lookup"><span data-stu-id="bf7cf-265">Microsoft.AspNet.WebApi.Owin</span></span>
- <span data-ttu-id="bf7cf-266">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="bf7cf-266">Microsoft.Owin.Host.SystemWeb</span></span>
- <span data-ttu-id="bf7cf-267">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="bf7cf-267">Microsoft.Owin.Security.OAuth</span></span>

<span data-ttu-id="bf7cf-268">スタートアップ クラスを作成し、認証および Web API を構成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-268">Create a startup class and configure authentication and Web API.</span></span> <span data-ttu-id="bf7cf-269">参照してください*AuthorizationServer\ResourceServer\Startup.cs*サンプル ダウンロードにします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-269">See *AuthorizationServer\ResourceServer\Startup.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample11.cs)]

<span data-ttu-id="bf7cf-270">参照してください*AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs*サンプル ダウンロードにします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-270">See *AuthorizationServer\ResourceServer\App\_Start\Startup.Auth.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample12.cs)]

<span data-ttu-id="bf7cf-271">参照してください*AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs*サンプル ダウンロードにします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-271">See *AuthorizationServer\ResourceServer\App\_Start\Startup.WebApi.cs* in the sample download.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample13.cs)]

- <span data-ttu-id="bf7cf-272">`UseCors`メソッドは、すべてのドメインに対して CORS を使用します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-272">`UseCors` method allows CORS for all domains.</span></span>
- <span data-ttu-id="bf7cf-273">`UseOAuthBearerAuthentication`メソッドは、OAuth ベアラー トークンの認証ミドルウェアを受信し、要求の承認ヘッダーからベアラー トークンを検証できます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-273">`UseOAuthBearerAuthentication` method enables OAuth bearer token authentication middleware which will receive and validate bearer token from authorization header in the request.</span></span>
- <span data-ttu-id="bf7cf-274">`Config.SuppressDefaultHostAuthenticaiton`既定値を非表示のアプリからの認証されたプリンシパルをホストするため、すべての要求がされる匿名この呼び出しの後です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-274">`Config.SuppressDefaultHostAuthenticaiton` suppresses default host authenticated principal from the app, therefore all requests will be anonymous after this call.</span></span>
- <span data-ttu-id="bf7cf-275">`HostAuthenticationFilter`だけ、指定した認証の種類の認証を有効にします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-275">`HostAuthenticationFilter` enables authentication just for the specified authentication type.</span></span> <span data-ttu-id="bf7cf-276">この例では、ベアラー認証の種類を勧めします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-276">In this case, it's bearer authentication type.</span></span>

<span data-ttu-id="bf7cf-277">認証済み id を示すためには、するためには、現在のユーザーの信頼性情報を出力する、ApiController を作成します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-277">In order to demonstrate the authenticated identity, we create an ApiController to output current user's claims.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample14.cs)]

<span data-ttu-id="bf7cf-278">承認サーバーと、リソース サーバーが同じコンピューター上にない場合は、OAuth ミドルウェア キーを使用して、別のコンピューターの暗号化し、ベアラー アクセス トークンの暗号化を解除します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-278">If the authorization server and the resource server are not on the same computer, the OAuth middleware will use the different machine keys to encrypt and decrypt bearer access token.</span></span> <span data-ttu-id="bf7cf-279">同じ両方のプロジェクト間での同じ秘密キーを共有するために追加して`machinekey`両方で設定*web.config*ファイル。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-279">In order to share the same private key between both projects, we add the same `machinekey` setting in both *web.config* files.</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample15.xml?highlight=8-10)]

## <a name="create-oauth-20-clients"></a><span data-ttu-id="bf7cf-280">OAuth 2.0 クライアントを作成されます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-280">Create OAuth 2.0 Clients</span></span>

 <span data-ttu-id="bf7cf-281">使用して、 [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet パッケージをクライアント コードを簡略化します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-281">We use the [DotNetOpenAuth.OAuth2.Client](http://www.nuget.org/packages/DotNetOpenAuth.OAuth2.Client) NuGet package to simplify the client code.</span></span>

### <a name="authorization-code-grant-client"></a><span data-ttu-id="bf7cf-282">認証コード Grant クライアント</span><span class="sxs-lookup"><span data-stu-id="bf7cf-282">Authorization Code Grant Client</span></span>

 <span data-ttu-id="bf7cf-283">このクライアントは、MVC アプリケーションです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-283">This client is an MVC application.</span></span> <span data-ttu-id="bf7cf-284">バックエンドからアクセス トークンを取得するには、認証コード付与フローがトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-284">It will trigger an authorization code grant flow to get the access token from backend.</span></span> <span data-ttu-id="bf7cf-285">次のように 1 つのページがあります。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-285">It has a single page as shown below:</span></span>

![](owin-oauth-20-authorization-server/_static/image3.png)

- <span data-ttu-id="bf7cf-286">**Authorize**ボタンがブラウザーをクライアントへのアクセス許可をリソース所有者に通知する承認サーバーにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-286">The **Authorize** button will redirect browser to the authorization server to notify the resource owner to grant access to this client.</span></span>
- <span data-ttu-id="bf7cf-287">**更新**ボタンはトークンを取得する、新しいアクセス トークンと更新トークンが現在の更新を使用します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-287">The **Refresh** button will get a new access token and refresh token using the current refresh token.</span></span>
- <span data-ttu-id="bf7cf-288">**アクセス保護されたリソースの API**ボタンは、リソース サーバーを現在のユーザーの信頼性情報データを取得し、ページに表示することを呼び出します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-288">The **Access Protected Resource API** button will call the resource server to get current user's claims data and show them on the page.</span></span>

<span data-ttu-id="bf7cf-289">サンプル コードをここでは、`HomeController`クライアントのです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-289">Here is the sample code of the `HomeController` of the client.</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample16.cs)]

<span data-ttu-id="bf7cf-290">`DotNetOpenAuth`既定では SSL が必要です。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-290">`DotNetOpenAuth` requires SSL by default.</span></span> <span data-ttu-id="bf7cf-291">追加する必要がありますので、このデモは、HTTP を使用して、次の構成ファイルに設定します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-291">Since our demo is using HTTP, you need to add following setting in the config file:</span></span>

[!code-xml[Main](owin-oauth-20-authorization-server/samples/sample17.xml?highlight=4-6)]

> [!WARNING]
> <span data-ttu-id="bf7cf-292">セキュリティの運用アプリケーションで無効 SSL ことはありません。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-292">Security - Never disable SSL in a production app.</span></span> <span data-ttu-id="bf7cf-293">ネットワーク経由で、クリア テキストで、ログイン資格情報を送信されているようになりましたされます。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-293">Your login credentials are now being sent in clear-text across the wire.</span></span> <span data-ttu-id="bf7cf-294">上記のコードでは、ローカルのサンプルのデバッグと探索についてのみです。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-294">The code above is just for local sample debugging and exploration.</span></span>


### <a name="implicit-grant-client"></a><span data-ttu-id="bf7cf-295">暗黙の Grant クライアント</span><span class="sxs-lookup"><span data-stu-id="bf7cf-295">Implicit Grant Client</span></span>

<span data-ttu-id="bf7cf-296">このクライアントは、JavaScript を使用してください。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-296">This client is using JavaScript to:</span></span>

1. <span data-ttu-id="bf7cf-297">新しいウィンドウを開き、承認サーバーの承認エンドポイントにリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-297">Open a new window and redirect to the authorize endpoint of the Authorization Server.</span></span>
2. <span data-ttu-id="bf7cf-298">アクセス トークンを取得 URL フラグメントから戻るリダイレクト時にします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-298">Get the access token from URL fragments when it redirects back.</span></span>

<span data-ttu-id="bf7cf-299">次の図は、このプロセスを示しています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-299">The following image shows this process:</span></span>

![](owin-oauth-20-authorization-server/_static/image4.png)

<span data-ttu-id="bf7cf-300">クライアントが 2 つのページにある必要があります。 ホーム ページで、コールバックのもう 1 つです。サンプルの JavaScript コードをここでは、 *Index.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-300">The client should have two pages: one for home page and the other for callback.Here is the sample JavaScript code found in the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample18.cshtml)]

<span data-ttu-id="bf7cf-301">ここでは、処理コードでコールバック*SignIn.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-301">Here is the callback handling code in *SignIn.cshtml* file:</span></span>

[!code-cshtml[Main](owin-oauth-20-authorization-server/samples/sample19.cshtml)]

> [!NOTE]
> <span data-ttu-id="bf7cf-302">JavaScript を外部ファイルに移動し、Razor のマークアップを組み込まないことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-302">A best practice is to move the JavaScript to an external file and not embed it with the Razor markup.</span></span> <span data-ttu-id="bf7cf-303">このサンプルをシンプルにするには、統合されました。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-303">To keep this sample simple, they have been combined.</span></span>


### <a name="resource-owner-password-credentials-grant-client"></a><span data-ttu-id="bf7cf-304">リソース所有者のパスワード許可クライアントの資格情報します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-304">Resource Owner Password Credentials Grant Client</span></span>

<span data-ttu-id="bf7cf-305">このクライアントをデモするコンソール アプリを使用しています。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-305">We uses a console app to demo this client.</span></span> <span data-ttu-id="bf7cf-306">コードを次に示します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-306">Here is the code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample20.cs)]

### <a name="client-credentials-grant-client"></a><span data-ttu-id="bf7cf-307">クライアント資格情報の付与クライアント</span><span class="sxs-lookup"><span data-stu-id="bf7cf-307">Client Credentials Grant Client</span></span>

<span data-ttu-id="bf7cf-308">リソース所有者のパスワード資格情報の付与と同様の場合、次に、コンソール アプリのコードを示します。</span><span class="sxs-lookup"><span data-stu-id="bf7cf-308">Similar to the Resource Owner Password Credentials Grant, here is console app code:</span></span>

[!code-csharp[Main](owin-oauth-20-authorization-server/samples/sample21.cs)]