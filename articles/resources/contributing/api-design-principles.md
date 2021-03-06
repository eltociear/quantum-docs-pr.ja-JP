---
title: 'Q # API 設計の原則'
description: 'Q # API 設計の原則'
author: cgranade
ms.author: chgranad
ms.date: 3/9/2020
ms.topic: article
uid: microsoft.quantum.contributing.api-design
ms.openlocfilehash: def6a9f12accfa399fd4db3783b9899fc743f025
ms.sourcegitcommit: 0181e7c9e98f9af30ea32d3cd8e7e5e30257a4dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85275495"
---
# <a name="q-api-design-principles"></a>Q # API 設計の原則

## <a name="introduction"></a>概要

言語およびプラットフォームとして、ユーザーは、クォンタムアプリケーションの記述、実行、理解、調査を行うことができます。
ユーザーを支援するために、Q # ライブラリを設計する際には、一連の API 設計原則に従って設計を進め、quantum 開発コミュニティで使用可能なライブラリを作成できるようにします。
この記事では、これらの原則について説明し、Q # Api を設計するときに適用する方法を示す例を示します。

> [!TIP]
> これは、ライブラリの開発と詳細なライブラリの投稿をガイドするための、非常に詳細なドキュメントです。
> Q # で独自のライブラリを作成している場合や、 [q # ライブラリリポジトリ](https://github.com/microsoft/QuantumLibraries)に大きな機能を提供している場合は、最も役に立つでしょう。
>
> 一方、Quantum 開発キットに投稿する方法については、後で説明することをお[勧めします。](xref:microsoft.quantum.contributing)
> Q # コードを書式設定する方法についての一般的な情報を探している場合は、[スタイルガイド](xref:microsoft.quantum.contributing.style)を確認することをお勧めします。

## <a name="general-principles"></a>一般原則

**主要原則:** クォンタムアプリケーションに重点を置いた Api を公開します。

- ✅アルゴリズムとアプリケーションの大まかな構造を反映する操作名と関数名を選択して**ください**。
- ⛔️は、主に低レベルの実装の詳細に焦点を当てた Api を公開し**ません**。

**主要原則:** 各 API の設計をサンプルのユースケースで開始し、Api を直感的に使用できるようにします。

- ✅パブリック API の各コンポーネントに、対応するユースケースがあることを確認してください。開始から使用できるすべてのを設計する必要はあり**ません**。
    別の方法として、公開されている Api は役に立たないようにしてください。ただし、API の各部分には、役に立つ*具体的*な例が含まれていることを確認してください。

  *例:*
  - @"microsoft.quantum.canon.applytoeachca"をとして使用することで `ApplyToEachCA(H, _)` 、多くのクォンタムアルゴリズムで共通のタスクである uniform 法則状態のレジスタを準備できます。 同じ操作を、準備、数値、および oracle ベースのアルゴリズムの他の多くのタスクにも使用できます。

- ✅ブレーンストーミングとワークショップの新しい API 設計を**行っ**て、直感的で、提案されたユースケースに適合することを再度確認します。

  *例:*
  - 現在の Q \# コードを調べて、新しい API 設計によって既存の実装がどのように簡略化され、明確になるかを確認します。
  - 主要ユーザーの代表者として提示された API 設計を確認します。

**主要原則:** 読み取り可能なコードをサポートし、奨励するように Api を設計します。

