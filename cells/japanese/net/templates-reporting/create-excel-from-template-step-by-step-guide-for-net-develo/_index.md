---
category: general
date: 2026-05-04
description: テンプレートからExcelを作成し、JSONをExcelにマッピングしてシート名を動的に設定します。JSONからExcelにデータを入力し、数分でJSONを使用してExcelを生成する方法を学びましょう。
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: ja
og_description: テンプレートから素早くExcelを作成します。このガイドでは、JSONをExcelにマッピングする方法、JSONからExcelを入力する方法、動的なワークシート名の使用方法、そしてJSONを使用してExcelを生成する方法を示します。
og_title: テンプレートからExcelを作成 – 完全な.NETチュートリアル
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: テンプレートからExcelを作成する – .NET開発者向けステップバイステップガイド
url: /ja/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# テンプレートから Excel を作成 – 完全 .NET チュートリアル

**テンプレートから Excel を作成**したいけど、JSON データとワークシート名の扱いに悩んでいませんか？同じような経験をした人はたくさんいます。多くのレポート作成プロジェクトでは、レイアウトはテンプレートが保持し、実際の値は JSON ペイロードが駆動しますが、両者を連携させるのは頭痛の種です。  

良いニュースは、数行の C# と Aspose Cells の SmartMarker エンジンさえあれば、**JSON から Excel を埋め込み**、詳細シートの名前を動的に変更し、UI に触れることなく **JSON で Excel を生成**できるということです。  

このチュートリアルでは、テンプレートの読み込み、JSON のマッピング、動的ワークシート名の設定、最終ブックの保存という一連の流れを解説します。最後まで読めば、任意の .NET サービスに貼り付けられる再利用可能なコードスニペットが手に入ります。外部ツールは不要、純粋にコードだけです。

---

## 必要なもの

- **Aspose.Cells for .NET**（v24.10 以降） – SmartMarker を提供するライブラリ。
- `{Master:Name}` や `{Detail:Item}` といった SmartMarker タグが埋め込まれた **template.xlsx** ファイル。
- マスタ‑詳細構造に合わせた **data.json** ファイル。
- .NET 6 以降を対象とした Visual Studio 2022（またはお好みの IDE）。

以上です。これらが揃っていれば、すぐに始められます。

---

## テンプレートから Excel を作成 – 概要

基本的な考え方はシンプルです。Excel ファイルを *テンプレート* とみなし、SmartMarker がプレースホルダーを JSON の値で置き換えます。さらに、ライブラリはマスターフィールドに基づいて詳細シートの名前を変更でき、**動的ワークシート命名 excel** の機能が光ります。

以下がそのまま実行可能なコードです。コンソールアプリにコピペし、パスを自分のファイルに合わせるだけで動作します。

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **期待される結果:**  
> - マスターシートに `Master.Name` の名前が表示されます。  
> - 詳細シートの名前が `Detail_JohnDoe` のように変更されます。  
> - すべての `{Detail:Item}` 行が JSON の items 配列で埋められます。

---

## JSON を Excel にマップ – データの読み込み

SmartMarker エンジンが魔法をかける前に、JSON は **正しく構成**され、テンプレートで使用する階層と一致している必要があります。典型的なマスタ‑詳細 JSON は次のようになります。

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**重要ポイント:**  
- キー `Master` と `Detail` はそれぞれ `{Master:…}` と `{Detail:…}` タグに直接対応します。  
- JSON 構造がずれると、SmartMarker は一致するタグを見つけられず、セルは空白のままになります。  

**ヒント:** オンラインバリデータや `System.Text.Json.JsonDocument.Parse(json)` を使って、構文エラーを早期に検出しましょう。

---

## JSON から Excel を埋め込む – SmartMarker 設定

SmartMarker はブック内のタグを走査し、データを注入します。**populate excel from json** のステップは先ほどの `Execute` 呼び出しに相当しますが、いくつか便利なオプションがあります。

| 設定 | 機能 | 使用シーン |
|------|------|------------|
| `Options.CaseSensitive` | タグ名を大文字小文字を区別して扱う。 | テンプレートで大文字小文字が混在し、厳密な一致が必要な場合。 |
| `Options.RemoveEmptyRows` | データが入らなかった行を削除する。 | 詳細項目がオプションで、最終シートをすっきりさせたいとき。 |
| `Options.EnableHyperlink` | JSON 内の URL をクリック可能なハイパーリンクに変換する。 | レポートにリンクを埋め込みたい場合。 |

