---
category: general
date: 2026-02-15
description: C#でフォントをコピーし、セルスタイルを適用する方法（簡単な例付き）。セルスタイルの取得方法と、セルの書式設定を使用してテキストボックスのフォントサイズを設定する方法を学びます。
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: ja
og_description: ワークシートのセルからフォントをコピーしてテキストボックスにセルスタイルを適用する方法。このガイドでは、セルスタイルの取得、セルの書式設定の使用、テキストボックスのフォントサイズの設定方法を示します。
og_title: Excelセルからフォントをコピーする方法 – 完全なC#チュートリアル
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Excelセルからテキストボックスへフォントをコピーする方法 – ステップバイステップガイド
url: /ja/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel のセルからフォントをコピーして TextBox に適用する方法 – 完全 C# チュートリアル

スプレッドシートのセルから **フォントをコピー** して、UI のテキストボックスをまったく同じ見た目にしたいこと、ありませんか？ あなただけではありません。多くのレポーティングツールやカスタムダッシュボードでは、Excel からデータを取得し、フォントファミリー、サイズ、カラーといった視覚的な忠実度を保つ必要があります。  

良いニュースは、数行の C# コードだけで **セルのスタイルを取得** し、フォントプロパティを読み取り、**セルのスタイルを適用** できることです。このチュートリアルでは、**セルの書式設定を使用** し、さらに **プログラムでテキストボックスのフォントサイズを設定** する完全な実行可能サンプルを順を追って解説します。

---

## 学べること

- グリッドコンポーネント（サンプルでは `gridJs`）から `TextBox` オブジェクトを取得する方法  
- 特定の Excel セル（`B2`）からフォントファミリー、サイズ、カラーを読み取る方法  
- 取得したフォント属性をテキストボックスにコピーし、UI をスプレッドシートと同一にする方法  
- カラー変換などの一般的な落とし穴と、コードを堅牢に保つための **プロのコツ**  
- コンソールアプリや WinForms プロジェクトにそのまま貼り付けられる実行可能コードスニペット  

**前提条件**  
以下がインストール済みであること：

1. .NET 6+（または .NET Framework 4.8）  
2. EPPlus NuGet パッケージ（Excel 操作用）  
3. `TextBoxes` 辞書を公開するグリッドコントロール（例では架空の `gridJs` を使用していますが、任意の UI ライブラリでも同様に機能します）

それでは、実装に取り掛かりましょう。

---

## Step 1: Set Up the Project and Load the Worksheet

まず、コンソールまたは WinForms プロジェクトを新規作成し、EPPlus を追加します。

```bash
dotnet add package EPPlus --version 6.*
```

次に、ブックを読み込み、コピーしたいスタイルを持つセルを取得します。

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**ポイント:** EPPlus は `Style` オブジェクトへの直接アクセスを提供し、その中に `Font` サブオブジェクトがあります。ここから `Name`、`Size`、`Color` を取得でき、これが **セルのスタイル取得** の核となります。

---

## Step 2: Grab the Target TextBox from Your Grid

UI グリッド（`gridJs`）が列名をキーとした辞書でテキストボックスを管理していると仮定すると、以下のように目的のテキストボックスを取得できます。

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

WinForms では `notesTextBox` が `TextBox` コントロール、WPF では `TextBox` 要素、Web ベースのグリッドでは JavaScript インターオップオブジェクトになるでしょう。重要なのは、操作可能な参照を取得できていることです。

---

## Step 3: Transfer the Font Family

ソースのスタイルと宛先コントロールが揃ったので、フォントファミリーをコピーします。

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**プロ tip:** すべての UI フレームワークが文字列を受け取る `FontFamily` プロパティを公開しているわけではありません。WinForms では `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);` のように設定します。使用しているフレームワークに合わせて調整してください。

---

## Step 4: Transfer the Font Size

フォントサイズは EPPlus では `float` 型で保持されています。そのまま適用します。

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

多くのコントロールはポイント単位を使用するため、変換なしで代入できます。CSS ベースのグリッドの場合は `"pt"` を付加する必要があるかもしれません。