- ✅ドメインの専門家と専門家以外の人がコードを読み**取れるようにしてください**。
- ✅**必要に**応じて実装の詳細について詳しく説明するために、上位レベルのアルゴリズム内で各操作と関数の効果に重点を置きます。
- ✅該当する場合は、一般的な[Q \# スタイルガイド](xref:microsoft.quantum.contributing.style)に従って**ください**。

**主要原則:** 安定した Api を設計し、上位互換性を提供します。

- ✅互換性に影響する変更が必要な場合は、古い Api を適切に廃止して**ください**。

- ✅廃止時に既存のユーザーコードが正しく動作するようにする "shim" 操作と関数**を提供し**ます。

  *例:*
  - に呼び出された操作の名前をに変更する場合は `EstimateExpectation` `EstimateAverage` 、 `EstimateExpectation` 既存のコードが引き続き正常に動作するように、新しい名前で元の操作を呼び出すという新しい操作を導入します。

- ✅属性**を使用し** @"microsoft.quantum.core.deprecated" て、廃止をユーザーに通知します。

- ✅操作または関数の名前を変更する**場合は、** 新しい名前をへの文字列入力として指定 `@Deprecated` します。

- プレビューリリースの場合は少なくとも6か月以上、サポートされているリリースでは少なくとも2年間は、既存の関数または操作を削除し**ない**ように⛔️します。

## <a name="functions-and-operations"></a>関数と操作

**重要な原則:** すべての関数と操作が API 内で明確に定義された1つの目的を持っていることを確認します。

- ⛔️は、関連のない複数のタスクを実行する関数や操作を公開し**ません**。

**重要な原則:** 可能な限り再利用できるように、関数と操作を設計し、将来のニーズを予測します。

- ✅同じ API と以前に存在していたライブラリの両方で、他の関数や操作との連携を構成するために、関数と操作**を設計し**ます。

  *例:*
  - この操作では、 @"microsoft.quantum.canon.delay" 入力に関して最小限の仮定が行われるため、Q # 標準ライブラリ全体またはユーザーによる定義に従って、いずれかの操作のアプリケーションを遅延させることができます。
    <!-- TODO: define bad example. -->

- ✅純粋に確定的なクラシックロジックを操作ではなく関数とし**て公開し**ます。

  *例:*
  - 浮動小数点の入力をランダムに記述できるサブルーチンで、操作としてではなく、ユーザーに公開する必要があり `Squared : Double -> Double` `Square : Double => Double` ます。 これにより、サブルーチンをより多くの場所 (たとえば、他の関数の内部) で呼び出すことができ、パフォーマンスと最適化に影響を与える有用な最適化情報がコンパイラに提供されます。
  - `ForEach<'TInput, 'TOutput>('TInput => 'TOutput, 'TInput[]) => 'TOutput[]`とは `Mapped<'TInput, 'TOutput>('TInput -> 'TOutput, 'TInput[]) -> 'TOutput[]` 、決定性に関して行われる保証とは異なります。どちらも、状況によって異なる場合があります。
  - クォンタム操作のアプリケーションを変換する API ルーチンは、決定的な方法で実行されることが多く、そのため、などの関数として使用できるようになり `CControlled<'T>(op : 'T => Unit) => ((Bool, 'T) => Unit)` ます。

- ✅必要に応じて型パラメーターを使用して、各関数および操作に対して適切な入力型を一般化して**ください**。

  *例:*
  - `ApplyToEach`は `<'T>(('T => Unit), 'T[]) => Unit` 、最も一般的なアプリケーションの特定の型ではなく、型 `((Qubit => Unit), Qubit[]) => Unit` です。

> [!TIP]
> 将来のニーズを予測することが重要ですが、ユーザーの具体的な問題を解決することも重要です。
> この重要な原則に基づいて行動することは、Api の開発を避けるために、常に慎重に検討してバランスを行う必要があります。

**重要な原則:** 予測可能な関数と操作の入力と出力の種類を選択し、呼び出し可能な目的を伝えます。

- ✅タプル型**を使用し**て、結合された入力と出力を論理的にグループ化します。 このような場合は、ユーザー定義型を使用することを検討してください。

  *例:*
  - 別の関数のローカル最小を出力する関数は、適切なシグネチャになる可能性のある、検索間隔を入力として受け取る必要がある場合があり `LocalMinima(fn : (Double -> Double), (left : Double, right : Double)) : Double` ます。
  - パラメーターシフト手法を使用して機械学習分類子の派生物を推定する操作では、シフトとシフト解除の両方のパラメーターベクトルを入力として取得する必要がある場合があります。 この場合、に似た入力が `(unshifted : Double[], shifted : Double[])` 適している可能性があります。

- ✅入力と出力の組の項目を、さまざまな関数や操作にわたって一貫し**て並べ替えます**。

  *例:*
  - 2つの関数または関数、またはそれぞれが回転角度とターゲット qubit を入力として使用することを検討している場合は、各入力タプルの順序が同じであることを確認します。 つまり、と `ApplyRotation(angle : Double, target : Qubit) : Unit is Adj + Ctl` を優先 `DelayedRotation(angle : Double, target : Qubit) : (Unit => Unit is Adj + Ctl)` し `ApplyRotation(target : Qubit, angle : Double) : Unit is Adj + Ctl` `DelayedRotation(angle : Double, target : Qubit) : (Unit => Unit is Adj + Ctl)` ます。

**重要な原則:** 部分アプリケーションなどの Q 言語機能で適切に動作するように関数と操作を設計し \# ます。

- ✅最も一般的に適用される入力が最初に発生するように、入力タプル内の項目**を並べ替えます**(つまり、部分的なアプリケーションがカリー化と同様に動作するようにします)。

  *例:*
  - 入力 `ApplyRotation` として浮動小数点数と qubit を受け取る演算は、通常、型の入力を期待する操作で使用するために、浮動小数点の入力と共に部分的に適用されることがあり `Qubit => Unit` ます。 そのため、`operation ApplyRotation(angle : Double, target : Qubit) : Unit is Adj + Ctl`
      部分的なアプリケーションで最も一貫して動作します。
  - 通常、このガイダンスでは、入力タプル内のすべてのすべての古典データを、入力タプルのすべての qubits の前に配置しますが、実際の API の呼び出し方法については、適切な判断を行います。

## <a name="user-defined-types"></a>ユーザー定義型

**重要な原則:** ユーザー定義型を使用すると、api の表現性と利便性を高めることができます。

- ✅新しいユーザー定義型**を導入し**て、長い型や複雑な型に便利なショートハンドを提供します。

  *例:*
  - 通常、3つの qubit 配列入力を持つ演算型を入力として取得したり、出力として返したりする場合は、次のような UDT を指定します。`newtype TimeDependentBlockEncoding = ((Qubit[], Qubit[], Qubit[]) => Unit is Adj + Ctl)`
      は、便利なショートハンドを提供するのに役立ちます。

- ✅特定の基本型を使用する必要があることを示すために、新しいユーザー定義型**を導入する**ことをお勧めします。

  *例:*
  - 特に、古典的なデータをクォンタムレジスタにエンコードする操作として解釈する必要がある操作は、ユーザー定義型でラベル付けすることをお勧めし `newtype InputEncoder = (Apply : (Qubit[] => Unit))` ます。

- ✅将来の拡張が可能な名前付きの項目を持つ新しいユーザー定義型**を導入し**ます (たとえば、後で追加の名前付き項目を含む可能性のある結果構造)。

  *例:*
  - 操作に `TrainModel` よって多数の構成オプションが公開されている場合、これらのオプションを新しい udt として公開 `TrainingOptions` し、新しい関数を提供 `DefaultTrainingOptions : Unit -> TrainingOptions` することで、ユーザーは TrainingOptions udt 値内の特定の名前付き項目をオーバーライドできます。さらに、ライブラリ開発者は、必要に応じて新しい udt 項目を追加できます。

- ✅新しいユーザー定義型の名前付き項目は、ユーザーが正しい組分解を知る必要があるように、優先的**に宣言し**ます。

  *例:*
  - 極分解で複素数を表す場合は、を優先 `newtype ComplexPolar = (Magnitude: Double, Argument: Double)` `newtype ComplexPolar = (Double, Double)` します。

**重要な原則:** ユーザー定義型を使用すると、認知の負荷が軽減され、ユーザーが追加の概念や用語を習得する必要がありません。

- ⛔️**ラップ**解除演算子 () を頻繁に使用する必要があるユーザー定義型を導入し `!` たり、通常は複数レベルのラップ解除が必要になることがあります。 次のような軽減策が考えられます。

  - 1つの項目を持つユーザー定義型を公開する場合は、その項目の名前を定義することを検討してください。 たとえば、「」を使用することを検討してください `newtype Encoder = (Apply : (Qubit[] => Unit is Adj + Ctl))` `newtype Encoder = (Qubit[] => Unit is Adj + Ctl)` 。

  - 他の関数および操作が "ラップされた" UDT インスタンスを直接受け入れることを保証する。

- ⛔️には、追加の表現力を提供せずに組み込み型を複製する新しいユーザー定義型は導入し**ません**。

  *例:*
  - UDT は `newtype QubitRegister = Qubit[]` 追加の表現力を提供 `Qubit[]` しないため、はっきり特典なしで使用するのは困難です。
  - UDT は、 `newtype LittleEndian = Qubit[]` 基になるレジスタがどのように使用および解釈されるかを文書にし、その基本型に対してさらに表現力を提供します。

- 厳密に要求されていない限り、⛔️アクセサー関数は導入し**ません**。  この場合は、名前付きの項目を強くお勧めします。

  *例:*
  - UDT を導入するときは `newtype Complex = (Double, Double)` 、関数とを導入するように定義をに変更することをお勧めし `newtype Complex = (Real : Double, Imag : Double)` `GetReal : Complex -> Double` `GetImag : Complex -> Double` ます。

## <a name="namespaces-and-organization"></a>名前空間と組織

**重要な原則:** それぞれの名前空間で、関数、操作、およびユーザー定義型の目的を明確に伝えることができる、予測可能な名前空間の名前を選択します。

- ✅**名前空間**をとして指定 `Publisher.Product.DomainArea` します。

  *例:*
  - Quantum 開発キットの quantum シミュレーション機能の一部として Microsoft が発行した関数、操作、および Udt は、名前空間に配置され `Microsoft.Quantum.Simulation` ます。
  - `Microsoft.Quantum.Math`数学ドメイン領域に関連する Quantum 開発キットの一部として Microsoft によって発行された名前空間を表します。

- ✅特定の機能に使用される操作、関数、およびユーザー定義型を名前空間に配置して、その機能が異なる問題ドメイン間で使用されている**場合でも**、その機能を説明する名前空間に配置します。

  *例:*
  - Quantum 開発キットの一部として Microsoft が発行した状態準備 Api は、に配置さ `Microsoft.Quantum.Preparation` れます。
  - Quantum 開発キットの一部として Microsoft が発行したクォンタムシミュレーション Api は、に配置さ `Microsoft.Quantum.Simulation` れます。

- ✅操作、関数、およびユーザー定義型を、特定のドメイン内でのみ使用される名前空間**に配置し**て、ユーティリティのドメインを示します。 必要に応じて、副名前空間を使用して、各ドメイン固有の名前空間内のフォーカスされたタスクを指定します。

  *例:*
  - Microsoft によって発行されたクォンタム機械学習ライブラリは、主に名前空間に配置され @"microsoft.quantum.machinelearning" ますが、データセットの例は名前空間によって提供され @"microsoft.quantum.machinelearning.datasets" ます。
  - Quantum 開発キットの一部として Microsoft によって発行された量子化学 Api は、に配置する必要があり `Microsoft.Quantum.Chemistry` ます。 ヨルダン--Wigner 分解の実装に固有の機能がに配置されている場合があり `Microsoft.Quantum.Chemistry.JordanWigner` ます。そのため、量子化学のドメイン領域の主要インターフェイスは実装に関係しません。

**主要原則:** 名前空間とアクセス修飾子を一緒に使用して、ユーザーに公開されている API サーフェイスに関する意図的なものにし、Api の実装とテストに関連する内部の詳細を非表示にします。

- ✅必要に応じて、API を実装するために必要なすべての関数と操作を、実装されている API と同じ名前空間**に配置し**ますが、"private" または "internal" キーワードでマークして、ライブラリのパブリック API サーフェイスの一部ではないことを示します。 アンダースコア () で始まる名前を使用して、 `_` プライベートおよび内部の操作と関数をパブリック呼び出しができるかを視覚的に区別します。

  *例:*
  - 操作名は、 `_Features` 特定の名前空間とアセンブリに対してプライベートであり、キーワードを使用する必要がある関数を示し `internal` ます。

- ✅特定の名前空間の API を実装するために多数のプライベート関数または操作が必要な場合**は、実装**されて終了する名前空間に一致する新しい名前空間にそれらを配置することがまれに `.Private` あります。

- ✅すべての単体テスト**は**、テスト対象の名前空間に一致する名前空間に配置し、で終了 `.Tests` します。

## <a name="naming-conventions-and-vocabulary"></a>名前付け規則とボキャブラリ

**主要原則:** さまざまな対象ユーザー (クォンタム初心者と専門家の両方を含む) で、明確で、アクセス可能で、読みやすい名前と用語を選択します。

- 差別的なまたは exclusionary 識別子の名前を使用したり、API ドキュメントのコメントに用語を使用したりすることは⛔️**ません**。

- ✅API ドキュメントコメントを使用して、関連するコンテキスト、例、参照を提供します。特に、より困難な概念につい**ては、** こちらを参照してください。

- ⛔️不要な識別子名を使用し**ない**でください。または、大量のクォンタムアルゴリズムの知識が必要です。

  *例:*
  - "振幅増幅の反復" を "Grover iteration" に優先します。

- ✅実装ではなく、呼び出し可能なの意図された効果を明確に伝える操作と関数の名前**を選択し**ます。 実装は[API ドキュメントコメント](xref:microsoft.quantum.guide.filestructure#documentation-comments)に記載されていることに注意してください。

  *例:*
  - 後者がどのように実装されているかを通知するため、"Hadamard test" に "推定重複" を優先します。

- ✅すべての Q api で、**一貫した**方法で単語を使用し \# ます。

  - **助動詞**

    - **アサート**: ターゲットコンピューターとその qubits の状態に関する想定が、物理リソースを使用していない可能性があるかどうかを確認します。 この動詞を使用する操作は、ライブラリや実行可能プログラムの機能に影響を与えずに、常に安全な状態にしておく必要があります。 ファクトとは異なり、アサーションは一般に、qubit レジスタの状態や実行環境などの外部の状態に依存します。 外部の状態に対する依存関係は副作用の一種であるため、アサーションは関数ではなく操作として公開する必要があります。

    - **推定**: 1 つまたは複数の連続した測定値を使用して、測定結果から古典の数量を見積もります。

      *例:*
      - @"microsoft.quantum.characterization.estimatefrequency"
      - @"microsoft.quantum.characterization.estimateoverlapbetweenstates"

    - **準備**: 特定の初期状態 (通常は $ \ket{00\cdots 0} $) で開始することが想定される1つ以上の qubits に対して、クォンタム操作または一連の操作を適用します。これにより、これらの qubits の状態が目的の終了状態に進化します。 一般に、指定された開始状態以外の状態で動作すると、未定義のユニタリ変換が発生する**可能性があり**ますが、操作とその adjoint "キャンセル" を保持し、操作なしを適用する**必要**があります。

      *例:*
      - @"microsoft.quantum.preparation.preparearbitrarystate"
      - @"microsoft.quantum.preparation.prepareuniformsuperposition"

    - **メジャー**: 1 つ以上の qubits にクォンタム操作または一連の操作を適用し、古典的なデータをバックアウトします。

      *例:*
      - @"microsoft.quantum.intrinsic.measure"
      - @"microsoft.quantum.arithmetic.measurefxp"
      - @"microsoft.quantum.arithmetic.measureinteger"

    - **適用**: クォンタム操作または操作のシーケンスを1つ以上の qubits に適用し、それらの qubits の状態が一貫した形で変化するようにします。 この動詞は Q の用語で最も一般的な動詞であり、 \# より具体的な動詞がより直接的に関連する場合には使用**しないでください**。

  - **名詞**:

    - **ファクト**: ターゲットコンピューターの状態、環境、またはコンピューターの qubits の状態ではなく、入力のみに依存するブール条件。 アサーションとは対照的に、ファクトは、そのファクトに対して指定された*値*にのみ影響します。 次に例を示します。

      *例:*
      - @"microsoft.quantum.diagnostics.equalityfacti": 2 つの整数入力に関する等価のファクトを表します。入力として指定された整数が互いに等しいか、または他のプログラムの状態に依存していないかのいずれかです。

    - **オプション:** 関数または演算に対して "省略可能な引数" として機能する複数の名前付き項目を含む UDT。 次に例を示します。

      *例:*
      - UDT には @"microsoft.quantum.machinelearning.trainingoptions" 、学習率、ミニバッチサイズ、および ML トレーニング用のその他の構成可能なパラメーターの名前付き項目が含まれています。

  - **形容詞**:

    - ⛔️ **New**: この形容詞は使用し**ないでください**。多くのプログラミング言語 (C++、C#、Java、TypeScript、PowerShell など) で動詞として使用する場合と混同しないようにしてください。

  - **前置詞:** 場合によっては、前置詞を使用して、関数名と操作名の名詞と動詞の役割をさらに明確に区別したり、明確にしたりすることができます。 ただし、そのためには控えめにする必要があります。

    - **次のようになります。** 関数の入力と出力が同じ情報を表しているが、出力ではその情報を元の表現ではなく*X* **として**表すことを表します。 これは、型変換関数では特に一般的です。

      *例:*
      - `IntAsDouble(2)`入力 ( `2` ) と出力 () の両方が `2.0` 同じ情報を質的しているが、異なる Q データ型を使用していることを示し \# ます。

    - **開始:** 一貫性を確保するために、この前置詞を使用**して、** 型変換関数や、が適切であるその他のケースを示すことはでき**ません**。

    - ⛔️ **:** この前置詞は、多くのプログラミング言語で動詞として使用する場合と混同しないように、使用しないことを**お勧め**します。
