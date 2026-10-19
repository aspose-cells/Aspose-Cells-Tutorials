---
category: general
date: 2026-09-21
description: C# で SmartMarkerOptions の ArrayAsSingle を設定し、JSON 配列を Excel ワークブックの単一セル値としてエクスポートする。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: ja
lastmod: 2026-09-21
og_description: C#でSmartMarkerOptionsのArrayAsSingleを設定し、JSON配列を単一セルの値としてエクスポートします。完全なステップバイステップの解決策をご覧ください。
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: C#でSmartMarkerOptionsのArrayAsSingleを設定する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#でJSON配列用にSmartMarkerOptionsのArrayAsSingleを設定する
url: /ja/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で SmartMarkerOptions の ArrayAsSingle を設定して JSON 配列を扱う方法

Excel ファイルを Aspose.Cells で生成する際に **SmartMarkerOptions の ArrayAsSingle を設定** したい場合は、このガイドで手順を確認できます。JSON 配列を複数行に分割せず、1 つのセルにそのまま保持する方法を紹介します。

スプレッドシートで JSON データを扱うときは、フラットな表示とコンパクトな表現のどちらかを選択する必要があります。タグのリストや識別子の集合などを保存するシナリオでは、JSON 文字列全体を 1 つのセルに保持したいことが多いです。`SmartMarkerOptions` の **ArrayAsSingle** フラグがそれを可能にします。

このチュートリアルで学べること:

* JSON 配列を保持した列を持つ `DataTable` を作成する
* Excel ワークシートに Smart Marker を配置する
* **SmartMarkerOptions の ArrayAsSingle を設定** して JSON 配列を単一セルの値として扱う
* マーカーを処理し、ブックを保存する
* 出力結果を確認する

> **前提条件** – Aspose.Cells for .NET ライブラリ（v23.12 以降）と .NET 開発環境（Visual Studio 2022 推奨）が必要です。C# と DataTable の基本的な知識が前提となります。

---

## 手順 1: JSON 配列を含むデータ ソースを準備する

まず、サービスやデータベースから取得したデータを模倣する `DataTable` を作成します。**Names** 列には、名前の配列を表す JSON 文字列が格納されます。

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*この手順の目的*  
Smart Marker は .NET オブジェクトから直接データを読み取ります。JSON 配列を文字列列に入れることで、正確な JSON 構文を保持したままセルに書き込めます。

---

## 手順 2: 新しいブックに Smart Marker を挿入する

新規ブックを作成し、最初のワークシートを選択して、テーブル全体と **Names** 列を参照する Smart Marker を記述します。

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

マーカー `&=dataTable.Names` は、`dataTable` の各行の **Names** 列の値でセルを置き換えるよう Aspose.Cells に指示します。行が 1 行だけなので、マーカーは 1 回だけ処理されます。

---

## 手順 3: **SmartMarkerOptions の ArrayAsSingle を設定する**

既定では、Aspose.Cells は配列のような文字列を別々の行に展開します。`ArrayAsSingle` を `true` に設定すると、この動作が上書きされ、JSON 文字列全体が単一セルに残ります。

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*`ArrayAsSingle` を有効にする理由*  
`ArrayAsSingle` が `false` の場合、エンジンは `["Alice","Bob"]` を 2 つの別々の値として解釈し、隣接する行に書き込みます。`true` にすると文字列全体が原子値として扱われ、Excel 内で JSON 形式を保持できるようになります。

---

## 手順 4: 設定したオプションで Smart Marker を処理する

先ほど設定したオプション オブジェクトを渡して、Smart Marker エンジンを実行します。

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

処理中、Aspose.Cells は `dataTable` を読み取り、マーカーを適用し、`ArrayAsSingle` フラグを尊重して JSON 配列をそのまま残します。

---

## 手順 5: ブックを保存し、結果を確認する

最後にブックをディスクに書き出します。生成されたファイルを Excel などのスプレッドシートビューアで開き、セル **A2** に正確な JSON 文字列が入っていることを確認してください。

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### 期待される出力

| A   |
|-----|
| **["Alice","Bob"]** |

セル **A2** には JSON 配列が単一のテキスト値として表示され、`DataTable` に格納されたままです。余分な行は作成されません。

---

## よくあるバリエーションとエッジケースの対処

| 状況 | 対応方法 |
|-----------|--------------|
| **JSON 配列を持つ複数行** | 同じ `ArrayAsSingle` 設定で対応可能。各行の JSON 配列はそれぞれのセルに保持されます。 |
| **異なる JSON 構造（オブジェクト、入れ子配列）** | JSON が文字列である限り、`ArrayAsSingle` はそのまま保持します。複雑なオブジェクトの場合は、引用符をエスケープする必要がある場合があります。 |
| **別のデータ ソース（例: List\<T\>）を使用** | `DataTable` を任意の列挙可能コレクションに置き換えてください。マーカー構文（`&=myList.Property`）は同じです。 |
| **XLSX ではなく CSV にエクスポート** | `ArrayAsSingle` は依然として有効ですが、CSV はセル書式を保持しないため、JSON を引用符で囲む必要があります。 |

**プロのコツ:** `ProcessSmartMarkers` を呼び出す **前に** 必ず `ArrayAsSingle` を設定してください。処理後にフラグを変更しても、既に生成されたセルには影響しません。

---

## 完全な実行可能サンプル

以下はコンソール アプリケーションにコピーペーストできる完全プログラムです。`using` ディレクティブとコメントをすべて含んでいます。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

プログラムを実行し、`SmartMarkerJson.xlsx` を開くと、セル **A2** に JSON 配列が保持されていることが確認できます。

---

## まとめ

C# で Aspose.Cells の Smart Marker を使用する際に、JSON 配列を単一セルの値として保持するための **SmartMarkerOptions の ArrayAsSingle 設定** 方法を習得しました。`DataTable` の作成、マーカーの挿入、`ArrayAsSingle` フラグの設定、処理、保存という手順は、Excel 内でコンパクトな JSON 表現が必要なあらゆるシナリオに再利用できます。

次に試すべきこと:

* **Aspose.Cells Smart Marker** を使ったコレクションのループ処理
* **入れ子 JSON オブジェクト** をセル書式でエクスポートするカスタマイズ
* 条件付き書式と Smart Marker を組み合わせたリッチ レポート作成

さまざまなデータ構造で実験し、結果を共有してください。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っており、追加の API 機能をマスターしたり、別の実装アプローチを探求したりするのに役立ちます。各リソースには、ステップバイステップの説明と完全なコード例が含まれています。

- [JSON から Excel ワークブックを作成 – 完全 Aspose.Cells ガイド](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Aspose Cells Net で Excel ワークブックを作成・構成](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose Cells Net で Excel ワークブックを作成・構成](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}