---
category: general
date: 2026-02-26
description: C# を使用して Excel をタブ区切りの txt ファイルにエクスポートする方法。Excel をタブとしてエクスポート、Excel を
  txt に変換、区切り文字付きで Excel をエクスポートする 3 つの簡単なステップを学びましょう。
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: ja
og_description: C# を使用して Excel をタブ区切りの txt ファイルにエクスポートする方法。このチュートリアルでは、Excel をタブとしてエクスポートする方法、Excel
  を txt に変換する方法、区切り文字付きで Excel をエクスポートする方法を示します。
og_title: Excelのエクスポート方法 – タブ区切りテキストガイド
tags:
- csharp
- excel
- file-conversion
title: Excelのエクスポート方法 – タブ区切りテキストガイド
url: /ja/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

.

Be careful to preserve markdown syntax exactly.

Let's craft translation.

Will keep code block placeholders as they are.

Will keep shortcodes at start and end.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel のエクスポート方法 – 完全 C# チュートリアル

スプレッドシートの書式を失わずに **Excel のデータをプレーンテキストファイルにエクスポート** したいと思ったことはありませんか？データパイプライン用に TSV（タブ区切り値）がすぐに必要だったり、`.txt` のみを読み取るレガシーシステムにデータを供給したりするケースがあります。どちらにせよ、スプレッドシートからデータを外部に出す際に壁にぶつかる開発者は少なくありません。

良いニュースです！たった 3 つのシンプルな手順で **Excel をタブ区切りテキストとしてエクスポート** し、**Excel を txt に変換** でき、後から考えが変わってもカスタム区切り文字を選択できます。以下に完全に実行可能な C# のサンプルと、各行が重要な理由、そして一般的な落とし穴を回避するためのヒントを示します。

> **Pro tip:** この手法は人気の Aspose.Cells ライブラリで動作しますが、`ExportTable` 系のメソッドを提供する任意の .NET Excel API にも概念は適用できます。

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。コードは最新のランタイムでコンパイル可能です。
- **Aspose.Cells for .NET**（無料トライアルまたはライセンス版）。NuGet でインストール: `dotnet add package Aspose.Cells`。
- `input.xlsx` という名前の入力ブックを、管理できるフォルダーに配置しておくこと。
- 少しの好奇心—Excel の内部構造を深く知る必要はありません。

これらが揃っていれば、すぐに解決策に取り掛かりましょう。

## Step 1 – エクスポートしたいブックをロード

まず、ソースファイルを指す `Workbook` オブジェクトを作成します。このオブジェクトはすべてのワークシート、名前付き範囲、書式情報を含む Excel ファイル全体を表します。

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*なぜ重要か:*  
ブックをロードすることでワークシートコレクション（`workbook.Worksheets`）にアクセスできるようになります。このオブジェクトがなければセルや範囲、エクスポート設定を指定できません。

> **Note:** ファイルがネットワーク共有上にある場合は `\\` を先頭に付けるか UNC パスを使用してください—Aspose.Cells は問題なく処理します。

## Step 2 – エクスポートオプションを設定（文字列として扱う & タブ区切り）

次に、データを書き出す方法をライブラリに指示します。`ExportAsString = true` と設定することで、すべてのセルがプレーン文字列として扱われ、ロケール固有の数値書式が除去されます。`Delimiter = "\t"` の部分が **Excel をタブでエクスポート** する核心です。

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*なぜ重要か:*  
`ExportAsString` を省略すると、`12345` のようなセルがロケールによっては `12,345` と変換され、下流のパーサが壊れる可能性があります。区切り文字は後からカンマやパイプなど任意の文字に変更でき、**タブ以外の区切り文字で Excel をエクスポート** したい場合にも対応できます。

## Step 3 – 特定の範囲をテキストファイルへエクスポート

最後に、対象範囲（この例では `A1:D10`）を選択し、`out.txt` に書き出します。`ExportTable` メソッドが重い処理をすべて担い、セルを読み取り、オプションを適用し、結果をディスクにストリームします。

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

実行後、`out.txt` の内容は次のようになります：

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

各列は **タブ** で区切られているため、`awk`、`PowerShell`、またはタブを認識する任意の CSV 互換ツールでそのまま利用できます。

### Quick Verification

生成されたファイルをプレーンテキストエディタ（Notepad、VS Code など）で開き、以下を確認してください：

1. 「空白文字を表示」モードにすると列が揃っていること。
2. 余分な引用符やカンマが出ていないこと。
3. すべての数値セルが Excel と同じ表示になっていること（`ExportAsString` の効果）。

何かおかしいと感じたら、元ブックで行や列が非表示になっていないか、正しいワークシートインデックスを参照しているかを再確認してください。

## Common Variations & Edge Cases

### Exporting an Entire Worksheet

シート全体を **Excel の範囲としてエクスポート** したい場合は、`sheet.Cells.MaxDisplayRange` を使用できます：

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Using a Different Delimiter

タブからパイプ（`|`）へ切り替えるのは、1 行変更するだけです：

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

これで **タブ以外の区切り文字で Excel をエクスポート** するシナリオにもコードを書き換える必要がなく対応できます。

### Handling Large Files (> 100 MB)

巨大なブックの場合は、メモリにすべて読み込まないようにストリーミングでエクスポートします：

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Converting Multiple Sheets in One Pass

複数シートを **Excel を txt に変換** したい場合は、シートをループ処理します：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

シートごとに個別の TSV ファイルが生成されるので、バッチ処理に便利です。

## Full Working Example (Copy‑Paste Ready)

以下はコンパイル可能な完全プログラムです。ファイルパスだけ自分の環境に合わせて置き換えてください。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Expected output:** 各列がタブ文字で区切られ、すべてのセル値が Excel と同じ表示になる `out.txt` が生成されます。

## Frequently Asked Questions

- **Does this work with .xls files?**  
  はい。Aspose.Cells はフォーマットを自動検出するので、古い `.xls` ファイルを `Workbook` に渡すだけで同じコードが動作します。

- **What if my data contains tabs?**  
  セル内のタブはそのまま保持されるため、TSV パーサが壊れる可能性があります。その場合は `exportOptions.Delimiter` をパイプ（`|`）などに変更してください。

- **Can I export formulas instead of values?**  
  `exportOptions.ExportAsString = false` に設定し、`ExportFormula = true` を含む `ExportTableOptions` のオーバーロードを使用します。出力には生の数式テキストが含まれます。

- **Is there a way to skip hidden rows?**  
  はい。`exportOptions.ExportHiddenRows = false`（既定は `true`）を設定すれば、非表示行は最終テキストファイルに含まれません。

## Conclusion

これで **Excel のデータをタブ区切りテキストとしてエクスポート** する、**Excel をタブでエクスポート** する、そして **Excel を txt に変換** するための、デリミタや範囲選択をフルコントロールできる実践的レシピが完成しました。Aspose.Cells の `ExportTable` メソッドを活用すれば、手動で CSV を組み立てる手間が省け、データの忠実性を保ちつつコードベースをすっきり保てます。

次のチャレンジに挑戦してみませんか？

- Web API 用に `MemoryStream` へ直接エクスポートする。  
- 先頭行の内容からヘッダー行を動的に生成する。  
- 新しい Excel アップロードを監視する Azure Function にこの処理を組み込む。

ぜひ試してみて、区切り文字を調整し、データを好きな場所へ流してください。Happy coding!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}