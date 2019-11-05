---
title: Quantum Development Kit に貢献する | Microsoft Docs
description: Quantum Development Kit に貢献する
author: cgranade
ms.author: chgranad
ms.date: 10/12/2018
ms.topic: article
uid: microsoft.quantum.contributing
ms.openlocfilehash: 4be86c5045ece62ae3af40090a2cd344d965e65f
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73057405"
---
# <a name="contributing-to-the-quantum-development-kit"></a><span data-ttu-id="c28cb-103">Quantum Development Kit に貢献する</span><span class="sxs-lookup"><span data-stu-id="c28cb-103">Contributing to the Quantum Development Kit</span></span> #

<span data-ttu-id="c28cb-104">Quantum Development Kit は、量子プログラムを作成するための単なるツールの集まりではありません。</span><span class="sxs-lookup"><span data-stu-id="c28cb-104">The Quantum Development Kit is more than a collection of tools for writing quantum programs.</span></span>
<span data-ttu-id="c28cb-105">これは、量子コンピューティングの研究、量子アルゴリズムを使用した調査、量子デバイス向けの新しいアプリケーションの開発、および量子プログラミングを最大限に活用するためのその他の作業を行う人々の広範囲のコミュニティの一部です。</span><span class="sxs-lookup"><span data-stu-id="c28cb-105">It's part of a broad community of people discovering quantum computing, performing research in quantum algorithms, developing new applications for quantum devices, and otherwise working to make the most out of the quantum programming.</span></span>
<span data-ttu-id="c28cb-106">このコミュニティのメンバーとして、Quantum Development Kit は、さまざまな背景を持つ量子開発者に必要な機能を提供することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="c28cb-106">As a member of that community, the Quantum Development Kit aims to offer quantum developers across a wide range of backgrounds with the features they need.</span></span>
<span data-ttu-id="c28cb-107">Quantum Development Kit へのコントリビューションは、他の量子開発者が使用するツールの改善、それらのツールの文書化、さらに量子プログラミング コミュニティでの発見や作成を改善するために役立つ新しい機能の作成などを通じて、このような目的を実現するために役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c28cb-107">Your contributions to the Quantum Development Kit help in realizing that goal by improving the tools used by other quantum developers, how those tools are documented, and even by creating new features and functionality that helps make the entire quantum programming community a better place to discover and create.</span></span>
<span data-ttu-id="c28cb-108">Microsoft は、皆さんのコントリビューション、そして皆さんと協力してコミュニティを最大限に活用できる機会を非常にうれしく思います。</span><span class="sxs-lookup"><span data-stu-id="c28cb-108">We're very thankful for your kind contributions, and for the opportunity to work with you to make our community the best that it can be.</span></span>

<span data-ttu-id="c28cb-109">このガイドでは、より広い量子プログラミング コミュニティへのコントリビューションを可能な限り有益なものにする方法に関するアドバイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="c28cb-109">In this guide, we provide some advice on how to make your contribution as useful as possible to the broader quantum programming community.</span></span>

## <a name="building-community"></a><span data-ttu-id="c28cb-110">コミュニティの構築</span><span class="sxs-lookup"><span data-stu-id="c28cb-110">Building Community</span></span> ##

<span data-ttu-id="c28cb-111">コントリビューションを行うときは、まず自分が貢献しているコミュニティを常に念頭に置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="c28cb-111">The very first thing about making a contribution is to always keep in mind the community that you are contributing to.</span></span>
<span data-ttu-id="c28cb-112">量子プログラミング コミュニティだけでなく、より広い範囲の仲間に対して礼儀正しく専門的に行動することで、皆さんの努力で最善の最も有効的なコミュニティを構築することができます。</span><span class="sxs-lookup"><span data-stu-id="c28cb-112">By acting respectfully and professionally towards your peers in the quantum programming community and more broadly, you can help to make sure that your efforts build the best and most welcoming community possible.</span></span>

