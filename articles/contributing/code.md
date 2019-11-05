---
title: 貢献するコード |Microsoft Docs
description: 貢献コード
author: cgranade
ms.author: chgranad
ms.date: 10/12/2018
ms.topic: article
uid: microsoft.quantum.contributing.code
ms.openlocfilehash: cca50e6c63d4bb982aa5f0a59fc19d08ecbec508
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2019
ms.locfileid: "73185904"
---
# <a name="contributing-code"></a><span data-ttu-id="75f4c-103">貢献コード</span><span class="sxs-lookup"><span data-stu-id="75f4c-103">Contributing Code</span></span> #

<span data-ttu-id="75f4c-104">問題の報告とドキュメントの改善に加えて、quantum 開発キットへのコードの投稿は、quantum プログラミングコミュニティでの同僚を支援する非常に直接的な方法である可能性があります。</span><span class="sxs-lookup"><span data-stu-id="75f4c-104">In addition to reporting issues and improving documentation, contributing code to the Quantum Development Kit can be a very direct way to help your peers in the quantum programming community.</span></span>
<span data-ttu-id="75f4c-105">コードを投稿することで、問題の修正、新しい例の提供、既存のライブラリの使いやすさの向上、またはまったく新しい機能の追加を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-105">By contributing code, you can help to fix issues, provide new examples, make existing libraries easier to use, or even add entirely new features.</span></span>

<span data-ttu-id="75f4c-106">このガイドでは、プル要求をレビューして、投稿を最大限に活用するために役立つ情報について少し詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-106">In this guide, we'll detail a bit of what we look for when we review pull requests to help your contribution do the most good.</span></span>

## <a name="what-we-look-for"></a><span data-ttu-id="75f4c-107">検索対象</span><span class="sxs-lookup"><span data-stu-id="75f4c-107">What We Look For</span></span> ##

<span data-ttu-id="75f4c-108">優れたコードの投稿物は、問題の修正、既存の機能の拡張、またはリポジトリのスコープ内にある新機能の追加を行うために、Quantum 開発キットリポジトリの既存の作業に基づいています。</span><span class="sxs-lookup"><span data-stu-id="75f4c-108">An ideal code contribution builds on the existing work in a Quantum Development Kit repository to fix issues, expand existing features, or to add new features that are within the scope of a repository.</span></span>
<span data-ttu-id="75f4c-109">コードの投稿を受け入れると、Quantum 開発キット自体の一部になります。これは、新しい機能がリリースされ、保持され、残りの Quantum 開発キットと同じ方法で開発されるようになります。</span><span class="sxs-lookup"><span data-stu-id="75f4c-109">When we accept a code contribution, it becomes a part of the Quantum Development Kit itself, such that new features will be released, maintained, and developed in the same way as the rest of the Quantum Development Kit.</span></span>
<span data-ttu-id="75f4c-110">このため、投稿物によって追加された機能が十分にテストされ、文書化されている場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="75f4c-110">Thus, it is helpful when functionality added by a contribution is well-tested and is documented.</span></span>

### <a name="unit-tests"></a><span data-ttu-id="75f4c-111">単体テスト</span><span class="sxs-lookup"><span data-stu-id="75f4c-111">Unit Tests</span></span> ###

