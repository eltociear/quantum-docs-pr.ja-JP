---
title: 相関 wavefunctions |Microsoft Docs
description: Quantum Dynamics の概念ドキュメント
author: guanghaolow
ms.author: gulow@microsoft.com
ms.date: 05/28/2019
ms.topic: article-type-from-white-list
uid: microsoft.quantum.chemistry.concepts.multireference
ms.openlocfilehash: 0b14f373d31c5b63e313e07810daf62d9195b1d3
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/26/2019
ms.locfileid: "73184034"
---
# <a name="correlated-wavefunctions"></a><span data-ttu-id="d7fda-103">相関 wavefunctions</span><span class="sxs-lookup"><span data-stu-id="d7fda-103">Correlated wavefunctions</span></span>

<span data-ttu-id="d7fda-104">多くのシステム (特に均衡ジオメトリの近くにある) では、 [Fock](xref:microsoft.quantum.chemistry.concepts.hartreefock)理論では、単一決定の参照状態を通じて分子プロパティの定性的な説明が提供されます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-104">For many systems, particularly those near the equilibrium geometry, [Hartree–Fock](xref:microsoft.quantum.chemistry.concepts.hartreefock) theory provides a qualitative description of molecular properties through a single-determinant reference state.</span></span> <span data-ttu-id="d7fda-105">ただし、定量的精度を実現するには、相関関係の影響も考慮する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7fda-105">However, in order to achieve quantitative accuracy, one must also consider correlation effects.</span></span> 

<span data-ttu-id="d7fda-106">このコンテキストでは、動的と非動的の相関関係を dinstinguish することが重要です。</span><span class="sxs-lookup"><span data-stu-id="d7fda-106">In this context, it is important to dinstinguish between dynamic and non-dynamic correlations.</span></span>
<span data-ttu-id="d7fda-107">Dynamical の相関関係は、原子のような傾向があるとしても、電子的な斥力のようなものではありません。</span><span class="sxs-lookup"><span data-stu-id="d7fda-107">Dynamical correlations arise from the tendency of electrons to stay apart, such as due to interelectronic repulsion.</span></span> <span data-ttu-id="d7fda-108">この効果は、参照状態の原子の excitations を考慮することによって、モデル化にすることができます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-108">This effect can be modelled by considering excitations of electrons out of the reference state.</span></span> <span data-ttu-id="d7fda-109">非動的な相関関係は、wavefunction が取り出しの順序で2つ以上の構成によって支配されている場合に発生します。これは、システムの定性的な説明だけを達成する場合でも同様です。</span><span class="sxs-lookup"><span data-stu-id="d7fda-109">Non-dynamic correlations arise when the wavefunction is dominated by two or more configurations at zeroth order, even to achieve only a qualitative description of the system.</span></span>
<span data-ttu-id="d7fda-110">これには、要因の法則があり、multireference wavefunction の例があります。</span><span class="sxs-lookup"><span data-stu-id="d7fda-110">This necessitates a superposition of determinants and is an example of a multireference wavefunction.</span></span>

<span data-ttu-id="d7fda-111">化学ライブラリを使用すると、法則の要因として、multireference の問題に取り出し order wavefunction を指定することができます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-111">The chemistry library provides a way to specify a zeroth order wavefunction for the multireference problem as a superposition of determinants.</span></span> <span data-ttu-id="d7fda-112">この方法は、スパース multireference wavefunctions と呼ばれ、法則を指定するのに十分な数のコンポーネントだけがある場合に有効です。</span><span class="sxs-lookup"><span data-stu-id="d7fda-112">This approach, which we call sparse multireference wavefunctions, is effective when only a few components suffice to specify the superposition.</span></span> <span data-ttu-id="d7fda-113">また、このライブラリには、汎用化されたユニタリ (クラスター ansatz) を使用した単一の決定参照の上に動的な相関関係を含めるメソッドも用意されています。</span><span class="sxs-lookup"><span data-stu-id="d7fda-113">The library also provides a method to include dynamic correlations on top of a single-determinant reference via the generalized unitary coupled-cluster ansatz.</span></span> <span data-ttu-id="d7fda-114">さらに、クォンタムコンピューターでこれらの状態を生成するクォンタム回線も構築されます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-114">Furthermore, it also constructs quantum circuits that generate these states on a quantum computer.</span></span> <span data-ttu-id="d7fda-115">これらの状態は[Broombridge スキーマ](xref:microsoft.quantum.libraries.chemistry.schema.broombridge)で指定できます。また、化学ライブラリを使用してこれらの状態を手動で指定する機能も用意されています。</span><span class="sxs-lookup"><span data-stu-id="d7fda-115">These states may be specified in the [Broombridge schema](xref:microsoft.quantum.libraries.chemistry.schema.broombridge), and we also provide the functionality to manually specify these states through the chemistry library.</span></span>

