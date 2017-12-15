---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: "ASP.NET Web ページ - 作業の開始の概要 |Microsoft ドキュメント"
author: tfitzmac
description: "WebMatrix は推奨されなくなりました統合開発環境として ASP.NET Web Pages のです。 Visual Studio または Visual Studio のコードを使用します。 このガイドにしています."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 615ddc31d0d857e5bf9a7f372b7efcf67d185905
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2017
---
<a name="introducing-aspnet-web-pages---getting-started"></a><span data-ttu-id="211ad-105">ASP.NET Web ページ - 作業の開始の概要</span><span class="sxs-lookup"><span data-stu-id="211ad-105">Introducing ASP.NET Web Pages - Getting Started</span></span>
====================
<span data-ttu-id="211ad-106">によって[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="211ad-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> > [!NOTE] 
> > 
> > <span data-ttu-id="211ad-107">WebMatrix は推奨されなくなりました統合開発環境として ASP.NET Web Pages のです。</span><span class="sxs-lookup"><span data-stu-id="211ad-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="211ad-108">使用して[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md)または[Visual Studio Code](https://code.visualstudio.com/)です。</span><span class="sxs-lookup"><span data-stu-id="211ad-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="211ad-109">このガイダンスとアプリケーションには、ASP.NET Web Pages (バージョン 2 またはそれ以降) の概要と Razor 構文を動的な web サイトを作成するための軽量なフレームワーク。</span><span class="sxs-lookup"><span data-stu-id="211ad-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="211ad-110">また、WebMatrix、ページとサイトを作成するためのツールを紹介します。</span><span class="sxs-lookup"><span data-stu-id="211ad-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="211ad-111">**レベル**: ASP.NET Web ページに新しいです。</span><span class="sxs-lookup"><span data-stu-id="211ad-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="211ad-112">**スキルと見なされます**: HTML、基本的なカスケード スタイル シート (CSS)。</span><span class="sxs-lookup"><span data-stu-id="211ad-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="211ad-113">学習する内容のセットの最初のチュートリアルで。</span><span class="sxs-lookup"><span data-stu-id="211ad-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="211ad-114">どのような ASP.NET Web Pages テクノロジし、何ができます。</span><span class="sxs-lookup"><span data-stu-id="211ad-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="211ad-115">WebMatrix です。</span><span class="sxs-lookup"><span data-stu-id="211ad-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="211ad-116">すべてをインストールする方法。</span><span class="sxs-lookup"><span data-stu-id="211ad-116">How to install everything.</span></span>
> - <span data-ttu-id="211ad-117">WebMatrix を使用して、web サイトを作成する方法。</span><span class="sxs-lookup"><span data-stu-id="211ad-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="211ad-118">説明されている機能/テクノロジ:</span><span class="sxs-lookup"><span data-stu-id="211ad-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="211ad-119">Microsoft Web Platform Installer です。</span><span class="sxs-lookup"><span data-stu-id="211ad-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="211ad-120">WebMatrix です。</span><span class="sxs-lookup"><span data-stu-id="211ad-120">WebMatrix.</span></span>
> - <span data-ttu-id="211ad-121">*.cshtml*ページ</span><span class="sxs-lookup"><span data-stu-id="211ad-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="211ad-122">最初、Mike 教皇は、このチュートリアルを書き込みました。</span><span class="sxs-lookup"><span data-stu-id="211ad-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="211ad-123">Tom FitzMacken Microsoft WebMatrix 3 を更新します。</span><span class="sxs-lookup"><span data-stu-id="211ad-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="211ad-124">このチュートリアルで使用されているソフトウェアのバージョン</span><span class="sxs-lookup"><span data-stu-id="211ad-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="211ad-125">ASP.NET Web Pages (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="211ad-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="211ad-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="211ad-126">WebMatrix 3</span></span>


## <a name="what-should-you-know"></a><span data-ttu-id="211ad-127">必要な知識</span><span class="sxs-lookup"><span data-stu-id="211ad-127">What Should You Know?</span></span>

<span data-ttu-id="211ad-128">慣れているものと仮定します。</span><span class="sxs-lookup"><span data-stu-id="211ad-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="211ad-129">**HTML**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-129">**HTML**.</span></span> <span data-ttu-id="211ad-130">深い専門知識は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="211ad-130">No in-depth expertise is required.</span></span> <span data-ttu-id="211ad-131">HTML、については説明しませんが、私たちもないものを使用して複雑です。</span><span class="sxs-lookup"><span data-stu-id="211ad-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="211ad-132">便利思います HTML チュートリアルへのリンクを提供します。</span><span class="sxs-lookup"><span data-stu-id="211ad-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="211ad-133">**カスケード スタイル シート (CSS)**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="211ad-134">同じ html です。</span><span class="sxs-lookup"><span data-stu-id="211ad-134">Same as with HTML.</span></span>
- <span data-ttu-id="211ad-135">**基本的なデータベース アイデア**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-135">**Basic database ideas**.</span></span> <span data-ttu-id="211ad-136">データのスプレッドシートを使用し、並べ替えを専門知識のレベルにあるデータをフィルター処理した場合、このチュートリアルのセットの仮定一般にします。</span><span class="sxs-lookup"><span data-stu-id="211ad-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="211ad-137">基本的なプログラミングの学習に該当するものもと仮定します。</span><span class="sxs-lookup"><span data-stu-id="211ad-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="211ad-138">ASP.NET Web ページは、c# と呼ばれるプログラミング言語を使用します。</span><span class="sxs-lookup"><span data-stu-id="211ad-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="211ad-139">任意の背景に関係するだけのプログラミングではありません。</span><span class="sxs-lookup"><span data-stu-id="211ad-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="211ad-140">前に web ページで、JavaScript を作成したこと場合、は、バック グラウンドの十分なを取得したらです。</span><span class="sxs-lookup"><span data-stu-id="211ad-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="211ad-141">プログラミングに慣れている場合、このチュートリアルを最初に設定動かさ緩やかに変化速度は新しいプログラマがもたらさありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="211ad-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="211ad-142">過去の最初のいくつかのチュートリアルにつれて、ただしを説明する小さい基本的なプログラミングおよびする処理が高速のクリップにに沿って移動されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="211ad-143">何が必要ですか。</span><span class="sxs-lookup"><span data-stu-id="211ad-143">What Do You Need?</span></span>

<span data-ttu-id="211ad-144">必要なもの:</span><span class="sxs-lookup"><span data-stu-id="211ad-144">Here's what you'll need:</span></span>

- <span data-ttu-id="211ad-145">Windows 8、Windows 7、Windows Server 2008、または Windows Server 2012 を実行しているコンピューター。</span><span class="sxs-lookup"><span data-stu-id="211ad-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="211ad-146">インターネット接続です。</span><span class="sxs-lookup"><span data-stu-id="211ad-146">A live internet connection.</span></span>
- <span data-ttu-id="211ad-147">管理者特権が (インストール プロセスに必要)。</span><span class="sxs-lookup"><span data-stu-id="211ad-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="211ad-148">ASP.NET Web ページとは何ですか。</span><span class="sxs-lookup"><span data-stu-id="211ad-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="211ad-149">ASP.NET Web ページは、動的な web ページの作成に使用できるフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="211ad-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="211ad-150">単純な HTML web ページは静的です。そのコンテンツは、ページ内にある固定の HTML マークアップで決定されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="211ad-151">ASP.NET Web Pages を作成するものと同様の動的なページを使用して、コードを使用して、実行時にページのコンテンツを作成できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="211ad-152">動的なページを使用して、さまざまな機能を実行できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="211ad-153">フォームを使用してユーザー入力の入力を要求し、ページの表示または外観に変更できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="211ad-154">ユーザーから情報を取得し、データベースでは、保存し、後で一覧表示できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="211ad-155">サイトから電子メールを送信できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-155">You can send email from your site.</span></span> <span data-ttu-id="211ad-156">Web (マッピング サービスなど) の他のサービスと対話し、それらのソースからの情報を統合するページを生成できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="211ad-157">WebMatrix は何ですか。</span><span class="sxs-lookup"><span data-stu-id="211ad-157">What is WebMatrix?</span></span>

<span data-ttu-id="211ad-158">WebMatrix は、web ページ エディター、データベース ユーティリティ、ページ、および web サイトをインターネットに公開するための機能をテストするための web サーバーを統合するツールです。</span><span class="sxs-lookup"><span data-stu-id="211ad-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="211ad-159">WebMatrix は無料であり、簡単にインストールし、使いやすい。</span><span class="sxs-lookup"><span data-stu-id="211ad-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="211ad-160">(でも単の HTML ページのほか、PHP などの他のテクノロジです。)</span><span class="sxs-lookup"><span data-stu-id="211ad-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="211ad-161">実際にはないかどうか*が*WebMatrix を使用した ASP.NET Web Pages を操作します。</span><span class="sxs-lookup"><span data-stu-id="211ad-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="211ad-162">エディター、テキストを使用してページを作成するなどしてへのアクセスのある web サーバーを使用してページをテストします。</span><span class="sxs-lookup"><span data-stu-id="211ad-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="211ad-163">ただし、WebMatrix、非常に簡単ではすべて、これらのチュートリアルは、全体にわたって WebMatrix を使用するようにします。</span><span class="sxs-lookup"><span data-stu-id="211ad-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="211ad-164">これらのチュートリアルについて</span><span class="sxs-lookup"><span data-stu-id="211ad-164">About These Tutorials</span></span>

<span data-ttu-id="211ad-165">このチュートリアルのセットは、ASP.NET Web Pages を使用する方法の概要です。</span><span class="sxs-lookup"><span data-stu-id="211ad-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="211ad-166">この入門チュートリアル セットの合計は 9 のチュートリアルです。</span><span class="sxs-lookup"><span data-stu-id="211ad-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="211ad-167">ASP.NET Web Pages の初心者から real、プロフェッショナルなデザインの web サイトを作成するのには一連のチュートリアルのセットの一部にできます。</span><span class="sxs-lookup"><span data-stu-id="211ad-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="211ad-168">この最初のチュートリアルでは、ASP.NET Web Pages を操作する方法の基礎を示すことで主要を設定します。</span><span class="sxs-lookup"><span data-stu-id="211ad-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="211ad-169">完了したら、この 1 つを終了し、Web ページをさらに詳しく調査する場所を取得する追加のチュートリアルのセットを操作できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="211ad-170">意図的に進む簡単に詳細な説明。</span><span class="sxs-lookup"><span data-stu-id="211ad-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="211ad-171">何かを説明するたびにこのチュートリアルのセットのお常に選択方法と考えることと簡単に理解します。</span><span class="sxs-lookup"><span data-stu-id="211ad-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="211ad-172">以降チュートリアルのセットより詳細に移動しより効率的なまたはより柔軟なアプローチ (もずっと楽しく) を表示します。</span><span class="sxs-lookup"><span data-stu-id="211ad-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="211ad-173">これらのチュートリアルでは、まず、基本を理解する必要があります。</span><span class="sxs-lookup"><span data-stu-id="211ad-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="211ad-174">開始したチュートリアルのセットでは、ASP.NET Web Pages のこれらの機能について説明します。</span><span class="sxs-lookup"><span data-stu-id="211ad-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="211ad-175">概要と、インストールされているすべてのものを取得します。</span><span class="sxs-lookup"><span data-stu-id="211ad-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="211ad-176">(内にある、チュートリアルをご覧になっている。)</span><span class="sxs-lookup"><span data-stu-id="211ad-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="211ad-177">ASP.NET Web Pages のプログラミングの基礎です。</span><span class="sxs-lookup"><span data-stu-id="211ad-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="211ad-178">データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="211ad-178">Creating a database.</span></span>
- <span data-ttu-id="211ad-179">作成して、ユーザー入力フォームを処理します。</span><span class="sxs-lookup"><span data-stu-id="211ad-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="211ad-180">追加、更新、およびデータベース内のデータを削除します。</span><span class="sxs-lookup"><span data-stu-id="211ad-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="211ad-181">新機能を作成しますか。</span><span class="sxs-lookup"><span data-stu-id="211ad-181">What Will You Create?</span></span>

<span data-ttu-id="211ad-182">このチュートリアルが設定され、以降の中心と web サイトと同様に、ムービーを一覧表示できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="211ad-183">動画の入力、編集、およびそれらを一覧表示することができます。</span><span class="sxs-lookup"><span data-stu-id="211ad-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="211ad-184">このチュートリアルのセットで作成したページがいくつかのとおりです。</span><span class="sxs-lookup"><span data-stu-id="211ad-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="211ad-185">1 つ目は、作成する ページの一覧を表示するムービーを示しています。</span><span class="sxs-lookup"><span data-stu-id="211ad-185">The first one shows the movie listing page that you'll create:</span></span>

![ムービーの一覧を示すはムービー アプリ](getting-started/_static/image1.png)

<span data-ttu-id="211ad-187">新しいムービーの情報をサイトに追加することができます、ページを次に示します。</span><span class="sxs-lookup"><span data-stu-id="211ad-187">And here's the page that lets you add new movie information to your site:</span></span>

![ムービーの追加 ページを示す完成したムービー アプリ](getting-started/_static/image2.png)

<span data-ttu-id="211ad-189">このチュートリアルの後続のセットのビルドでは、設定し、電子メールを送信して、ソーシャル メディアとの統合の画像のアップロード、ログインしてもらうように、多くの機能を追加します。</span><span class="sxs-lookup"><span data-stu-id="211ad-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="211ad-190">Azure で実行されているこのアプリを参照してください。</span><span class="sxs-lookup"><span data-stu-id="211ad-190">See this App Running on Azure</span></span>

<span data-ttu-id="211ad-191">ライブ web アプリとして実行している完成したサイトを参照してもよろしいですか。</span><span class="sxs-lookup"><span data-stu-id="211ad-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="211ad-192">Azure アカウントに、アプリの完全なバージョンを展開するには、次のボタンをクリックするだけです。</span><span class="sxs-lookup"><span data-stu-id="211ad-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="211ad-193">Azure アカウントを Azure にこのソリューションを展開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="211ad-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="211ad-194">アカウントがない場合は、次のオプションがあります。</span><span class="sxs-lookup"><span data-stu-id="211ad-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="211ad-195">[無料の Azure アカウントを開設](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604)-クレジットを取得するでも使用されているアカウントを維持する最大と使用する無料の Azure サービスおよび有料の Azure サービスを試す使用できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-195">[Open an Azure account for free](https://azure.microsoft.com/en-us/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="211ad-196">[MSDN サブスクライバー特典をアクティブ化](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-お客様の MSDN サブスクリプションでは、クレジット有料の Azure サービスを使用できるすべての月です。</span><span class="sxs-lookup"><span data-stu-id="211ad-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="211ad-197">すべてのインストール</span><span class="sxs-lookup"><span data-stu-id="211ad-197">Installing Everything</span></span>

<span data-ttu-id="211ad-198">Microsoft Web Platform Installer を使用して、すべてのものをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="211ad-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="211ad-199">実際には、インストーラーをインストールし、他のすべてのインストールに使用することです。</span><span class="sxs-lookup"><span data-stu-id="211ad-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="211ad-200">少なくともを持っていることがある Web ページを使用して、Windows XP SP3 をインストールまたは Windows Server 2008 またはそれ以降。</span><span class="sxs-lookup"><span data-stu-id="211ad-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="211ad-201">[Web Pages ページ](../../../index.md)ASP.NET web サイトのをクリックして**インストール**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET Web サイトを示す&quot;WebMatrix のインストール&quot;ボタン](getting-started/_static/image3.png)

<span data-ttu-id="211ad-203">ライセンス条項および WebMatrix をインストールする前にプライバシーに関する声明に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="211ad-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![インストールを開始する用語を受け入れる](getting-started/_static/image4.png)

<span data-ttu-id="211ad-205">をクリックして**実行**インストールを開始します。</span><span class="sxs-lookup"><span data-stu-id="211ad-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="211ad-206">(インストーラーを保存する場合は、クリックして**保存**し、保存したフォルダーからインストーラーを実行します)。</span><span class="sxs-lookup"><span data-stu-id="211ad-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="211ad-207">WebMatrix をインストールする準備ができて、Web Platform Installer が表示されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="211ad-208">**[インストール]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="211ad-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="211ad-209">インストール プロセスでは、コンピューターにインストールする必要がある出し、プロセスを開始します。</span><span class="sxs-lookup"><span data-stu-id="211ad-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="211ad-210">インストールする必要のあるものだけによって処理にかかる任意の場所、数分間から数分です。</span><span class="sxs-lookup"><span data-stu-id="211ad-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="211ad-211">選択**同意**ライセンス条項に同意します。</span><span class="sxs-lookup"><span data-stu-id="211ad-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="211ad-212">こんにちは, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="211ad-212">Hello, WebMatrix</span></span>

<span data-ttu-id="211ad-213">実行されると、インストール処理は WebMatrix を自動的に起動できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="211ad-214">インストールされていない場合、Windows から、**開始**] メニューの [起動**Microsoft WebMatrix**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="211ad-215">WebMatrix を初めて起動すると、Microsoft アカウントで Microsoft Azure にサインインする機会が与えられます。</span><span class="sxs-lookup"><span data-stu-id="211ad-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="211ad-216">サインインすると、Azure 経由で 10 個の無料の web アプリが表示されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="211ad-217">これらの free web アプリは、アプリをテストする便利な手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="211ad-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="211ad-218">場合は、Azure アカウントを既に必要はありませんが、MSDN サブスクリプションが、 [MSDN サブスクリプション特典をアクティブ化](https://www.windowsazure.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)です。</span><span class="sxs-lookup"><span data-stu-id="211ad-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/en-us/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="211ad-219">それ以外の場合、ほんの数分で無料の試用アカウントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="211ad-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="211ad-220">詳細については、「 [Azure 無料評価版](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)です。</span><span class="sxs-lookup"><span data-stu-id="211ad-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="211ad-221">このチュートリアルを続行する今すぐにサインインする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="211ad-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="211ad-222">署名しないようになりました場合、は、後でサインインするオプションが続行されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="211ad-223">最後の[トピック](publishing.md)シリーズをこのチュートリアルでは、web サイトを Azure に配置する方法をについて説明以外のトピックを完了にサインインする必要がありますはそのため、します。</span><span class="sxs-lookup"><span data-stu-id="211ad-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="211ad-224">この時点では、いずれかはサインイン、Microsoft アカウントまたは選択して**Not Now**右下隅にします。</span><span class="sxs-lookup"><span data-stu-id="211ad-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![サインイン](getting-started/_static/image7.png)

<span data-ttu-id="211ad-226">を開始するにを空白の web サイトを作成し、ページを追加します。</span><span class="sxs-lookup"><span data-stu-id="211ad-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="211ad-227">このセットの後のチュートリアルでは、組み込みの web サイト テンプレートのいずれかで再生されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="211ad-228">[スタート] ウィンドウ**新規**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-228">In the start window, click **New**.</span></span>

![WebMatrix の起動画面](getting-started/_static/image8.png)

<span data-ttu-id="211ad-230">テンプレートは、構築済みのファイルおよびさまざまな種類の web サイトのページです。</span><span class="sxs-lookup"><span data-stu-id="211ad-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="211ad-231">すべての既定で使用可能なテンプレートを表示するには、テンプレート ギャラリー オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="211ad-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![テンプレート ギャラリーの選択](getting-started/_static/image9.png)

<span data-ttu-id="211ad-233">**クイック スタート**ウィンドウで、**空サイト**から、 **ASP.NET**をグループ化し、新しいサイト"WebPagesMovies"という名前です。</span><span class="sxs-lookup"><span data-stu-id="211ad-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![空のサイト テンプレートが選択されていると WebMatrix のクイック スタート ウィンドウ](getting-started/_static/image10.png)

<span data-ttu-id="211ad-235">**[次へ]**をクリックします。</span><span class="sxs-lookup"><span data-stu-id="211ad-235">Click **Next**.</span></span>

<span data-ttu-id="211ad-236">Microsoft アカウントにサインインしている場合は、Azure でサイトを作成することが表示されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="211ad-237">既定の名前、サイトの名前に基づく**WebPagesMovies.azurewebsites.net**をお勧めします。 ただし、感嘆符はこの名前が Windows Azure で使用できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="211ad-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="211ad-238">わかりやすくするため、次のように選択します。 **Skip**を Azure に web サイトを作成すると、今すぐをバイパスします。</span><span class="sxs-lookup"><span data-stu-id="211ad-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="211ad-239">この系列に後で Azure にサイトが公開します。</span><span class="sxs-lookup"><span data-stu-id="211ad-239">Later in this series, we will publish the site to Azure.</span></span>

![azure サイトを作成します。](getting-started/_static/image11.png)

<span data-ttu-id="211ad-241">WebMatrix は、作成し、サイトが開きます。</span><span class="sxs-lookup"><span data-stu-id="211ad-241">WebMatrix creates and opens the site:</span></span>

![WebMatrix で新しい WebPagesMovies サイトを開く](getting-started/_static/image12.png)

<span data-ttu-id="211ad-243">上部は、クイック アクセス ツールバーとリボンがあります。</span><span class="sxs-lookup"><span data-stu-id="211ad-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="211ad-244">左下に表示ワークスペース セレクター タスク間切り替えた (**サイト**、**ファイル**、**データベース**、**レポート**)。</span><span class="sxs-lookup"><span data-stu-id="211ad-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="211ad-245">右側は、コンテンツ ウィンドウおよびレポートのエディターです。</span><span class="sxs-lookup"><span data-stu-id="211ad-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="211ad-246">下部にして場合によっては表示されますメッセージの通知バー。</span><span class="sxs-lookup"><span data-stu-id="211ad-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="211ad-247">WebMatrix と機能の詳細、これらのチュートリアルを進めるときに学習します。</span><span class="sxs-lookup"><span data-stu-id="211ad-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="211ad-248">Web ページを作成します。</span><span class="sxs-lookup"><span data-stu-id="211ad-248">Creating a Web Page</span></span>

<span data-ttu-id="211ad-249">WebMatrix と ASP.NET Web Pages について理解しておくには、単純なページを作成します。</span><span class="sxs-lookup"><span data-stu-id="211ad-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="211ad-250">ワークスペース セレクターで選択、**ファイル**ワークスペース。</span><span class="sxs-lookup"><span data-stu-id="211ad-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="211ad-251">このワークスペースでは、ファイルとフォルダーを操作することができます。</span><span class="sxs-lookup"><span data-stu-id="211ad-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="211ad-252">左側のウィンドウは、サイトのファイル構造を示しています。</span><span class="sxs-lookup"><span data-stu-id="211ad-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="211ad-253">ファイルに関連するタスクを表示するリボン変更します。</span><span class="sxs-lookup"><span data-stu-id="211ad-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix でファイル ワークスペース](getting-started/_static/image13.png)

<span data-ttu-id="211ad-255">リボンでは、下の矢印をクリックして**新規** をクリックし、**新しいファイル**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![使用して、&quot;新規&quot;新しいファイルを作成するには、リボンのコマンド](getting-started/_static/image14.png)

<span data-ttu-id="211ad-257">WebMatrix には、ファイルの種類の一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="211ad-258">選択**CSHTML**、し、、**名前**ボックスに、"HelloWorld"を入力します。</span><span class="sxs-lookup"><span data-stu-id="211ad-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="211ad-259">ASP.NET Web Pages ページ、CSHTML ページです。</span><span class="sxs-lookup"><span data-stu-id="211ad-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![名前付き HelloWorld.cshtml の新しい CSHTML ページの作成](getting-started/_static/image15.png)

<span data-ttu-id="211ad-261">**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="211ad-261">Click **OK**.</span></span>

<span data-ttu-id="211ad-262">WebMatrix は、ページが作成され、エディターで開きます。</span><span class="sxs-lookup"><span data-stu-id="211ad-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix エディターで新しい HelloWorld ページ](getting-started/_static/image16.png)

<span data-ttu-id="211ad-264">ご覧のように、ページには、上部の次のようなブロックを除くのほとんどの場合の通常 HTML マークアップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="211ad-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="211ad-265">コードを追加、すぐにわかります。</span><span class="sxs-lookup"><span data-stu-id="211ad-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="211ad-266">注意して、ページのさまざまな部分&mdash;要素名、属性、テキスト、および上部にあるブロック-は、すべて異なる色。</span><span class="sxs-lookup"><span data-stu-id="211ad-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="211ad-267">これと呼ばれる*構文の強調表示*とそれを簡単にクリアします。</span><span class="sxs-lookup"><span data-stu-id="211ad-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="211ad-268">これは、WebMatrix で web ページを使用しやすく機能の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="211ad-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="211ad-269">コンテンツを追加、`<head>`と`<body>`要素は、次の例と同様にします。</span><span class="sxs-lookup"><span data-stu-id="211ad-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="211ad-270">(する場合は、だけ次のブロックをコピーして全体の既存のページをコードに置き換えます。)</span><span class="sxs-lookup"><span data-stu-id="211ad-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="211ad-271">クイック アクセス ツールバーまたは、**ファイル** メニューのをクリックして**保存**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix クイック アクセス ツールバーの [保存] ボタン](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="211ad-273">ページのテスト</span><span class="sxs-lookup"><span data-stu-id="211ad-273">Testing the Page</span></span>

<span data-ttu-id="211ad-274">**ファイル** ワークスペースを右クリックし、 *HelloWorld.cshtml*ページし、をクリックして**ブラウザーで起動**です。</span><span class="sxs-lookup"><span data-stu-id="211ad-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![WebMatrix のリボンの [実行] ボタンを使用し、ページを実行しています。](getting-started/_static/image18.png)

<span data-ttu-id="211ad-276">WebMatrix は、コンピューター上のページのテストに使用できる組み込みの web サーバー (IIS Express) を開始します。</span><span class="sxs-lookup"><span data-stu-id="211ad-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="211ad-277">(せず、WebMatrix で IIS Express が発行する必要が、ページ、web サーバーにどこかにテストすることも前にします。)ページは、既定のブラウザーで表示されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![&quot;Hello World&quot;ブラウザーで実行されているページ](getting-started/_static/image19.png)

<span data-ttu-id="211ad-279">WebMatrix では、ページをテストするときに、ブラウザーで URL がよう`http://localhost:33651/HelloWorld.cshtml.`名前*localhost*ページは、自分のコンピューター上にある web サーバーによって処理されていることを意味、ローカル サーバーを指します。</span><span class="sxs-lookup"><span data-stu-id="211ad-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="211ad-280">前述のように、WebMatrix には、ページを起動するときに実行される IIS Express という名前の web サーバー プログラムが含まれています。</span><span class="sxs-lookup"><span data-stu-id="211ad-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="211ad-281">数値*localhost* (たとえば、 *localhost:33651*) を指す、*ポート番号*コンピューターにします。</span><span class="sxs-lookup"><span data-stu-id="211ad-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="211ad-282">これは、""IIS Express を使用するチャネルのこの特定の web サイトの数です。</span><span class="sxs-lookup"><span data-stu-id="211ad-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="211ad-283">ポート番号は、サイトを作成すると異なっているすべてのサイトを作成することは 1024 ~ 65536 範囲からランダムに選択されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="211ad-284">(独自のサイトをテストするときに、ポート番号ほぼ確実になります 33561 よりも数が異なる)。別のポートを使用して、web サイトごとに、IIS Express を保存できます直線がどのサイトに通信することができます。</span><span class="sxs-lookup"><span data-stu-id="211ad-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="211ad-285">表示されない、パブリック web サーバーにサイトを発行するときに後で*localhost* URL にします。</span><span class="sxs-lookup"><span data-stu-id="211ad-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="211ad-286">その時点では、ような一般的な URL が表示されます`http://myhostingsite/mywebsite/HelloWorld.cshtml`か、どのようなページです。</span><span class="sxs-lookup"><span data-stu-id="211ad-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="211ad-287">このチュートリアル シリーズの後で、サイトの発行について学びます。</span><span class="sxs-lookup"><span data-stu-id="211ad-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="211ad-288">一部のサーバー側コードを追加します。</span><span class="sxs-lookup"><span data-stu-id="211ad-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="211ad-289">ブラウザーを終了し、WebMatrix 内のページに戻ります。</span><span class="sxs-lookup"><span data-stu-id="211ad-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="211ad-290">次のコードのように見えるように、コード ブロックに行を追加します。</span><span class="sxs-lookup"><span data-stu-id="211ad-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="211ad-291">これは、少しの Razor コードです。</span><span class="sxs-lookup"><span data-stu-id="211ad-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="211ad-292">現在の日付と時刻を取得および値を配置するには、おそらく明確では、*変数*という`currentDateTime`です。</span><span class="sxs-lookup"><span data-stu-id="211ad-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="211ad-293">詳細をお読みを次のチュートリアルでは、Razor 構文の詳細。</span><span class="sxs-lookup"><span data-stu-id="211ad-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="211ad-294">ページの本文で後に、`<p>Hello World!</p>`要素、次の追加。</span><span class="sxs-lookup"><span data-stu-id="211ad-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="211ad-295">このコードに含まれる値を取得する、`currentDateTime`上部にある変数し、ページのマークアップに挿入します。</span><span class="sxs-lookup"><span data-stu-id="211ad-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="211ad-296">`@`文字は、ページ内の ASP.NET Web ページ コードをマークします。</span><span class="sxs-lookup"><span data-stu-id="211ad-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="211ad-297">(WebMatrix の変更を保存するページを実行する前に) もう一度ページを実行します。</span><span class="sxs-lookup"><span data-stu-id="211ad-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="211ad-298">この日付が表示する時間とページの時間。</span><span class="sxs-lookup"><span data-stu-id="211ad-298">This time you see the date and time in the page.</span></span>

![&quot;Hello World&quot;動的に生成された時刻の表示を使用してブラウザーで実行されているページ](getting-started/_static/image20.png)

<span data-ttu-id="211ad-300">しばらく待ってから、ブラウザーでページを更新します。</span><span class="sxs-lookup"><span data-stu-id="211ad-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="211ad-301">日付と時刻の表示が更新されます。</span><span class="sxs-lookup"><span data-stu-id="211ad-301">The date and time display is updated.</span></span>

<span data-ttu-id="211ad-302">ブラウザーでページ ソースを見てください。</span><span class="sxs-lookup"><span data-stu-id="211ad-302">In the browser, look at the page source.</span></span> <span data-ttu-id="211ad-303">次のマークアップようになります。</span><span class="sxs-lookup"><span data-stu-id="211ad-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="211ad-304">注意して、`@{ }`上部のブロックがないです。</span><span class="sxs-lookup"><span data-stu-id="211ad-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="211ad-305">日付と時刻が表示された文字の実際の文字列に注意してください (`1/18/2012 2:49:50 PM`または) ではなく、`@currentDateTime`に表示されていたように、 *.cshtml*ページ。</span><span class="sxs-lookup"><span data-stu-id="211ad-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="211ad-306">ここでは、ページを実行したときに、ASP.NET のすべてのコード (はここではほとんどありません) でマークされたと処理を何が起こった`@`です。</span><span class="sxs-lookup"><span data-stu-id="211ad-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="211ad-307">コードの出力は、し、その出力が、ページに挿入します。</span><span class="sxs-lookup"><span data-stu-id="211ad-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="211ad-308">これは、ASP.NET Web Pages がについて</span><span class="sxs-lookup"><span data-stu-id="211ad-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="211ad-309">ASP.NET Web Pages で動的 web コンテンツが生成されることを読み取るときにここで確認した新機能をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="211ad-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="211ad-310">作成したページには、前に説明した同じ HTML マークアップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="211ad-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="211ad-311">また、あらゆる種類の作業を実行するコードを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="211ad-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="211ad-312">この例では、現在の日付と時刻を取得する簡単な作業をでした。</span><span class="sxs-lookup"><span data-stu-id="211ad-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="211ad-313">学習したようにコードを挿入する html ページの出力を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="211ad-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="211ad-314">他のユーザーが要求したとき、 *.cshtml* web サーバーの手にまだある間に、ブラウザー、ASP.NET のページがページを処理します。</span><span class="sxs-lookup"><span data-stu-id="211ad-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="211ad-315">ASP.NET は、コードの出力 (もしあれば) ページに挿入します HTML として。</span><span class="sxs-lookup"><span data-stu-id="211ad-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="211ad-316">コード処理が完了したら、ASP.NET は、結果のページをブラウザーに送信します。</span><span class="sxs-lookup"><span data-stu-id="211ad-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="211ad-317">ブラウザーが受け取ることは、HTML です。</span><span class="sxs-lookup"><span data-stu-id="211ad-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="211ad-318">ダイアグラムを次に示します。</span><span class="sxs-lookup"><span data-stu-id="211ad-318">Here's a diagram:</span></span>

![ASP.NET が動的に HTML を生成の概念フロー](getting-started/_static/image21.png)

<span data-ttu-id="211ad-320">考え方は単純な場合、ですは、コードを実行できる、多くの興味深いタスクとを動的にコンテンツを追加できます HTML ページに多くの興味深い方法があります。</span><span class="sxs-lookup"><span data-stu-id="211ad-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="211ad-321">ASP.NET *.cshtml*任意の HTML ページなどのページでは、ブラウザー自体 (JavaScript と jQuery コード) で実行されるコードを含めることもできます。</span><span class="sxs-lookup"><span data-stu-id="211ad-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="211ad-322">このチュートリアルのセットと以降では、これらがすべてを調べてみます。</span><span class="sxs-lookup"><span data-stu-id="211ad-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="211ad-323">次へ直近の見通し</span><span class="sxs-lookup"><span data-stu-id="211ad-323">Coming Up Next</span></span>

<span data-ttu-id="211ad-324">このシリーズの次のチュートリアルでは、ASP.NET Web Pages は、もう少しプログラミングを調査します。</span><span class="sxs-lookup"><span data-stu-id="211ad-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="211ad-325">その他のリソース</span><span class="sxs-lookup"><span data-stu-id="211ad-325">Additional Resources</span></span>

<span data-ttu-id="211ad-326">[ASP.NET web サイトを最初から作成](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch)です。</span><span class="sxs-lookup"><span data-stu-id="211ad-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="211ad-327">これは、具体的には、チュートリアル WebMatrix (ASP.NET Web ページではない) の使用方法です。</span><span class="sxs-lookup"><span data-stu-id="211ad-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="211ad-328">入る、少し詳細については、このチュートリアルのセットには触れません WebMatrix の他の機能の一部です。</span><span class="sxs-lookup"><span data-stu-id="211ad-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="211ad-329">次へ</span><span class="sxs-lookup"><span data-stu-id="211ad-329">Next</span></span>](intro-to-web-pages-programming.md)