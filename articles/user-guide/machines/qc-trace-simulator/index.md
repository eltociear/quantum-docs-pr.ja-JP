---
title: 量子コンピューターのトレース シミュレーター
description: Microsoft 量子コンピューターのトレース シミュレーターを使用して、従来型のコードをデバッグし、量子プログラムのリソース要件を見積もる方法について説明します。
author: vadym-kl
ms.author: vadym@microsoft.com
ms.date: 12/11/2017
ms.topic: article
uid: microsoft.quantum.machines.qc-trace-simulator.intro
ms.openlocfilehash: 4cec688da35951271d87396d9b6a8fed744defc6
ms.sourcegitcommit: 0181e7c9e98f9af30ea32d3cd8e7e5e30257a4dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85273499"
---
# <a name="quantum-trace-simulator"></a><span data-ttu-id="c1ee3-103">量子トレース シミュレーター</span><span class="sxs-lookup"><span data-stu-id="c1ee3-103">Quantum Trace Simulator</span></span>

<span data-ttu-id="c1ee3-104">Microsoft 量子コンピューターのトレース シミュレーターは、量子コンピューターの状態を実際にシミュレートせずに、量子プログラムを実行します。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-104">The Microsoft quantum computer trace simulator executes a quantum program without actually simulating the state of a quantum computer.</span></span>  <span data-ttu-id="c1ee3-105">このため、トレース シミュレーターでは、何千もの量子ビットを使用する量子プログラムを実行できます。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-105">For this reason, the trace simulator can execute quantum programs that use thousands of qubits.</span></span>  <span data-ttu-id="c1ee3-106">これは主に次の 2 つの目的で役立ちます。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-106">It is useful for two main purposes:</span></span> 

* <span data-ttu-id="c1ee3-107">量子プログラムの一部である、従来型のコードのデバッグ。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-107">Debugging classical code that is part of a quantum program.</span></span> 
* <span data-ttu-id="c1ee3-108">量子プログラムの特定のインスタンスを量子コンピューターで実行するために必要なリソースの推定。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-108">Estimating the resources required to run a given instance of a quantum program on a quantum computer.</span></span>

