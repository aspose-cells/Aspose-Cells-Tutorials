---
category: general
date: 2026-03-22
description: C#でラムダ式を使用してExcelの数式を操作する方法。セルに数式を書き込む方法、範囲を配列に変換する方法、配列をコンソールに表示する方法、そしてExcelで余接（cotangent）を計算する方法を学びます。
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: ja
og_description: C#でラムダ式を使用してExcelの数式を操作し、範囲を配列に変換し、セルに数式を書き込み、コンソールに配列を表示し、Excelで余接を計算する方法。
og_title: C#でラムダ式をExcelの数式と共に使用する方法 – ステップバイステップ
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: C#でラムダ式をExcel数式と共に使用する方法 – 完全ガイド
url: /ja/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Excel の数式で Lambda を使用する方法 – 完全ガイド

C# から Excel を自動化するときに **lambda の使い方** を考えたことはありませんか？ あなただけではありません。多くの開発者が、Excel の新しい動的配列関数の力と C# の `LAMBDA` 機能を組み合わせる必要があるときに壁にぶつかります。良いニュースは、部品がどのように組み合わさるかが分かれば、実はかなりシンプルだということです。

このチュートリアルでは、**セルに数式を書き込む**、**範囲を配列に変換する**、**コンソールにその配列を表示する**、さらには **Excel で余接（cotangent）を計算する** までを順に解説し、`REDUCE` 呼び出しの中で **lambda の使い方** を示します。最後まで読むと、Aspose.Cells（または類似のライブラリ）を参照した任意の .NET プロジェクトに貼り付けられる実行可能なコードスニペットが手に入ります。

---

## 学習内容

- C# を使用して **セルに数式を書き込む** 方法。
- `EXPAND` 関数を使用して **範囲を配列に変換する** 方法。
- 計算後に **コンソールに配列を表示する** 方法。
- `COT` と `COTH` を使用して **Excel で余接（cotangent）を計算する** 方法。
- C# から Excel の `REDUCE` 関数内で **lambda の使い方** の正確な構文。

> **前提条件:** .NET の最新バージョン（Core 6 以上または .NET Framework 4.7 以上）と、NuGet 経由でインストールした Aspose.Cells for .NET ライブラリが必要です。

---

## 手順 1: ワークブックの設定とセルへの数式書き込み

最初に新しいワークブックを作成し、最初のワークシートを取得します。その後、**セルに数式を書き込む** – この例では `A1` に `EXPAND` 呼び出しの結果が格納されます。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**なぜ重要か:** コードから直接数式を書き込むことで、Excel を開くことなく動的に複雑なスプレッドシートを生成できます。また、次のステップで **範囲を配列に変換する** 準備にもなります。

---

## 手順 2: EXPAND で範囲を配列に変換

`EXPAND` は、Excel が小さな範囲を大きな行列に変換する方法です。数式を `A1` に配置すると、Excel はそのセルから 4 × 5 のブロックをスピルします。C# からは値を手動でコピーする必要はなく、`Calculate` を呼び出すとライブラリが重い処理を行ってくれます。

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**lambda の使い方:** まだですが、続きにご期待ください。まずシートにデータを用意し、次に lambda で集約します。

---

## 手順 3: REDUCE 内で LAMBDA を使用 – “lambda の使い方” の核心

Excel 365 で導入された `REDUCE` は、**初期値**、**範囲**、そして各要素をどのように結合するかを指示する **LAMBDA** を受け取ります。C# からは単に数式文字列を割り当てるだけで、lambda は Excel の数式内にあり、C# のコードには存在しません。

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**説明:**  
- `0` は開始時のアキュムレータ（`acc`）です。  
- `A1:D4` は処理対象の範囲（スピルの最初の 4 列）です。  
- `LAMBDA(acc, x, acc + x)` は、各セル（`x`）をアキュムレータに加算するよう Excel に指示します。  

これがスプレッドシート上で集計するための **lambda の使い方** の本質です。

---

## 手順 4: Excel で余接（cotangent）を計算 – 度数から双曲線へ

三角関数の結果が必要な場合、Excel の `COT` と `COTH` 関数はとても簡単です。これらをそれぞれ `G1` と `G2` に配置します。

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**便利な理由:** **Excel で余接を計算する** 方法を知っていれば、特にワークブックが開発者以外と共有される場合に、カスタムの数学コードを書く手間を省けます。

---

## 手順 5: 計算を強制し、拡張された配列を取得

ここでワークブックにすべての数式を評価させ、`A1` からスピルされた配列を取得します。これが **コンソールに配列を表示** する段階です。

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**表示内容:**  
- 行ごとに整形された 4 × 5 行列が出力されます。  
- `REDUCE` lambda によって計算された合計。  
- 2 つの余接（cotangent）値。

これで **セルに数式を書き込む** から **コンソールに配列を表示** までの流れが完了です。

---

## 完全動作例（コピー＆ペースト可能）

以下はコンソールアプリに貼り付けて使用できる完全なプログラムです。まず `Aspose.Cells` NuGet パッケージを追加することを忘れずに（`dotnet add package Aspose.Cells`）。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**期待されるコンソール出力（値はデフォルトの B1:C2 の内容により変わります。デフォルトでは 0 です）:**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

実行前に `B1:C2` に任意の数値を入力しても構いません。マトリックスはその値を反映します。

---

## プロのコツとよくある落とし穴

- **Pro tip:** スピル範囲の開始位置を変更したい場合は、対象セル（`A1`）を変更するだけです。`EXPAND` 関数はアンカーを尊重します。
- **Watch out for:** 元範囲の空セルはスピルされた配列で `0` となり、`REDUCE` の合計に影響を与える可能性があります。
- **Edge case:** ワークブックに揮発性関数（例: `NOW()`）に依存する数式がある場合、すべての数式を設定した後に `workbook.Calculate()` を呼び出して、最新の状態にしてください。
- **Performance note:** 大規模なスピルの場合、`EXPAND` 呼び出しでサイズを制限することを検討してください。そうしないと不要なメモリを確保してしまう可能性があります。
- **互換性:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}