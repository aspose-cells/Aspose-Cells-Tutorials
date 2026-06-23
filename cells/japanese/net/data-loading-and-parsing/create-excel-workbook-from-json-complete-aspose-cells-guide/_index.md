---
category: general
date: 2026-02-14
description: Aspose.Cells を使用して Excel ワークブックを作成し、JSON の処理方法、JSON を Excel に変換する方法、JSON
  を Excel にロードする方法を簡単な手順で学びましょう。
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: ja
og_description: Aspose.CellsでExcelブックを作成し、JSONの処理方法を学び、JSONをExcelに変換し、JSONをExcelに迅速かつ確実にロードします。
og_title: JSONからExcelブックを作成 – ステップバイステップ Aspose.Cells チュートリアル
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: JSONからExcelブックを作成する – 完全なAspose.Cellsガイド
url: /ja/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON から Excel ワークブックを作成 – 完全 Aspose.Cells ガイド

JSON の一部から **Excel ワークブックを作成** したいと思ったことはありませんか？ でも、どこから始めればいいか分からないことも多いでしょう。JSON ペイロードがあり、レポートやデータ交換のためにきれいなスプレッドシートが必要になる開発者は多いです。  

良いニュースです。**Aspose.Cells** を使えば、その JSON を数行のコードでフル機能の Excel ファイルに変換できます。このチュートリアルでは、**JSON の処理方法**、**JSON から Excel への変換**、そして強力な `SmartMarkerProcessor` を使用した **JSON の Excel へのロード** を順を追って解説します。最後まで読めば、保存可能なワークブックが手に入り、調整できるオプションの全体像がつかめます。

## 学べること

- JSON 処理のために Aspose.Cells プロジェクトをセットアップする方法。  
- JSON 配列から **Excel ワークブックを作成** するために必要な正確なコード。  
- `ArrayAsSingle` オプションが重要になる理由と、変更すべきタイミング。  
- 大規模な JSON 構造の取り扱い、エラーハンドリング、ファイル保存のコツ。  

> **前提条件:** .NET 6+（または .NET Framework 4.6+）、Aspose.Cells for .NET NuGet パッケージ、C# の基本的な理解。その他のライブラリは不要です。

---

## 手順 1: Aspose.Cells をインストールし、必要な名前空間を追加

コードを実行する前に、プロジェクトに Aspose.Cells ライブラリを参照設定してください。

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **プロのコツ:** Visual Studio を使用している場合、NuGet パッケージ マネージャー UI でも同様にインストールできます。*Aspose.Cells* を検索して **Install** をクリックするだけです。

---

## 手順 2: 変換したい JSON データを用意

`SmartMarkerProcessor` は任意の JSON 文字列で動作しますが、配列の解釈方法を決める必要があります。この例では、単純な数値配列を **単一レコード** として扱います。フラットな値リストが欲しいときに便利です。

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **なぜ重要か:** デフォルトでは、Aspose.Cells は各配列要素を個別のレコードとして扱います。`ArrayAsSingle = true` を設定すると、配列全体が 1 つのレコードにまとめられ、レポートシナリオにマッチします。

---

## 手順 3: 新しい Workbook インスタンスを作成

ここで実際にメモリ上に **Excel ワークブックを作成** します。まだファイルは書き込まれていません。コンテナの準備だけです。

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

この時点で `workbook.Worksheets[0]` は *Sheet1* という名前の空白シートです。必要に応じて後で名前を変更できます。

---

## 手順 4: JSON 処理用に SmartMarker オプションを設定

`SmartMarkerOptions` クラスを使うと、JSON の解釈方法を細かく制御できます。今回のシナリオで重要なのは `ArrayAsSingle` フラグです。

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **変更すべきタイミング:** JSON が行のコレクション（例: オブジェクトの配列）を表す場合は、`ArrayAsSingle` を `false` のままにします。各オブジェクトが自動的に新しい行になります。

---

## 手順 5: ワークシートで Smart Marker 処理を実行

ワークブックとオプションの準備ができたら、JSON をプロセッサに渡します。プロセッサはワークシート内のスマートマーカー（プレースホルダー）を走査し、JSON のデータで置き換えます。明示的なマーカーが無い場合、プロセッサはデフォルトのレイアウトを作成します。

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

