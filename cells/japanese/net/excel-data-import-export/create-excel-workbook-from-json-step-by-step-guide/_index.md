---
category: general
date: 2026-03-25
description: JSON から Excel ワークブックを作成し、ワークブックを xlsx として保存します。JSON を xlsx にエクスポートする方法、JSON
  から Excel を生成する方法、そして数分で JSON から Excel にデータを入力する方法を学びましょう。
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: ja
og_description: JSONから即座にExcelブックを作成します。このガイドでは、JSONをxlsxにエクスポートする方法、JSONからExcelを生成する方法、そしてAspose.Cellsを使用してJSONからExcelにデータを入力する方法を示します。
og_title: JSONからExcelワークブックを作成する – 完全C#チュートリアル
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: JSONからExcelブックを作成する – ステップバイステップガイド
url: /ja/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON から Excel ワークブックを作成 – 完全 C# チュートリアル

JSON ペイロードから **excel workbook を作成** したいけど、どこから手を付ければいいか分からないことはありませんか？ 同じ壁にぶつかる開発者は多いです。API データをきれいなスプレッドシートに変換しようとするときに。朗報です！数行の C# と Aspose.Cells さえあれば、**export json to xlsx**、**generate excel from json**、**populate excel from json** をサードパーティのコンバータを使わずに実現できます。

このガイドでは、RAW な JSON 文字列を SmartMarker に流し込み、最終的に **save workbook as xlsx** でディスクに保存するまでの全工程を順を追って解説します。最後には、次のような Excel ファイルが手に入ります。

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **プロのコツ:** すでにプロジェクト内で Aspose.Cells を使用している場合、同じ `Workbook` インスタンスを複数の JSON インポートに再利用できます。バッチ処理に最適です。

---

## 必要なもの

- **.NET 6+**（または C# 10 をサポートする最近の .NET Framework）
- **Aspose.Cells for .NET** – NuGet でインストール: `dotnet add package Aspose.Cells`
- C# の基本的な構文理解（Excel の深い知識は不要）

以上です。外部サービスや COM インターロップは不要、純粋にマネージドコードだけです。

---

## Step 1: 新しい Excel ワークブックを初期化

まず最初に、フレッシュなワークブックオブジェクトを作成します。空の Excel ファイルを開くイメージです。後でデータを投入します。

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

なぜ新しいワークブックから始めるのか？ クリーンな状態を保証し、前回の実行で残ったスタイルを防ぎ、ファイルサイズを最小に保てます。自動化パイプラインに最適です。

---

## Step 2: インポートしたい JSON データを用意

デモ用に小さな JSON 配列を使用しますが、実際には Web サービス、ファイル、データベースクエリから取得した任意の有効な JSON に置き換えられます。

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

二重エスケープされた引用符（`\"`）に注意してください。これは C# の文字列リテラル構文です。実際のシナリオでは、たとえば次のようにファイルから読み込むことが多いでしょう。

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Step 3: SmartMarker に配列全体を 1 レコードとして扱うよう指示

Aspose.Cells の SmartMarker エンジンはコレクションを自動的に反復処理できます。**ArrayAsSingle** を有効にすると、JSON 配列全体を単一レコードとして扱い、フラットなテーブルを作成できます。

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

このフラグを忘れると、SmartMarker は要素ごとに別シートを作成しようとします。シンプルなテーブルを生成したい場合は絶対に避けたい挙動です。

---

## Step 4: ワークシートに SmartMarker トークンを配置

SmartMarker トークンは `${jsonArray}` のような形です。プロセッサが実行されると、トークンは JSON ソースから取得したデータに置き換えられます。トークンはセル **A1** に配置し、出力が左上から始まるようにします。

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

処理前にヘッダー行を事前に書式設定しても構いません。たとえば、1 行目を太字にする例:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Step 5: SmartMarker プロセッサを実行

ここで魔法が起きます。プロセッサは JSON を読み取り、各プロパティを列にマッピングし、トークンの下に行を書き込みます。

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

内部的には Aspose.Cells が次のことを行います:

1. JSON を .NET オブジェクトにパースする。
2. プロパティ名（`Name`, `Score`）を列ヘッダーにマッチさせる。
3. 各配列要素を新しい行として書き込む。

JSON に入れ子オブジェクトが含まれる場合は、ドット表記（`${parent.child}`）で参照できます。複雑なレポート作成に便利です。

---

## Step 6: ワークブックを XLSX ファイルとして保存

最後に、ワークブックをディスクに永続化します。拡張子 `.xlsx` は Excel（および多くのスプレッドシートアプリ）に対して OpenXML ワークブックであることを示します。

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Web API を作成している場合は、ワークブックを直接 HTTP 応答にストリームすることも可能です:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## 完全動作サンプル

以下は、上記手順すべてを組み込んだ、すぐに実行できるコンソールアプリのコードです。新しいコンソールプロジェクトに貼り付けて **F5** を押すだけです。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**期待される結果:** `json-single.xlsx` を開くと、太字ヘッダーの下に 2 行が表示されます。`John` のスコアは `90`、`Anna` は `85`。列名は JSON のプロパティ名から自動的に推測されます。

---

## よくある質問とエッジケース

### JSON キーにスペースや特殊文字が含まれる場合は？

SmartMarker は有効な識別子名を期待します。スペースはアンダースコアに置き換えるか、カスタムマッピングを使用してください:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### 大量の JSON 配列（数千行）をエクスポートしたい場合は？

プロセッサは内部でストリーミング処理を行うため、メモリ使用量は抑えられます。ただし、次のような調整が有効です:

- ワークシートの `MaxRows` 制限を拡張する（`worksheet.Cells.MaxRow = 1_048_576;` – Excel の最大行数）。
- パフォーマンス向上のためにグリッドラインを非表示にする（`worksheet.IsGridlinesVisible = false;`）。

### 同じブックに複数の JSON テーブルを追加できる？

可能です。別々の範囲に異なる SmartMarker トークン（例: `A10` の `${orders}`、`D1` の `${customers}`）を配置し、トークンごとに `Process` を呼び出すか、両方の配列を含む複合 JSON オブジェクトを渡して一度に処理します。

---

## ボーナス: 簡易チャートの追加（任意）

スコアを可視化したい場合は、データが投入された後に簡単な縦棒グラフを追加できます:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

チャートは自動的に新しく追加された行を参照し、ワンステップで洗練されたレポートが完成します。

---

## 結論

Aspose.Cells の SmartMarker 機能を使って、**JSON 文字列から excel workbook を作成**し、**export json to xlsx**、**generate excel from json**、**populate excel from json** ができるようになりました。ワークブックの初期化、SmartMarker の設定、JSON の処理、ファイル保存という一連の流れは数行のコードで実現でき、巨大データセットにもスケールします。

次のステップは？ 静的な JSON を API 呼び出しに置き換えてみる、スコアに応じた条件付き書式を追加する、あるいはデータドメインごとにシートを分けて生成するなどです。同じパターンは CSV、XML、データベースの結果セットにも応用可能です—ソース文字列を変えて SmartMarker トークンだけ調整すれば OK です。

Happy coding, and may your spreadsheets always be tidy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}