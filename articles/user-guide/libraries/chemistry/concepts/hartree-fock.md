---
title: ハーツリー-Fock 理論
description: 量子システムの初期状態を構築する簡単な方法である、Fock 理論について説明します。
author: nathanwiebe2
ms.author: nawiebe@microsoft.com
ms.date: 10/09/2017
ms.topic: article-type-from-white-list
uid: microsoft.quantum.chemistry.concepts.hartreefock
ms.openlocfilehash: 6fa63cbe13fe98565ffb42b56f3ade86720cedb3
ms.sourcegitcommit: 0181e7c9e98f9af30ea32d3cd8e7e5e30257a4dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85275944"
---
# <a name="hartreefock-theory"></a><span data-ttu-id="e29a2-103">ハーツリー– Fock 理論</span><span class="sxs-lookup"><span data-stu-id="e29a2-103">Hartree–Fock Theory</span></span>

<span data-ttu-id="e29a2-104">おそらく、量子化学シミュレーションの最も重要な数量は、Hamiltonian 行列の最低エネルギー eigenvector であるグラウンド州です。</span><span class="sxs-lookup"><span data-stu-id="e29a2-104">Perhaps the most important quantity in quantum chemistry simulation is the ground state, which is the minimum energy eigenvector of the Hamiltonian matrix.</span></span>
<span data-ttu-id="e29a2-105">これは、反応率などのほとんどの分子の温度の量は、反力のある経路でのステップの開始と終了を示すクォンタムの状態と、その中間状態が通常はグラウンドの状態であることが多いためです。</span><span class="sxs-lookup"><span data-stu-id="e29a2-105">This is because for most molecules at room temperature quantities such as reaction rates are dominated by free energy differences between quantum states that describe the beginning and end of a step in a reaction pathway and at room temperature such intermediate state are usually ground states.</span></span>
<span data-ttu-id="e29a2-106">通常、グラウンドの状態は、急激に多くの構成を分散しているため、(quantum コンピューターの場合でも) 学習するのは困難です。</span><span class="sxs-lookup"><span data-stu-id="e29a2-106">While the ground state is typically too hard to learn (even with a quantum computer) because it is a distribution over an exponentially large number of configurations.</span></span>
<span data-ttu-id="e29a2-107">グラウンドステートエネルギーなどの数量を学習できます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-107">Quantities such as ground state energy can be learned.</span></span>
<span data-ttu-id="e29a2-108">たとえば、$ \ket{\psi} $ が純粋なクォンタムの状態である場合、システムがその状態にある平均エネルギーを、\ begin{\hat{H}} E = \ ロウ {/psi} \ket{\psi} に渡します。</span><span class="sxs-lookup"><span data-stu-id="e29a2-108">For example, if $\ket{\psi}$ is any pure quantum state then \begin{equation} E = \bra{ \psi } \hat{H} \ket{\psi} \end{equation} gives the mean energy that the system has in that state.</span></span>
<span data-ttu-id="e29a2-109">その後、グラウンドの状態は、そのような最小値を示す状態になります。</span><span class="sxs-lookup"><span data-stu-id="e29a2-109">The ground state then is the state that gives the smallest such value.</span></span> <span data-ttu-id="e29a2-110">結果として、実際の状態にできるだけ近い状態を選択することは、エネルギーを直接 (可変の eigensolvers で行っているように)、またはフェーズの推定を通じて直接予測するために非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="e29a2-110">As a result, choosing a state that is as close as possible to the true ground state is vitally important for estimating the energy either directly (as is done in variational eigensolvers) or through phase estimation.</span></span>

<span data-ttu-id="e29a2-111">[ハー] ツリー– Fock 理論では、クォンタムシステムの初期状態を簡単に構築できます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-111">Hartree–Fock theory gives a simple way to construct the initial state for quantum systems.</span></span> <span data-ttu-id="e29a2-112">これにより、量子システムのグラウンドの状態に対して、1対後の決定を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-112">It yields a single Slater-determinant approximation to the ground state of a quantum system.</span></span> <span data-ttu-id="e29a2-113">最終的には、Fock 内で、地表のエネルギーを最小にする回転が検出されます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-113">To that end, it finds a rotation within Fock-space that minimizes the ground state energy.</span></span> <span data-ttu-id="e29a2-114">特に、$N $ 原子のシステムの場合、メソッドは prod_ ローテーションを実行します。 \ket {j = 0} ^ {N-1} a ^ \ dagger_j/ {0} prod_ map {j = 0} ^ {N-1} e ^ {u} a ^ dagger_j e ^ {-u} \ket {0} \defeq\ prod_ {j = 0} ^ {N-1} \widetilde{a} ^ \ dagger_j \Ket {0} 、Hermitian を使用して、(つまり、$u =-u ^ \ ダガー $) マトリックス $u = \ sum_ {pq} u_ {pq} a ^ \ dagger_p a_q $。</span><span class="sxs-lookup"><span data-stu-id="e29a2-114">In particular, for a system of $N$ electrons the method performs the rotation \begin{equation} \prod_{j=0}^{N-1} a^\dagger_j \ket{0} \mapsto \prod_{j=0}^{N-1} e^{u} a^\dagger_j e^{-u} \ket{0}\defeq\prod_{j=0}^{N-1}  \widetilde{a}^\dagger_j  \ket{0}, \end{equation} with an anti-Hermitian (i.e. $u= -u^\dagger$) matrix $u = \sum_{pq} u_{pq} a^\dagger_p a_q$.</span></span> <span data-ttu-id="e29a2-115">マトリックス $u $ は回転ローテーションを表し、$ \widetilde{a} ^ \ dagger_j $ と $ \widetilde{a} _j $ は、を使用する原子の作成および annihilation 演算子を表していることに注意してください– Fock 分子。</span><span class="sxs-lookup"><span data-stu-id="e29a2-115">It should be noted that the matrix $u$ represents the orbital rotations and $\widetilde{a}^\dagger_j$ and $\widetilde{a}_j$ represent creation and annihilation operators for electrons occupying Hartree–Fock molecular spin-orbitals.</span></span>


