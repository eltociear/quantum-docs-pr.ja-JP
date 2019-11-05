---
title: 無効になった qubits use checker |クォンタムコンピューターのトレースシミュレーター |Microsoft Docs
description: クォンタムコンピューターのトレースシミュレーターの概要
author: vadym-kl
ms.author: vadym@microsoft.com
ms.date: 12/11/2017
ms.topic: article
uid: microsoft.quantum.machines.qc-trace-simulator.invalidated-qubits
ms.openlocfilehash: 7403381b995ab660aa5cbc5a52b1e12c5c9ce442
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73184969"
---
# <a name="invalidated-qubits-use-checker"></a><span data-ttu-id="388e8-103">無効になった Qubits 使用チェッカー</span><span class="sxs-lookup"><span data-stu-id="388e8-103">Invalidated Qubits Use Checker</span></span>

<span data-ttu-id="388e8-104">`Invalidated Qubits Use Checker` は、コード内の潜在的なバグを検出するように設計された quantum コンピューター [TraceSimulator](xref:microsoft.quantum.machines.qc-trace-simulator.intro)の一部です。</span><span class="sxs-lookup"><span data-stu-id="388e8-104">The `Invalidated Qubits Use Checker` is a part of the quantum computer [TraceSimulator](xref:microsoft.quantum.machines.qc-trace-simulator.intro) designed for detecting potential bugs in the code.</span></span> <span data-ttu-id="388e8-105">`Invalidated Qubits Use Checker`によって検出された問題を示すために、次の Q # コードを考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="388e8-105">Consider the following piece of Q# code to illustrate the issues detected by the `Invalidated Qubits Use Checker`.</span></span>

```qsharp
operation UseReleasedQubitTest () : Unit {
    mutable q = new Qubit[1];
    using (ans = Qubit()) {
        set q w/= 0 <- ans;
    }
    H(q[0]);
}
```

<span data-ttu-id="388e8-106">`H` が `q[0]` に適用されると、既に解放されている qubit を指します。</span><span class="sxs-lookup"><span data-stu-id="388e8-106">When `H` is applied to `q[0]` it points to an already released qubit.</span></span> <span data-ttu-id="388e8-107">これにより、未定義の動作が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="388e8-107">This can cause undefined behavior.</span></span> <span data-ttu-id="388e8-108">`Invalidated Qubits Use Checker` が有効になっている場合、既に解放されている qubit に操作が適用されると、例外 `InvalidatedQubitsUseCheckerException` がスローされます。</span><span class="sxs-lookup"><span data-stu-id="388e8-108">When the `Invalidated Qubits Use Checker` is enabled, the exception `InvalidatedQubitsUseCheckerException` will be thrown if an operation is applied to an already released qubit.</span></span> <span data-ttu-id="388e8-109">詳細については、 [InvalidatedQubitsUseCheckerException](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.InvalidatedQubitsUseCheckerException)の API ドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="388e8-109">See the API documentation on [InvalidatedQubitsUseCheckerException](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.InvalidatedQubitsUseCheckerException) for more details.</span></span>

## <a name="using-the-invalidated-qubits-use-checker-in-your-c-program"></a><span data-ttu-id="388e8-110">無効化された Qubits を使用しC#てプログラムで使用する</span><span class="sxs-lookup"><span data-stu-id="388e8-110">Using the Invalidated Qubits Use Checker in your C# Program</span></span>

<span data-ttu-id="388e8-111">次に、`Invalidated Qubits Use Checker` が有効C#になっているクォンタムコンピューター `Trace
Simulator` を使用するためのドライバーコードの例を示します。</span><span class="sxs-lookup"><span data-stu-id="388e8-111">The following is an example of C# driver code for using the quantum computer `Trace
Simulator` with the `Invalidated Qubits Use Checker` enabled:</span></span> 

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
            var traceSimCfg = new QCTraceSimulatorConfiguration();
            traceSimCfg.useInvalidatedQubitsUseChecker = true; // enables useInvalidatedQubitsUseChecker
            QCTraceSimulator sim = new QCTraceSimulator(traceSimCfg);
            var res = MyQuantumProgram.Run().Result;
            System.Console.WriteLine("Press any key to continue...");
            System.Console.ReadKey();
        }
    }
}
```

<span data-ttu-id="388e8-112">クラス `QCTraceSimulatorConfiguration` には、クォンタムコンピューターのトレースシミュレーターの構成が格納され、`QCTraceSimulator` コンストラクターの引数として指定できます。</span><span class="sxs-lookup"><span data-stu-id="388e8-112">The class `QCTraceSimulatorConfiguration` stores the configuration of the quantum computer trace simulator and can be provided as an argument for the `QCTraceSimulator` constructor.</span></span> <span data-ttu-id="388e8-113">`useInvalidatedQubitsUseChecker` が true に設定されている場合、`Invalidated Qubits Use Checker` が有効になります。</span><span class="sxs-lookup"><span data-stu-id="388e8-113">When `useInvalidatedQubitsUseChecker` is set to true the `Invalidated Qubits Use Checker` is enabled.</span></span> <span data-ttu-id="388e8-114">詳細については、 [Qctracesimulator](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulator)および[Qctracesimulatorconfiguration](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulatorConfiguration)に関する API ドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="388e8-114">See the API documentation on [QCTraceSimulator](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulator) and [QCTraceSimulatorConfiguration](https://docs.microsoft.com/dotnet/api/Microsoft.Quantum.Simulation.Simulators.QCTraceSimulators.QCTraceSimulatorConfiguration) for more details.</span></span>

## <a name="see-also"></a><span data-ttu-id="388e8-115">関連項目</span><span class="sxs-lookup"><span data-stu-id="388e8-115">See also</span></span> ##

- <span data-ttu-id="388e8-116">クォンタムコンピューターの[トレースシミュレーター](xref:microsoft.quantum.machines.qc-trace-simulator.intro)の概要。</span><span class="sxs-lookup"><span data-stu-id="388e8-116">The quantum computer [Trace Simulator](xref:microsoft.quantum.machines.qc-trace-simulator.intro) overview.</span></span>