---
category: general
date: 2026-07-03
description: C#でSEQUENCEを使用してExcelに連番を生成する方法。C#およびASP.NETでExcelブックを作成し、数行のコードでExcelファイルを作成する方法を学びましょう。
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: ja
og_description: C#でSEQUENCEを使用してExcelに連番を生成する方法。C# と ASP.NET で Excel ブックを作成し、Excel
  ファイルを生成するステップバイステップガイド。
og_title: C#でSEQUENCEを使用する方法 – Excelワークブックの作成
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: C#でSEQUENCEを使用する方法 – Excelワークブックを作成
url: /ja/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で SEQUENCE を使用する方法 – Excel ワークブックの作成

C# から Excel シートに数値のリストを **SEQUENCE の使い方** で出力したいと思ったことはありませんか？ あなた一人ではありません。レポート ダッシュボードを作成したり、データ グリッドにデータを供給したり、単に ID をすばやく生成したりする場合でも、このテクニックをマスターすればループを書き回す手間が省けます。

このチュートリアルでは **C# で Excel ワークブックを作成** し、セル A1 に `SEQUENCE` 動的配列数式を挿入し、インクリメンタルな数値の列を作ります。また、そのファイルを ASP.NET コントローラから配信する方法も紹介します — **ASP.NET で Excel ファイルを作成** もカバーします。最後には、コード一行で **Excel スタイルのインクリメンタル番号を生成** できるようになります。

## 必要なもの

- .NET 6+（コードは .NET Framework 4.6+ でも動作します）  
- **Aspose.Cells for .NET** NuGet パッケージ（または `Workbook`/`Worksheet` オブジェクトを提供する任意のライブラリ）  
- Web ダウンロード部分を試したい場合は、基本的な ASP.NET Core または MVC プロジェクト  

以上です。COM インタープ、Office のインストールは不要です。

---

## SEQUENCE を使って増分番号を生成する方法

Excel の `SEQUENCE(rows, [columns], [start], [step])` 関数は **スピル** 範囲を返します。ここでは 5 行、1 列、開始値 10、ステップ 2 を指定します。数式は次のようになります。

```excel
=SEQUENCE(5,1,10,2)
```

Excel がこの数式を評価すると、セル A1:A5 には **10, 12, 14, 16, 18** が入ります。C# のループを書かなくても、数式が重い処理を担ってくれるのがポイントです。

以下は、ワークブックを作成し、数式を挿入し、計算を強制し、ファイルを保存する完全な C# スニペットです。

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**期待される出力** – *DynamicArray.xlsx* を開くと次のようになります。

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

これが C# における **SEQUENCE の使い方** の全容です。シンプルですよね？ でももう少し掘り下げてみましょう。

### ループの代わりに SEQUENCE を使う理由

- **パフォーマンス** – Excel が独自のエンジンで計算を行うため、非常に最適化されています。  
- **保守性** – 数式は自己文書化されており、シートを開いた人はすぐに意図を理解できます。  
- **動的リサイズ** – `rows` 引数を変更すれば、スピル範囲が自動的に拡張されます。

---

## C# で Excel ワークブックを作成 – ステップバイステップ

**create excel workbook c#** に不慣れな方は、以下のチェックリストでよくある落とし穴を回避できます。

1. **Aspose.Cells パッケージを追加**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   （ClosedXML や EPPlus でも構いませんが、ここで示す API は上記コードに合わせています。）

2. **ライセンスを設定**（トライアルの場合はオプション）。  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **`Workbook` をインスタンス化** – これで新しい空のワークブックが手に入ります。

4. **ワークシートを参照** – `workbook.Worksheets[0]` がデフォルトシート *Sheet1* です。

5. **SEQUENCE 数式を適用** – 前述の通りです。

6. **計算** – `workbook.CalculateFormula()` でスピルを強制します。これをしないと、ファイルには数式だけが保存されます。

7. **保存** – ディスク、`MemoryStream`、または直接 HTTP 応答に書き込めます。

### プロ・ティップ

メモリ上でワークブックを扱い、Web API で返したい場合は `MemoryStream` を使用します。

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET で Excel ファイルを作成 – ブラウザへストリーミング

**create excel workbook c#** が分かったら、次は ASP.NET Core コントローラに組み込んで、ユーザーがリアルタイムでダウンロードできるようにします。

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

ユーザーが `/api/excel/download` にアクセスすると、ブラウザは *DynamicArray.xlsx* のダウンロードを促します。このファイルには **SEQUENCE 数式** によって生成された **インクリメンタル番号の Excel 列** がすでに含まれています。

### クライアントが古い Excel バージョンを使用している場合は？

動的配列（`SEQUENCE` を含む）は Excel 365/2019 で導入されました。下位互換が必要な場合は、手動で埋める方法にフォールバックします。

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

このスニペットは、**インクリメンタル番号を Excel で生成** する従来のアプローチを示しています。

---

## よくある質問とエッジケース

- **反復計算を有効にする必要がありますか？**  
  いいえ。`SEQUENCE` は非反復関数なので、`CalculateFormula()` だけで十分です。

- **横方向にスピルさせたい場合は？**  
  第2引数を変更します：`=SEQUENCE(1,5,10,2)` は B1:F1 に横方向に展開します。

- **SEQUENCE を他の関数と組み合わせられますか？**  
  もちろんです。例：`=INDEX(A:A, SEQUENCE(5,1,10,2))` で別列から行を取得できます。

- **ワークブックのサイズは問題になりますか？**  
  数式自体のサイズ影響は無視できる程度です。手動で何百万ものセルにデータを書き込むときだけサイズが問題になります。

---

## 結論

C# で **SEQUENCE の使い方** を利用して **Excel ワークブックを作成** し、**ASP.NET で Excel ファイルを作成** して配信し、**インクリメンタル番号を Excel スタイルで生成** する方法を解説しました。重要なポイントは、Excel の動的配列エンジンにカウントを任せ、.NET のコードはオーケストレーションに集中させることです。

ぜひ実験してみてください — `rows`、`start`、`step` を変えたり、横方向にスピルさせたり、`IF` や `FILTER` と組み合わせて高度なレポートを作ったり。準備ができたら、複数シートを連結したり、CSV としてエクスポートして下流システムに渡したりしてみましょう。

ツイストやアイデアがあればコメントで共有してください。GitHub でも気軽に ping してください。Happy coding!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを発展させた関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Aspose.Cells .NET で Excel ワークブックを作成・構成する方法：ステップバイステップ ガイド](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells for .NET で Excel ファイルを作成・保存する完全ガイド](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Aspose.Cells for .NET（2023 年ガイド）で Excel ワークブックを作成・スタイル設定する方法](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}