---

## Step 5: Transfer the Font Colour

カラー変換は最も手間がかかります。EPPlus はカラーを ARGB 整数で保持しますが、UI フレームワークは `System.Drawing.Color` や CSS の HEX 文字列を期待することが多いです。

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **動作の理由:** `GetColor()` はテーマベースのカラーを解決し、具体的な `System.Drawing.Color` を返します。セルがデフォルトカラー（明示的な設定なし）を使用している場合は、null 参照例外を防ぐために黒をデフォルトとして使用します。

---

## Full Working Example

すべてを組み合わせた最小コンソールアプリです。Excel ファイルを読み取り、**B2** のフォントを取得し、モックテキストボックスに適用します。

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**期待される出力（B2 が Arial、12 pt、青の場合）**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

プログラムを実行し、UI を開くと「Notes」テキストボックスがセル **B2** と同じフォントスタイルになっているはずです。手動で調整する必要はありません。

---

## Frequently Asked Questions & Edge Cases

### セルが明示的な RGB 値ではなくテーマカラーを使用している場合は？

EPPlus の `GetColor()` はテーマカラーを具体的な `System.Drawing.Color` に自動変換します。ただし、古いライブラリでテーマインデックスしか返さない場合は、自前でパレットマッピングを実装する必要があります。

### 太字や斜体など、他のスタイル属性もコピーできますか？

もちろん可能です。`ExcelStyle.Font` オブジェクトは `Bold`、`Italic`、`Underline`、`Strike` も公開しています。対応する UI プロパティに設定すれば OK です。

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### グリッドコントロールが `FontColor` プロパティを持っていない場合は？

多くのモダン UI フレームワークは対応していますが、CSS 文字列しか受け付けない場合は `Color` を HEX に変換します。

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### 複数セルを一括で処理したい場合は？

対象範囲をループし、各セルのスタイルを取得して対応するテキストボックスに適用します。多数の行を処理する場合は、スタイルオブジェクトをキャッシュしてパフォーマンス低下を防ぎましょう。

---

## Pro Tips & Common Pitfalls

- **ExcelPackage をキャッシュ** – セルごとにファイルを開閉するとコストが高くなります。ブックは一度だけ読み込み、`ExcelWorksheet` オブジェクトを再利用してください。  
- **null カラーに注意** – デフォルトカラーを継承しているセルは `null` を返すことがあります。必ずフォールバック（黒またはコントロールの既定色）を用意しましょう。  
- **DPI スケーリングに留意** – 高 DPI モニター向けにフォントが大きく見えることがあります。必要に応じて `Graphics.DpiX` で調整してください。  
- **スレッド安全性** – EPPlus はスレッドセーフではありません。並列処理が必要な場合は、スレッドごとに別々の `ExcelPackage` インスタンスを作成してください。

---

## Conclusion

これで **Excel のセルからフォントをコピー** し、C# で **セルのスタイルを任意のテキストボックスに適用** する方法が分かりました。セルの `Style` を取得し、`Font` プロパティを抽出、UI 要素に割り当てることで、手作業の調整なしに視覚的一貫性を保てます。  

本稿の完全ソリューションは、ブックの読み込み、セルスタイル取得、テキストボックスへのフォントファミリー・サイズ・カラー設定という **セル書式設定の使用** と **テキストボックスのフォントサイズ設定** のコア部分を網羅しています。  

次のステップとして、背景色や罫線、セル内容全体のコピーに拡張してみてください。リッチセルレンダリングをサポートするデータグリッドライブラリを使用している場合、Excel から取得した同一スタイリング情報をそのまま供給でき、UI とレポートの完全な同期が実現します。  

質問があればコメントを残すか、関連記事「動的 Excel‑to‑UI バインディング」や「テーマ対応カラー変換」もぜひご覧ください。Happy coding!

---

![Excel のセルからフォントをコピーして TextBox に適用する例](placeholder-image.jpg "Excel のセルからフォントをコピーして TextBox に適用する方法")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}