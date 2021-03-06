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
# <a name="tutorial-explore-entanglement-with-q"></a>チュートリアル:Q\# でのもつれの確認

このチュートリアルでは、量子ビットの操作および測定を行い、重ね合わせともつれの効果を示す、Q# プログラムの作成方法を説明します。

量子のもつれを示すため、Bell というアプリケーションを記述します。
Bell という名前は、ベル状態を表しています。これは、量子の重ね合わせともつれの最も簡単な例を表すために使用される、2 つの量子ビットの特定の量子の状態です。

## <a name="pre-requisites"></a>前提条件

コーディングを開始する準備ができたら、続行する前に次の手順を実行してください。 

* 任意の言語および開発環境を使用して、Quantum 開発キットを[インストール](xref:microsoft.quantum.install)します。
* 既に QDK をインストールしている場合は、バージョンが[最新](xref:microsoft.quantum.update)であることを確認する

また、QDK をインストールしなくても、Q # プログラミング言語の概要と、クォンタムコンピューティングの最初の概念を確認することで、このナレーションに従うことができます。

## <a name="in-this-tutorial-youll-learn-how-to"></a>このチュートリアルでは、次の作業を行う方法について説明します。

> [!div class="checklist"]
> * Q での操作の作成と結合\#
> * 法則、entangle に qubits を配置する操作を作成し、それらを測定します。
> * シミュレーターで実行される Q # プログラムを使用したクォンタムの例を示します。 

## <a name="demonstrating-qubit-behavior-with-the-qdk"></a>QDK を使用した qubit 動作のデモンストレーション

