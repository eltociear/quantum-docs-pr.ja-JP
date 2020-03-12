---
title: 'Q # API 設計の原則'
description: 'Q # API 設計の原則'
author: cgranade
ms.author: chgranad
ms.date: 3/9/2020
ms.topic: article
uid: microsoft.quantum.contributing.api-design
ms.openlocfilehash: 03c32331f8988181ec6fedcfc207d752b4a880b2
ms.sourcegitcommit: d61b388651351e5abd4bfe7a672e88b84a6697f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "79024204"
---
# <a name="q-api-design-principles"></a><span data-ttu-id="923a4-103">Q # API 設計の原則</span><span class="sxs-lookup"><span data-stu-id="923a4-103">Q# API Design Principles</span></span>

## <a name="introduction"></a><span data-ttu-id="923a4-104">はじめに</span><span class="sxs-lookup"><span data-stu-id="923a4-104">Introduction</span></span>

<span data-ttu-id="923a4-105">言語およびプラットフォームとして、ユーザーは、クォンタムアプリケーションの記述、実行、理解、調査を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-105">As a language and as a platform, Q# empowers users to write, run, understand, and explore quantum applications.</span></span>
<span data-ttu-id="923a4-106">ユーザーを支援するために、Q # ライブラリを設計する際には、一連の API 設計原則に従って設計を進め、quantum 開発コミュニティで使用可能なライブラリを作成できるようにします。</span><span class="sxs-lookup"><span data-stu-id="923a4-106">In order to empower users, when we design Q# libraries, we follow a set of API design principles to guide our designs and to help us make usable libraries for the the quantum development community.</span></span>
<span data-ttu-id="923a4-107">この記事では、これらの原則について説明し、Q # Api を設計するときに適用する方法を示す例を示します。</span><span class="sxs-lookup"><span data-stu-id="923a4-107">This article lists these principles, and gives examples to help guide how to apply them when designing Q# APIs.</span></span>

> [!TIP]
> <span data-ttu-id="923a4-108">これは、ライブラリの開発と詳細なライブラリの投稿をガイドするための、非常に詳細なドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="923a4-108">This is a fairly detailed document that's intended to help guide library development and in-depth library contributions.</span></span>
> <span data-ttu-id="923a4-109">Q # で独自のライブラリを作成している場合や、 [q # ライブラリリポジトリ](https://github.com/microsoft/QuantumLibraries)に大きな機能を提供している場合は、最も役に立つでしょう。</span><span class="sxs-lookup"><span data-stu-id="923a4-109">You'll probably find it most useful if you're writing your own libraries in Q#, or if you're contributing larger features to the [Q# libraries repository](https://github.com/microsoft/QuantumLibraries).</span></span>
>
> <span data-ttu-id="923a4-110">一方、Quantum 開発キットに投稿する方法については、後で説明することをお[勧めします。](xref:microsoft.quantum.contributing)</span><span class="sxs-lookup"><span data-stu-id="923a4-110">On the other hand, if you're looking to learn how to contribute to the Quantum Development Kit more generally, we suggest starting with the [contribution guide](xref:microsoft.quantum.contributing).</span></span>
> <span data-ttu-id="923a4-111">Q # コードを書式設定する方法についての一般的な情報を探している場合は、[スタイルガイド](xref:microsoft.quantum.contributing.style)を確認することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="923a4-111">If you're looking for more general information about how we recommend formatting your Q# code, you may be interested in checking out the [style guide](xref:microsoft.quantum.contributing.style).</span></span>

## <a name="general-principles"></a><span data-ttu-id="923a4-112">一般的な原則</span><span class="sxs-lookup"><span data-stu-id="923a4-112">General Principles</span></span>

<span data-ttu-id="923a4-113">**主要原則:** クォンタムアプリケーションに重点を置いた Api を公開します。</span><span class="sxs-lookup"><span data-stu-id="923a4-113">**Key principle:** Expose APIs that places the focus on quantum applications.</span></span>

- <span data-ttu-id="923a4-114">アルゴリズムとアプリケーションの高レベルの構造を反映する操作と関数の名前**を選択 ✅** ます。</span><span class="sxs-lookup"><span data-stu-id="923a4-114">✅ **DO** choose operation and function names that reflect the   high-level structure of algorithms and applications.</span></span>
- <span data-ttu-id="923a4-115">⛔️は、主に低レベルの実装の詳細に焦点を当てた Api を公開し**ません**。</span><span class="sxs-lookup"><span data-stu-id="923a4-115">⛔️ **DON'T** expose APIs that focus primarily on low-level   implementation details.</span></span>

<span data-ttu-id="923a4-116">**主要原則:** 各 API の設計をサンプルのユースケースで開始し、Api を直感的に使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="923a4-116">**Key principle:** Start each API design with sample use cases to ensure that APIs are intuitive to use.</span></span>

- <span data-ttu-id="923a4-117">✅、パブリック API の各コンポーネントに対応するユースケースがあることを確認します。開始から使用できるすべてのを設計する必要はあり**ません**。</span><span class="sxs-lookup"><span data-stu-id="923a4-117">✅ **DO** ensure that each component of a public API has a corresponding use case, rather than trying to design for all possible uses from the start.</span></span>
    <span data-ttu-id="923a4-118">別の方法として、公開されている Api は役に立たないようにしてください。ただし、API の各部分には、役に立つ*具体的*な例が含まれていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="923a4-118">Put differently, don't introduce public APIs in case they are useful, but make sure that each part of an API has a *concrete* example in which it will be useful.</span></span>

  <span data-ttu-id="923a4-119">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-119">*Examples:*</span></span>
  - <span data-ttu-id="923a4-120">@"microsoft.quantum.canon.applytoeachca" を `ApplyToEachCA(H, _)` として使用して、複数のクォンタムアルゴリズムの一般的なタスクである uniform 法則状態でレジスタを準備することができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-120">@"microsoft.quantum.canon.applytoeachca" can be used as `ApplyToEachCA(H, _)` to prepare registers in a uniform superposition state, a common task in many quantum algorithms.</span></span> <span data-ttu-id="923a4-121">同じ操作を、準備、数値、および oracle ベースのアルゴリズムの他の多くのタスクにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="923a4-121">The same operation can also be used for many other tasks in preparation, numerics, and oracle-based algorithms.</span></span>

