---
title: Q# でのエンタングルメントの確認
description: Q# で量子プログラムを作成する方法について説明します。 Quantum Development Kit (QDK) を使用してベル状態アプリケーションを開発する
author: geduardo
ms.author: v-edsanc@microsoft.com
ms.date: 05/29/2020
ms.topic: tutorial
uid: microsoft.quantum.write-program
ms.openlocfilehash: 16c93b3dd17363c06602529cb34e8fc84aadc7a8
ms.sourcegitcommit: af10179284967bd7a72a52ae7e1c4da65c7d128d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85415424"
---
# <a name="tutorial-explore-entanglement-with-q"></a><span data-ttu-id="f5f48-104">チュートリアル:Q\# でのもつれの確認</span><span class="sxs-lookup"><span data-stu-id="f5f48-104">Tutorial: Explore entanglement with Q\#</span></span>

<span data-ttu-id="f5f48-105">このチュートリアルでは、量子ビットの操作および測定を行い、重ね合わせともつれの効果を示す、Q# プログラムの作成方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-105">In this tutorial, we show you how to write a Q# program that manipulates and measures qubits and demonstrates the effects of superposition and entanglement.</span></span>

<span data-ttu-id="f5f48-106">量子のもつれを示すため、Bell というアプリケーションを記述します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-106">You will write an application called Bell to demonstrate quantum entanglement.</span></span>
<span data-ttu-id="f5f48-107">Bell という名前は、ベル状態を表しています。これは、量子の重ね合わせともつれの最も簡単な例を表すために使用される、2 つの量子ビットの特定の量子の状態です。</span><span class="sxs-lookup"><span data-stu-id="f5f48-107">The name Bell is in reference to Bell states, which are specific quantum states of two qubits that are used to represent the simplest examples of superposition and quantum entanglement.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="f5f48-108">前提条件</span><span class="sxs-lookup"><span data-stu-id="f5f48-108">Pre-requisites</span></span>

<span data-ttu-id="f5f48-109">コーディングを開始する準備ができたら、続行する前に次の手順を実行してください。</span><span class="sxs-lookup"><span data-stu-id="f5f48-109">If you are ready to start coding, follow these steps before proceeding:</span></span> 

* <span data-ttu-id="f5f48-110">任意の言語および開発環境を使用して、Quantum 開発キットを[インストール](xref:microsoft.quantum.install)します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-110">[Install](xref:microsoft.quantum.install) the Quantum Development Kit using your  preferred language and development environment.</span></span>
* <span data-ttu-id="f5f48-111">既に QDK をインストールしている場合は、バージョンが[最新](xref:microsoft.quantum.update)であることを確認する</span><span class="sxs-lookup"><span data-stu-id="f5f48-111">If you already have the QDK installed, make sure you have [updated](xref:microsoft.quantum.update) to the latest version</span></span>

<span data-ttu-id="f5f48-112">また、QDK をインストールしなくても、Q # プログラミング言語の概要と、クォンタムコンピューティングの最初の概念を確認することで、このナレーションに従うことができます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-112">You can also follow along with the narrative without installing the QDK, reviewing  the overviews of the Q# programming language and the first concepts of quantum computing.</span></span>

## <a name="in-this-tutorial-youll-learn-how-to"></a><span data-ttu-id="f5f48-113">このチュートリアルでは、次の作業を行う方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-113">In this tutorial, you'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f5f48-114">Q での操作の作成と結合\#</span><span class="sxs-lookup"><span data-stu-id="f5f48-114">Create and combine operations in Q\#</span></span>
> * <span data-ttu-id="f5f48-115">法則、entangle に qubits を配置する操作を作成し、それらを測定します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-115">Create operations to put qubits in superposition, entangle and measure them.</span></span>
> * <span data-ttu-id="f5f48-116">シミュレーターで実行される Q # プログラムを使用したクォンタムの例を示します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-116">Demonstrate quantum entanglement with a Q# program run in a simulator.</span></span> 

## <a name="demonstrating-qubit-behavior-with-the-qdk"></a><span data-ttu-id="f5f48-117">QDK を使用した qubit 動作のデモンストレーション</span><span class="sxs-lookup"><span data-stu-id="f5f48-117">Demonstrating qubit behavior with the QDK</span></span>