## <a name="sparse-multi-reference-wavefunction"></a><span data-ttu-id="d7fda-116">スパースマルチ参照 wavefunction</span><span class="sxs-lookup"><span data-stu-id="d7fda-116">Sparse multi-reference wavefunction</span></span>
<span data-ttu-id="d7fda-117">複数参照の状態 $ \ket{\psi_{\rm {MCSCF}}} $ は、$-電子を後で決定する $N の線形の組み合わせとして明示的に指定できます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-117">A multi-reference state $\ket{\psi_{\rm {MCSCF}}}$ may be specified explicitly as a linear combination of $N$-electron Slater determininants.</span></span>
<span data-ttu-id="d7fda-118">\begin{align} \ket{\psi_{\rm {MCSCF}} <}{0}i_N i_2 \lambda_{i_1、i_2、\ cドット、i_N} a ^ & dagger< < a ^ \dagger_{i_N}\ket ですが、していないことを確認してください (& a)。、、、、および。</span><span class="sxs-lookup"><span data-stu-id="d7fda-118">\begin{align} \ket{\psi_{\rm {MCSCF}}} \propto \sum_{i_1 < i_2 < \cdots < i_N} \lambda_{i_1,i_2,\cdots,i_N} a^\dagger_{i_1}a^\dagger_{i_2}\cdots a^\dagger_{i_N}\ket{0}.</span></span>
<span data-ttu-id="d7fda-119">\end{align} たとえば、次のように、州 $ \ propto (0.1 a ^ & dagger\ket >-dagger/0.2 a ^ & dagger){0}$ を化学ライブラリに指定することができます (& d)。この例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="d7fda-119">\end{align} For example, the state $\propto(0.1 a^\dagger_1a^\dagger_2a^\dagger_6 - 0.2 a^\dagger_2a^\dagger_1a^\dagger_5)\ket{0}$ may be specified in the chemistry library as follows.</span></span>
```csharp
// Create a list of tuples where the first item of each 
// tuple are indices to the creation operators acting on the
// vacuum state, and the second item is the coefficient
// of that basis state.
var superposition = new[] {
    (new[] {1, 2, 6}, 0.1),
    (new[] {2, 1, 5}, -0.2) };

// Create a fermion wavefunction object that represents the superposition.
var wavefunction = new FermionWavefunction<int>(superposition);
```
<span data-ttu-id="d7fda-120">法則コンポーネントのこの明示的な表現は、いくつかのコンポーネントのみを指定する必要がある場合に有効です。</span><span class="sxs-lookup"><span data-stu-id="d7fda-120">This explicit representation of the superposition components is effective when only a few components need to be specified.</span></span> <span data-ttu-id="d7fda-121">望ましい状態を正確にキャプチャするために多くのコンポーネントが必要な場合は、この表現を使用しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d7fda-121">One should avoid using this representation when many components are required to accurately capture the desired state.</span></span> <span data-ttu-id="d7fda-122">この理由は、クォンタムコンピューターでこの状態を準備するクォンタム回線のゲートコストであり、少なくとも法則コンポーネントの数を使用して線形的にスケーリングし、法則の quadratically の1つの値で最大をスケールします。</span><span class="sxs-lookup"><span data-stu-id="d7fda-122">The reason for this is the gate cost of quantum circuit that prepares this state on a quantum computer, which scales at least linearly with the number of superposition components, and at most quadratically with the one-norm of the superposition amplitudes.</span></span>

