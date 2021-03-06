---
title: Q の変数#
description: 説明の入力
author: gillenhaalb
ms.author: a-gibec@microsoft.com
ms.date: 03/05/2020
ms.topic: article
uid: microsoft.quantum.guide.variables
ms.openlocfilehash: 08301f408dcb2211ba25c582a5e5aa43310b714a
ms.sourcegitcommit: a3775921db1dc5c653c97b8fa8fe2c0ddd5261ff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885290"
---
# <a name="variables-in-q"></a>Q の変数#

Q # は、変更可能なシンボルと変更できないシンボル、または式にバインド/割り当てられている*変数*を区別します。
一般に、変更できないシンボルを使用することをお勧めします。これにより、コンパイラはより多くの最適化を実行できるためです。

バインディングの左側は、記号の組と式の右辺で構成されています。

## <a name="immutable-variables"></a>変更できない変数

キーワードを使用して、操作または関数内で再利用するために、Q # の任意の型の値を変数に割り当てることができ `let` ます。 

変更できないバインドは、キーワードで構成され、 `let` その後にシンボルまたは記号の組、等号 `=` (=)、および終端のセミコロンをバインドする式で構成されます。

次に例を示します。

```qsharp
let measurementOperator = [PauliX, PauliZ, PauliZ, PauliX, PauliI];
```

これにより、P# li の特定の配列が変数名 (または "symbol") に割り当てら `measurementOperator` れます。

> [!NOTE]
> 前の例では、ステートメントの右辺の式が明確であるため、新しい変数の型を明示的に指定する必要はありません `let` 。コンパイラは正しい型を推論します。 

を使用して定義された変数 `let` は*変更*できません。つまり、変数を定義すると、どのような方法でも変更できなくなります。
これにより、操作のバリアントを適用するために変数に対して並べ替えを行う従来のロジックの最適化など、いくつかの有益な最適化が可能に `Adjoint` なります。

## <a name="mutable-variables"></a>変更可能な変数

で変数を作成する代わりに、キーワードを使用して `let` `mutable` 最初に作成した後で再バインドできる変更*可能*な変数を作成し `set` ます。

ステートメントの一部として宣言およびバインドされているシンボルは `mutable` 、後でコード内で別の値に再バインドできます。 シンボルが後でコード内で再バインドされる場合、その型は変更されず、新しくバインドされた値はその型と互換性がある必要があります。

### <a name="rebinding-of-mutable-symbols"></a>再バインド (変更可能なシンボルの)

ステートメントを使用して、変更可能な変数を再バインドすることができ `set` ます。
このような再バインドは、キーワードと、 `set` その後にシンボルまたは記号の組、等号 (=) を再 `=` バインドする式、および終端のセミコロンで構成されます。

次に、再バインドステートメントの手法の例をいくつか示します。

#### <a name="apply-and-reassign-statements"></a>Apply ステートメントと再割り当てステートメント

特定の種類の `set` -ステートメント (*適用および再割り当て*ステートメント) は、右辺が二項演算子のアプリケーションで構成されており、結果が演算子の左辺の引数に再バインドされる場合に、簡単に連結できる方法を提供します。 例:

```qsharp
mutable counter = 0;
for (i in 1 .. 2 .. 10) {
    set counter += 1;
    // ...
}
```
`counter`ループの各反復処理でカウンターの値をインクリメントし `for` ます。 前のコードはと同じです。 

```qsharp
mutable counter = 0;
for (i in 1 .. 2 .. 10) {
    set counter = counter + 1;
    // ...
}
```

左辺の型が式の型と一致するすべての二項演算子に対して、同様のステートメントを使用できます。 これらのステートメントは、値を累積する便利な方法を提供します。

たとえば、 `qubits` 行政、次のように qubits のレジスタです。
```qsharp
mutable results = new Result[0];   // results is an empty array of type Result[]
for (q in qubits) {
    set results += [M(q)];         // concatenate the outcome from measuring q to the existing array
    // ...
}
...                                // results contains the measurement outcomes from the whole register
```

#### <a name="update-and-reassign-statements"></a>更新と再割り当てのステートメント