これらは次のようにチェーンできます。

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## 動的ワークシート命名 Excel – 詳細シート名の設定

多くのプロジェクトで要求されるやや高度な要件が **動的ワークシート命名 excel** です。固定の “Detail” シートではなく、顧客名や注文番号などをシート名に含めたいことがあります。

次の行：

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

はまさにそれを実現します。プレースホルダー `{Master.Name}` は JSON が処理された *後* に置き換えられるため、新しいシート名は `Detail_JohnDoe` になります。  

**エッジケース:** シート名に使用できない文字（`:`、`\`、`/`、`?`、`*`、`[`、`]`）が含まれる場合、Aspose が自動でサニタイズします。特定の形式が必要な場合は、JSON 側で事前に文字列をクリーンアップしてください。

---

## JSON を使用して Excel を生成 – 実行と保存

コードの最後の 2 行（`Execute` と `Save`）が **generate excel using json** の核心です。内部では Aspose が JSON をデータテーブルに変換し、テンプレートを走査して出力ファイルを書き込みます。

複数のブックをループで生成したい場合（例: 顧客ごとに 1 つずつ）、`Workbook` のインスタンス化をループ内部に移し、出力ファイル名を動的に変更すれば OK です。

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

このパターンはバッチレポートサービスでよく使われます。

---

## よくある落とし穴とプロのコツ

- **タグが見つからない:** セルに `{Master:Name}` がそのまま残っている場合、タグが認識されていません。スペルと、タグがセル内にあるか（コメントではないか）を確認してください。  
- **大容量 JSON:** データ量が膨大な場合は、JSON をストリーミングしたり、文字列ではなく `DataTable` を使用してメモリ負荷を軽減しましょう。  
- **スレッド安全性:** `Workbook` インスタンスはスレッドセーフではありません。並列処理を行う場合は、スレッドごとに新しいインスタンスを作成してください。  
- **ファイルロック:** コード実行中にテンプレートが Excel で開かれていると `IOException` が発生します。必ずテンプレートは閉じた状態で実行しましょう。

> **プロ tip:** テンプレートのオリジナルは読み取り専用フォルダーに保存しておくと、デバッグ時の誤上書きを防げます。

---

## 完全動作サンプルのまとめ

改めて、全コードをコメント付きで示します。非自明な行すべてにインラインコメントを入れています。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

このコンソールアプリを実行すると、`output.xlsx` が生成され、詳細シートがリネームされ、すべてのデータが埋め込まれます。

---

## 次のステップと関連トピック

- **PDF へのエクスポート:** ワークブック生成後に `wb.Save("report.pdf", SaveFormat.Pdf);` を呼び出すだけで PDF 版を出力できます。  
- **チャートへのデータ注入:** SmartMarker はチャートのデータソースもサポートしています。JSON 配列をチャートの系列範囲にバインドすれば OK。  
- **条件付き書式:** テンプレート側で Excel の組み込みルールを設定しておけば、SmartMarker 置換後もそのまま残ります。  
- **パフォーマンスチューニング:** 高負荷シナリオでは、`Workbook` インスタンスを `Clone` して再利用し、ファイル I/O を削減すると効果的です。

JSON 構造やリネームパターンを変えて実験したり、複数テンプレートを組み合わせてみたりしてください。**create excel from template** を Aspose.Cells で実装すれば、請求書、ダッシュボード、あらゆるレポートに柔軟に対応できます。

---

## ビジュアルサマリー

![Create Excel from Template workflow showing JSON → SmartMarker → Dynamic Sheet Naming](/images/create-excel-from-template-workflow.png "Create Excel from Template workflow diagram")

*(Alt テキストに主要キーワードを含めて SEO 対策)*

---

### まとめ

**テンプレートから Excel を作成**、**JSON を Excel にマップ**、**JSON から Excel を埋め込む**、**動的ワークシート命名 excel**、そして **JSON で Excel を生成** するために必要なすべてを網羅しました。コードは完成形で、各行の意図も解説済みです。これで、より大規模なレポートパイプラインを構築する土台が整いました。

実装上の疑問やカスタマイズしたい点があれば、下のコメント欄で教えてください。一緒に解決していきましょう。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}