## <a name="unitary-coupled-cluster-wavefunction"></a><span data-ttu-id="d7fda-123">イン wavefunction クラスターの組み合わせ</span><span class="sxs-lookup"><span data-stu-id="d7fda-123">Unitary coupled-cluster wavefunction</span></span>
<span data-ttu-id="d7fda-124">Chemistery ライブラリを使用して、wavefunction $ \ket{\psi_{\rm {UCC}} $ という組み合わせを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-124">It is also possible to specify a unitary coupled-cluster wavefunction $\ket{\psi_{\rm {UCC}}}$ using the chemistery library.</span></span> <span data-ttu-id="d7fda-125">このような状況では、"$ \ket{\psi_{\rm{SCF}}} $" という1つの決定の参照状態があります。</span><span class="sxs-lookup"><span data-stu-id="d7fda-125">In this situation, we have a single-determinant reference state, say, $\ket{\psi_{\rm{SCF}}}$.</span></span> <span data-ttu-id="d7fda-126">次に、参照状態に作用するユニタリ演算子を使用して、implicity の wavefunction の構成要素を指定します。</span><span class="sxs-lookup"><span data-stu-id="d7fda-126">The components of the unitary coupled-cluster wavefunction are then specified implicity through a unitary operator acting on a reference state.</span></span>
<span data-ttu-id="d7fda-127">このユニタリ演算子は、通常、$e ^ {T-T ^-dagger} $ として記述されます。ここで $T-T ^ \ ダガー $ は、Hermitian クラスター演算子です。</span><span class="sxs-lookup"><span data-stu-id="d7fda-127">This unitary operator is commonly written as $e^{T-T^\dagger}$, where $T-T^\dagger$ is the anti-Hermitian cluster operator.</span></span> <span data-ttu-id="d7fda-128">したがって、\begin{align} \ket{\psi_{\rm {UCC}}} = e ^ {T-T ^ \dagger}\ket{\psi_{\rm{SCF}}}.</span><span class="sxs-lookup"><span data-stu-id="d7fda-128">Thus \begin{align} \ket{\psi_{\rm {UCC}}} = e^{T-T^\dagger}\ket{\psi_{\rm{SCF}}}.</span></span>
<span data-ttu-id="d7fda-129">\end{align}</span><span class="sxs-lookup"><span data-stu-id="d7fda-129">\end{align}</span></span>

<span data-ttu-id="d7fda-130">また、クラスター演算子 $T = T_1 + T_2 + \ cドット $ を部分に分割することも一般的です。ここでは、各 $T 部分に $j $ body という用語が含まれています。</span><span class="sxs-lookup"><span data-stu-id="d7fda-130">It is also common to split the cluster operator $T = T_1 + T_2 + \cdots$ into parts, where each part $T_j$ contains $j$-body terms.</span></span> <span data-ttu-id="d7fda-131">一般化された結合クラスター理論では、1つの本体のクラスター演算子 (単一) は、\begin{align} T_1 = という形式になっています。 T ^ {p} _ {q} a ^ \dagger_p a_q, \end{align}</span><span class="sxs-lookup"><span data-stu-id="d7fda-131">In generalized coupled-cluster theory, the one-body cluster operator (singles) is of the form \begin{align} T_1 = \sum_{pq}t^{p}_{q} a^\dagger_p a_q, \end{align}</span></span>

<span data-ttu-id="d7fda-132">また、2つのボディを持つクラスター演算子 (double) は、\begin{align} T_2 =-sum} _ {rs} a ^ \dagger_p a ^ & daggera_r a_s という形式です。</span><span class="sxs-lookup"><span data-stu-id="d7fda-132">and two-body cluster operator (doubles) is of the form \begin{align} T_2 = \sum_{pqrs}t^{pq}_{rs} a^\dagger_p a^\dagger_q a_r a_s.</span></span>
<span data-ttu-id="d7fda-133">\end{align}</span><span class="sxs-lookup"><span data-stu-id="d7fda-133">\end{align}</span></span>

<span data-ttu-id="d7fda-134">高順序の用語 (3 要素、となど) は可能ですが、現在は化学ライブラリではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="d7fda-134">Higher-order terms (triples, quadruples, etc.) are possible, but not currently supported by the chemistry library.</span></span>

<span data-ttu-id="d7fda-135">たとえば、let $ \ket{\psi_{\rm{SCF}}} = a ^ & dagger_1 a ^ \dagger_2\ket{0}$、let $T = 0.123 a ^ a_1 + 0.456 a ^-dagger + a ^ a_1 a_2-0.789 a ^ dagger/3a ^ \dagger_2 a_1 a_0 $ のようにします。</span><span class="sxs-lookup"><span data-stu-id="d7fda-135">For example, let $\ket{\psi_{\rm{SCF}}} = a^\dagger_1 a^\dagger_2\ket{0}$, and let $T= 0.123 a^\dagger_0 a_1 + 0.456 a^\dagger_0a^\dagger_3 a_1 a_2 - 0.789 a^\dagger_3a^\dagger_2 a_1 a_0$.</span></span> <span data-ttu-id="d7fda-136">この状態は、次のように化学ライブラリでインスタンス化されます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-136">Then this state is instantiated in the chemistry library as follows.</span></span>
```csharp
// Create a list of indices of the creation operators
// for the single-reference state
var reference = new[] { 1, 2 };

// Create a list describing the cluster operator
// The first half of each list of integers will be
// associated with the creation operators, and
// the second half with the annihilation operators.
var clusterOperator = new[]
{
    (new [] {0, 1}, 0.123),
    (new [] {0, 3, 1, 2}, 0.456),
    (new [] {3, 2, 1, 0}, 0.789)
};

// Create a fermion wavefunction object that represents the 
// unitary coupled-cluster wavefunction. It is assumed implicity
// that the exponent of the unitary coupled-cluster operator
// is the cluster operator minus its Hermitian conjugate.
var wavefunction = new FermionWavefunction<int>(reference, clusterOperator);
```