右側に[コピーと更新の式](xref:microsoft.quantum.guide.expressions#copy-and-update-expressions)がある場合も同様の連結が存在します。
それに応じて、ユーザー定義型および*配列項目*の*名前付き項目*に対して、*更新と再割り当て*のステートメントが存在します。  

```qsharp
newtype Complex = (Re : Double, Im : Double);

function ComplexSum(reals : Double[], ims : Double[]) : Complex[] {
    mutable res = Complex(0.,0.);

    for (r in reals) {
        set res w/= Re <- res::Re + r; // update-and-reassign statement
    }
    for (i in ims) {
        set res w/= Im <- res::Im + i; // update-and-reassign statement
    }
    return res;
}
```

配列の場合、 [`Microsoft.Quantum.Arrays`](xref:microsoft.quantum.arrays) Q # 標準ライブラリでは、多くの一般的な配列の初期化と操作に必要なツールが提供されるため、最初に配列項目を更新する必要がなくなります。 

必要に応じて、更新ステートメントと再割り当てステートメントで代替手段を提供します。

```qsharp
operation GenerateRandomInts(max : Int, nSamples : Int) : Int[] {
    mutable samples = new Double[0];
    for (i in 1 .. nSamples) {
        set samples += [RandomInt(max)];
    }
    return samples;
}

operation SampleUniformDistrbution(nSamples : Int, nSteps : Int) : Double[] {
    let normalization = 1. / IntAsDouble(nSteps);
    mutable samples = GenerateRandomInts(nSteps, nSamples);
    
    for (i in IndexRange(samples) {
        let value = IntAsDouble(samples[i]);
        set samples w/= i <- normalization * value; // update-and-reassign statement
    }
}

```

に用意されている配列のライブラリツールを使用すると、 [`Microsoft.Quantum.Arrays`](xref:microsoft.quantum.arrays) たとえば、インデックスの要素が指定された値を `Pauli` `i` 取得し、 `Pauli` その他のすべてのエントリが id () である型の配列を返す関数を簡単に定義でき `PauliI` ます。

このような関数の2つの定義を次に示します。2つ目は、ツールを利用することです。

```qsharp
function PauliEmbedding(pauli : Pauli, length : Int, location : Int) : Pauli[] {
    mutable pauliArray = new Pauli[length];             // initialize pauliArray of given length
    for (index in 0 .. length - 1) {                    // iterate over the integers in the length range
        set pauliArray w/= index <-                     // change the value at index to input pauli or PauliI
            index == location ? pauli | PauliI;         // cond. expression evaluating to pauli if index==location and PauliI if not
    }    
    return pauliArray;
}
```

配列内の各インデックスを反復処理し、条件付きでまたはに設定するのではなく、を使用して `PauliI` `pauli` `ConstantArray` [`Microsoft.Quantum.Arrays`](xref:microsoft.quantum.arrays) 型の配列を作成 `PauliI` し、次にインデックスで特定の値を変更したコピーと更新の式を返すだけです `location` 。

```qsharp
function PauliEmbedding(pauli : Pauli, length : Int, location : Int) : Pauli[] {
    return ConstantArray(length, PauliI) w/ location <- pauli;
}
```

## <a name="tuple-deconstruction"></a>タプル分解

1つの変数を割り当てるだけでなく、 `let` `mutable` キーワードまたはその他のバインド構成要素 (など) を使用して、 `set` [タプル型](xref:microsoft.quantum.guide.types#tuple-types)の内容をアンパックできます。
このフォームの割り当ては、そのタプルの要素を*分解*と言います。

バインドの右側がタプルの場合は、代入時にそのタプルを分解できます。
このような deconstructions には、入れ子になった組を含めることができます。また、右辺の組の構造がシンボルの組の形状と互換性がある限り、完全または部分的な分解は有効です。

次に例を示します。

```qsharp
let (i, f) = (5, 0.1); // i is bound to 5 and f to 0.1
mutable (a, (_, b)) = (1, (2, 3)); // a is bound to 1, b is bound to 3
mutable (x, y) = ((1, 2), [3, 4]); // x is bound to (1,2), y is bound to [3,4]
set (x, _, y) = ((5, 6), 7, [8]);  // x is rebound to (5,6), y is rebound to [8]
let (r1, r2) = MeasureTwice(q1, PauliX, q2, PauliY);
```

## <a name="binding-scopes"></a>スコープのバインド

一般に、シンボルバインドはスコープ外に出、ステートメントブロックの最後では動作しなくなります。
このルールには次の 2 つの例外があります。

- ループのループ変数のバインドは、for ループの `for` 本体のスコープ内にありますが、ループの終了後には適用されません。
- ループの3つの部分 `repeat` / `until` (本文、テスト、および修正) はすべて1つのスコープとして機能するので、本文にバインドされているシンボルはテストとフィックスアップで使用できます。

両方の種類のループでは、ループの各パスが独自のスコープ内で実行されるため、以前のパスからのバインドは、後のパスでは使用できません。
これらのループの詳細については、「[制御フロー](xref:microsoft.quantum.guide.controlflow)」を参照してください。

内部ブロックは、外側のブロックからシンボルバインドを継承します。
シンボルをバインドできるのは、ブロックごとに1回だけです。スコープ内にある別のシンボルと同じ名前のシンボルを定義することはできません ("シャドウ" はありません)。
有効なシーケンスは次のとおりです。

```qsharp
if (a == b) {
    ...
    let n = 5;
    ...             // n is 5
}
let n = 8;
...                 // n is 8
```

および

```qsharp
if (a == b) {
    ...
    let n = 5;
    ...             // n is 5
} else {
    ...
    let n = 8;
    ...             // n is 8
}
...                 // n is not bound to a value
```

ただし、これは無効になります。

```qsharp
let n = 5;
...                 // n is 5
let n = 8;          // Error!!
...
```

次のようになります。

```qsharp
let n = 8;
if (a == b) {
    ...             // n is 8
    let n = 5;      // Error!
    ...
}
...
```

## <a name="next-steps"></a>次の手順

Q # での[Qubits の](xref:microsoft.quantum.guide.qubits)使用について説明します。