データ開始セルを正確に指定したい場合は、セル **A1** に `"${Array}"` のようなマーカーを事前に追加できます。このチュートリアルではデフォルト動作に任せ、配列の値が **A1** から連続したセルに書き込まれます。

---

## 手順 6: ワークブックをディスク（またはストリーム）に保存

最終ステップはワークブックの永続化です。ファイル、メモリストリーム、あるいは Web API から直接返すことも可能です。

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

プログラム全体を実行すると、数値 **1**, **2**, **3** がそれぞれセル **A1**, **A2**, **A3** に配置された Excel ファイルが生成されます。

---

## 完全動作サンプル

以下は、すべての手順をまとめたコンソール アプリケーションの完全版です。新しい C# コンソール プロジェクトに貼り付けて **F5** を押すだけで動作します。

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Excel での期待出力**

| Numbers |
|---------|
| 1       |
| 2       |
| 3       |

ヘッダー行（「Numbers」）は任意ですが、手動セル編集とスマートマーカー処理を組み合わせる例として示しています。

---

## よくある質問とエッジケース

### JSON が配列ではなくオブジェクトの場合は？

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

`SmartMarkerProcessor` は引き続き使用可能です。ワークシートに `${Name}`, `${Age}`, `${Country}` などのマーカーを配置し、`StartSmartMarkerProcessing` を呼び出します。プロセッサが各マーカーを対応する値に置き換えます。

### 大容量（数 MB）の JSON ファイルを扱うには？

- **JSON をストリームで処理:** 文字列全体をロードせず、`StreamReader` で読み込み、テキストを `StartSmartMarkerProcessing` に渡す。  
- **メモリ上限を増やす:** `OutOfMemoryException` が出た場合は `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` を設定。  
- **チャンク処理:** JSON を小さな配列に分割し、各チャンクを新しいワークシートで処理。

### XLSX ではなく CSV にエクスポートしたい？

もちろん可能です。処理後に次のコードを呼び出すだけです。

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

データ配置は同じで、ファイル形式だけが CSV に変わります。

### JSON 読み込み後にセルの書式（フォント、色）を設定したい？

スマートマーカー処理の後に書式を適用します。

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

プロセッサが先に実行されるため、後から適用した書式は上書きされません。

---

## ヒントとベストプラクティス

- **`ArrayAsSingle` は必ず意図的に設定** – このフラグを忘れると予期しない行重複が発生しやすいです。  
- **JSON のバリデーションを先に実施** – 不正な文字列は `JsonParseException` をスローします。`try/catch` でラップしてエラーハンドリングを行いましょう。  
- **名前付きスマートマーカー**（`${Orders}`）を使用すると、入れ子オブジェクトを扱う際の可読性が向上します。  
- **Web API から返す場合はメモリ上に保持**; `MemoryStream` を返すことで不要なディスク I/O を回避できます。  
- **バージョン互換性:** 上記コードは Aspose.Cells 23.12 以降で動作します。古いバージョンを使用している場合はリリースノートを確認してください。

---

## まとめ

このガイドでは、Aspose.Cells を使って **JSON から Excel ワークブックを作成** する方法を、ライブラリのインストールから最終保存まで網羅的に解説しました。`SmartMarkerProcessor` とそのオプションをマスターすれば、**JSON を Excel にロード**、**JSON を Excel に変換**、さらには複雑なレポートシナリオ向けに出力をカスタマイズすることも可能です。  

次のステップに進みませんか？ 入れ子になったオブジェクト配列を試したり、条件付き書式を追加したり、結果を PDF にエクスポートしたり、すべて同じ Aspose.Cells API で実現できます。これでデータから Excel へのパイプラインは数行のコードで完成です。  

質問や問題があれば、下のコメント欄に投稿してください。コーディングを楽しみながら、JSON を美しいスプレッドシートに変換しましょう！ 

![Create Excel workbook with JSON data](/images/create-excel-workbook-json.png "Illustration of a JSON array being transformed into an Excel sheet")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}