<span data-ttu-id="c28cb-113">この取り組みの一環として、すべての Quantum Development Kit プロジェクトは、[Microsoft オープンソースの倫理規定](https://opensource.microsoft.com/codeofconduct/)を採用しています。</span><span class="sxs-lookup"><span data-stu-id="c28cb-113">As a part of that effort, all Quantum Development Kit projects have adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).</span></span>
<span data-ttu-id="c28cb-114">詳しくは、[倫理規定についてよくある質問](https://opensource.microsoft.com/codeofconduct/faq/)に関する記事を参照するか、[opencode@microsoft.com](mailto:opencode@microsoft.com) 宛てに質問またはコメントをお送りください。</span><span class="sxs-lookup"><span data-stu-id="c28cb-114">For more information, please see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.</span></span>

## <a name="what-kinds-of-contributions-help-the-community"></a><span data-ttu-id="c28cb-115">どのようなコントリビューションがコミュニティに役立ちますか。</span><span class="sxs-lookup"><span data-stu-id="c28cb-115">What Kinds of Contributions Help the Community?</span></span> ##

<span data-ttu-id="c28cb-116">コントリビューションを通じて、量子プログラミング コミュニティを支援する方法はさまざまです。</span><span class="sxs-lookup"><span data-stu-id="c28cb-116">There are lots of different ways to help the quantum programming community through your contributions.</span></span>
<span data-ttu-id="c28cb-117">このガイドでは、Quantum Development Kit に特に関連する 3 つの方法に焦点を当てます。</span><span class="sxs-lookup"><span data-stu-id="c28cb-117">In this guide, we'll focus on three ways that are especially relevant to the Quantum Development Kit.</span></span>
<span data-ttu-id="c28cb-118">これらの方法はすべて、ユーザーを支援する量子コミュニティの構築に不可欠です。</span><span class="sxs-lookup"><span data-stu-id="c28cb-118">All of these ways are critical to building a quantum community that empowers people.</span></span>
<span data-ttu-id="c28cb-119">ただし、これがすべてという訳ではありません。量子プログラミングの発展のため、コミュニティの構築に役立つその他の方法を調べることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="c28cb-119">That said, this is definitely not an exhaustive list — we encourage you to explore other ways to help the community build on the promise of quantum programming!</span></span>

- <span data-ttu-id="c28cb-120">**バグの報告**</span><span class="sxs-lookup"><span data-stu-id="c28cb-120">**Reporting bugs.**</span></span> <span data-ttu-id="c28cb-121">バグとその他の種類の問題を修正するための最初の手順は、それらを特定することです。</span><span class="sxs-lookup"><span data-stu-id="c28cb-121">The first step in fixing bugs and other kinds of problems is to identify them.</span></span> <span data-ttu-id="c28cb-122">Quantum Development Kit でバグを発見した場合は、その問題を修正し、量子プログラミング コミュニティに向けたより優れたツール セットを作成できるよう、ぜひご報告ください。</span><span class="sxs-lookup"><span data-stu-id="c28cb-122">If you've found a bug in the Quantum Development Kit, letting us know helps us fix it and make a better set of tools for the quantum programming community.</span></span>
- <span data-ttu-id="c28cb-123">**ドキュメントの改善**</span><span class="sxs-lookup"><span data-stu-id="c28cb-123">**Improving documentation.**</span></span> <span data-ttu-id="c28cb-124">ドキュメント セットは、常に改善し、より詳細な情報を記述し、アクセスしやすくすることができます。</span><span class="sxs-lookup"><span data-stu-id="c28cb-124">Any documentation set can always be better, can cover more details, be made more accessible.</span></span>
- <span data-ttu-id="c28cb-125">**コードの開発協力**</span><span class="sxs-lookup"><span data-stu-id="c28cb-125">**Contributing code.**</span></span> <span data-ttu-id="c28cb-126">当然ながら、最も直接的に貢献する方法の 1 つは、新しいコードを Quantum Development Kit に追加することです。</span><span class="sxs-lookup"><span data-stu-id="c28cb-126">Of course, one of the most direct ways to contribute is by adding new code to the Quantum Development Kit.</span></span>

<span data-ttu-id="c28cb-127">このようなさまざまな種類のコントリビューションは、すべて非常に価値があり、高く評価されます。</span><span class="sxs-lookup"><span data-stu-id="c28cb-127">These different kinds of contributions are all immensely valuable, and are greatly appreciated.</span></span>
<span data-ttu-id="c28cb-128">このガイドの残りの部分では、各種コントリビューションを行う方法についてのアドバイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="c28cb-128">In the rest of the guide, we'll offer advice on how to make each kind of contribution.</span></span>

## <a name="where-do-contributions-go"></a><span data-ttu-id="c28cb-129">コントリビューションはどこで行いますか。</span><span class="sxs-lookup"><span data-stu-id="c28cb-129">Where Do Contributions Go?</span></span> ##

<span data-ttu-id="c28cb-130">Quantum Development Kit には、量子プログラムを作成するためのプラットフォームを実現するために連携する多くの構成要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c28cb-130">The Quantum Development Kit includes a number of different pieces that all work together to realize a platform for writing quantum programs.</span></span>
<span data-ttu-id="c28cb-131">これらの各構成要素は別々のリポジトリに存在しているため、最初に行うべきことの 1 つが各コントリビューションに最適な場所がどこかを整理することです。</span><span class="sxs-lookup"><span data-stu-id="c28cb-131">Each of these different pieces finds its home on a different repository, so the one of the earlier things to sort out is where each contribution best belongs.</span></span>

- <span data-ttu-id="c28cb-132">[**microsoft/Quantum**](https://github.com/Microsoft/Quantum):Quantum Development Kit の使用を開始するためのサンプルとツール。</span><span class="sxs-lookup"><span data-stu-id="c28cb-132">[**microsoft/Quantum**](https://github.com/Microsoft/Quantum): Samples and tools to help get started with the Quantum Development Kit.</span></span>
- <span data-ttu-id="c28cb-133">[**microsoft/QuantumLibraries**](https://github.com/Microsoft/QuantumLibraries):Quantum Development Kit 用の標準およびドメイン固有のライブラリ。</span><span class="sxs-lookup"><span data-stu-id="c28cb-133">[**microsoft/QuantumLibraries**](https://github.com/Microsoft/QuantumLibraries): Standard and domain-specific libraries for the Quantum Development Kit.</span></span>
- <span data-ttu-id="c28cb-134">[**microsoft/QuantumKatas**](https://github.com/Microsoft/QuantumKatas):量子コンピューティングと Q# プログラミング言語を学習するためのマイペースで進められるプログラミング演習。</span><span class="sxs-lookup"><span data-stu-id="c28cb-134">[**microsoft/QuantumKatas**](https://github.com/Microsoft/QuantumKatas): Self-paced programming exercises for learning quantum computing and the Q# programming language.</span></span>
- <span data-ttu-id="c28cb-135">[**microsoft/qsharp-compiler**](https://github.com/microsoft/qsharp-compiler):Q# コンパイラ、Visual Studio 拡張機能、および Visual Studio Code 拡張機能。</span><span class="sxs-lookup"><span data-stu-id="c28cb-135">[**microsoft/qsharp-compiler**](https://github.com/microsoft/qsharp-compiler): The Q# compiler, Visual Studio extension, and Visual Studio Code extension.</span></span>
- <span data-ttu-id="c28cb-136">[**microsoft/qsharp-runtime**](https://github.com/microsoft/qsharp-runtime):Quantum Development Kit のシミュレーション フレームワーク、コード生成、シミュレーション ターゲット マシン。</span><span class="sxs-lookup"><span data-stu-id="c28cb-136">[**microsoft/qsharp-runtime**](https://github.com/microsoft/qsharp-runtime): Simulation framework, code generation, and simulation target machines for the Quantum Development Kit.</span></span>
- <span data-ttu-id="c28cb-137">[**microsoft/iqsharp**](https://github.com/microsoft/iqsharp):Jupyter カーネル、Q# の Python ホスト機能、およびクラウド環境で IQ# を使用するための Docker イメージ。</span><span class="sxs-lookup"><span data-stu-id="c28cb-137">[**microsoft/iqsharp**](https://github.com/microsoft/iqsharp): Jupyter kernel and Python host functionality for Q#, as well as Docker images for using IQ# in cloud environments.</span></span>
- <span data-ttu-id="c28cb-138">[**MicrosoftDocs/quantum-docs-pr**](https://github.com/MicrosoftDocs/quantum-docs-pr): https://docs.microsoft.com/quantum で公開されているドキュメントのソース コード。</span><span class="sxs-lookup"><span data-stu-id="c28cb-138">[**MicrosoftDocs/quantum-docs-pr**](https://github.com/MicrosoftDocs/quantum-docs-pr): Source code for the documentation published at https://docs.microsoft.com/quantum.</span></span>

> [!NOTE]
> <span data-ttu-id="c28cb-139">現時点では、[**microsoft/Quantum-NC**](https://github.com/microsoft/Quantum-NC) リポジトリに関するコードとドキュメントのコントリビューションは受け付けておりませんが、バグ報告については歓迎しています。</span><span class="sxs-lookup"><span data-stu-id="c28cb-139">We unfortunately cannot accept code and documentation contributions on the [**microsoft/Quantum-NC**](https://github.com/microsoft/Quantum-NC) repository at this time, but we still very much appreciate bug reports.</span></span>

<span data-ttu-id="c28cb-140">また、さまざまなイベント、または Quantum Development Kit に関連する補助機能に重点を置いた他の特化されたリポジトリもあります。</span><span class="sxs-lookup"><span data-stu-id="c28cb-140">There are also a few other, more specialized repositories focusing on different events, or on auxillary functionality related to the Quantum Development Kit.</span></span>

- <span data-ttu-id="c28cb-141">[**msr-quarc/qsharp.sty**](https://github.com/msr-quarc/qsharp.sty):Q# 構文の LaTeX 形式サポート。</span><span class="sxs-lookup"><span data-stu-id="c28cb-141">[**msr-quarc/qsharp.sty**](https://github.com/msr-quarc/qsharp.sty): LaTeX formatting support for Q# syntax.</span></span>
- <span data-ttu-id="c28cb-142">[**msr-quarc/intern-workshop-2019**](https://github.com/msr-quarc/intern-workshop-2019):2019 年のインターン ワークショップで行われた Deutsch–Jozsa チュートリアルの IQ# Notebook</span><span class="sxs-lookup"><span data-stu-id="c28cb-142">[**msr-quarc/intern-workshop-2019**](https://github.com/msr-quarc/intern-workshop-2019): IQ# Notebook for Deutsch–Jozsa tutorial given at the 2019 intern workshop.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c28cb-143">次の手順</span><span class="sxs-lookup"><span data-stu-id="c28cb-143">Next steps</span></span> ##

<span data-ttu-id="c28cb-144">Quantum Development Kit コミュニティに参加していただき、ありがとうございます。ぜひご協力ください。</span><span class="sxs-lookup"><span data-stu-id="c28cb-144">Thanks for being a part of the Quantum Development Kit community, we're excited for your contributions!</span></span>
<span data-ttu-id="c28cb-145">コントリビューションの詳細については、次のいずれかのガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c28cb-145">If you'd like to learn more about contributing, please continue with one of the following guides.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c28cb-146">バグを報告する方法</span><span class="sxs-lookup"><span data-stu-id="c28cb-146">Learn how to report bugs</span></span>](xref:microsoft.quantum.contributing.reporting)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c28cb-147">ドキュメントの投稿方法</span><span class="sxs-lookup"><span data-stu-id="c28cb-147">Learn how to contribute documentation</span></span>](xref:microsoft.quantum.contributing.docs)

> [!div class="nextstepaction"]
> [<span data-ttu-id="c28cb-148">プル要求を開く方法</span><span class="sxs-lookup"><span data-stu-id="c28cb-148">Learn how to open pull requests</span></span>](xref:microsoft.quantum.contributing.pulls)