- <span data-ttu-id="923a4-122">新しい API 設計を brainstorm およびワークショップに ✅ て、**直感的で、** 提案されたユースケースを満たすことを再確認します。</span><span class="sxs-lookup"><span data-stu-id="923a4-122">✅ **DO** brainstorm and workshop new API designs to double-check   that they are intuitive and meet proposed use cases.</span></span>

  <span data-ttu-id="923a4-123">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-123">*Examples:*</span></span>
  - <span data-ttu-id="923a4-124">現在の Q\# コードを調べて、新しい API 設計によって既存の実装がどのように簡略化され、明確になるかを確認します。</span><span class="sxs-lookup"><span data-stu-id="923a4-124">Inspect current Q\# code to see how new API designs could   simplify and clarify existing implementations.</span></span>
  - <span data-ttu-id="923a4-125">主要ユーザーの代表者として提示された API 設計を確認します。</span><span class="sxs-lookup"><span data-stu-id="923a4-125">Review proposed API designs with representatives of primary   audiences.</span></span>

<span data-ttu-id="923a4-126">**主要原則:** 読み取り可能なコードをサポートし、奨励するように Api を設計します。</span><span class="sxs-lookup"><span data-stu-id="923a4-126">**Key principle:** Design APIs to support and encourage readable code.</span></span>

