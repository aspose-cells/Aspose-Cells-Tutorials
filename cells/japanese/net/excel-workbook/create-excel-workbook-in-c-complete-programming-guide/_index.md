---
category: general
date: 2026-06-05
description: C#でExcelブックを素早く作成し、セルの数値書式の設定方法、Excelセルのエクスポート方法、そしてセルの値を小数点以下2桁の文字列に変換する方法を学びましょう。
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: ja
og_description: C#でExcelブックを作成し、セルの数値書式設定をマスターし、Excelセルを文字列としてエクスポートし、数値を小数点以下2桁でフォーマットする。
og_title: C#でExcelブックを作成する – 完全ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: C#でExcelワークブックを作成する – 完全プログラミングガイド
url: /ja/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel ワークブックを作成する – 完全プログラミングガイド

COM インターロップや乱雑な CSV トリックに悩まされずに C# で **Excel ワークブックを作成** する方法を考えたことはありませんか？ あなただけではありません。多くの開発者が、.NET ネイティブなクリーンな方法で .xlsx ファイルを作成し、セルに数値を入れ、そしてその値をきれいにフォーマットされた文字列としてエクスポートしたいと考えています。

このチュートリアルでは、まさにそれを順を追って解説します — 空のワークブックから始め、セルの数値書式を設定し、数値を小数点以下2桁でフォーマットし、最後に **Excel セルを文字列としてエクスポートする方法** を学びます。最後までで、**セルの値を文字列に変換** する際に精度を失わない方法も確認できます。

> **プロのコツ:** 以下のアプローチは **Aspose.Cells for .NET** ライブラリを使用しています。このライブラリは実績のある商用レベルの API です。無料の代替手段を求める場合は、EPPlus や ClosedXML も同様に機能しますが、コードスニペットは若干異なります。

## 前提条件

- .NET 6.0 SDK（または最近の .NET バージョン）をインストールしておくこと。
- Visual Studio 2022 または C# 拡張機能が入った VS Code。
- **Aspose.Cells** NuGet パッケージ（`Install-Package Aspose.Cells`）。

他に依存関係は不要です — すべてはライブラリ内部に収められています。

## ステップ 1: Aspose.Cells をインストールし、プロジェクトをセットアップする

ターミナル（または Package Manager Console）を開き、以下を実行します:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

これにより `ExcelDemo` という新しいコンソールアプリが作成され、`Aspose.Cells` アセンブリが取得されます。

このステップが重要な理由: ライブラリがなければ、**Excel ワークブック** オブジェクトを作成したり、型安全にセルを操作したりできません。

## ステップ 2: ワークブックを作成し、最初のワークシートを取得する

次に `Program.cs` を開き、デフォルトコードを以下のスニペットに置き換えます。これは **Excel ワークブックを作成** したときに最初に行うこと、すなわち `Workbook` クラスをインスタンス化し、デフォルトシートへの参照を取得する方法を示しています。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **なぜ？** `Workbook` オブジェクトは Excel ファイルのメモリ上の表現です。デフォルトでは 1 つのワークシートが含まれており、ゼロベースのインデックスでアクセスします。

## ステップ 3: 特定のセルに数値を入力する

行 5、列 2（ゼロベースのインデックス）を対象にし、十進数を挿入しましょう。これは後で **小数点以下2桁で数値をフォーマット** する例示になります。

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

`PutValue` メソッドは生の double を格納します。この時点では、書式を適用しない限り Excel は完全な精度で表示します。

## ステップ 4: セルの数値書式を設定する（小数点以下2桁）

ここで **セルの数値書式を設定** します。`Style` オブジェクトを使い、カスタム数値書式 `"0.00"`（ちょうど小数点以下2桁）を定義します。

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

文字列変換ではなくスタイルを使う理由は何ですか？ セルを数値型のままにしておくことで、計算可能な性質（合計、平均など）が保持され、必要な表示だけを行えます。

## ステップ 5: セルの値をフォーマット済み文字列としてエクスポートする

時には **Excel セルをエクスポートする方法** の値をプレーンテキストとして必要とすることがあります — たとえばログファイルに書き込む、または Web API で送信する場合です。Aspose.Cells はセルにエクスポートオプションを付与でき、同じ数値書式で文字列として値をレンダリングするようライブラリに指示します。

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## ステップ 6: フォーマット済み文字列を取得する（セルの値を文字列に変換）

実際にエクスポートを実行し、結果を確認しましょう。`ExportString` メソッドはセルの内容を文字列として返し、付与した `ExportTableOptions` を適用します。

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

プログラムを実行すると、コンソールに次のように出力されます:

```
Formatted cell value: 12345.68
```

`12345.6789` が `12345.68` に丸められていることに注目してください — これが **小数点以下2桁で数値をフォーマット** した効果です。

## ステップ 7: （オプション）ワークブックをディスクに保存する

実際の `.xlsx` ファイル内で結果を確認したい場合は、`Save` を呼び出すだけです:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

`DemoWorkbook.xlsx` を開くと、セル **C6** に同じ数値が小数点以下2桁でフォーマットされた状態で表示されます。

## エッジケースとよくある質問

### セルに既にスタイルが設定されている場合は？

`GetStyle` メソッドは既存のスタイルのコピーを返すため、以前の書式設定（フォント、色など）は保持されます。上書きするのは `Custom` プロパティだけで、他はそのままです。

### 文化設定は小数点区切り文字にどう影響しますか？

Aspose.Cells はスレッドの `CultureInfo` を尊重します。ドットの代わりにカンマが必要な場合は、次のように設定します:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

同じ `"0.00"` 書式が `12 345,68` と表示されます。

### 複数セルの範囲を一度にエクスポートできますか？

はい。`Worksheet.ExportDataTable` または範囲アドレスを指定した `Worksheet.ExportString` を使用します。単一セル用に定義した `ExportTableOptions` は、範囲全体でも再利用できます。

### 値を丸めずに切り捨てたい場合は？

カスタム書式を丸めモード付きの `"0.00"` に変更するか、値を設定する前に手動で切り捨てます:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## 完全動作例（コピー＆ペースト可能）

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**期待されるコンソール出力**

```
Formatted cell value: 12345.68
```

`DemoWorkbook.xlsx` を開き → セル **C6** に移動 → 同じ数値が小数点以下2桁で表示されているのが確認できます。

## 結論

ここまでで、C# で **Excel ワークブックを作成** し、**セルの数値書式を設定**、**小数点以下2桁で数値をフォーマット**、**Excel セルをエクスポートする方法** を理解し、**セルの値を文字列に変換** して下流処理に利用するために必要なすべてを網羅しました。

主なポイントは次の通りです:

1. `Workbook` と `Worksheet` を使用して、メモリ上に Excel ファイルを作成する。
2. カスタムスタイル（`"0.00"`）を適用して、小数点以下2桁の表示を強制する。
3. 同じ書式を保持した文字列表現が必要な場合は、セルに `ExportTableOptions` を付与する。

ここからは実験が可能です — さらにセルを追加したり、条件付き書式を適用したり、チャートを生成したりできます。フォントのスタイリングや数式の追加に興味がある場合は、Aspose.Cells のドキュメントで **セルのスタイリング** と **数式評価** を確認してください。

C# における Excel 自動化でさらに質問がありますか？ コメントを残してください。ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、完全に動作するコード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells .NET でワークブック操作をマスターする：Excel ファイルの読み込みとセル先行関係の追跡を効果的に行う](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Aspose.Cells for .NET で Excel セルの書式設定とワークブック管理をマスターする](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Aspose.Cells for .NET をマスターする：高度な Excel ワークブックとセル管理](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}