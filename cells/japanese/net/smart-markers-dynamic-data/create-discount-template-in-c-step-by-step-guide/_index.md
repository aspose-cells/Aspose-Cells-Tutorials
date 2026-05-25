---
category: general
date: 2026-02-14
description: 割引テンプレートをすばやく作成し、スプレッドシートで割引を適用する方法、テンプレートへのデータ注入、そしてスマートマーカー用の変数プレフィックスの定義を学びましょう。
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: ja
og_description: C#で割引テンプレートを作成する。スプレッドシートで割引を適用し、テンプレートにデータを注入し、スマートマーカー用の変数プレフィックスを定義する方法を学びます。
og_title: 割引テンプレートの作成 – 完全なC#ウォークスルー
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: C#で割引テンプレートを作成する – ステップバイステップガイド
url: /ja/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Discount テンプレートの作成 – 完全 C# ハンドブック

販売レポート用に **discount テンプレートを作成** したいが、数値をスプレッドシートに自動で流し込む方法が分からない…という経験はありませんか？ あなたは一人ではありません。このチュートリアルでは、**discount テンプレートを作成**し、**スプレッドシートのセルに割引を適用**し、**テンプレートにデータを注入**し、さらにスマートマーカー用の **variable prefix** を定義する方法を、クリーンな C# コードで解説します。

まず問題点を整理し、すぐにコピー＆ペーストできる動作するソリューションに飛び込みます。最後まで読めば、請求書、価格表、あるいは動的割引が必要な任意のスプレッドシートを生成する際に再利用できるパターンが手に入ります。

---

## 学べること

- 割引対応のスプレッドシートテンプレートの設計方法
- マーカーを見つけやすくするためのカスタム `VariablePrefix` / `VariableSuffix` の設定方法
- 匿名オブジェクト (`discountData`) を `SmartMarkerProcessor` に渡す手順
- 結果として生成される数式（`=IF(#Discount#>0, A1*(1-#Discount#), A1)`）が自動的に最終価格を計算する仕組み
- ゼロ割引行や複数割引階層といったエッジケースの処理ヒント

**前提条件** – .NET 6 以上のランタイム、`Aspose.Cells`（または同等）ライブラリへの参照、`SmartMarkerProcessor` を提供するもの、そして基本的な C# 文法の理解があれば OK。特別な前提はありません。

---

## Step 1: スプレッドシートに Discount テンプレートを作成

まず新規ブック（または既存ブック）を開き、割引を適用するプレースホルダーを配置します。テンプレートは「スマートマーカー」が置かれた普通の Excel ファイルです。

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**ポイント**: 数式内に `#Discount#` を埋め込むことで、プロセッサに割引値の挿入位置を指示しています。`SmartMarkerProcessor` は後で `#Discount#` を提供した数値に置き換え、数式の他の部分はそのまま残します。

---

## Step 2: スマートマーカー用の Variable Prefix を定義

多くのライブラリはデフォルトで `${Variable}` や `{{Variable}}` を探しますが、ここでは人間が読みやすいマーカーを使用したいので、**variable prefix** と **suffix** を明示的に設定します。

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**プロチップ**: `#` を使うとマーカーが短くなり、Excel の数式バーでも見つけやすくなります。既存の Excel 関数と衝突する可能性がある場合は、別のペア（例: `[[` と `]]`）を選んでください。

---

## Step 3: SmartMarkerProcessor でテンプレートにデータを注入

実際の割引値を渡します。プロセッサはシート全体を走査し、すべての `#Discount#` を匿名オブジェクトから取得した値に置き換えます。

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

この呼び出しの後、セル `B2` の数式は次のようになります。

```
=IF(0.1>0, A2*(1-0.1), A2)
```

ブックが計算されると、`B2` は **90** と表示されます。つまり、元の価格 100 に対して 10 % の割引が適用された結果です。

**なぜ動くのか**: `StartSmartMarkerProcessing` が各セルを走査し、`#Discount#` トークンを数値に置換します。トークンが `IF` 文の中にあるため、割引が 0 の場合でもスプレッドシート側で正しく処理されます。

---

## Step 4: スプレッドシートで割引を適用 – 結果を確認

計算をトリガーし、最終価格をコンソールに出力します。このステップで **apply discount in spreadsheet** のフローが正常に完了したことが確認できます。

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**期待される出力**

```
Original: 100
Discounted (10%): 90
```

`discountData.Discount` を `0.25` に変更して再実行すれば、出力は自動的に 25 % 割引を反映します。追加のコードは不要です。

---

## Step 5: エッジケースと複数割引の取り扱い

### Zero‑Discount 行

商品がセール対象でない場合があります。先ほど設定した `IF` 文がこのシナリオをすでにカバーしており、`#Discount#` が `0` のときは元の価格がそのまま通ります。

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### 複数割引列

行ごとに別々の割引が必要な場合は、`#Discount1#`、`#Discount2#` といったマーカーを各行に付与し、コレクションを渡します。

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

プロセッサはマーカーを順にマッチさせるため、各行に正しい値が割り当てられます。

---

## 完全動作サンプル

以下は、上記手順をすべて組み込んだコピー可能なプログラムです。`Program.cs` として保存し、`Aspose.Cells` への参照を追加して実行してください。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

実行すると期待通りの数値がコンソールに表示され、`DiscountedPricing.xlsx` が生成されます。Excel で開くと、数式がすでに解決された状態になっています。

---

## まとめ

これで **discount テンプレートの作成**、**スプレッドシートでの割引適用**、**テンプレートへのデータ注入**、そして **スマートマーカー用の variable prefix の定義** が、数行の C# コードで実現できました。このパターンはスケーラブルです。匿名オブジェクトを変更したり、コレクションで一括更新したりすれば、どんな割引シナリオにも対応できます。

次のステップに挑戦してみませんか？

- 割引に加えて税金計算を組み込む
- 割引率をハードコーディングせず、データベースから取得する
- 高割引行をハイライトする条件付き書式を使用する

これらの拡張はコアアイデアを保ちつつ、discount テンプレートの有用性をさらに高めます。

質問や面白いユースケースがあればコメントで教えてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}