<span data-ttu-id="75f4c-112">キャノンなどのライブラリを構成する Q # 関数、操作、およびユーザー定義型は、 [**Microsoft/QuantumLibraries**](https://github.com/Microsoft/QuantumLibraries/)リポジトリでの開発の一部として自動的にテストされます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-112">The Q# functions, operations, and user-defined types that make up libraries such as the canon are automatically tested as a part of development on the [**Microsoft/QuantumLibraries**](https://github.com/Microsoft/QuantumLibraries/) repository.</span></span>
<span data-ttu-id="75f4c-113">たとえば、新しいプル要求が開かれたときに、 [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines/)構成によって、クォンタムプログラミングコミュニティが依存している既存の機能が、プル要求の変更によって中断されていないことが確認されます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-113">When a new pull request is opened, for instance, our [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines/) configuration will check that the changes in the pull request do not break any existing functionality that the quantum programming community depends on.</span></span>
<span data-ttu-id="75f4c-114">これらのテストは、 [xunit](https://xunit.github.io/)フレームワークのテストとして Q # の関数と操作を公開する、 [Microsoft の Quantum](https://www.nuget.org/packages/Microsoft.Quantum.Xunit/)パッケージを使用して作成されます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-114">These tests are written using the [Microsoft.Quantum.Xunit](https://www.nuget.org/packages/Microsoft.Quantum.Xunit/) package, which exposes Q# functions and operations as tests for the [xUnit](https://xunit.github.io/) framework.</span></span>

<span data-ttu-id="75f4c-115">[`Standard/tests/Standard.Tests.csproj`](https://github.com/microsoft/QuantumLibraries/blob/master/Standard/tests/Standard.Tests.csproj)は、この xunit 統合を使用して、`Test`で終了するすべての関数または操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-115">The [`Standard/tests/Standard.Tests.csproj`](https://github.com/microsoft/QuantumLibraries/blob/master/Standard/tests/Standard.Tests.csproj) uses this xUnit integration to run any functions or operations ending in `Test`.</span></span>
<span data-ttu-id="75f4c-116">たとえば、次の関数を使用すると、<xref:microsoft.quantum.canon.fst> と <xref:microsoft.quantum.canon.snd> 関数が両方とも代表的な例で正しい出力を返すようになります。</span><span class="sxs-lookup"><span data-stu-id="75f4c-116">For instance, the following function is used to ensure that the <xref:microsoft.quantum.canon.fst> and <xref:microsoft.quantum.canon.snd> functions both return the right outputs in a representative example.</span></span>
<span data-ttu-id="75f4c-117">`Fst` または `Snd` の出力が正しくない場合は、`fail` ステートメントを使用してテストが失敗します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-117">If the output of `Fst` or `Snd` is incorrect, the `fail` statement is used to cause the test to fail.</span></span>

```qsharp
function PairTest () : Unit {
    let pair = (12, PauliZ);

    if (Fst(pair) != 12) {
        let actual = Fst(pair);
        fail $"Expected 12, actual {actual}.";
    }

    if (Snd(pair) != PauliZ) {
        let actual = Snd(pair);
        fail $"Expected PauliZ, actual {actual}.";
    }
}
```

<span data-ttu-id="75f4c-118">より複雑な条件を確認するには、「標準ライブラリ」ガイドの[「テスト」セクション](xref:microsoft.quantum.libraries.diagnostics)の手法を使用します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-118">More complicated conditions can be checked using the techniques in the [testing section](xref:microsoft.quantum.libraries.diagnostics) of the standard libraries guide.</span></span>
<span data-ttu-id="75f4c-119">たとえば、次のテストでは、<xref:microsoft.quantum.canon.applywith> によって呼び出された `H(q); X(q); H(q);` が `Z(q)`と同じものであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-119">For instance, the following test checks that `H(q); X(q); H(q);` as called by <xref:microsoft.quantum.canon.applywith> does the same thing as `Z(q)`.</span></span>

```qsharp
operation WithTest () : Unit {
    let actual = ApplyWith(H, X, _);
    let expected = Z;
    AssertOperationsEqualReferenced(ApplyToEach(actual, _), ApplyToEachA(expected, _), 4);
}
```

<span data-ttu-id="75f4c-120">新しい機能を追加する場合は、新しいテストを追加して、意図した内容が確実に行われるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="75f4c-120">When adding new features, it's a good idea to also add new tests to make sure that your contribution does what it's supposed to.</span></span>
<span data-ttu-id="75f4c-121">これにより、コミュニティの他のメンバーが機能を保守および開発できるようになり、特に、機能に依存する可能性があることを他の開発者が知ることができます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-121">This helps the rest of the community to maintain and develop your feature, and in particular helps other developers know that they can rely on your feature.</span></span>

> [!NOTE]
> <span data-ttu-id="75f4c-122">これも同様に機能します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-122">This works the other way around, too!</span></span>
> <span data-ttu-id="75f4c-123">一部のテストが欠落している既存の機能がある場合は、テストカバレッジの追加を支援することで、コミュニティに大きな貢献をします。</span><span class="sxs-lookup"><span data-stu-id="75f4c-123">If there's an existing feature that's missing some tests, helping us add test coverage would make a great contribution to the community.</span></span>

<span data-ttu-id="75f4c-124">ローカルでは、Visual Studio テストエクスプローラーまたは `dotnet test` コマンドを使用して単体テストを実行できます。これにより、プル要求を開く前に投稿を確認できます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-124">Locally, unit tests can be run using the Visual Studio Test Explorer or the `dotnet test` command, so that you can check your contribution before opening up a pull request.</span></span>

<!-- TODO:
### Comments and Documentation ###

### Citations and References ### -->

## <a name="when-well-reject-a-pull-request"></a><span data-ttu-id="75f4c-125">プル要求を却下する場合</span><span class="sxs-lookup"><span data-stu-id="75f4c-125">When We'll Reject a Pull Request</span></span> ##

<span data-ttu-id="75f4c-126">場合によっては、投稿のプル要求を拒否することがあります。</span><span class="sxs-lookup"><span data-stu-id="75f4c-126">Sometimes, we'll reject the pull request for a contribution.</span></span>
<span data-ttu-id="75f4c-127">このような状況が発生したとしても、特定の貢献を受け入れることができない理由がいくつかあるので、これは悪いことではありません。</span><span class="sxs-lookup"><span data-stu-id="75f4c-127">If this happens to you, it doesn't mean that it's bad, as there's a number of reasons why we might not be able to accept a particular contribution.</span></span>
<span data-ttu-id="75f4c-128">おそらく、多くの場合、クォンタムプログラミングコミュニティに貢献しているのは良い方法ですが、Quantum 開発キットリポジトリは開発に適していません。</span><span class="sxs-lookup"><span data-stu-id="75f4c-128">Perhaps most commonly, a contribution to the quantum programming community is a really good one, but the Quantum Development Kit repositories aren't the right place to develop it.</span></span>
<span data-ttu-id="75f4c-129">このような場合は、独自のリポジトリ---、Quantum 開発キットの強度の一部にすることを強くお勧めします。これは、キャノンおよび化学を配布するのと同じ方法で、GitHub と NuGet.org を使用して独自のライブラリを簡単に作成および配布できることです。ライブラリを今すぐお試しください。</span><span class="sxs-lookup"><span data-stu-id="75f4c-129">In such cases, we strongly encourage you to make your own repository --- part of the strength of the Quantum Development Kit is that it's easy to make and distribute your own libraries using GitHub and NuGet.org, the same way that we distribute the canon and chemistry libraries today.</span></span>

<span data-ttu-id="75f4c-130">それ以外の場合は、管理と開発の準備が整っていないため、適切な投稿を拒否することがあります。</span><span class="sxs-lookup"><span data-stu-id="75f4c-130">At other times, we may reject a good contribution simply because we aren't yet ready to maintain and develop it.</span></span>
<span data-ttu-id="75f4c-131">すべてを実行するのは困難な場合があるため、ロードマップとしてどのような機能を使用できるかを計画します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-131">It can be difficult to do everything, so we plan out what features we're best able to work on as a roadmap.</span></span>
<span data-ttu-id="75f4c-132">これは、サードパーティ製のライブラリとして機能をリリースすることによって、非常に意味があります。</span><span class="sxs-lookup"><span data-stu-id="75f4c-132">This can be another case where releasing a feature as a third-party library can make a lot of sense.</span></span>
<span data-ttu-id="75f4c-133">または、機能を変更して、最適な作業を行うことができるように、ロードマップに適合するように、機能を変更することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="75f4c-133">Alternatively, we may ask for your help in modifying a feature to better fit into our roadmap so that we can do the best work we can with it.</span></span>

<span data-ttu-id="75f4c-134">また、プル要求を使用するのに役立つドキュメントや単体テストが必要な場合、または、ユーザーが機能を見つけるのが困難になるように、他の Q # ライブラリのスタイルとして十分に異なっている場合にも、プル要求の変更を要求します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-134">We'll also ask for changes to a pull request if it requires more documentation or unit tests to help us make use of it, or if it differs enough in style from the rest of the Q# libraries that it will make it harder for users to find your feature.</span></span>
<span data-ttu-id="75f4c-135">このような場合は、投稿を容易にするために追加または変更できるものについて、コードレビューでアドバイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-135">In these cases, we'll try to offer some advice in code reviews about what can be added or changed to make your contribution easier for us to include.</span></span>

<span data-ttu-id="75f4c-136">最後に、 [Microsoft オープンソース](https://opensource.microsoft.com/codeofconduct/)倫理規定に記載されているように、クォンタムコンピューティングコミュニティに悪影響を及ぼす投稿を受け入れることはできません。</span><span class="sxs-lookup"><span data-stu-id="75f4c-136">Finally, we cannot accept contributions that cause harm the quantum computing community, as outlined in the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).</span></span>
<span data-ttu-id="75f4c-137">私たちは、現在のすばらしい多様性の中でも、今後もさらに包括的になるように、共同作業がクォンタムコンピューティングコミュニティ全体に提供されるようにしたいと考えています。</span><span class="sxs-lookup"><span data-stu-id="75f4c-137">We want to ensure that contributions serve the entire quantum computing community, both in its current wonderful diversity, and in the future as it grows to become still more inclusive.</span></span>
<span data-ttu-id="75f4c-138">この目標を達成するための支援を歓迎します。</span><span class="sxs-lookup"><span data-stu-id="75f4c-138">We appreciate your help in realizing this goal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75f4c-139">次のステップ</span><span class="sxs-lookup"><span data-stu-id="75f4c-139">Next steps</span></span> ##

<span data-ttu-id="75f4c-140">Quantum 開発キットを利用して、quantum プログラミングコミュニティ全体にとって優れたリソースを作成しようとしていただき、誠にありがとうございます。</span><span class="sxs-lookup"><span data-stu-id="75f4c-140">Thanks for helping to make the Quantum Development Kit a great resource for the entire quantum programming community!</span></span>
<span data-ttu-id="75f4c-141">詳細については、Q # のスタイルに関する次のガイドを参照してください。</span><span class="sxs-lookup"><span data-stu-id="75f4c-141">To learn more, please continue with the following guide on Q# style.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75f4c-142">Q # スタイルのガイドラインについて学習する</span><span class="sxs-lookup"><span data-stu-id="75f4c-142">Learn about Q# style guidelines</span></span>](xref:microsoft.quantum.contributing.style)