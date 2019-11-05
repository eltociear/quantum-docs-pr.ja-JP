---
title: Quantum 開発キット-完全な状態シミュレーター |Microsoft Docs
description: Microsoft の Quantum 開発キットの完全な状態シミュレーターの概要
author: anpaz-msft
ms.author: anpaz@microsoft.com
ms.date: 12/7/2017
ms.topic: article
uid: microsoft.quantum.machines.full-state-simulator
ms.openlocfilehash: ab0e65765d27e301a59948d7c02105a523022e68
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73184680"
---
# <a name="quantum-development-kit-full-state-simulator"></a><span data-ttu-id="228e1-103">Quantum 開発キット-完全な状態シミュレーター</span><span class="sxs-lookup"><span data-stu-id="228e1-103">Quantum Development Kit Full State Simulator</span></span>

<span data-ttu-id="228e1-104">Quantum Development Kit には、Microsoft Research の[Liq $ Ui | \rangle $](http://stationq.github.io/Liquid/)に似た完全な状態のクォンタムシミュレーターが用意されています。</span><span class="sxs-lookup"><span data-stu-id="228e1-104">The Quantum Development Kit provides a full state quantum simulator similar to [LIQ$Ui|\rangle$](http://stationq.github.io/Liquid/) from Microsoft Research.</span></span>
<span data-ttu-id="228e1-105">このシミュレーターを使用すると、コンピューターの Q # で記述されたクォンタムアルゴリズムを実行およびデバッグできます。</span><span class="sxs-lookup"><span data-stu-id="228e1-105">This simulator can be used to execute and debug quantum algorithms written in Q# on your computer.</span></span>

<span data-ttu-id="228e1-106">このクォンタムシミュレーターは `QuantumSimulator` クラスを介して公開されます。</span><span class="sxs-lookup"><span data-stu-id="228e1-106">This quantum simulator is exposed via the `QuantumSimulator` class.</span></span> <span data-ttu-id="228e1-107">シミュレーターを使用するには、このクラスのインスタンスを作成し、残りのパラメーターと共に実行するクォンタム操作の `Run` メソッドに渡すだけです。</span><span class="sxs-lookup"><span data-stu-id="228e1-107">To use the simulator, simply create an instance of this class and pass it to the `Run` method of the quantum operation you want to execute along with the rest of the parameters:</span></span>

```csharp
    using (var sim = new QuantumSimulator())
    {
        var res = myOperation.Run(sim).Result;
        ///...
    }
```

## <a name="idisposable"></a><span data-ttu-id="228e1-108">IDisposable</span><span class="sxs-lookup"><span data-stu-id="228e1-108">IDisposable</span></span>

<span data-ttu-id="228e1-109">`QuantumSimulator` クラスは <xref:System.IDisposable>を実装しているため、シミュレーターのインスタンスが使用されなくなったら、`Dispose` メソッドを呼び出す必要があります。</span><span class="sxs-lookup"><span data-stu-id="228e1-109">The `QuantumSimulator` class implements <xref:System.IDisposable>, thus the `Dispose` method should be called once the instance of the simulator is not used anymore.</span></span> <span data-ttu-id="228e1-110">これを行う最善の方法は、上記の例のように、シミュレーターを `using` ステートメント内にラップすることです。</span><span class="sxs-lookup"><span data-stu-id="228e1-110">The best way to do this is to wrap the simulator within a `using` statement, as in the example above.</span></span>

## <a name="seed"></a><span data-ttu-id="228e1-111">シード</span><span class="sxs-lookup"><span data-stu-id="228e1-111">Seed</span></span>

<span data-ttu-id="228e1-112">`QuantumSimulator` は、乱数ジェネレーターを使用して、クォンタムのランダム性をシミュレートします。</span><span class="sxs-lookup"><span data-stu-id="228e1-112">The `QuantumSimulator` uses a random number generator to simulate quantum randomness.</span></span> <span data-ttu-id="228e1-113">テスト目的では、決定的な結果が得られる場合があります。</span><span class="sxs-lookup"><span data-stu-id="228e1-113">For testing purposes, it is sometimes useful to have deterministic results.</span></span> <span data-ttu-id="228e1-114">これを実現するには、`randomNumberGeneratorSeed` パラメーターを使用して `QuantumSimulator`のコンストラクターに乱数ジェネレーターのシードを指定します。</span><span class="sxs-lookup"><span data-stu-id="228e1-114">This can be accomplished by providing a seed for the random number generator in the `QuantumSimulator`'s constructor via the `randomNumberGeneratorSeed` parameter:</span></span>

```csharp
    using (var sim = new QuantumSimulator(randomNumberGeneratorSeed: 42))
    {
        var res = myOperationTest.Run(sim).Result;
        ///...
    }
```

## <a name="threads"></a><span data-ttu-id="228e1-115">Threads</span><span class="sxs-lookup"><span data-stu-id="228e1-115">Threads</span></span>

<span data-ttu-id="228e1-116">`QuantumSimulator` は、 [OpenMP](http://www.openmp.org/)を使用して、必要な線形代数を並列化します。</span><span class="sxs-lookup"><span data-stu-id="228e1-116">The `QuantumSimulator` uses [OpenMP](http://www.openmp.org/) to parallelize the linear algebra required.</span></span> <span data-ttu-id="228e1-117">既定では、OpenMP は使用可能なすべてのハードウェアスレッドを使用します。これは、必要な調整によって実際の作業が dwarf されるため、少数の qubits を持つプログラムの実行速度が低下することを意味します。</span><span class="sxs-lookup"><span data-stu-id="228e1-117">By default OpenMP uses all available hardware threads, which means that programs with small numbers of qubits will often run slowly because the coordination required will dwarf the actual work.</span></span> <span data-ttu-id="228e1-118">これは、`OMP_NUM_THREADS` 環境変数を小さい数値に設定することによって修正できます。</span><span class="sxs-lookup"><span data-stu-id="228e1-118">This can be fixed by setting the environment variable `OMP_NUM_THREADS` to a small number.</span></span> <span data-ttu-id="228e1-119">経験則として、1つのスレッドは最大4つの qubits に適しています。また、qubits ごとに追加のスレッドが適していますが、これはアルゴリズムに大きく依存しています。</span><span class="sxs-lookup"><span data-stu-id="228e1-119">As a very rough rule of thumb, 1 thread is good for up to about 4 qubits, and then an additional thread per qubit is good, although this is highly dependent on your algorithm.</span></span>