<span data-ttu-id="f5f48-118">従来のビットでは単一のバイナリ値 (0、1 など) が保持されるのに対し、[量子ビット](xref:microsoft.quantum.glossary#qubit)の状態は 0 と 1 の**重ね合わせ**になることができます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-118">Where classical bits hold a single binary value such as a 0 or 1, the state of a [qubit](xref:microsoft.quantum.glossary#qubit) can be in a **superposition** of 0 and 1.</span></span>  <span data-ttu-id="f5f48-119">概念上、qubit の状態は、抽象空間 (ベクターとも呼ばれます) の方向と考えることができます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-119">Conceptually, the state of a qubit can be thought of as a direction in an abstract space (also known as a vector).</span></span>  <span data-ttu-id="f5f48-120">Qubit 状態は、可能な任意の方向にすることができます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-120">A qubit state can be in any of the possible directions.</span></span> <span data-ttu-id="f5f48-121">2 つの**従来の状態**とは、0 を測定する確率が 100% になる方向と、1 を測定する確率が 100% になる方向のことです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-121">The two **classical states** are the two directions; representing 100% chance of measuring 0 and 100% chance of measuring 1.</span></span>

<span data-ttu-id="f5f48-122">測定の動作により、2 進法の結果が生成され、量子ビットの状態が変わります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-122">The act of measurement produces a binary result and changes a qubit state.</span></span>
<span data-ttu-id="f5f48-123">測定値によって、0または1の2進値が生成されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-123">Measurement  produces a binary value, either 0 or 1.</span></span>  <span data-ttu-id="f5f48-124">量子ビットは重ね合わせ (あらゆる方向にある) の状態から古典的状態のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-124">The qubit goes from being in superposition (any direction) to one of the classical states.</span></span>  <span data-ttu-id="f5f48-125">その後、介在する操作なしで同じ測定を繰り返すと、同じ 2 進数の結果が生成されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-125">Thereafter, repeating the same measurement without any intervening operations produces the same binary result.</span></span>  

<span data-ttu-id="f5f48-126">複数の量子ビットは[**もつれさせる**](xref:microsoft.quantum.glossary#entanglement)ことができます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-126">Multiple qubits can be [**entangled**](xref:microsoft.quantum.glossary#entanglement).</span></span>  <span data-ttu-id="f5f48-127">もつれのある 1 つの量子ビットを測定すると、もう一方の量子ビットの状態に関する知識も更新されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-127">When we make a measurement of one entangled qubit, our knowledge of the state of the other(s) is updated as well.</span></span>

<span data-ttu-id="f5f48-128">これで、Q# がこの動作を表現する方法を説明できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f5f48-128">Now, we're ready to demonstrate how Q# expresses this behavior.</span></span>  <span data-ttu-id="f5f48-129">考えられる最も単純なプログラムから始め、量子の重ね合わせと量子のもつれを表すように構築します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-129">You start with the simplest program possible and build it up to demonstrate quantum superposition and quantum entanglement.</span></span>

## <a name="creating-a-q-project"></a><span data-ttu-id="f5f48-130">Q # プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="f5f48-130">Creating a Q# project</span></span>

<span data-ttu-id="f5f48-131">まず、新しい Q # プロジェクトを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-131">The first thing we have to do is to create a new Q# project.</span></span> <span data-ttu-id="f5f48-132">このチュートリアルでは、 [VS Code のコマンドラインアプリケーション](xref:microsoft.quantum.install.standalone)に基づいて環境を使用します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-132">In this tutorial we are going to use the environment based on [command line applications with VS Code](xref:microsoft.quantum.install.standalone).</span></span>

<span data-ttu-id="f5f48-133">新しいプロジェクトを作成するには VS Code 次のようにします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-133">To create a new project, in VS Code:</span></span> 

1. <span data-ttu-id="f5f48-134">[ **View**  ->  **コマンドパレット**の表示] をクリックし、[ **Q #: 新しいプロジェクトの作成**] を選択します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-134">Click **View** -> **Command Palette** and select **Q#: Create New Project**.</span></span>
2. <span data-ttu-id="f5f48-135">[**スタンドアロンコンソールアプリケーション**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-135">Click **Standalone console application**.</span></span>
3. <span data-ttu-id="f5f48-136">プロジェクトを保存する場所に移動し、[**プロジェクトの作成**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-136">Navigate to the location to save the project and click **Create Project**.</span></span>
4. <span data-ttu-id="f5f48-137">プロジェクトが正常に作成されたら、右下にある [**新しいプロジェクトを開く**] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-137">When the project is successfully created, click **Open new project...** in the lower right.</span></span>

<span data-ttu-id="f5f48-138">この例では、プロジェクトを呼び出しました `Bell` 。</span><span class="sxs-lookup"><span data-stu-id="f5f48-138">In this case we called the project `Bell`.</span></span> <span data-ttu-id="f5f48-139">これに `Bell.csproj` より、プロジェクトファイルと、アプリケーションを `Program.qs` 記述するために使用する Q # アプリケーションのテンプレートの2つのファイルが生成されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-139">This generates two files: `Bell.csproj`, the project file and `Program.qs`, a template of a Q# application that we will use to write our application.</span></span> <span data-ttu-id="f5f48-140">の内容は次のようになり `Program.qs` ます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-140">The content of `Program.qs` should be:</span></span>

```qsharp
   namespace Bell {

      open Microsoft.Quantum.Canon;
      open Microsoft.Quantum.Intrinsic;
    

      @EntryPoint()
      operation HelloQ() : Unit {
          Message("Hello quantum world!");
      }
   }
```

## <a name="write-the-q-application"></a><span data-ttu-id="f5f48-141">Q アプリケーションを作成する \#</span><span class="sxs-lookup"><span data-stu-id="f5f48-141">Write the Q\# application</span></span>
 
<span data-ttu-id="f5f48-142">私たちの目標は、Q# を使って量子ビットを操作してその状態を変更するための、特定の量子の状態にある 2 つの量子ビットを準備し、重ね合わせともつれの効果を示すことです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-142">Our goal is to prepare two qubits in a specific quantum state, demonstrating how to operate on qubits with Q# to change their state and demonstrate the effects of superposition and entanglement.</span></span> <span data-ttu-id="f5f48-143">ここでは、qubit の状態、操作、および測定について説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-143">We will build this up piece by piece to introduce qubit states, operations, and measurement.</span></span>

### <a name="initialize-qubit-using-measurement"></a><span data-ttu-id="f5f48-144">測定を使用して qubit を初期化する</span><span class="sxs-lookup"><span data-stu-id="f5f48-144">Initialize qubit using measurement</span></span>

<span data-ttu-id="f5f48-145">以下に示す最初のコードは、Q# で量子ビットを操作する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-145">In the first code below, we show you how to work with qubits in Q#.</span></span>  <span data-ttu-id="f5f48-146">2つの操作を紹介 [`M`](xref:microsoft.quantum.intrinsic.m) し、 [`X`](xref:microsoft.quantum.intrinsic.x) qubit の状態を変換します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-146">We’ll introduce two operations, [`M`](xref:microsoft.quantum.intrinsic.m) and [`X`](xref:microsoft.quantum.intrinsic.x) that transform the state of a qubit.</span></span> <span data-ttu-id="f5f48-147">このコード スニペットでは、量子ビットをパラメーターと見なす操作 `SetQubitState` が定義されています。もう 1 つのパラメーター `desired` は量子ビットが目的とする状態を表しています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-147">In this code snippet, an operation `SetQubitState` is defined that takes as a parameter a qubit and another parameter, `desired`, representing the state that we would like the qubit to be in.</span></span>  <span data-ttu-id="f5f48-148">操作 `SetQubitState` は、操作 `M` を使用して、量子ビットに対する測定を実行します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-148">The operation `SetQubitState` performs a measurement on the qubit using the operation `M`.</span></span>  <span data-ttu-id="f5f48-149">Q # では、qubit 測定値は常に `Zero` またはを返し `One` ます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-149">In Q#, a qubit measurement always returns either `Zero` or `One`.</span></span>  <span data-ttu-id="f5f48-150">測定値が目的の値と等しくない値を返す場合、 `SetQubitState` は qubit を "反転" します。つまり、演算子は演算を実行します。これにより、 `X` qubit 状態が戻り値の確率が返され、元に戻される新しい状態に変更 `Zero` され `One` ます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-150">If the measurement returns a value not equal to the desired value, `SetQubitState` “flips” the qubit; that is, it executes an `X` operation, which changes the qubit state to a new state in which the probabilities of a measurement returning `Zero` and `One` are reversed.</span></span> <span data-ttu-id="f5f48-151">これにより、は `SetQubitState` 常にターゲットの qubit を目的の状態にします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-151">This way, `SetQubitState` always puts the target qubit in the desired state.</span></span>

<span data-ttu-id="f5f48-152">の内容を `Program.qs` 次のコードに置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-152">Replace the contents of `Program.qs` with the following code:</span></span>


```qsharp
   namespace Bell {
       open Microsoft.Quantum.Intrinsic;
       open Microsoft.Quantum.Canon;

       operation SetQubitState(desired : Result, q1 : Qubit) : Unit {
           if (desired != M(q1)) {
               X(q1);
           }
       }
   }
```

<span data-ttu-id="f5f48-153">この操作により、量子ビットが従来の状態に設定されます。つまり、`Zero` が 100% 返されるか、`One` が 100% 返されるかのどちらかです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-153">This operation may now be called to set a qubit to a classical state, either returning `Zero` 100% of the time or returning `One` 100% of the time.</span></span>
<span data-ttu-id="f5f48-154">`Zero` および `One` は、量子ビットの測定結果として考えられる 2 とおりの結果を表す定数です。</span><span class="sxs-lookup"><span data-stu-id="f5f48-154">`Zero` and `One` are constants that represent the only two possible results of a measurement of a qubit.</span></span>

<span data-ttu-id="f5f48-155">`SetQubitState` 操作で量子ビットが測定されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-155">The operation `SetQubitState` measures the qubit.</span></span> <span data-ttu-id="f5f48-156">量子ビットが目的の状態にある場合は、`SetQubitState` をそのままにしておきます。それ以外の場合は、`X` 操作を実行することで量子ビットの状態が目的の状態に変更されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-156">If the qubit is in the state we want, `SetQubitState` leaves it alone; otherwise, by executing the `X` operation, we change the qubit state to the desired state.</span></span>

#### <a name="about-q-operations"></a><span data-ttu-id="f5f48-157">Q# 操作について</span><span class="sxs-lookup"><span data-stu-id="f5f48-157">About Q# operations</span></span>

<span data-ttu-id="f5f48-158">Q# 操作は、量子のサブルーチンです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-158">A Q# operation is a quantum subroutine.</span></span> <span data-ttu-id="f5f48-159">つまり、これは、他のクォンタム操作の呼び出しを含む呼び出し可能なルーチンです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-159">That is, it is a callable routine that contains calls to other quantum operations.</span></span>

<span data-ttu-id="f5f48-160">操作の引数は、かっこ内にタプルとして指定します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-160">The arguments to an operation are specified as a tuple, within parentheses.</span></span>

<span data-ttu-id="f5f48-161">操作の戻り値の型は、コロンの後に指定します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-161">The return type of the operation is specified after a colon.</span></span> <span data-ttu-id="f5f48-162">この場合、`SetQubitState` 操作には戻り値がないため、`Unit` を返すように設定されています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-162">In this case, the `SetQubitState` operation has no return, so it is marked as returning `Unit`.</span></span> <span data-ttu-id="f5f48-163">これは、F# における `unit` の Q# 版にあたります。C# では `void`、Python では空のタプル (`Tuple[()]`) とほぼ同じです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-163">This is the Q# equivalent of `unit` in F#, which is roughly analogous to `void` in C#, and an empty tuple (`Tuple[()]`) in Python.</span></span>

<span data-ttu-id="f5f48-164">最初の Q# 操作では、次の 2 つの量子操作を使用しました。</span><span class="sxs-lookup"><span data-stu-id="f5f48-164">You have used two quantum operations in your first Q# operation:</span></span>

* <span data-ttu-id="f5f48-165">[`M`](xref:microsoft.quantum.intrinsic.m)Qubit の状態を測定する操作。</span><span class="sxs-lookup"><span data-stu-id="f5f48-165">The [`M`](xref:microsoft.quantum.intrinsic.m) operation, which measures the state of the qubit</span></span>
* <span data-ttu-id="f5f48-166">[`X`](xref:microsoft.quantum.intrinsic.x)Qubit の状態を反転する操作。</span><span class="sxs-lookup"><span data-stu-id="f5f48-166">The [`X`](xref:microsoft.quantum.intrinsic.x) operation, which flips the state of a qubit</span></span>

<span data-ttu-id="f5f48-167">量子操作により、量子ビットの状態が変換されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-167">A quantum operation transforms the state of a qubit.</span></span> <span data-ttu-id="f5f48-168">従来の論理ゲートの類義語として、量子操作の代わりに、量子ゲートが話題になることがあります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-168">Sometime people talk about quantum gates instead of operations, in analogy to classical logic gates.</span></span> <span data-ttu-id="f5f48-169">これは初期の量子コンピューティングでは、アルゴリズムが単なる理論上の構成要素であり、古典コンピューティングの回路図に似た図で視覚化されていたことに端を発します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-169">This is rooted in the early days of quantum computing when algorithms were merely a theoretical construct and visualized as diagrams similarly to circuit diagrams in classical computing.</span></span>

### <a name="counting-measurement-outcomes"></a><span data-ttu-id="f5f48-170">測定結果のカウント</span><span class="sxs-lookup"><span data-stu-id="f5f48-170">Counting measurement outcomes</span></span>

<span data-ttu-id="f5f48-171">`SetQubitState` 操作の効果を示すため、`TestBellState` 操作を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-171">To demonstrate the effect of the `SetQubitState` operation, a `TestBellState` operation is then added.</span></span> <span data-ttu-id="f5f48-172">この操作では、`Zero` または `One` を入力として受け取り、その入力で `SetQubitState` 操作を何回か呼び出して、`Zero` が量子ビットの測定から返された回数と `One` が返された回数をカウントします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-172">This operation takes as input a `Zero` or `One`, and calls the `SetQubitState` operation some number of times with that input, and counts the number of times that `Zero` was returned from the measurement of the qubit and the number of times that `One` was returned.</span></span> <span data-ttu-id="f5f48-173">当然ながら、`TestBellState` 操作のこの最初のシミュレーションでは、`Zero` がパラメーターとして設定された量子ビットのすべての測定で `Zero` を返し、`One` がパラメーターとして設定された量子ビットのすべての測定で `One` を返すことが想定されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-173">Of course, in this first simulation of the `TestBellState` operation, we expect that the output will show that all measurements of the qubit set with `Zero` as the parameter input will return `Zero`, and all measurements of a qubit set with `One` as the parameter input will return `One`.</span></span> <span data-ttu-id="f5f48-174">さらに、 `TestBellState` 法則と entangを示すためのコードをに追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-174">Further on, we’ll add code to `TestBellState` to demonstrate superposition and entanglement.</span></span>

<span data-ttu-id="f5f48-175">`Bell.qs` ファイルの名前空間内、`SetQubitState` 操作の終了後に次の操作を追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-175">Add the following operation to the `Bell.qs` file, inside the namespace, after the end of the `SetQubitState` operation:</span></span>

```qsharp
   operation TestBellState(count : Int, initial : Result) : (Int, Int) {

       mutable numOnes = 0;
       using (qubit = Qubit()) {

           for (test in 1..count) {
               SetQubitState(initial, qubit);
               let res = M(qubit);

               // Count the number of ones we saw:
               if (res == One) {
                   set numOnes += 1;
               }
           }
            
           SetQubitState(Zero, qubit);
       }

       // Return number of times we saw a |0> and number of times we saw a |1>
       Message("Test results (# of 0s, # of 1s): ");
       return (count - numOnes, numOnes);
   }
```
<span data-ttu-id="f5f48-176">`return`コンソールで関数 () を使用して説明メッセージを出力するために、の前に行を追加しました `Message` 。</span><span class="sxs-lookup"><span data-stu-id="f5f48-176">Note that we added a line before the `return` to print an explanatory message in the console with the function (`Message`)[microsoft.quantum.intrinsic.message]</span></span>

<span data-ttu-id="f5f48-177">この操作 (`TestBellState`) では、`count` 回ループし、指定された `initial` 値を量子ビットに設定して、結果を測定 (`M`) します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-177">This operation (`TestBellState`) will loop for `count` iterations, set a specified `initial` value on a qubit and then measure (`M`) the result.</span></span> <span data-ttu-id="f5f48-178">これにより、測定した 0 と 1 の数がいくつあるかの統計情報が収集され、呼び出し元に返されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-178">It will gather statistics on how many zeros and ones we've measured and return them to the caller.</span></span> <span data-ttu-id="f5f48-179">ここでは、もう 1 つの必要な操作を実行しています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-179">It performs one other necessary operation.</span></span> <span data-ttu-id="f5f48-180">他のユーザーがこの量子ビットに既知の状態を割り当てることができるよう、終了する前にこの量子ビットを既知の状態 (`Zero`) にリセットします。</span><span class="sxs-lookup"><span data-stu-id="f5f48-180">It resets the qubit to a known state (`Zero`) before returning it allowing others to allocate this qubit in a known state.</span></span> <span data-ttu-id="f5f48-181">この操作は、`using` ステートメントに必須です。</span><span class="sxs-lookup"><span data-stu-id="f5f48-181">This is required by the `using` statement.</span></span>

#### <a name="about-variables-in-q"></a><span data-ttu-id="f5f48-182">Q の変数について\#</span><span class="sxs-lookup"><span data-stu-id="f5f48-182">About variables in Q\#</span></span>

<span data-ttu-id="f5f48-183">既定では、Q# の変数は不変です。バインド後に変数の値を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="f5f48-183">By default, variables in Q# are immutable; their value may not be changed after they are bound.</span></span> <span data-ttu-id="f5f48-184">`let` キーワードは、不変変数のバインドを示すために使用します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-184">The `let` keyword is used to indicate the binding of an immutable variable.</span></span> <span data-ttu-id="f5f48-185">操作の引数は常に不変です。</span><span class="sxs-lookup"><span data-stu-id="f5f48-185">Operation arguments are always immutable.</span></span>

<span data-ttu-id="f5f48-186">先ほどの例の `numOnes` のように、値を変更できる変数が必要な場合は、`mutable` キーワードを使用して変数を宣言できます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-186">If you need a variable whose value can change, such as `numOnes` in the example, you can declare the variable with the `mutable` keyword.</span></span> <span data-ttu-id="f5f48-187">可変変数の値は、`setQubitState` ステートメントを使用して変更できます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-187">A mutable variable's value may be changed using a `setQubitState` statement.</span></span>

<span data-ttu-id="f5f48-188">どちらの場合も、変数の型はコンパイラによって推論されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-188">In both cases, the type of a variable is inferred by the compiler.</span></span> <span data-ttu-id="f5f48-189">Q# では、変数に型の注釈は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="f5f48-189">Q# doesn't require any type annotations for variables.</span></span>

#### <a name="about-using-statements-in-q"></a><span data-ttu-id="f5f48-190">`using`Q のステートメントについて\#</span><span class="sxs-lookup"><span data-stu-id="f5f48-190">About `using` statements in Q\#</span></span>

<span data-ttu-id="f5f48-191">`using` ステートメントも Q# に特有です。</span><span class="sxs-lookup"><span data-stu-id="f5f48-191">The `using` statement is also special to Q#.</span></span> <span data-ttu-id="f5f48-192">これは、コードのブロックで使用するために量子ビットを割り当てる場合に使用されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-192">It is used to allocate qubits for use in a block of code.</span></span> <span data-ttu-id="f5f48-193">Q# では、複雑なアルゴリズムの有効期間全体にわたってリソースが固定されるのではなく、すべての量子ビットが動的に割り当てられ、解放されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-193">In Q#, all qubits are dynamically allocated and released, rather than being fixed resources that are there for the entire lifetime of a complex algorithm.</span></span> <span data-ttu-id="f5f48-194">`using` ステートメントは、ブロックの最初で一連の量子ビットを割り当て、ブロックの最後でその量子ビットを解放します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-194">A `using` statement allocates a set of qubits at the start, and releases those qubits at the end of the block.</span></span>

## <a name="execute-the-code-from-the-command-line"></a><span data-ttu-id="f5f48-195">コマンドラインからコードを実行する</span><span class="sxs-lookup"><span data-stu-id="f5f48-195">Execute the code from the command line</span></span>

<span data-ttu-id="f5f48-196">コードを実行するには、コマンドを指定したときに実行さ*れる*呼び出し可能なコンパイラを指定する必要があり `dotnet run` ます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-196">In order to run the code we need to specify the compiler *which* callable to run when we provide the `dotnet run` command.</span></span> <span data-ttu-id="f5f48-197">これを行うには、呼び出し先の直前にを含む行を追加することにより、Q # ファイルを簡単に変更し `@EntryPoint()` ます。 `TestBellState` この場合は、操作です。</span><span class="sxs-lookup"><span data-stu-id="f5f48-197">This is done with a simple change in the Q# file by adding a line with `@EntryPoint()` directly preceding the callable: the `TestBellState` operation in this case.</span></span> <span data-ttu-id="f5f48-198">完全なコードは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-198">The full code should be:</span></span>

```qsharp
namespace Bell {
    open Microsoft.Quantum.Canon;
    open Microsoft.Quantum.Intrinsic;

    operation SetQubitState(desired : Result, target : Qubit) : Unit {
        if (desired != M(target)) {
            X(target);
        }
    }

    @EntryPoint()
    operation TestBellState(count : Int, initial : Result) : (Int, Int) {

        mutable numOnes = 0;
        using (qubit = Qubit()) {

            for (test in 1..count) {
                SetQubitState(initial, qubit);
                let res = M(qubit);

                // Count the number of ones we saw:
                if (res == One) {
                    set numOnes += 1;
                }
            }

            SetQubitState(Zero, qubit);
        }

    // Return number of times we saw a |0> and number of times we saw a |1>
    Message("Test results (# of 0s, # of 1s): ");
    return (count - numOnes, numOnes);
    }
}
```

<span data-ttu-id="f5f48-199">プログラムを実行するには、 `count` `initial` コマンドラインから引数と引数を指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-199">To run the program we need to specify `count` and `initial` arguments from the command line.</span></span> <span data-ttu-id="f5f48-200">たとえば、とのように選択し `count = 1000` `initial = One` ます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-200">Let's choose for example `count = 1000` and `initial = One`.</span></span> <span data-ttu-id="f5f48-201">次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-201">Enter the following command:</span></span>

```dotnetcli
dotnet run --count 1000 --initial One
```

<span data-ttu-id="f5f48-202">次の出力が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-202">And you should observe the following output:</span></span>

```output
Test results (# of 0s, # of 1s):
(0, 1000)
```

<span data-ttu-id="f5f48-203">を試してみると、次のことを確認する `initial = Zero` 必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-203">If you try with `initial = Zero` you should observe:</span></span>

```dotnetcli
dotnet run --count 1000 --initial Zero
```
```output
Test results (# of 0s, # of 1s):
(1000, 0)
```

## <a name="prepare-superposition"></a><span data-ttu-id="f5f48-204">重ね合わせ状態を作成する</span><span class="sxs-lookup"><span data-stu-id="f5f48-204">Prepare superposition</span></span>

<span data-ttu-id="f5f48-205">次に、Q # で法則に qubits を配置する方法を見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="f5f48-205">Now let’s look at how Q# expresses ways to put qubits in superposition.</span></span>  <span data-ttu-id="f5f48-206">量子ビットの状態は、0 と 1 の重ね合わせにできることを思い出してください。</span><span class="sxs-lookup"><span data-stu-id="f5f48-206">Recall that the state of a qubit can be in a superposition of 0 and 1.</span></span>  <span data-ttu-id="f5f48-207">これを行うには、`Hadamard` 操作を使用します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-207">We’ll use the `Hadamard` operation to accomplish this.</span></span> <span data-ttu-id="f5f48-208">量子ビットが従来の状態のいずれか (測定で常に `One` または `Zero` を返す) である場合、`Hadamard` (`H`) 操作によって、量子ビットの測定で 50% の `Zero` および 50% の `One` を返す状態に量子ビットが配置されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-208">If the qubit is in either of the classical states (where a measurement returns `Zero` always or `One` always), then the `Hadamard` or `H` operation will put the qubit in a state where a measurement of the qubit will return `Zero` 50% of the time and return `One` 50% of the time.</span></span>  <span data-ttu-id="f5f48-209">概念上、量子ビットは `Zero` と `One` の中間にあると考えることができます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-209">Conceputually, the qubit can be thought of as halfway between the `Zero` and `One`.</span></span>  <span data-ttu-id="f5f48-210">ここで、`TestBellState` 操作をシミュレートすると、測定後の結果は、ほぼ同数の `Zero` と `One` を返します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-210">Now, when we simulate the `TestBellState` operation, we will see the results will return roughly an equal number of `Zero` and `One` after measurement.</span></span>  

### <a name="x-flips-qubit-state"></a><span data-ttu-id="f5f48-211">`X`qubit 状態を反転します</span><span class="sxs-lookup"><span data-stu-id="f5f48-211">`X` flips qubit state</span></span>

<span data-ttu-id="f5f48-212">まず、量子ビットを反転してみます (量子ビットが `Zero` の状態にある場合は `One` になり、その逆も同様になります)。</span><span class="sxs-lookup"><span data-stu-id="f5f48-212">First we'll just try to flip the qubit (if the qubit is in `Zero` state will flip to `One` and vice versa).</span></span> <span data-ttu-id="f5f48-213">これは、`TestBellState` で測定する前に `X` 操作を実行することで実現されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-213">This is accomplished by performing an `X` operation before we measure it in `TestBellState`:</span></span>

```qsharp
X(qubit);
let res = M(qubit);
```

<span data-ttu-id="f5f48-214">結果は逆順になります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-214">Now the results are reversed:</span></span>

```dotnetcli
dotnet run --count 1000 --initial One
```

```output
Test results (# of 0s, # of 1s):
(1000, 0)
```

```dotnetcli
dotnet run --count 1000 --initial Zero
```
```output
Test results (# of 0s, # of 1s):
(0, 1000)
```

<span data-ttu-id="f5f48-215">次に、qubits のクォンタムプロパティについて説明します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-215">Now let's explore the quantum properties of the qubits.</span></span>

### <a name="h-prepares-superposition"></a><span data-ttu-id="f5f48-216">`H`法則を準備する</span><span class="sxs-lookup"><span data-stu-id="f5f48-216">`H` prepares superposition</span></span>

<span data-ttu-id="f5f48-217">必要なのは、先ほどの実行の `X` 操作を `H` すなわち Hadamard 操作に置き換えることだけです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-217">All we need to do is replace the `X` operation in the previous run with an `H` or Hadamard operation.</span></span> <span data-ttu-id="f5f48-218">これは、量子ビットを 0 から 1 まで完全に反転させるのではなく、半分だけ反転します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-218">Instead of flipping the qubit all the way from 0 to 1, we will only flip it halfway.</span></span> <span data-ttu-id="f5f48-219">`TestBellState` の行を置き換えると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-219">The replaced lines in `TestBellState` now look like:</span></span>

```qsharp
H(qubit);
let res = M(qubit);
```

<span data-ttu-id="f5f48-220">結果はさらに興味深いものになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-220">Now the results get more interesting:</span></span>

```dotnetcli
dotnet run --count 1000 --initial One
```

```output
Test results (# of 0s, # of 1s):
(496, 504)
```

```dotnetcli
dotnet run --count 1000 --initial Zero
```

```output
Test results (# of 0s, # of 1s):
(506, 494)
```

<span data-ttu-id="f5f48-221">測定するたびに、従来型の値が要求されますが、量子ビットは 0 と 1 の中間にあるため、(統計的に) 半分が 0、半分が 1 になります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-221">Every time we measure, we ask for a classical value, but the qubit is halfway between 0 and 1, so we get (statistically) 0 half the time and 1 half the time.</span></span>
<span data-ttu-id="f5f48-222">これは**重ね合わせ**と呼ばれる現象で、これによって初めて量子状態を実際に観測できます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-222">This is known as **superposition** and gives us our first real view into a quantum state.</span></span>

## <a name="prepare-entanglement"></a><span data-ttu-id="f5f48-223">もつれ状態を作成する</span><span class="sxs-lookup"><span data-stu-id="f5f48-223">Prepare entanglement</span></span>

<span data-ttu-id="f5f48-224">では、Q# がどのように量子ビットのもつれを表現するかを見てみましょう。</span><span class="sxs-lookup"><span data-stu-id="f5f48-224">Now let’s look at how Q# expresses ways to entangle qubits.</span></span>
<span data-ttu-id="f5f48-225">まず、最初の量子ビットを初期状態に設定してから、`H` 操作を使用してそれを重ね合わせに配置します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-225">First, we set the first qubit to the initial state and then use the `H` operation to put it into superposition.</span></span>  <span data-ttu-id="f5f48-226">次に、最初の qubit を測定する前に、 `CNOT` 制御されていないを表す新しい操作 () を使用します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-226">Then, before we measure the first qubit, we use a new operation (`CNOT`), which stands for Controlled-NOT.</span></span>  <span data-ttu-id="f5f48-227">2 つの量子ビットに対してこの操作を実行した結果、最初の量子ビットが `One` である場合には 2 番目の量子ビットが反転されます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-227">The result of executing this operation on two qubits is to flip the second qubit if the first qubit is `One`.</span></span>  <span data-ttu-id="f5f48-228">これで、2 つの量子ビットがもつれ状態になります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-228">Now, the two qubits are entangled.</span></span>  <span data-ttu-id="f5f48-229">最初の量子ビットの統計情報は変わっていませんが (測定後、50-50 の確率で `Zero` または `One`)、2 番目の量子ビットを測定すると、最初の量子ビットを測定した結果と__常に__同じになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-229">Our statistics for the first qubit haven't changed (50-50 chance of a `Zero` or a `One` after measurement), but now when we measure the second qubit, it is __always__ the same as what we measured for the first qubit.</span></span> <span data-ttu-id="f5f48-230">この `CNOT` が 2 つの量子ビットをもつれさせ、片方に何かが起きると、もう片方にも同じことが起こるようになっています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-230">Our `CNOT` has entangled the two qubits, so that whatever happens to one of them, happens to the other.</span></span> <span data-ttu-id="f5f48-231">測定を反対にしても (最初の量子ビットの前に 2 番目の量子ビットを測定する)、同じことが起こります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-231">If you reversed the measurements (did the second qubit before the first), the same thing would happen.</span></span> <span data-ttu-id="f5f48-232">最初の測定値はランダムであり、2 回目の測定値は最初に検出されたものと完全に一致します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-232">The first measurement would be random and the second would be in lock step with whatever was discovered for the first.</span></span>

<span data-ttu-id="f5f48-233">最初に、ではなく2つの qubits を割り当てる必要があり `TestBellState` ます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-233">The first thing we'll need to do is allocate two qubits instead of one in `TestBellState`:</span></span>

```qsharp
using ((q0, q1) = (Qubit(), Qubit())) {
```

<span data-ttu-id="f5f48-234">これにより、`TestBellState` で測定 (`M`) する前に、新しい操作 (`CNOT`) を追加できます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-234">This will allow us to add a new operation (`CNOT`) before we measure  (`M`) in `TestBellState`:</span></span>

```qsharp
SetQubitState(initial, q0);
SetQubitState(Zero, q1);

H(q0);
CNOT(q0, q1);
let res = M(q0);
```

<span data-ttu-id="f5f48-235">最初の量子ビットを初期化するために別の `SetQubitState` 操作を追加し、開始時に常に `Zero` 状態になるようにしました。</span><span class="sxs-lookup"><span data-stu-id="f5f48-235">We've added another `SetQubitState` operation to initialize the first qubit to make sure that it's always in the `Zero` state when we start.</span></span>

<span data-ttu-id="f5f48-236">また、2 番目の量子ビットを解放する前にリセットする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-236">We also need to reset the second qubit before releasing it.</span></span>

```qsharp
SetQubitState(Zero, q0);
SetQubitState(Zero, q1);
```

<span data-ttu-id="f5f48-237">完全なルーチンは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-237">The full routine now looks like this:</span></span>

```qsharp
    operation TestBellState(count : Int, initial : Result) : (Int, Int) {

        mutable numOnes = 0;
        using ((q0, q1) = (Qubit(), Qubit())) {
            for (test in 1..count) {
                SetQubitState(initial, q0);
                SetQubitState(Zero, q1);

                H(q0);
                CNOT(q0,q1);
                let res = M(q0);

                // Count the number of ones we saw:
                if (res == One) {
                    set numOnes += 1;
                }
            }

            SetQubitState(Zero, q0);
            SetQubitState(Zero, q1);
        }

        // Return number of times we saw a |0> and number of times we saw a |1>
        return (count-numOnes, numOnes);
    }
```

<span data-ttu-id="f5f48-238">これを実行すると、以前とまったく同じ 50-50 の結果が得られます。</span><span class="sxs-lookup"><span data-stu-id="f5f48-238">If we run this, we'll get exactly the same 50-50 result we got before.</span></span> <span data-ttu-id="f5f48-239">しかし、ここで興味深いのは、2 番目の量子ビットが測定される最初の量子ビットに対してどのように反応するかです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-239">However, what we're interested in is how the second qubit reacts to the first being measured.</span></span> <span data-ttu-id="f5f48-240">この統計情報は、新しいバージョンの `TestBellState` の操作で追加します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-240">We'll add this statistic with a new version of the `TestBellState` operation:</span></span>

```qsharp
    operation TestBellState(count : Int, initial : Result) : (Int, Int, Int) {
        mutable numOnes = 0;
        mutable agree = 0;
        using ((q0, q1) = (Qubit(), Qubit())) {
            for (test in 1..count) {
                SetQubitState(initial, q0);
                SetQubitState(Zero, q1);

                H(q0);
                CNOT(q0, q1);
                let res = M(q0);

                if (M(q1) == res) {
                    set agree += 1;
                }

                // Count the number of ones we saw:
                if (res == One) {
                    set numOnes += 1;
                }
            }
            
            SetQubitState(Zero, q0);
            SetQubitState(Zero, q1);
        }

        // Return times we saw |0>, times we saw |1>, and times measurements agreed
        Message("Test results (# of 0s, # of 1s, # of agreements)");
        return (count-numOnes, numOnes, agree);
    }
```

<span data-ttu-id="f5f48-241">新しい戻り値 (`agree`) は、最初の量子ビットの測定値が 2 番目の量子ビットの測定値と一致した回数を追跡します。</span><span class="sxs-lookup"><span data-stu-id="f5f48-241">The new return value (`agree`) keeps track of every time the measurement from the first qubit matches the measurement of the second qubit.</span></span>

<span data-ttu-id="f5f48-242">取得したコードを実行すると、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f5f48-242">Running the code we obtain:</span></span>

```dotnetcli
dotnet run --count 1000 --initial One
```
```output
(505, 495, 1000)
```
```dotnetcli
dotnet run --count 1000 --initial Zero
```
```output
Test results (# of 0s, # of 1s, # of agreements)
(507, 493, 1000)
```

<span data-ttu-id="f5f48-243">概要で述べたように、最初の量子ビットの統計情報は変わっていませんが (50-50 の確率で 0 または 1)、2 番目の量子ビットを測定すると、最初の量子ビットを測定した結果と__常に__同じになります。これは、もつれ状態にあるからです。</span><span class="sxs-lookup"><span data-stu-id="f5f48-243">As stated in the overview, our statistics for the first qubit haven't changed (50-50 chance of a 0 or a 1), but now when we measure the second qubit, it is __always__ the same as what we measured for the first qubit, because they are entangled!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5f48-244">次のステップ</span><span class="sxs-lookup"><span data-stu-id="f5f48-244">Next steps</span></span>

<span data-ttu-id="f5f48-245">[グローバーの検索](xref:microsoft.quantum.quickstarts.search)のチュートリアルでは、最も人気のある量子コンピューティング アルゴリズムの 1 つである、グローバーの検索をビルドして実行する方法を示しています。また、量子コンピューティングに関する実際の問題を解決するために使用できる Q# プログラムの優れた例を紹介しています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-245">The tutorial [Grover’s search](xref:microsoft.quantum.quickstarts.search) shows you how to build and run Grover search, one of the most popular quantum computing algorithms and offers a nice example of a Q# program that can be used to solve real problems with quantum computing.</span></span>  

<span data-ttu-id="f5f48-246">「[Get Started with the Quantum Development Kit](xref:microsoft.quantum.welcome)」(Quantum Development Kit の概要) では、Q# と量子コンピューティングのその他の学習方法も紹介しています。</span><span class="sxs-lookup"><span data-stu-id="f5f48-246">[Get Started with the Quantum Development Kit](xref:microsoft.quantum.welcome) recommends more ways to learn Q# and quantum programming.</span></span>