---
category: general
date: 2026-02-21
description: C#でセルスタイルを素早く作成する。セルへのスタイル適用方法、セル内テキストの中央揃え、セルの配置設定、そしてセル書式設定のマスターを学ぶ。
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: ja
og_description: C#でセルスタイルを作成し、セルにスタイルを適用する方法、セル内のテキストを中央揃えにする方法、セルの配置を設定する方法を、わかりやすいステップバイステップのガイドで学びましょう。
og_title: C#でセルスタイルを作成 – セルにスタイルを適用してテキストを中央揃え
tags:
- C#
- Aspose.Cells
- Excel automation
title: C#でセルスタイルを作成 – セルにスタイルを適用し、テキストを中央揃えする方法
url: /ja/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でセルスタイルを作成 – スタイル適用とテキストのセンタリング完全ガイド

Excel のワークシートで **セルスタイルを作成** したいと思ったことはありませんか？でもどこから始めればいいか分からないことも多いでしょう。多くの自動化プロジェクトでは、**セルにスタイルを適用** できるかどうかが、味気ないスプレッドシートと洗練されたレポートの違いになります。

このチュートリアルでは、セル内のテキストを **センタリング** し、配置を設定し、細い枠線を追加する方法を示す、完全に実行可能なサンプルをステップバイステップで解説します。数行の C# コードで完了します。最後まで読めば、各要素がなぜ重要なのか、そして自分のシナリオに合わせてどう調整すればよいかが分かります。

## 本チュートリアルで得られること

- Aspose.Cells（または類似のライブラリ）を使用した **セルスタイルの作成** ワークフローを明確に理解できる。
- コンソールアプリにコピー＆ペーストできる、**セルにスタイルを適用** する正確なコード。
- **セル内テキストのセンタリング**、**セルの配置設定**、および結合セルやカスタム数値書式といったエッジケースの取り扱いに関する洞察。
- スタイル拡張のヒント—異なるフォント、背景色、条件付き書式など。

> **前提条件:** Visual Studio 2022（または任意の C# IDE）と Aspose.Cells for .NET の NuGet パッケージ。その他の依存関係は不要です。

---

## ステップ 1: プロジェクトのセットアップと名前空間のインポート

**セルスタイルを作成** する前に、Excel ライブラリへの参照があるプロジェクトが必要です。

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*この点が重要な理由:* `Aspose.Cells` をインポートすると、`Workbook`、`Worksheet`、`Style`、`Border` クラスが利用可能になります。別のライブラリ（例: EPPlus）を使用する場合はクラス名が変わりますが、概念は同じです。

---

## ステップ 2: ワークブックを作成し、最初のセルを取得

まず、フォーマットしたいセルへの参照を取得して **セルスタイルを作成** します。

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

`var` ではなく `Cell` を使用したのは、明示的な型指定が初心者にとってコードを分かりやすくするためです。`PutValue` の呼び出しで文字列を書き込んでいるので、後でスタイル効果を確認できます。

---

## ステップ 3: スタイルを定義 – テキストをセンタリングし、細い枠線を追加

**セルスタイルの作成** の核心です。水平・垂直の配置、細い枠線、いくつかのオプション設定を行います。

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*この操作の目的:*  
- **HorizontalAlignment** と **VerticalAlignment** を組み合わせることで、**セル内テキストのセンタリング** の質問に答えます。  
- 4 方向すべてに枠線を付けることで、ヘッダーなどに適した箱型ラベルになります。  
- 背景色は必須ではありませんが、後でスタイルを拡張できる例として示しています。

---

## ステップ 4: 定義したスタイルを対象セルに適用

スタイルができたら、**セルにスタイルを適用** します。

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

これだけです—Aspose.Cells が内部のスタイルコレクションにコピーしてくれます。範囲全体に同じ書式を適用したい場合は、`ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });` を使用できます。

---

## ステップ 5: ワークブックを保存し、結果を確認

簡単に保存すれば、Excel でファイルを開き、テキストが本当にセンタリングされ枠線が表示されているか確認できます。

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*期待される出力:* **StyledCell.xlsx** を開くと、セル **A1** に「Hello, styled world!」が水平・垂直ともにセンタリングされ、薄いグレーの枠線で囲まれ、薄いグレーの背景色が設定されています。

---

## よくあるバリエーションとエッジケース

### 1. 結合領域内でテキストをセンタリング

セル **A1:C1** を結合した後でもテキストをセンタリングしたい場合は、結合後に左上のセルにスタイルを適用します。

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. 数値書式を使用する

**セルの配置設定** と同時に、特定の数値書式で数字を表示したいケースです。

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

配置はセンタリングされたままで、数値は `12,345.68` と表示されます。

### 3. スタイルの効率的な再利用

各セルごとに新しい `Style` を作成するとパフォーマンスが低下します。代わりに 1 つのスタイルオブジェクトを作成し、複数のセルや範囲で再利用しましょう。`StyleFlag` クラスを使えば、必要な部分だけを適用でき、メモリ使用量を削減できます。

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## プロのコツと注意点

- **垂直方向の配置を忘れずに** – 水平だけセンタリングすると、行が高い場合に見た目が崩れます。  
- **枠線の種類:** `CellBorderType.Thin` はほとんどのレポートで十分ですが、階層を示したいときは `Medium` や `Dashed` に切り替えられます。  
- **カラー処理:** .NET Core を対象とする場合は `System.Drawing.Common` パッケージから `System.Drawing.Color` を使用しないとランタイムエラーになります。  
- **保存形式:** 古い Excel バージョンとの互換性が必要な場合は、`SaveFormat.Xlsx` を `SaveFormat.Xls` に変更してください。

---

![Create cell style example](https://example.com/images/create-cell-style.png "C# でセルスタイルを作成")

*代替テキスト: セルにセンタリングされたテキストと細い枠線が表示されたスクリーンショット（セルスタイル作成チュートリアル）*

---

## 完全動作サンプル（コピー＆ペースト用）

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

このプログラムを実行し、**StyledCell.xlsx** を開くと、前述の結果が確認できます。テキスト、枠線スタイル、背景色などを自由に変更して、ブランドに合わせてカスタマイズしてください。

---

## まとめ

ここまでで、**セルスタイルを作成** し、**セルにスタイルを適用**、そして **セル内テキストを水平・垂直にセンタリング** する方法を学びました。これらの基本ブロックをマスターすれば、ヘッダーの装飾や合計のハイライト、レポートテンプレート全体の構築が C# だけで完結します。

次のステップとしては、以下に挑戦してみてください。

- **行全体に同じスタイルを適用** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`)。  
- **条件付き書式** を追加して、セルの値に応じて背景色を変える。  
- **PDF へエクスポート** し、スタイルを保持したまま配布。

スタイリングは可読性と美観の両方を高める重要な作業です。試行錯誤を重ね、やがてスプレッドシートがコードと同じくらいプロフェッショナルに見えるようになるでしょう。

*Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}