<span data-ttu-id="d7fda-137">代わりに、整数のインデックスではなく `SpinOrbital` のインデックスを指定することによって、スピン convervation を明示的にすることができます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-137">Spin convervation may be made explicit by instead specifying `SpinOrbital` indices instead of integer indices.</span></span> <span data-ttu-id="d7fda-138">たとえば、let $ \ket{\psi_{\rm{SCF}}} = a ^ & d。 \uparrow} a ^ \uparrow} \downarrow}\ket{0}$、let $T = 0.123 a ^ & dagger、a_ {1、\uparrow} + 0.456 a ^-dagger、\uparrow} a ^-a_ {1, \uparrow} a_ {2, \ のようにして使用することができます。downarrow}-0.789 a ^ \uparrow}, \uparrow} a_ {1, \uparrow} a_ {0, \uparrow} $ be spin convserving. ($ {1, {0, $ be spin)</span><span class="sxs-lookup"><span data-stu-id="d7fda-138">For example, let $\ket{\psi_{\rm{SCF}}} = a^\dagger_{1,\uparrow} a^\dagger_{2, \downarrow}\ket{0}$, and let $T= 0.123 a^\dagger_{0, \uparrow} a_{1, \uparrow} + 0.456 a^\dagger_{0, \uparrow} a^\dagger_{3, \downarrow} a_{1, \uparrow} a_{2, \downarrow} - 0.789 a^\dagger_{3,\uparrow} a^\dagger_{2,\uparrow} a_{1,\uparrow} a_{0, \uparrow}$ be spin convserving.</span></span> <span data-ttu-id="d7fda-139">この状態は、次のように化学ライブラリでインスタンス化されます。</span><span class="sxs-lookup"><span data-stu-id="d7fda-139">Then this state is instantiated in the chemistry library as follows.</span></span>
```csharp
// Create a list of indices of the creation operators
// for the single-reference state
var reference = new[] { (1, Spin.u), (2, Spin.d) }.ToSpinOrbitals();

// Create a list describing the cluster operator
// The first half of each list of integers will be
// associated with the creation operators, and
// the second half with the annihilation operators.
var clusterOperator = new[]
{
    (new [] {(0, Spin.u), (1, Spin.u)}, 0.123),
    (new [] {(0, Spin.u), (3, Spin.d), (1, Spin.u), (2, Spin.d)}, 0.456),
    (new [] {(3, Spin.u), (2, Spin.u), (1, Spin.u), (0, Spin.u)}, 0.789)
}.Select(o => (o.Item1.ToSpinOrbitals(), o.Item2);

// Create a fermion wavefunction object that represents the 
// unitary coupled-cluster wavefunction. It is assumed implicity
// that the exponent of the unitary coupled-cluster operator
// is the cluster operator minus its Hermitian conjugate.
var wavefunctionSpinOrbital = new FermionWavefunction<SpinOrbital>(reference, clusterOperator);

// Convert the wavefunction indexed by spin-orbitals to one indexed
// by integers
var wavefunctionInteger = wavefunctionSpinOrbital.ToIndexing(IndexConvention.UpDown);
```

<span data-ttu-id="d7fda-140">また、会話クラスターのすべての操作を列挙する便利な関数も用意されています。この関数では、annihilate のみが使用されています。</span><span class="sxs-lookup"><span data-stu-id="d7fda-140">We also provide a convenience function that enumerates over all spin-conversing cluster operators that annihilate only occupied spin-orbitals and excite to only unoccupied spin-orbitals.</span></span>
```csharp
// Create a list of indices of the creation operators
// for the single-reference state
var reference = new[] { (1, Spin.u), (2, Spin.d) }.ToSpinOrbitals();

// Generate all spin-conversing excitations from spin-orbitals 
// occupied by the reference state to virtual orbitals.
var generatedExcitations = reference.CreateAllUCCSDSingletExcitations(nOrbitals: 3).Excitations;

// This is the list of expected spin-consvering excitations
var expectedExcitations = new[]
{
    new []{ (0, Spin.u), (1,Spin.u)},
    new []{ (2, Spin.u), (1,Spin.u)},
    new []{ (0, Spin.d), (2,Spin.d)},
    new []{ (1, Spin.d), (2,Spin.d)},
    new []{ (0, Spin.u), (0, Spin.d), (2, Spin.d), (1,Spin.u)},
    new []{ (0, Spin.u), (1, Spin.d), (2, Spin.d), (1,Spin.u)},
    new []{ (0, Spin.d), (2, Spin.u), (2, Spin.d), (1,Spin.u)},
    new []{ (1, Spin.d), (2, Spin.u), (2, Spin.d), (1,Spin.u)}
}.Select(o => new IndexOrderedSequence<SpinOrbital>(o.ToLadderSequence()));

// The following two assertions are true, and verify that the generated 
// excitations exactly match the expected excitations.
var bool0 = generatedExcitations.Keys.All(expectedExcitations.Contains);
var bool1 = generatedExcitations.Count() == expectedExcitations.Count();
```