従来のビットでは単一のバイナリ値 (0、1 など) が保持されるのに対し、[量子ビット](xref:microsoft.quantum.glossary#qubit)の状態は 0 と 1 の**重ね合わせ**になることができます。  概念上、qubit の状態は、抽象空間 (ベクターとも呼ばれます) の方向と考えることができます。  Qubit 状態は、可能な任意の方向にすることができます。 2 つの**従来の状態**とは、0 を測定する確率が 100% になる方向と、1 を測定する確率が 100% になる方向のことです。

測定の動作により、2 進法の結果が生成され、量子ビットの状態が変わります。
測定値によって、0または1の2進値が生成されます。  量子ビットは重ね合わせ (あらゆる方向にある) の状態から古典的状態のいずれかになります。  その後、介在する操作なしで同じ測定を繰り返すと、同じ 2 進数の結果が生成されます。  

複数の量子ビットは[**もつれさせる**](xref:microsoft.quantum.glossary#entanglement)ことができます。  もつれのある 1 つの量子ビットを測定すると、もう一方の量子ビットの状態に関する知識も更新されます。

これで、Q# がこの動作を表現する方法を説明できるようになりました。  考えられる最も単純なプログラムから始め、量子の重ね合わせと量子のもつれを表すように構築します。

## <a name="creating-a-q-project"></a>Q # プロジェクトを作成する

まず、新しい Q # プロジェクトを作成する必要があります。 このチュートリアルでは、 [VS Code のコマンドラインアプリケーション](xref:microsoft.quantum.install.standalone)に基づいて環境を使用します。

新しいプロジェクトを作成するには VS Code 次のようにします。 

1. [ **View**  ->  **コマンドパレット**の表示] をクリックし、[ **Q #: 新しいプロジェクトの作成**] を選択します。
2. [**スタンドアロンコンソールアプリケーション**] をクリックします。
3. プロジェクトを保存する場所に移動し、[**プロジェクトの作成**] をクリックします。
4. プロジェクトが正常に作成されたら、右下にある [**新しいプロジェクトを開く**] をクリックします。

この例では、プロジェクトを呼び出しました `Bell` 。 これに `Bell.csproj` より、プロジェクトファイルと、アプリケーションを `Program.qs` 記述するために使用する Q # アプリケーションのテンプレートの2つのファイルが生成されます。 の内容は次のようになり `Program.qs` ます。

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

## <a name="write-the-q-application"></a>Q アプリケーションを作成する \#
 
私たちの目標は、Q# を使って量子ビットを操作してその状態を変更するための、特定の量子の状態にある 2 つの量子ビットを準備し、重ね合わせともつれの効果を示すことです。 ここでは、qubit の状態、操作、および測定について説明します。

### <a name="initialize-qubit-using-measurement"></a>測定を使用して qubit を初期化する

以下に示す最初のコードは、Q# で量子ビットを操作する方法を示しています。  2つの操作を紹介 [`M`](xref:microsoft.quantum.intrinsic.m) し、 [`X`](xref:microsoft.quantum.intrinsic.x) qubit の状態を変換します。 このコード スニペットでは、量子ビットをパラメーターと見なす操作 `SetQubitState` が定義されています。もう 1 つのパラメーター `desired` は量子ビットが目的とする状態を表しています。  操作 `SetQubitState` は、操作 `M` を使用して、量子ビットに対する測定を実行します。  Q # では、qubit 測定値は常に `Zero` またはを返し `One` ます。  測定値が目的の値と等しくない値を返す場合、 `SetQubitState` は qubit を "反転" します。つまり、演算子は演算を実行します。これにより、 `X` qubit 状態が戻り値の確率が返され、元に戻される新しい状態に変更 `Zero` され `One` ます。 これにより、は `SetQubitState` 常にターゲットの qubit を目的の状態にします。

の内容を `Program.qs` 次のコードに置き換えます。


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

この操作により、量子ビットが従来の状態に設定されます。つまり、`Zero` が 100% 返されるか、`One` が 100% 返されるかのどちらかです。
`Zero` および `One` は、量子ビットの測定結果として考えられる 2 とおりの結果を表す定数です。

`SetQubitState` 操作で量子ビットが測定されます。 量子ビットが目的の状態にある場合は、`SetQubitState` をそのままにしておきます。それ以外の場合は、`X` 操作を実行することで量子ビットの状態が目的の状態に変更されます。

#### <a name="about-q-operations"></a>Q# 操作について

Q# 操作は、量子のサブルーチンです。 つまり、これは、他のクォンタム操作の呼び出しを含む呼び出し可能なルーチンです。

操作の引数は、かっこ内にタプルとして指定します。

操作の戻り値の型は、コロンの後に指定します。 この場合、`SetQubitState` 操作には戻り値がないため、`Unit` を返すように設定されています。 これは、F# における `unit` の Q# 版にあたります。C# では `void`、Python では空のタプル (`Tuple[()]`) とほぼ同じです。

最初の Q# 操作では、次の 2 つの量子操作を使用しました。

* [`M`](xref:microsoft.quantum.intrinsic.m)Qubit の状態を測定する操作。
* [`X`](xref:microsoft.quantum.intrinsic.x)Qubit の状態を反転する操作。

量子操作により、量子ビットの状態が変換されます。 従来の論理ゲートの類義語として、量子操作の代わりに、量子ゲートが話題になることがあります。 これは初期の量子コンピューティングでは、アルゴリズムが単なる理論上の構成要素であり、古典コンピューティングの回路図に似た図で視覚化されていたことに端を発します。

### <a name="counting-measurement-outcomes"></a>測定結果のカウント

`SetQubitState` 操作の効果を示すため、`TestBellState` 操作を追加します。 この操作では、`Zero` または `One` を入力として受け取り、その入力で `SetQubitState` 操作を何回か呼び出して、`Zero` が量子ビットの測定から返された回数と `One` が返された回数をカウントします。 当然ながら、`TestBellState` 操作のこの最初のシミュレーションでは、`Zero` がパラメーターとして設定された量子ビットのすべての測定で `Zero` を返し、`One` がパラメーターとして設定された量子ビットのすべての測定で `One` を返すことが想定されます。 さらに、 `TestBellState` 法則と entangを示すためのコードをに追加します。

`Bell.qs` ファイルの名前空間内、`SetQubitState` 操作の終了後に次の操作を追加します。

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
`return`コンソールで関数 () を使用して説明メッセージを出力するために、の前に行を追加しました `Message` 。

この操作 (`TestBellState`) では、`count` 回ループし、指定された `initial` 値を量子ビットに設定して、結果を測定 (`M`) します。 これにより、測定した 0 と 1 の数がいくつあるかの統計情報が収集され、呼び出し元に返されます。 ここでは、もう 1 つの必要な操作を実行しています。 他のユーザーがこの量子ビットに既知の状態を割り当てることができるよう、終了する前にこの量子ビットを既知の状態 (`Zero`) にリセットします。 この操作は、`using` ステートメントに必須です。

#### <a name="about-variables-in-q"></a>Q の変数について\#

既定では、Q# の変数は不変です。バインド後に変数の値を変更することはできません。 `let` キーワードは、不変変数のバインドを示すために使用します。 操作の引数は常に不変です。

先ほどの例の `numOnes` のように、値を変更できる変数が必要な場合は、`mutable` キーワードを使用して変数を宣言できます。 可変変数の値は、`setQubitState` ステートメントを使用して変更できます。

どちらの場合も、変数の型はコンパイラによって推論されます。 Q# では、変数に型の注釈は必要ありません。

#### <a name="about-using-statements-in-q"></a>`using`Q のステートメントについて\#

`using` ステートメントも Q# に特有です。 これは、コードのブロックで使用するために量子ビットを割り当てる場合に使用されます。 Q# では、複雑なアルゴリズムの有効期間全体にわたってリソースが固定されるのではなく、すべての量子ビットが動的に割り当てられ、解放されます。 `using` ステートメントは、ブロックの最初で一連の量子ビットを割り当て、ブロックの最後でその量子ビットを解放します。

## <a name="execute-the-code-from-the-command-line"></a>コマンドラインからコードを実行する

コードを実行するには、コマンドを指定したときに実行さ*れる*呼び出し可能なコンパイラを指定する必要があり `dotnet run` ます。 これを行うには、呼び出し先の直前にを含む行を追加することにより、Q # ファイルを簡単に変更し `@EntryPoint()` ます。 `TestBellState` この場合は、操作です。 完全なコードは次のようになります。

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

プログラムを実行するには、 `count` `initial` コマンドラインから引数と引数を指定する必要があります。 たとえば、とのように選択し `count = 1000` `initial = One` ます。 次のコマンドを入力します。

```dotnetcli
dotnet run --count 1000 --initial One
```

次の出力が表示されます。

```output
Test results (# of 0s, # of 1s):
(0, 1000)
```

を試してみると、次のことを確認する `initial = Zero` 必要があります。

```dotnetcli
dotnet run --count 1000 --initial Zero
```
```output
Test results (# of 0s, # of 1s):
(1000, 0)
```

## <a name="prepare-superposition"></a>重ね合わせ状態を作成する

次に、Q # で法則に qubits を配置する方法を見てみましょう。  量子ビットの状態は、0 と 1 の重ね合わせにできることを思い出してください。  これを行うには、`Hadamard` 操作を使用します。 量子ビットが従来の状態のいずれか (測定で常に `One` または `Zero` を返す) である場合、`Hadamard` (`H`) 操作によって、量子ビットの測定で 50% の `Zero` および 50% の `One` を返す状態に量子ビットが配置されます。  概念上、量子ビットは `Zero` と `One` の中間にあると考えることができます。  ここで、`TestBellState` 操作をシミュレートすると、測定後の結果は、ほぼ同数の `Zero` と `One` を返します。  

### <a name="x-flips-qubit-state"></a>`X`qubit 状態を反転します

まず、量子ビットを反転してみます (量子ビットが `Zero` の状態にある場合は `One` になり、その逆も同様になります)。 これは、`TestBellState` で測定する前に `X` 操作を実行することで実現されます。

```qsharp
X(qubit);
let res = M(qubit);
```

結果は逆順になります。

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

次に、qubits のクォンタムプロパティについて説明します。

### <a name="h-prepares-superposition"></a>`H`法則を準備する

必要なのは、先ほどの実行の `X` 操作を `H` すなわち Hadamard 操作に置き換えることだけです。 これは、量子ビットを 0 から 1 まで完全に反転させるのではなく、半分だけ反転します。 `TestBellState` の行を置き換えると、次のようになります。

```qsharp
H(qubit);
let res = M(qubit);
```

結果はさらに興味深いものになります。

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

測定するたびに、従来型の値が要求されますが、量子ビットは 0 と 1 の中間にあるため、(統計的に) 半分が 0、半分が 1 になります。
これは**重ね合わせ**と呼ばれる現象で、これによって初めて量子状態を実際に観測できます。

## <a name="prepare-entanglement"></a>もつれ状態を作成する

では、Q# がどのように量子ビットのもつれを表現するかを見てみましょう。
まず、最初の量子ビットを初期状態に設定してから、`H` 操作を使用してそれを重ね合わせに配置します。  次に、最初の qubit を測定する前に、 `CNOT` 制御されていないを表す新しい操作 () を使用します。  2 つの量子ビットに対してこの操作を実行した結果、最初の量子ビットが `One` である場合には 2 番目の量子ビットが反転されます。  これで、2 つの量子ビットがもつれ状態になります。  最初の量子ビットの統計情報は変わっていませんが (測定後、50-50 の確率で `Zero` または `One`)、2 番目の量子ビットを測定すると、最初の量子ビットを測定した結果と__常に__同じになります。 この `CNOT` が 2 つの量子ビットをもつれさせ、片方に何かが起きると、もう片方にも同じことが起こるようになっています。 測定を反対にしても (最初の量子ビットの前に 2 番目の量子ビットを測定する)、同じことが起こります。 最初の測定値はランダムであり、2 回目の測定値は最初に検出されたものと完全に一致します。

最初に、ではなく2つの qubits を割り当てる必要があり `TestBellState` ます。

```qsharp
using ((q0, q1) = (Qubit(), Qubit())) {
```

これにより、`TestBellState` で測定 (`M`) する前に、新しい操作 (`CNOT`) を追加できます。

```qsharp
SetQubitState(initial, q0);
SetQubitState(Zero, q1);

H(q0);
CNOT(q0, q1);
let res = M(q0);
```

最初の量子ビットを初期化するために別の `SetQubitState` 操作を追加し、開始時に常に `Zero` 状態になるようにしました。

また、2 番目の量子ビットを解放する前にリセットする必要があります。

```qsharp
SetQubitState(Zero, q0);
SetQubitState(Zero, q1);
```

完全なルーチンは、次のようになります。

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

これを実行すると、以前とまったく同じ 50-50 の結果が得られます。 しかし、ここで興味深いのは、2 番目の量子ビットが測定される最初の量子ビットに対してどのように反応するかです。 この統計情報は、新しいバージョンの `TestBellState` の操作で追加します。

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

新しい戻り値 (`agree`) は、最初の量子ビットの測定値が 2 番目の量子ビットの測定値と一致した回数を追跡します。

取得したコードを実行すると、次のようになります。

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

概要で述べたように、最初の量子ビットの統計情報は変わっていませんが (50-50 の確率で 0 または 1)、2 番目の量子ビットを測定すると、最初の量子ビットを測定した結果と__常に__同じになります。これは、もつれ状態にあるからです。

## <a name="next-steps"></a>次のステップ

[グローバーの検索](xref:microsoft.quantum.quickstarts.search)のチュートリアルでは、最も人気のある量子コンピューティング アルゴリズムの 1 つである、グローバーの検索をビルドして実行する方法を示しています。また、量子コンピューティングに関する実際の問題を解決するために使用できる Q# プログラムの優れた例を紹介しています。  

「[Get Started with the Quantum Development Kit](xref:microsoft.quantum.welcome)」(Quantum Development Kit の概要) では、Q# と量子コンピューティングのその他の学習方法も紹介しています。