- <span data-ttu-id="923a4-127">✅、ドメインの専門家や専門家以外の人がコードを**読み取ることが**できるようにします。</span><span class="sxs-lookup"><span data-stu-id="923a4-127">✅ **DO** ensure that code is readable by domain experts and   non-experts alike.</span></span>
- <span data-ttu-id="923a4-128">✅**は**、上位レベルのアルゴリズム内で各操作と関数の効果に重点を置きます。ドキュメントを使用して、必要に応じて実装の詳細について掘り下げます。</span><span class="sxs-lookup"><span data-stu-id="923a4-128">✅ **DO** place the focus on the effects of each operation and   function within the high-level algorithm, using documentation to   delve into implementation details as appropriate.</span></span>
- <span data-ttu-id="923a4-129">✅、必要に応じて、一般的な[Q\# スタイルガイド](xref:microsoft.quantum.contributing.style)に従って**ください**。</span><span class="sxs-lookup"><span data-stu-id="923a4-129">✅ **DO** follow the common [Q\# style guide](xref:microsoft.quantum.contributing.style) whenever applicable.</span></span>

<span data-ttu-id="923a4-130">**主要原則:** 安定した Api を設計し、上位互換性を提供します。</span><span class="sxs-lookup"><span data-stu-id="923a4-130">**Key principle:** Design APIs to be stable and to provide forward compatibility.</span></span>

- <span data-ttu-id="923a4-131">互換性に影響する変更が必要な**場合は、✅ に**よって古い api が適切に廃止されます。</span><span class="sxs-lookup"><span data-stu-id="923a4-131">✅ **DO** deprecate old APIs gracefully when breaking changes are   required.</span></span>

- <span data-ttu-id="923a4-132">✅**は**、既存のユーザーコードが非推奨になったときに正しく動作するようにする "shim" 操作と関数を提供します。</span><span class="sxs-lookup"><span data-stu-id="923a4-132">✅ **DO** provide "shim" operations and functions that allow   existing user code to operate correctly during deprecation.</span></span>

  <span data-ttu-id="923a4-133">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-133">*Examples:*</span></span>
  - <span data-ttu-id="923a4-134">`EstimateExpectation` と呼ばれる操作の名前を `EstimateAverage`に変更する場合は、既存のコードが引き続き正常に動作するように、元の操作を新しい名前で呼び出す `EstimateExpectation` という新しい操作を導入します。</span><span class="sxs-lookup"><span data-stu-id="923a4-134">When renaming an operation called `EstimateExpectation` to   `EstimateAverage`, introduce a new operation called   `EstimateExpectation` that calls the original operation at   its new name, so that existing code can continue to work   correctly.</span></span>

- <span data-ttu-id="923a4-135">✅ は、@"microsoft.quantum.core.deprecated" 属性を**使用して**、廃止をユーザーに通知します。</span><span class="sxs-lookup"><span data-stu-id="923a4-135">✅ **DO** use the @"microsoft.quantum.core.deprecated" attribute to communicate deprecations to the user.</span></span>

- <span data-ttu-id="923a4-136">✅ 操作または関数の名前を変更する場合は、新しい名前を `@Deprecated`への文字列入力とし**て指定し**ます。</span><span class="sxs-lookup"><span data-stu-id="923a4-136">✅ When renaming an operation or function, **DO** provide the new   name as a string input to `@Deprecated`.</span></span>

- <span data-ttu-id="923a4-137">プレビューリリースの場合は少なくとも6か月以上、サポートされているリリースでは少なくとも2年間は、既存の関数または操作を削除し**ない**ように⛔️します。</span><span class="sxs-lookup"><span data-stu-id="923a4-137">⛔️ **DON'T** remove existing functions or operations without a   deprecation period of at least six months for preview releases,   or at least two years for supported releases.</span></span>

## <a name="functions-and-operations"></a><span data-ttu-id="923a4-138">関数と操作</span><span class="sxs-lookup"><span data-stu-id="923a4-138">Functions and Operations</span></span>

<span data-ttu-id="923a4-139">**重要な原則:** すべての関数と操作が API 内で明確に定義された1つの目的を持っていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="923a4-139">**Key principle:** ensure that every function and operation has a single well-defined purpose within the API.</span></span>

- <span data-ttu-id="923a4-140">⛔️は、関連のない複数のタスクを実行する関数や操作を公開し**ません**。</span><span class="sxs-lookup"><span data-stu-id="923a4-140">⛔️ **DON'T** expose functions and operations that perform multiple   unrelated tasks.</span></span>

<span data-ttu-id="923a4-141">**重要な原則:** 可能な限り再利用できるように、関数と操作を設計し、将来のニーズを予測します。</span><span class="sxs-lookup"><span data-stu-id="923a4-141">**Key principle:** design functions and operations to be as reusable as possible, and to anticipate future needs.</span></span>

- <span data-ttu-id="923a4-142">✅**は**、同じ API と以前の既存のライブラリの両方で、他の関数や操作に合わせて関数と操作を設計する必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-142">✅ **DO** design functions and operations to compose well with other   functions and operations, both in the same API and in previously   existing libraries.</span></span>

  <span data-ttu-id="923a4-143">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-143">*Examples:*</span></span>
  - <span data-ttu-id="923a4-144">@"microsoft.quantum.canon.delay" 操作では、入力に関して最小限の仮定が行われるため、Q # 標準ライブラリ全体またはユーザーによる定義に従って、いずれかの操作のアプリケーションを遅延させることができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-144">The @"microsoft.quantum.canon.delay" operation makes minimal assumptions about its input, and thus can be used to delay applications of either operations across the Q# standard library or as defined by users.</span></span>
    <!-- TODO: define bad example. -->

- <span data-ttu-id="923a4-145">✅**は**、純粋に確定的なクラシックロジックを操作ではなく関数として公開します。</span><span class="sxs-lookup"><span data-stu-id="923a4-145">✅ **DO** expose purely deterministic classical logic as   as functions rather than operations.</span></span>

  <span data-ttu-id="923a4-146">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-146">*Examples:*</span></span>
  - <span data-ttu-id="923a4-147">浮動小数点入力をランダムに記述できるサブルーチンでは、操作 `Square : Double => Double`ではなく、`Squared : Double -> Double` としてユーザーに公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-147">A subroutine which squares its floating-point input can be written deterministically, and so should be exposed to the user as `Squared : Double -> Double` rather than as an operation `Square : Double => Double`.</span></span> <span data-ttu-id="923a4-148">これにより、サブルーチンをより多くの場所 (たとえば、他の関数の内部) で呼び出すことができ、パフォーマンスと最適化に影響を与える有用な最適化情報がコンパイラに提供されます。</span><span class="sxs-lookup"><span data-stu-id="923a4-148">This allows for the subroutine to be called in more places (e.g.: inside of other functions), and provides useful optimization information to the compiler that can affect performance and optimizations.</span></span>
  - <span data-ttu-id="923a4-149">`ForEach<'TInput, 'TOutput>('TInput => 'TOutput, 'TInput[]) => 'TOutput[]` と `Mapped<'TInput, 'TOutput>('TInput -> 'TOutput, 'TInput[]) -> 'TOutput[]` は、決定性に関して行われる保証とは異なります。どちらも、さまざまな状況で役立ちます。</span><span class="sxs-lookup"><span data-stu-id="923a4-149">`ForEach<'TInput, 'TOutput>('TInput => 'TOutput, 'TInput[]) => 'TOutput[]` and `Mapped<'TInput, 'TOutput>('TInput -> 'TOutput, 'TInput[]) -> 'TOutput[]` differ in the guarantees made with respect to   determinism; both are useful in different circumstances.</span></span>
  - <span data-ttu-id="923a4-150">クォンタム操作のアプリケーションを変換する API ルーチンは、決定論的な方法で実行されることが多いため、`CControlled<'T>(op : 'T => Unit) => ((Bool, 'T) => Unit)`などの関数として使用できます。</span><span class="sxs-lookup"><span data-stu-id="923a4-150">API routines that transform the application of quantum   operations can often be carried out in a deterministic     fashion and hence can be made available as functions such as   `CControlled<'T>(op : 'T => Unit) => ((Bool, 'T) => Unit)`.</span></span>

- <span data-ttu-id="923a4-151">✅**は**、必要に応じて型パラメーターを使用して、各関数および操作に対して適切な入力型を一般化する必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-151">✅ **DO** generalize the input type as much as reasonable for each   function and operation, using type parameters as needed.</span></span>

  <span data-ttu-id="923a4-152">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-152">*Examples:*</span></span>
  - <span data-ttu-id="923a4-153">`ApplyToEach` には、最も一般的なアプリケーションの種類である `((Qubit => Unit), Qubit[]) => Unit`ではなく、型 `<'T>(('T => Unit), 'T[]) => Unit` があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-153">`ApplyToEach` has type `<'T>(('T => Unit), 'T[]) => Unit` rather than the specific type of its most common   application, `((Qubit => Unit), Qubit[]) => Unit`.</span></span>

> [!TIP]
> <span data-ttu-id="923a4-154">将来のニーズを予測することが重要ですが、ユーザーの具体的な問題を解決することも重要です。</span><span class="sxs-lookup"><span data-stu-id="923a4-154">It is important to anticipate future needs, but it is also important to solve concrete problems for your users.</span></span>
> <span data-ttu-id="923a4-155">この重要な原則に基づいて行動することは、Api の開発を避けるために、常に慎重に検討してバランスを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-155">Acting on this key principle thus always requires careful consideration and balancing to avoid developing APIs "just in case."</span></span>

<span data-ttu-id="923a4-156">**重要な原則:** 予測可能な関数と操作の入力と出力の種類を選択し、呼び出し可能な目的を伝えます。</span><span class="sxs-lookup"><span data-stu-id="923a4-156">**Key principle:** choose input and output types for functions and operations that are predictable, and that communicate the purpose of a callable.</span></span>

- <span data-ttu-id="923a4-157">✅ タプル型を使用して、入力と出力を論理的にグループ化します。**これ**は、まとめて考慮した場合にのみ重要です。</span><span class="sxs-lookup"><span data-stu-id="923a4-157">✅ **DO** use tuple types to logically group inputs and outputs that are only significant when considered together.</span></span> <span data-ttu-id="923a4-158">このような場合は、ユーザー定義型を使用することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="923a4-158">Consider using a user-defined type in these cases.</span></span>

  <span data-ttu-id="923a4-159">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-159">*Examples:*</span></span>
  - <span data-ttu-id="923a4-160">別の関数のローカル最小を出力する関数は、検索範囲の範囲を入力として受け取る必要がある場合があります。これは、`LocalMinima(fn : (Double -> Double), (left : Double, right : Double)) : Double` が適切なシグネチャである可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="923a4-160">A function to output the local minima of another function   may need to take bounds of a search interval as input, such   that `LocalMinima(fn : (Double -> Double), (left : Double, right : Double)) : Double` may be an appropriate signature.</span></span>
  - <span data-ttu-id="923a4-161">パラメーターシフト手法を使用して機械学習分類子の派生物を推定する操作では、シフトとシフト解除の両方のパラメーターベクトルを入力として取得する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-161">An operation to estimate a derivative of a machine learning classifier using the parameter shift technique may need to take both the shifted and unshifted parameter vectors as inputs.</span></span> <span data-ttu-id="923a4-162">この場合、`(unshifted : Double[], shifted : Double[])` に似た入力が適している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-162">An input similar to `(unshifted : Double[], shifted : Double[])` may be appropriate in this case.</span></span>

- <span data-ttu-id="923a4-163">✅**は**、入力と出力の組の項目を、さまざまな関数や操作にわたって一貫して並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="923a4-163">✅ **DO** order items in input and output tuples consistently   across different functions and operations.</span></span>

  <span data-ttu-id="923a4-164">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-164">*Examples:*</span></span>
  - <span data-ttu-id="923a4-165">2つの関数または関数、またはそれぞれが回転角度とターゲット qubit を入力として使用することを検討している場合は、各入力タプルの順序が同じであることを確認します。</span><span class="sxs-lookup"><span data-stu-id="923a4-165">If considering two or functions or operations that each take a rotation angle and a target qubit as inputs, ensure that they are ordered the same in each input tuple.</span></span> <span data-ttu-id="923a4-166">つまり、`ApplyRotation(angle : Double, target : Qubit) : Unit is Adj + Ctl` を優先し、`ApplyRotation(target : Qubit, angle : Double) : Unit is Adj + Ctl` と `DelayedRotation(angle : Double, target : Qubit) : (Unit => Unit is Adj + Ctl)`に `DelayedRotation(angle : Double, target : Qubit) : (Unit => Unit is Adj + Ctl)` します。</span><span class="sxs-lookup"><span data-stu-id="923a4-166">That is, prefer `ApplyRotation(angle : Double, target : Qubit) : Unit is Adj + Ctl` and `DelayedRotation(angle : Double, target : Qubit) : (Unit => Unit is Adj + Ctl)` to `ApplyRotation(target : Qubit, angle : Double) : Unit is Adj + Ctl` and `DelayedRotation(angle : Double, target : Qubit) : (Unit => Unit is Adj + Ctl)`.</span></span>

<span data-ttu-id="923a4-167">**重要な原則:** 部分アプリケーションなどの Q\# 言語機能に適した関数と操作を設計します。</span><span class="sxs-lookup"><span data-stu-id="923a4-167">**Key principle:** design functions and operations to work well with Q\# language features such as partial application.</span></span>

- <span data-ttu-id="923a4-168">✅**は**、最も一般的に適用される入力 (つまり、部分的なアプリケーションがカリー化と同様に動作するように) を最初に実行するように入力タプル内の項目を並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="923a4-168">✅ **DO** order items in input tuples such that the most commonly   applied inputs occur first (i.e.: so that partial application   acts similarly to currying).</span></span>

  <span data-ttu-id="923a4-169">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-169">*Examples:*</span></span>
  - <span data-ttu-id="923a4-170">入力として浮動小数点数と qubit を受け取る演算 `ApplyRotation` は、通常、型 `Qubit => Unit`の入力を期待する操作で使用するために、最初に浮動小数点入力と共に部分的に適用されることがあります。</span><span class="sxs-lookup"><span data-stu-id="923a4-170">An operation `ApplyRotation` that takes a floating-point number and a qubit as inputs may often be partially applied with the floating-point input first for use with operations that expect an input of type `Qubit => Unit`.</span></span> <span data-ttu-id="923a4-171">したがって、`operation ApplyRotation(angle : Double, target : Qubit) : Unit is Adj + Ctl` のシグネチャ</span><span class="sxs-lookup"><span data-stu-id="923a4-171">Thus, a signature of `operation ApplyRotation(angle : Double, target : Qubit) : Unit is Adj + Ctl`</span></span>
      <span data-ttu-id="923a4-172">部分的なアプリケーションで最も一貫して動作します。</span><span class="sxs-lookup"><span data-stu-id="923a4-172">would work most consistently with partial application.</span></span>
  - <span data-ttu-id="923a4-173">通常、このガイダンスでは、入力タプル内のすべてのすべての古典データを、入力タプルのすべての qubits の前に配置しますが、実際の API の呼び出し方法については、適切な判断を行います。</span><span class="sxs-lookup"><span data-stu-id="923a4-173">Typically, this guidance means placing all classical data   before all qubits in input tuples, but use good judgment and   examine how your API is called in practice.</span></span>

## <a name="user-defined-types"></a><span data-ttu-id="923a4-174">ユーザー定義型</span><span class="sxs-lookup"><span data-stu-id="923a4-174">User-Defined Types</span></span>

<span data-ttu-id="923a4-175">**重要な原則:** ユーザー定義型を使用すると、api の表現性と利便性を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-175">**Key principle:** use user-defined types to help make APIs more expressive and convenient to use.</span></span>

- <span data-ttu-id="923a4-176">新しいユーザー定義型を導入して、長い型や複雑な型を簡単に使用**できるように**✅ ます。</span><span class="sxs-lookup"><span data-stu-id="923a4-176">✅ **DO** introduce new user-defined types to provide helpful   shorthand for long and/or complicated types.</span></span>

  <span data-ttu-id="923a4-177">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-177">*Examples:*</span></span>
  - <span data-ttu-id="923a4-178">通常、3つの qubit 配列入力を持つ演算型が入力として取得される場合、または出力として返される場合は、などの UDT を指定し `newtype TimeDependentBlockEncoding = ((Qubit[], Qubit[], Qubit[]) => Unit is Adj + Ctl)`</span><span class="sxs-lookup"><span data-stu-id="923a4-178">In cases where an operation type with three qubit array inputs is commonly taken as an input or returned as an output, providing a UDT such as `newtype TimeDependentBlockEncoding = ((Qubit[], Qubit[], Qubit[]) => Unit is Adj + Ctl)`</span></span>
      <span data-ttu-id="923a4-179">は、便利なショートハンドを提供するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="923a4-179">can help provide a useful shorthand.</span></span>

- <span data-ttu-id="923a4-180">特定の基本型を使用する必要があることを示すために、新しいユーザー定義型**を導入 ✅** ます。</span><span class="sxs-lookup"><span data-stu-id="923a4-180">✅ **DO** introduce new user-defined types to indicate that a given   base type should only be used in a very particular sense.</span></span>

  <span data-ttu-id="923a4-181">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-181">*Examples:*</span></span>
  - <span data-ttu-id="923a4-182">特に、古典的なデータをクォンタムレジスタにエンコードする操作として解釈する必要がある操作は、ユーザー定義型 `newtype InputEncoder = (Apply : (Qubit[] => Unit))`のラベルに適している場合があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-182">An operation that should be interpreted specifically as an   operation that encodes classical data into a quantum   register may be appropriate to label with a user-defined   type `newtype InputEncoder = (Apply : (Qubit[] => Unit))`.</span></span>

- <span data-ttu-id="923a4-183">今後の拡張が可能な名前付きの項目を使用して、新しいユーザー定義型**を導入 ✅** ます (たとえば、後で追加の名前付き項目を含む可能性のある結果構造)。</span><span class="sxs-lookup"><span data-stu-id="923a4-183">✅ **DO** introduce new user-defined types with named items that   allow for future extensibility (e.g.: a results structure that   may contain additional named items in the future).</span></span>

  <span data-ttu-id="923a4-184">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-184">*Examples:*</span></span>
  - <span data-ttu-id="923a4-185">操作 `TrainModel` によって多数の構成オプションが公開され、これらのオプションが `TrainingOptions` 新しい UDT として公開され、新しい関数が提供され `DefaultTrainingOptions : Unit -> TrainingOptions` ユーザーは、TrainingOptions UDT 値内の特定の名前付き項目をオーバーライドできますが、ライブラリ開発者は必要に応じて新しい UDT 項目を追加できます。</span><span class="sxs-lookup"><span data-stu-id="923a4-185">When an operation `TrainModel` exposes a large number of   configuration options, exposing these options as a new   `TrainingOptions` UDT and providing a new function   `DefaultTrainingOptions : Unit -> TrainingOptions` allows   users to override specific named items in TrainingOptions   UDT values while still allowing library developers to add   new UDT items as appropriate.</span></span>

- <span data-ttu-id="923a4-186">✅、新しいユーザー定義型の名前付き項目を宣言して、ユーザーに正しい組分解を知ら**せるように**する必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-186">✅ **DO** declare named items for new user-defined types in   preference to requiring users to know the correct tuple   deconstruction.</span></span>

  <span data-ttu-id="923a4-187">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-187">*Examples:*</span></span>
  - <span data-ttu-id="923a4-188">極分解で複素数を表す場合は、`newtype ComplexPolar = (Double, Double)`に `newtype ComplexPolar = (Magnitude: Double, Argument: Double)` を優先します。</span><span class="sxs-lookup"><span data-stu-id="923a4-188">When representing a complex number in its polar   decomposition, prefer   `newtype ComplexPolar = (Magnitude: Double, Argument: Double)` to   `newtype ComplexPolar = (Double, Double)`.</span></span>

<span data-ttu-id="923a4-189">**重要な原則:** ユーザー定義型を使用すると、認知の負荷が軽減され、ユーザーが追加の概念や用語を習得する必要がありません。</span><span class="sxs-lookup"><span data-stu-id="923a4-189">**Key principle:** use user-defined types in ways reduce  cognitive load and that don't require the user to learn additional concepts and nomenclature.</span></span>

- <span data-ttu-id="923a4-190">⛔️ラップ解除演算子 (`!`) を頻繁に使用する必要があるユーザー定義型を導入したり、通常は複数レベルのラップ解除が必要になること**があります**。</span><span class="sxs-lookup"><span data-stu-id="923a4-190">⛔️ **DON'T** introduce user-defined types that require the user to make frequent use of the unwrap operator (`!`), or that commonly require multiple levels of unwrapping.</span></span> <span data-ttu-id="923a4-191">次のような軽減策が考えられます。</span><span class="sxs-lookup"><span data-stu-id="923a4-191">Possible mitigation strategies include:</span></span>

  - <span data-ttu-id="923a4-192">1つの項目を持つユーザー定義型を公開する場合は、その項目の名前を定義することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="923a4-192">When exposing a user-defined type with a single item, consider defining a name for that item.</span></span> <span data-ttu-id="923a4-193">たとえば、`newtype Encoder = (Qubit[] => Unit is Adj + Ctl)`を優先する `newtype Encoder = (Apply : (Qubit[] => Unit is Adj + Ctl))` を検討します。</span><span class="sxs-lookup"><span data-stu-id="923a4-193">For instance, consider `newtype Encoder = (Apply : (Qubit[] => Unit is Adj + Ctl))` in preference to `newtype Encoder = (Qubit[] => Unit is Adj + Ctl)`.</span></span>

  - <span data-ttu-id="923a4-194">他の関数および操作が "ラップされた" UDT インスタンスを直接受け入れることを保証する。</span><span class="sxs-lookup"><span data-stu-id="923a4-194">Ensuring that other functions and operations can accept   "wrapped" UDT instances directly.</span></span>

- <span data-ttu-id="923a4-195">⛔️には、追加の表現力を提供せずに組み込み型を複製する新しいユーザー定義型は導入し**ません**。</span><span class="sxs-lookup"><span data-stu-id="923a4-195">⛔️ **DON'T** introduce new user-defined types that duplicate   built-in types without providing additional expressiveness.</span></span>

  <span data-ttu-id="923a4-196">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-196">*Examples:*</span></span>
  - <span data-ttu-id="923a4-197">UDT `newtype QubitRegister = Qubit[]` は、`Qubit[]`に対して追加の表現力を提供しないため、はっきり特典なしで使用するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="923a4-197">A UDT `newtype QubitRegister = Qubit[]` provides no   additional expressiveness over `Qubit[]`, and is thus harder   to use with no discernable benefit.</span></span>
  - <span data-ttu-id="923a4-198">UDT `newtype LittleEndian = Qubit[]` は、基になるレジスタがどのように使用および解釈されるかを文書化し、その基本型に対して追加の表現力を提供します。</span><span class="sxs-lookup"><span data-stu-id="923a4-198">A UDT `newtype LittleEndian = Qubit[]` documents how the   underlying register is to be used and interpreted, and thus   provides additional expressiveness over its base type.</span></span>

- <span data-ttu-id="923a4-199">厳密に要求されていない限り、⛔️アクセサー関数は導入し**ません**。  この場合は、名前付きの項目を強くお勧めします。</span><span class="sxs-lookup"><span data-stu-id="923a4-199">⛔️ **DON'T** introduce accessor functions unless strictly required;   strongly prefer named items in this case.</span></span>

  <span data-ttu-id="923a4-200">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-200">*Examples:*</span></span>
  - <span data-ttu-id="923a4-201">UDT `newtype Complex = (Double, Double)`を導入する場合は、`newtype Complex = (Real : Double, Imag : Double)` するように定義を変更して、関数 `GetReal : Complex -> Double` および `GetImag : Complex -> Double`を導入することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="923a4-201">When introducing a UDT `newtype Complex = (Double, Double)`,   prefer modifying the definition to   `newtype Complex = (Real : Double, Imag : Double)` to introducing   functions `GetReal : Complex -> Double` and   `GetImag : Complex -> Double`.</span></span>

## <a name="namespaces-and-organization"></a><span data-ttu-id="923a4-202">名前空間と組織</span><span class="sxs-lookup"><span data-stu-id="923a4-202">Namespaces and Organization</span></span>

<span data-ttu-id="923a4-203">**重要な原則:** それぞれの名前空間で、関数、操作、およびユーザー定義型の目的を明確に伝えることができる、予測可能な名前空間の名前を選択します。</span><span class="sxs-lookup"><span data-stu-id="923a4-203">**Key principle:** choose namespace names that are predictable and that clearly communicate the purpose of functions, operations, and user-defined types in each namespace.</span></span>

- <span data-ttu-id="923a4-204">✅**名前**空間を `Publisher.Product.DomainArea`として指定します。</span><span class="sxs-lookup"><span data-stu-id="923a4-204">✅ **DO** name namespaces as `Publisher.Product.DomainArea`.</span></span>

  <span data-ttu-id="923a4-205">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-205">*Examples:*</span></span>
  - <span data-ttu-id="923a4-206">Quantum 開発キットの quantum シミュレーション機能の一部として Microsoft が発行した関数、操作、および Udt は、`Microsoft.Quantum.Simulation` 名前空間に配置されます。</span><span class="sxs-lookup"><span data-stu-id="923a4-206">Functions, operations, and UDTs published by Microsoft as a   part of the quantum simulation feature of the Quantum   Development Kit are placed in the   `Microsoft.Quantum.Simulation` namespace.</span></span>
  - <span data-ttu-id="923a4-207">`Microsoft.Quantum.Math` は、Microsoft によって発行された名前空間を表します。これは、数学のドメイン領域に関する Quantum 開発キットの一部として公開されています。</span><span class="sxs-lookup"><span data-stu-id="923a4-207">`Microsoft.Quantum.Math` represents a namespace   published by Microsoft as part of the Quantum Development   Kit pertaining to the mathematics domain area.</span></span>

- <span data-ttu-id="923a4-208">特定の機能で使用されている操作、関数、およびユーザー定義型を名前空間に配置して、その機能が異なる問題ドメインで使用されている**場合でも**、その機能を説明する名前空間に ✅ します。</span><span class="sxs-lookup"><span data-stu-id="923a4-208">✅ **DO** place operations, functions, and user-defined types used   for specific functionality into a namespace that describes that   functionality, even when that functionality is used across   different problem domains.</span></span>

  <span data-ttu-id="923a4-209">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-209">*Examples:*</span></span>
  - <span data-ttu-id="923a4-210">Quantum 開発キットの一部として Microsoft が発行した状態準備 Api は、`Microsoft.Quantum.Preparation`に配置されます。</span><span class="sxs-lookup"><span data-stu-id="923a4-210">State preparation APIs published by Microsoft as a part of   the Quantum Development Kit would be placed into   `Microsoft.Quantum.Preparation`.</span></span>
  - <span data-ttu-id="923a4-211">Quantum 開発キットの一部として Microsoft が発行したクォンタムシミュレーション Api は、`Microsoft.Quantum.Simulation`に配置されます。</span><span class="sxs-lookup"><span data-stu-id="923a4-211">Quantum simulation APIs published by Microsoft as a part of the Quantum   Development Kit would be placed into   `Microsoft.Quantum.Simulation`.</span></span>

- <span data-ttu-id="923a4-212">✅**は**、特定のドメイン内でのみ使用される操作、関数、およびユーザー定義型を、ユーティリティのドメインを示す名前空間に配置します。</span><span class="sxs-lookup"><span data-stu-id="923a4-212">✅ **DO** place operations, functions, and user-defined types used only within specific domains into namespaces indicating their domain of utility.</span></span> <span data-ttu-id="923a4-213">必要に応じて、副名前空間を使用して、各ドメイン固有の名前空間内のフォーカスされたタスクを指定します。</span><span class="sxs-lookup"><span data-stu-id="923a4-213">If needed, use subnamespaces to indicate focused tasks within each domain-specific namespace.</span></span>

  <span data-ttu-id="923a4-214">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-214">*Examples:*</span></span>
  - <span data-ttu-id="923a4-215">Microsoft が発行したクォンタム機械学習ライブラリは、主に @"microsoft.quantum.machinelearning" 名前空間に配置されますが、データセットの例は @"microsoft.quantum.machinelearning.datasets" 名前空間によって提供されます。</span><span class="sxs-lookup"><span data-stu-id="923a4-215">The quantum machine learning library published by Microsoft is largely   placed into the @"microsoft.quantum.machinelearning" namespace, but example   datasets are provided by the @"microsoft.quantum.machinelearning.datasets"   namespace.</span></span>
  - <span data-ttu-id="923a4-216">Quantum 開発キットの一部として Microsoft によって発行された量子化学 Api は、`Microsoft.Quantum.Chemistry`に配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-216">Quantum chemistry APIs published by Microsoft as a part of the Quantum Development Kit should be placed into `Microsoft.Quantum.Chemistry`.</span></span> <span data-ttu-id="923a4-217">ヨルダン化学分解の実装に固有の機能が `Microsoft.Quantum.Chemistry.JordanWigner`に配置されている場合があります。そのため、量子化学ドメイン領域の主要インターフェイスは、実装には関係ありません。</span><span class="sxs-lookup"><span data-stu-id="923a4-217">Functionality specific to implementing the Jordan--Wigner decomposition may be placed in `Microsoft.Quantum.Chemistry.JordanWigner`, so that the primary interface for the quantum chemistry domain area is not concerned with implementations.</span></span>

<span data-ttu-id="923a4-218">**主要原則:** 名前空間とアクセス修飾子を一緒に使用して、ユーザーに公開されている API サーフェイスに関する意図的なものにし、Api の実装とテストに関連する内部の詳細を非表示にします。</span><span class="sxs-lookup"><span data-stu-id="923a4-218">**Key principle:** Use namespaces and access modifiers together to be intentional about the API surface exposed to users, and to hide internal details related to implementation and testing of your APIs.</span></span>

- <span data-ttu-id="923a4-219">✅、API を実装するために必要なすべての関数と操作を、実装されている API と同じ名前空間**に配置しますが、"** private" または "internal" キーワードでマークして、ライブラリのパブリック API サーフェイスの一部ではないことを示すことができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-219">✅ Whenever reasonable, **DO** place all functions and operations needed to implement an API into the same namespace as the API being implemented, but marked with the "private" or "internal" keywords to indicate that they are not part of the public API surface for a library.</span></span> <span data-ttu-id="923a4-220">アンダースコア (`_`) で始まる名前を使用して、プライベートおよび内部の操作と関数をパブリック呼び出しができるかを視覚的に区別します。</span><span class="sxs-lookup"><span data-stu-id="923a4-220">Use a name beginning with an underscore (`_`) to visually distinguish private and internal operations and functions from public callables.</span></span>

  <span data-ttu-id="923a4-221">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-221">*Examples:*</span></span>
  - <span data-ttu-id="923a4-222">操作名 `_Features` は、指定された名前空間とアセンブリに対してプライベートであり、`internal` キーワードを伴う関数を示します。</span><span class="sxs-lookup"><span data-stu-id="923a4-222">The operation name `_Features` indicates a function that is   private to a given namespace and assembly, and should be   accompanied by either the `internal` keyword.</span></span>

- <span data-ttu-id="923a4-223">特定の名前空間の API を実装するために多数のプライベート関数または操作のセットが必要になることはまれの ✅、実装され、`.Private`で終了する名前空間に一致する新しい名前空間にそれら**を配置します。**</span><span class="sxs-lookup"><span data-stu-id="923a4-223">✅ In the rare case that an extensive set of private functions or operations are needed to implement the API for a given namespace, **DO** place them in a new namespace matching the namespace being implemented and ending in `.Private`.</span></span>

- <span data-ttu-id="923a4-224">✅ **、** すべての単体テストを、テスト対象の名前空間に一致する名前空間に配置し、`.Tests`で終了します。</span><span class="sxs-lookup"><span data-stu-id="923a4-224">✅ **DO** place all unit tests into namespaces matching the     namespace under test and ending in `.Tests`.</span></span>

## <a name="naming-conventions-and-vocabulary"></a><span data-ttu-id="923a4-225">名前付け規則とボキャブラリ</span><span class="sxs-lookup"><span data-stu-id="923a4-225">Naming Conventions and Vocabulary</span></span>

<span data-ttu-id="923a4-226">**主要原則:** さまざまな対象ユーザー (クォンタム初心者と専門家の両方を含む) で、明確で、アクセス可能で、読みやすい名前と用語を選択します。</span><span class="sxs-lookup"><span data-stu-id="923a4-226">**Key principle:** Choose names and terminology that are clear, accessible, and readable across a diverse range of audiences, including both quantum novices and experts.</span></span>

- <span data-ttu-id="923a4-227">差別的なまたは exclusionary 識別子の名前を使用したり、API ドキュメントのコメントに用語を使用したりすることは⛔️**ません**。</span><span class="sxs-lookup"><span data-stu-id="923a4-227">⛔️ **DON'T** use discriminatory or exclusionary identifier names,   nor terminology in API documentation comments.</span></span>

- <span data-ttu-id="923a4-228">API ドキュメントコメントを使用して、関連するコンテキスト、例、および参照を提供します。特に、より困難な概念につい**ては、** 「」を参照してください。 ✅</span><span class="sxs-lookup"><span data-stu-id="923a4-228">✅ **DO** use API documentation comments to provide relevant   context, examples, and references, especially for more difficult   concepts.</span></span>

- <span data-ttu-id="923a4-229">⛔️不要な識別子名を使用し**ない**でください。または、大量のクォンタムアルゴリズムの知識が必要です。</span><span class="sxs-lookup"><span data-stu-id="923a4-229">⛔️ **DON'T** use identifier names that are unnecessarily esoteric,   or that require significant quantum algorithms knowledge to   read.</span></span>

  <span data-ttu-id="923a4-230">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-230">*Examples:*</span></span>
  - <span data-ttu-id="923a4-231">"振幅増幅の反復" を "Grover iteration" に優先します。</span><span class="sxs-lookup"><span data-stu-id="923a4-231">Prefer "amplitude amplification iteration" to "Grover   iteration."</span></span>

- <span data-ttu-id="923a4-232">✅**は**、実装ではなく、呼び出し可能なの意図された効果を明確に伝える操作と関数の名前を選択します。</span><span class="sxs-lookup"><span data-stu-id="923a4-232">✅ **DO** choose operations and function names that clearly communicate the intended effect of a callable, and not its implementation.</span></span> <span data-ttu-id="923a4-233">実装は、にすることができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-233">Note that the implementation can and should be</span></span>

  <span data-ttu-id="923a4-234">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-234">*Examples:*</span></span>
  - <span data-ttu-id="923a4-235">後者がどのように実装されているかを通知するため、"Hadamard test" に "推定重複" を優先します。</span><span class="sxs-lookup"><span data-stu-id="923a4-235">Prefer "estimate overlap" to "Hadamard test," as the latter   communicates how the former is implemented.</span></span>

- <span data-ttu-id="923a4-236">すべての Q\# Api で、一貫した方法で単語**を使用 ✅** ます。</span><span class="sxs-lookup"><span data-stu-id="923a4-236">✅ **DO** use words in a consistent fashion across all Q\# APIs:</span></span>

  - <span data-ttu-id="923a4-237">**助動詞**</span><span class="sxs-lookup"><span data-stu-id="923a4-237">**Verbs:**</span></span>

    - <span data-ttu-id="923a4-238">**アサート**: ターゲットコンピューターとその qubits の状態に関する想定が、物理リソースを使用していない可能性があるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="923a4-238">**Assert**: Check that an assumption about the state of a target machine and its qubits holds, possibly by using unphysical resources.</span></span> <span data-ttu-id="923a4-239">この動詞を使用する操作は、ライブラリや実行可能プログラムの機能に影響を与えずに、常に安全な状態にしておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-239">Operations using this verb should always be safely removable without affecting the functionality of libraries and executable programs.</span></span> <span data-ttu-id="923a4-240">ファクトとは異なり、アサーションは一般に、qubit レジスタの状態や実行環境などの外部の状態に依存します。</span><span class="sxs-lookup"><span data-stu-id="923a4-240">Note that unlike facts, assertions may in general depend on external state, such as the state of a qubit register, the execution environment or so forth.</span></span> <span data-ttu-id="923a4-241">外部の状態に対する依存関係は副作用の一種であるため、アサーションは関数ではなく操作として公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-241">As dependency on external state is a kind of side effect, assertions must be exposed as operations rather than functions.</span></span>

    - <span data-ttu-id="923a4-242">**推定**: 1 つまたは複数の連続した測定値を使用して、測定結果から古典の数量を見積もります。</span><span class="sxs-lookup"><span data-stu-id="923a4-242">**Estimate**: Using one or more possibly repeated   measurements, estimate a classical quantity from   measurement results.</span></span>

      <span data-ttu-id="923a4-243">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-243">*Examples:*</span></span>
      - @"microsoft.quantum.characterization.estimatefrequency"
      - @"microsoft.quantum.characterization.estimateoverlapbetweenstates"

    - <span data-ttu-id="923a4-244">**準備**: 特定の初期状態 (通常は $ \ket{00\cdots 0} $) で開始することが想定される1つ以上の qubits に対して、クォンタム操作または一連の操作を適用します。これにより、これらの qubits の状態が目的の終了状態に進化します。</span><span class="sxs-lookup"><span data-stu-id="923a4-244">**Prepare**: Apply a quantum operation or sequence of operations to one or more qubits assumed to start in a particular initial state (typically $\ket{00\cdots 0}$), causing the state of those qubits to evolve to a desired end state.</span></span> <span data-ttu-id="923a4-245">一般に、指定された開始状態以外の状態で動作すると、未定義のユニタリ変換が発生する**可能性があり**ますが、操作とその adjoint "キャンセル" を保持し、操作なしを適用する**必要**があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-245">In general, acting on states other than the given starting state **MAY** result in an undefined unitary transformation, but **SHOULD** still preserve that an operation and its adjoint "cancel out" and apply a no-op.</span></span>

      <span data-ttu-id="923a4-246">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-246">*Examples:*</span></span>
      - @"microsoft.quantum.preparation.preparearbitrarystate"
      - @"microsoft.quantum.preparation.prepareuniformsuperposition"

    - <span data-ttu-id="923a4-247">**メジャー**: 1 つ以上の qubits にクォンタム操作または一連の操作を適用し、古典的なデータをバックアウトします。</span><span class="sxs-lookup"><span data-stu-id="923a4-247">**Measure**: Apply a quantum operation or sequence of   operations to one or more qubits, reading classical data   back out.</span></span>

      <span data-ttu-id="923a4-248">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-248">*Examples:*</span></span>
      - @"microsoft.quantum.intrinsic.measure"
      - @"microsoft.quantum.arithmetic.measurefxp"
      - @"microsoft.quantum.arithmetic.measureinteger"

    - <span data-ttu-id="923a4-249">**適用**: クォンタム操作または操作のシーケンスを1つ以上の qubits に適用し、それらの qubits の状態が一貫した形で変化するようにします。</span><span class="sxs-lookup"><span data-stu-id="923a4-249">**Apply**: Apply a quantum operation or sequence of operations to one or more qubits, causing the state of those qubits to change in a coherent fashion.</span></span> <span data-ttu-id="923a4-250">この動詞は、Q\# の用語で最も一般的な動詞であり、より具体的な動詞がより直接的に関連する場合は使用**しないでください**。</span><span class="sxs-lookup"><span data-stu-id="923a4-250">This verb is the most general verb in Q\# nomenclature, and **SHOULD NOT BE** used when a more specific verb is more directly relevant.</span></span>

  - <span data-ttu-id="923a4-251">**名詞**:</span><span class="sxs-lookup"><span data-stu-id="923a4-251">**Nouns**:</span></span>

    - <span data-ttu-id="923a4-252">**ファクト**: ターゲットコンピューターの状態、環境、またはコンピューターの qubits の状態ではなく、入力のみに依存するブール条件。</span><span class="sxs-lookup"><span data-stu-id="923a4-252">**Fact**: A Boolean condition which depends only on its inputs and not on the state of a target machine, its environment, or the state of the machine's qubits.</span></span> <span data-ttu-id="923a4-253">アサーションとは対照的に、ファクトは、そのファクトに対して指定された*値*にのみ影響します。</span><span class="sxs-lookup"><span data-stu-id="923a4-253">By contrast with an assertion, a fact is only sensitive to the *values* provided to that fact.</span></span> <span data-ttu-id="923a4-254">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="923a4-254">For example:</span></span>

      <span data-ttu-id="923a4-255">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-255">*Examples:*</span></span>
      - <span data-ttu-id="923a4-256">@"microsoft.quantum.diagnostics.equalityfacti": 2 つの整数入力に関する等価のファクトを表します。入力として指定された整数が互いに等しいか、または他のプログラムの状態に依存していないかのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="923a4-256">@"microsoft.quantum.diagnostics.equalityfacti": represents an equality fact about two integer inputs; either the integers provided as input are equal to each other, or they are not, independent of any other program state.</span></span>

    - <span data-ttu-id="923a4-257">**オプション:** 関数または演算に対して "省略可能な引数" として機能する複数の名前付き項目を含む UDT。</span><span class="sxs-lookup"><span data-stu-id="923a4-257">**Options:** A UDT containing several named items that can act as "optional arguments" to a function or operation.</span></span> <span data-ttu-id="923a4-258">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="923a4-258">For example:</span></span>

      <span data-ttu-id="923a4-259">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-259">*Examples:*</span></span>
      - <span data-ttu-id="923a4-260">@"microsoft.quantum.machinelearning.trainingoptions" UDT には、学習率、ミニバッチサイズ、および ML トレーニング用のその他の構成可能なパラメーターの名前付き項目が含まれています。</span><span class="sxs-lookup"><span data-stu-id="923a4-260">The @"microsoft.quantum.machinelearning.trainingoptions" UDT includes named items for learning rate, minibatch size, and other configurable parameters for ML training.</span></span>

  - <span data-ttu-id="923a4-261">**形容詞**:</span><span class="sxs-lookup"><span data-stu-id="923a4-261">**Adjectives**:</span></span>

    - <span data-ttu-id="923a4-262">⛔️ **New**: この形容詞は使用し**ないでください**。多くのプログラミング言語 (: C++、 C#Java、TypeScript、PowerShell など) で動詞として使用する場合と混同しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="923a4-262">⛔️ **New**: This adjective **SHOULD NOT** be used, as to avoid confusion   with its usage as a verb in many   programming languages (e.g.: C++, C#, Java, TypeScript, PowerShell).</span></span>

  - <span data-ttu-id="923a4-263">**前置詞:** 場合によっては、前置詞を使用して、関数名と操作名の名詞と動詞の役割をさらに明確に区別したり、明確にしたりすることができます。</span><span class="sxs-lookup"><span data-stu-id="923a4-263">**Prepositions:** In some cases, prepositions can be used to further disambiguate or clarify the roles of nouns and verbs in function and operation names.</span></span> <span data-ttu-id="923a4-264">ただし、そのためには控えめにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="923a4-264">Care should be taken to do so sparingly and consistently, however.</span></span>

    - <span data-ttu-id="923a4-265">**次のようになります。** 関数の入力と出力が同じ情報を表しているが、出力ではその情報を元の表現ではなく*X* **として**表すことを表します。</span><span class="sxs-lookup"><span data-stu-id="923a4-265">**As:** Represents that a function's input and output represent the same information, but that the output represents that information **as** an *X* instead of its original representation.</span></span> <span data-ttu-id="923a4-266">これは、型変換関数では特に一般的です。</span><span class="sxs-lookup"><span data-stu-id="923a4-266">This is especially common for type conversion functions.</span></span>

      <span data-ttu-id="923a4-267">*例:*</span><span class="sxs-lookup"><span data-stu-id="923a4-267">*Examples:*</span></span>
      - <span data-ttu-id="923a4-268">`IntAsDouble(2)` は、入力 (`2`) と出力 (`2.0`) の両方が同じ情報を表していますが、異なる Q\# データ型を使用していることを示しています。</span><span class="sxs-lookup"><span data-stu-id="923a4-268">`IntAsDouble(2)` indicates that both the input (`2`) and the output (`2.0`)   represent qualitatively the same information, but using   different Q\# data types to do so.</span></span>

    - <span data-ttu-id="923a4-269">**開始:** 一貫性を確保するために、この前置詞を使用**して、** 型変換関数や、が適切であるその他のケースを示すことはでき**ません**。</span><span class="sxs-lookup"><span data-stu-id="923a4-269">**From:** To ensure consistency, this preposition   **SHOULD NOT** be used to indicate type conversion   functions or any other case where **As** is appropriate.</span></span>

    - <span data-ttu-id="923a4-270">⛔️ **:** この前置詞は、多くのプログラミング言語で動詞として使用する場合と混同しないように、使用しないことを**お勧め**します。</span><span class="sxs-lookup"><span data-stu-id="923a4-270">⛔️ **To:** This preposition **SHOULD NOT** be used, as to   avoid confusion with its usage as a verb in many   programming languages.</span></span>