<span data-ttu-id="e29a2-116">次に、$ $u $ は、予測エネルギー $ \bra {0} \ prod_ {j = 0} ^ {N-1} \widetilde{a} \_ j \_ /製品 {k = 0} ^ {N-1} \widetilde{a} ^ \ dagger_k \ket $ を最小化するように最適化されてい {0} ます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-116">The matrix $u$ is then optimized to minimize the expected energy $\bra{0} \prod_{j=0}^{N-1}  \widetilde{a}\_j  H \prod\_{k=0}^{N-1}  \widetilde{a}^\dagger_k\ket{0}$.</span></span> <span data-ttu-id="e29a2-117">このような最適化の問題は一般的には困難ですが、実際には、Fock アルゴリズムは、特に均衡ジオメトリの閉じたシェルの分子の最適化の問題に対して、ほぼ最適なソリューションに迅速に収束する傾向があります。</span><span class="sxs-lookup"><span data-stu-id="e29a2-117">While such optimization problems may be generically hard, in practice the Hartree–Fock algorithm tends to rapidly converge to a near-optimal solution to the optimization problem, especially for closed-shell molecules in the equilibrium geometries.</span></span> <span data-ttu-id="e29a2-118">これらの状態は、オブジェクトのインスタンスとして指定でき `FermionWavefunction` ます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-118">We may specify these states as an instance of the `FermionWavefunction` object.</span></span> <span data-ttu-id="e29a2-119">たとえば、$a ^ \ dagger_ ^ \ dagger_ a ^ \ dagger_ \ket $ の状態は、次のように {1} {2} {6} {0} 化学ライブラリでインスタンス化されます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-119">For instance, the state $a^\dagger_{1}a^\dagger_{2}a^\dagger_{6}\ket{0}$ is instantiated in the chemistry library as follows.</span></span>
```csharp
// Create a list of integer indices of the creation operators
var indices = new[] { 1, 2, 6 };

// Convert the list of indices to a `FermionWavefunction` object.
// In this case, the indices are integers, so we use the `int`
// type specialization.
var wavefunction = new FermionWavefunction<int>(indices);
```
<span data-ttu-id="e29a2-120">また、インデックスを使用して wave 関数のインデックスを作成し、次のように `SpinOrbital` これらのインデックスを整数に変換することもできます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-120">It is also possible to index wave functions with `SpinOrbital` indices, and then convert these indices to integers as follows.</span></span>
```csharp
// Create a list of spin orbital indices of the creation operators
var indices = new[] { (0, Spin.d), (1,Spin.u), (3, Spin.u) };

// Convert the list of indices to a `FermionWavefunction` object.
var wavefunctionSpinOrbital = new FermionWavefunction<SpinOrbital>(indices.ToSpinOrbitals());

// Convert a wavefunction indexed by spin orbitals to
// one indexed by integers
var wavefunctionInt = wavefunctionSpinOrbital.ToIndexing(IndexConvention.UpDown);
```

<span data-ttu-id="e29a2-121">Fock 理論に関する最も印象的な機能は、原子の間に entangを持たないクォンタム状態を生成することです。</span><span class="sxs-lookup"><span data-stu-id="e29a2-121">The most striking feature about Hartree–Fock theory is that it yields a quantum state that has no entanglement between the electrons.</span></span>
<span data-ttu-id="e29a2-122">これは、多くの場合、分子 systems のプロパティに関する適切な定性的な説明を提供することを意味します。</span><span class="sxs-lookup"><span data-stu-id="e29a2-122">This means that it often provides a suitable qualitative description of properties of molecular systems.</span></span> 

<span data-ttu-id="e29a2-123">次のように、Fock 状態をから再構築することもでき `FermionHamiltonian` ます。</span><span class="sxs-lookup"><span data-stu-id="e29a2-123">The Hartree-Fock state may also be reconstructed from a `FermionHamiltonian`  as follows.</span></span>
```csharp
// We initialize a fermion Hamiltonian.
var fermionHamiltonian = new FermionHamiltonian();

// Create a Hartree-Fock state from the Hamiltonian 
// with, say, `4` occupied spin orbitals.
var wavefunction = fermionHamiltonian.CreateHartreeFockState(nElectrons: 4);
```

<span data-ttu-id="e29a2-124">ただし、厳密に相関されたシステムの場合は特に、正確な結果を取得するために、Fock 理論を超える量子状態が発生するようにします。</span><span class="sxs-lookup"><span data-stu-id="e29a2-124">However, obtaining accurate results, especially for strongly correlated systems, necessitate quantum states that go beyond Hartree–Fock theory.</span></span>