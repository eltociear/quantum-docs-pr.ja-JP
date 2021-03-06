---
title: Quantum Katas の概要
description: Microsoft Quantum Development Kit (QDK) で提供される kata (トレーニング演習) について説明します。
author: bradben
ms.author: bradben
ms.date: 06/02/2020
ms.topic: overview
uid: microsoft.quantum.overview.katas
ms.openlocfilehash: 1c4dfa5c47aa38935cd5936cd256e357b6605371
ms.sourcegitcommit: 0181e7c9e98f9af30ea32d3cd8e7e5e30257a4dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85276214"
---
# <a name="learn-quantum-computing-with-the-quantum-katas"></a>Quantum Katas を使用して量子コンピューティングを学習する

[Quantum Katas](https://github.com/Microsoft/QuantumKatas/) は、量子コンピューティングと Q # プログラミングの要素を同時に学習することを目的とした、オープンソースのマイペースで進められるチュートリアルおよびプログラミング演習です。

## <a name="learning-by-doing"></a>実践的学習

このプロジェクトで収集したチュートリアルと演習では、非常にシンプルな内容から非常に難しい内容に移行していく特定のトピックを網羅したプログラミング タスクを用意し、これを実践して学習する方法にウェイトを置いています。 各タスクでは、何らかのコードを入力することが求められます。最初のタスクに必要なのは 1 行だけかもしれませんが、その後のタスクではかなりのコード フラグメントが必要になる場合があります。

最も重要な点として、katas には、タスクに対するソリューションを設定、実行、および検証するテスト フレームワークが含まれています。 これにより、ご自分のソリューションに関するフィードバックをすぐに得ることができ、間違っている場合にはご自分のアプローチを再検討することができます。

katas を使用すれば任意の環境で学習することができます。

* Binder 環境内でオンラインになっている Jupyter Notebook
* ローカル コンピューターで実行されている Jupyter Notebook
* Visual Studio
* Visual Studio Code

## <a name="what-can-i-learn-with-the-quantum-katas"></a>Quantum Katas を使用して学習できることは何ですか?

量子コンピューティングの基礎を知り、量子アルゴリズムとプロトコルについて詳しく理解します。 量子コンピューティングの基本的な概念をしっかりと確実に把握するために、最初にこのラーニングパスに従うことをお勧めします。 もちろん、複雑な算術演算など、使い慣れたトピックをスキップし、好きな順序でアルゴリズムを学習することができます。

### <a name="introduction-to-quantum-computing-concepts"></a>量子コンピューティングの概念について

| Kata | 説明 |
|:-----|-------------|
|[複雑な算術演算](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/ComplexArithmetic)|このチュートリアルでは、量子コンピューティングを使用するために必要な数学的な一部の背景 (虚数、複素数など) について説明します。|
|[線形代数](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/LinearAlgebra)|線形代数は、量子コンピューティングで量子の状態や操作を表すために使用されます。 このチュートリアルでは、マトリックスとベクターを含む基本について説明します。|
|[量子ビットの概念](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/Qubit)|量子コンピューティングの主要な概念の 1 つである量子ビットについて説明します。 |
|[単一量子ビットの量子ゲート](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/SingleQubitGates)|このチュートリアルでは、量子アルゴリズムの構成要素として機能し、さまざまな方法でクォンタムの量子ビットの状態を変換する単一量子ビットの量子ゲートを紹介します。|
|[マルチ量子システム](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/MultiQubitSystems)|このチュートリアルでは、マルチ量子システム、数学表記と Q# コードでのその表現、およびもつれの概念について説明します。|
|[マルチ量子ビットの量子ゲート](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/MultiQubitGates)|このチュートリアルでは、「[単一量子ビットの量子ゲート](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/SingleQubitGates)」チュートリアルに従っており、マルチ量子ビット システムに量子ゲートを適用することに重点を置いています。|

### <a name="quantum-computing-fundamentals"></a>量子コンピューティングの基礎

| Kata | 説明 |
|:-----|-------------|
|[量子ゲートの認識](https://github.com/microsoft/QuantumKatas/tree/master/BasicGates)|Q# での基本的な量子ゲートについて理解を深めるために設計された一連の演習です。 基本的な単一量子ビットおよびマルチ量子ビット ゲート、adjoint ゲートと制御されたゲートに関する演習が含まれ、ゲートを使用して量子ビットの状態を変更する方法を学習します。|
|[量子重ね合わせの作成](https://github.com/microsoft/QuantumKatas/tree/master/Superposition)|Q# での重ね合わせとプログラミングの概念を理解するための演習が含まれています。 基本的な単一量子ビットおよびマルチ量子ビット ゲート、重ね合わせ、および Q# でのフロー制御と再帰に関する演習が含まれています。|
|[測定を使用した量子の状態の識別](https://github.com/microsoft/QuantumKatas/tree/master/Measurements)|演習を解いて、量子測定と直交状態および非直交状態について学びます。 |
|[共同測定](https://github.com/microsoft/QuantumKatas/tree/master/JointMeasurements)|共同パリティ測定について、および[測定](xref:microsoft.quantum.intrinsic.measure)操作を使用して量子の状態を区別する方法について説明します。|

### <a name="algorithms"></a>アルゴリズム

| Kata | 説明 |
|:-----|-------------|
|[量子テレポーテーション](https://github.com/microsoft/QuantumKatas/tree/master/Teleportation)|この kata では、従来型の通信と以前に共有された量子のもつれのみを使用して、量子の状態を伝達できるようにするプロトコルである量子テレポーテーションについて説明します。|
|[超密度符号化](https://github.com/microsoft/QuantumKatas/tree/master/SuperdenseCoding)|超密度符号化は、以前に共有されていた量子のもつれを使用して 1 つの量子ビットのみを送信することによって、2 ビットの従来の情報を送信できるようにするプロトコルです。  |
|[Deutsch–Jozsa アルゴリズム](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/ExploringDeutschJozsaAlgorithm)|このアルゴリズムは、従来の決定論的アルゴリズムよりも指数関数的に高速な量子アルゴリズムの最初の例の 1 つとして有名です。|
|[グローバーの検索アルゴリズムの上位レベルのプロパティを探索](https://github.com/microsoft/QuantumKatas/tree/master/tutorials/ExploringGroversAlgorithm)|量子コンピューティングにおいて最も有名なアルゴリズムの 1 つについて詳しく説明します。 特定の出力が生成されるブラック ボックス (くじ) への入力を見つける問題を解きます。 |
|[グローバーの検索アルゴリズムの実装](https://github.com/microsoft/QuantumKatas/tree/master/GroversAlgorithm)|この kata では、グローバーの検索アルゴリズムを詳しく説明し、おみくじの作成方法を紹介し、アルゴリズムの手順を実行して、最終的にすべてをまとめています。|
|[グローバーのアルゴリズムを使用した実際の問題を解く: SAT の問題](https://github.com/microsoft/QuantumKatas/tree/master/SolveSATWithGrover)|[充足可能性問題](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem) (SAT) を例として使用して、グローバーのアルゴリズムを使って実際の問題を解く一連の演習です。  |
|[グローバーのアルゴリズムを使用した実際の問題を解く: グラフの色分けの問題](https://github.com/microsoft/QuantumKatas/tree/master/GraphColoring)| この kata では、グローバーのアルゴリズムをさらに詳しく説明し、例としてグラフの色分けの問題を使用して[制約充足問題](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem)を解きます。 |

### <a name="protocols-and-libraries"></a>プロトコルとライブラリ

| Kata | 説明 |
|:-----|-------------|
|[量子キー配布用の BB84 プロトコル](https://github.com/microsoft/QuantumKatas/tree/master/KeyDistribution_BB84)|量子キーを使用して暗号化キーを交換する、量子キー配布プロトコル [BB84](https://en.wikipedia.org/wiki/BB84) について学習し、これを実装します。 |
|[ビット反転エラー訂正コード](https://github.com/microsoft/QuantumKatas/tree/master/QEC_BitFlipCode)|量子エラー訂正 (QEC) の最も単純なコード、3 量子ビットのビット反転コードを使用して、量子エラー訂正について説明します。|
|[位相推定](https://github.com/microsoft/QuantumKatas/blob/master/PhaseEstimation)|位相推定アルゴリズムは、量子コンピューティングの最も基本的な構成要素の一部です。 量子位相推定を扱ったこれらの演習を使用して、位相推定について、および Q# で位相推定ルーチンを準備して実行する方法を説明します。|
|[量子の算術: リップルキャリー加算器](https://github.com/microsoft/QuantumKatas/blob/master/RippleCarryAdder)|量子コンピューターでの[リップルキャリー](https://en.wikipedia.org/wiki/Adder_(electronics)#Ripple-carry_adder)加算について説明する一連の解説演習です。 埋め込みの量子加算器を作成し、別のアルゴリズムを使ってそこに展開して、最後に、埋め込みの量子減算器を作成します。   |

### <a name="entanglement-games"></a>もつれゲーム

| Kata | 説明 |
|:-----|-------------|
|[CHSH ゲーム](https://github.com/microsoft/QuantumKatas/tree/master/CHSHGame)|[CHSH](https://en.wikipedia.org/wiki/CHSH_inequality) ゲームの実装を使用して、量子のもつれを確認します。 この[非ローカル](https://en.wikipedia.org/wiki/Quantum_refereed_game)のゲームでは、量子のもつれをどのように使用して、純粋な従来の戦略では実現できなかったプレーヤーが勝つチャンスを増やすことができるかを示します。|
|[GHZ ゲーム](https://github.com/microsoft/QuantumKatas/tree/master/GHZGame)|GHZ ゲームも非ローカルのゲームですが、プレーヤーは 3 人です。|
|[Mermin-Peres 魔方陣ゲーム](https://github.com/microsoft/QuantumKatas/tree/master/MagicSquareGame)|一連の演習により[量子擬似テレパシー](https://en.wikipedia.org/wiki/Quantum_pseudo-telepathy#The_Mermin%E2%80%93Peres_magic_square_game)を理解して、魔方陣ゲームを解きます。  |

## <a name="resources"></a>リソース

[Quantum Katas](https://github.com/microsoft/QuantumKatas) の全シリーズを参照

[kata のオンライン実行](https://aka.ms/try-quantum-katas)