<span data-ttu-id="c1ee3-109">トレース シミュレーターは、測定を行う必要がある場合に、ユーザーによって提供される追加情報を使用します。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-109">The trace simulator relies on additional information provided by the user when measurements must be performed.</span></span> <span data-ttu-id="c1ee3-110">詳細については、「[測定結果の確率を指定する](#providing-the-probability-of-measurement-outcomes)」セクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-110">See Section [Providing the probability of measurement outcomes](#providing-the-probability-of-measurement-outcomes) for more details on this.</span></span> 

## <a name="providing-the-probability-of-measurement-outcomes"></a><span data-ttu-id="c1ee3-111">測定結果の確率を指定する</span><span class="sxs-lookup"><span data-stu-id="c1ee3-111">Providing the Probability of Measurement Outcomes</span></span>

<span data-ttu-id="c1ee3-112">量子アルゴリズムには、2 種類の測定値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-112">There are two kinds of measurements that appear in quantum algorithms.</span></span> <span data-ttu-id="c1ee3-113">最初の種類は、ユーザーが結果の確率を知っている場合に使用するため、補助的な役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-113">The first kind plays an auxiliary role where the user usually knows the probability of the outcomes.</span></span> <span data-ttu-id="c1ee3-114">この場合、ユーザーは <xref:microsoft.quantum.intrinsic> 名前空間の <xref:microsoft.quantum.intrinsic.assertprob> を使用して、知っている確率を表すことができます。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-114">In this case the user can write <xref:microsoft.quantum.intrinsic.assertprob> from the <xref:microsoft.quantum.intrinsic> namespace to express this knowledge.</span></span> <span data-ttu-id="c1ee3-115">次の例を使って説明します。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-115">The following example illustrates this:</span></span>

```qsharp
operation TeleportQubit(source : Qubit, target : Qubit) : Unit {
    using (qubit = Qubit()) {
        H(qubit);
        CNOT(qubit, target);
        CNOT(source, qubit);
        H(source);

        AssertProb([PauliZ], [source], Zero, 0.5, "Outcomes must be equally likely", 1e-5);
        AssertProb([PauliZ], [q], Zero, 0.5, "Outcomes must be equally likely", 1e-5);

        if (M(source) == One)  { Z(target); X(source); }
        if (M(q) == One) { X(target); X(q); }
    }
}
```

<span data-ttu-id="c1ee3-116">トレース シミュレーターが `AssertProb` を実行すると、`source` と `q` で `PauliZ` を測定した結果は、確率が0.5 の `Zero` となることを記録します。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-116">When the trace simulator executes `AssertProb` it will record that measuring `PauliZ` on `source` and `q` should be given an outcome of `Zero` with probability 0.5.</span></span> <span data-ttu-id="c1ee3-117">シミュレーターが後で `M` を実行すると、記録された結果の確率の値が検出され、`M` は確率が0.5 の `Zero` または `One` を返します。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-117">When the simulator executes `M` later, it will find the recorded values of the outcome probabilities and `M` will return `Zero` or `One` with probability 0.5.</span></span> <span data-ttu-id="c1ee3-118">量子状態を追跡するシミュレーターで同じコードを実行すると、シミュレーターは `AssertProb` で指定された確率が正しいかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-118">When the same code is executed on a simulator that keeps track of the quantum state, such a simulator will check that the provided probabilities in `AssertProb` are correct.</span></span>

## <a name="running-your-program-with-the-quantum-computer-trace-simulator"></a><span data-ttu-id="c1ee3-119">量子コンピューターのトレース シミュレーターを使用してプログラムを実行する</span><span class="sxs-lookup"><span data-stu-id="c1ee3-119">Running your Program with the Quantum Computer Trace Simulator</span></span> 

<span data-ttu-id="c1ee3-120">量子コンピューターのトレース シミュレーターは、ターゲット コンピューターの 1 つとして見なすことができます。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-120">The quantum computer trace simulator may be viewed as just another target machine.</span></span> <span data-ttu-id="c1ee3-121">量子コンピューターを使用するための C# ドライバー プログラムは、他の量子シミュレーターで使用するものとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-121">The C# driver program for using it is very similar to the one for any other quantum Simulator:</span></span> 

```csharp
using Microsoft.Quantum.Simulation.Core;
using Microsoft.Quantum.Simulation.Simulators;
using Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators;

namespace Quantum.MyProgram
{
    class Driver
    {
        static void Main(string[] args)
        {
            QCTraceSimulator sim = new QCTraceSimulator();
            var res = MyQuantumProgram.Run(sim).Result;
            System.Console.WriteLine("Press any key to continue...");
            System.Console.ReadKey();
        }
    }
}
```

<span data-ttu-id="c1ee3-122">`AssertProb` によって注釈が付けられていない測定が少なくとも 1 つある場合は、シミュレーターによって `Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators` 名前空間から `UnconstrainedMeasurementException` がスローされることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-122">Note that if there is at least one measurement not annotated using `AssertProb`, the simulator will throw `UnconstrainedMeasurementException` from the `Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators` namespace.</span></span> <span data-ttu-id="c1ee3-123">詳細については [UnconstrainedMeasurementException](xref:Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.UnconstrainedMeasurementException) に関する API ドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-123">See the API documentation on [UnconstrainedMeasurementException](xref:Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.UnconstrainedMeasurementException) for more details.</span></span>

<span data-ttu-id="c1ee3-124">量子プログラムの実行に加えて、トレース シミュレーターには、プログラム内のバグを検出し、量子プログラム リソースの推定を行うための 5 つのコンポーネントが付属しています。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-124">In addition to running quantum programs, the trace simulator comes with five components for detecting bugs in programs and performing quantum program resource estimates:</span></span> 

* [<span data-ttu-id="c1ee3-125">Distinct Inputs Checker</span><span class="sxs-lookup"><span data-stu-id="c1ee3-125">Distinct Inputs Checker</span></span>](xref:microsoft.quantum.machines.qc-trace-simulator.distinct-inputs)
* [<span data-ttu-id="c1ee3-126">Invalidated Qubits Use Checker</span><span class="sxs-lookup"><span data-stu-id="c1ee3-126">Invalidated Qubits Use Checker</span></span>](xref:microsoft.quantum.machines.qc-trace-simulator.invalidated-qubits)
* [<span data-ttu-id="c1ee3-127">Primitive Operations Counter</span><span class="sxs-lookup"><span data-stu-id="c1ee3-127">Primitive Operations Counter</span></span>](xref:microsoft.quantum.machines.qc-trace-simulator.primitive-counter)
* [<span data-ttu-id="c1ee3-128">Circuit Depth Counter</span><span class="sxs-lookup"><span data-stu-id="c1ee3-128">Circuit Depth Counter</span></span>](xref:microsoft.quantum.machines.qc-trace-simulator.depth-counter)
* [<span data-ttu-id="c1ee3-129">Circuit Width Counter</span><span class="sxs-lookup"><span data-stu-id="c1ee3-129">Circuit Width Counter</span></span>](xref:microsoft.quantum.machines.qc-trace-simulator.width-counter)

<span data-ttu-id="c1ee3-130">これらの各コンポーネントは、`QCTraceSimulatorConfiguration` で適切なフラグを設定することによって有効にすることができます。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-130">Each of these components may be enabled by setting appropriate flags in `QCTraceSimulatorConfiguration`.</span></span> <span data-ttu-id="c1ee3-131">これらの各コンポーネントの使用方法の詳細については、対応する参照ファイルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-131">More details about using each of these components are provided in the corresponding reference files.</span></span> <span data-ttu-id="c1ee3-132">具体的な詳細については [QCTraceSimulatorConfiguration](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulatorConfiguration) に関する API ドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c1ee3-132">See the API documentation on [QCTraceSimulatorConfiguration](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulatorConfiguration) for specific details.</span></span>

## <a name="see-also"></a><span data-ttu-id="c1ee3-133">関連項目</span><span class="sxs-lookup"><span data-stu-id="c1ee3-133">See also</span></span>
<span data-ttu-id="c1ee3-134">量子コンピューターの[トレース シミュレーター](xref:Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulator)向け C# リファレンス</span><span class="sxs-lookup"><span data-stu-id="c1ee3-134">The quantum computer [trace simulator](xref:Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulator) C# reference</span></span> 
