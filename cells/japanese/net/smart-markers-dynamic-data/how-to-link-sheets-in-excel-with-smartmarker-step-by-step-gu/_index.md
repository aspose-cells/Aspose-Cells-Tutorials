---
category: general
date: 2026-06-08
description: SmartMarkerProcessor を使用して Excel でマスタ‑詳細レポートのシートをリンクする方法。マスタシートにデータを入力し、マスタ‑詳細の
  Excel レポートを簡単に生成します。
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: ja
og_description: SmartMarkerProcessor を使用して Excel のシートをリンクする方法。マスタシートにデータを入力し、数分でマスタ・詳細レポートを生成する方法を学びましょう。
og_title: SmartMarkerでExcelのシートをリンクする方法 – ステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: SmartMarkerでExcelのシートをリンクする方法 – ステップバイステップガイド
url: /ja/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelでシートをリンクする方法 – SmartMarkerによるステップバイステップガイド

Excelで手動で行をコピーしたり、無限に続くVBAループを書いたりせずに、**シートをリンクする方法**を考えたことはありませんか？ あなただけではありません。データが変化しても同期したままのクリーンなマスタ‑デティールレポートが必要になると、多くの開発者が壁にぶつかります。良いニュースは、SmartMarkerProcessorがその面倒な作業を代行し、数行のC#コードで完全なマスタ‑デティールブックを作成できることです。

このチュートリアルでは、**マスターシートを作成する**手順、詳細シートの設定、そして最終的に**マスターディテールレポートを生成する**手順を順に解説します。最後まで読むと、任意の.NETプロジェクトに組み込める再利用可能なパターンが手に入ります。

> **Prerequisite note:** GrapeCity Documents for Excel (GcExcel) バージョン2024以降、.NET開発環境（Visual Studio 2022 が推奨）、基本的なC#の知識が必要です。GcExcel以外の追加NuGetパッケージは不要です。

---

## ソリューションの概要

コードに入る前に、SmartMarkerの文脈で「シートをリンクする」とは実際に何を意味するのかを分解してみましょう：

1. **Master sheet** – エンティティごとに1行を保持します（例：顧客リスト）。
2. **Detail sheet** – マスタ行に属する行を含みます（例：各顧客の注文）。
3. **SmartMarker syntax** – プロセッサに2つのデータテーブルを結びつける方法を指示する小さなマークアップ言語（`{MasterSheet}#master;{DetailSheet}#detail`）。
4. **Processor options** – `MasterDetail` を有効にすると、エンジンはマスタ行を自動的に繰り返し、関連する詳細行をその下に埋め込みます。

これらの要素を理解しておくと、後でアプローチを調整しやすくなります（たとえば、3層のネストや条件付き書式が必要になる場合）。実装を進める際は、この概念モデルを手元に置いておきましょう。

## 手順 1: マスタ‑デティール処理用の階層データを準備する

最初に必要なのは、マスタ‑デティールの関係を表すデータソースです。実際のシナリオではデータベースから取得することが多いですが、分かりやすさのために匿名オブジェクトリテラルを使用します。

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Why this matters:** SmartMarkerは関係を自動的に推測せず、対応するプロパティ名（`MasterId` → `Id`）を探します。このようにデータを構造化することで、プロセッサに明確なマップを提供し、**シートをリンクする方法**を効果的に実現する基盤となります。

> **Pro tip:** データが `DataTable` オブジェクトにある場合は、同じ名前のプロパティとして公開すればOKです—SmartMarkerは任意の列挙可能コレクションで動作します。

## 手順 2: ワークブックを作成しテンプレートをロードする

SmartMarkerは既存のExcelワークブック（通常はシート名とプレースホルダーマーカーが設定されたテンプレート）に対して動作します。ここではメモリ上でワークブックを作成し、*MasterSheet* と *DetailSheet* という名前の空白シートを2つ追加します。

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

レイアウトをExcelで先に設計したい場合は、ディスク上の `.xlsx` ファイル（`wb.Open("Template.xlsx")`）をロードすることもできます。重要なのは、シート名がSmartMarker文字列で参照する名前と一致していることです。

## 手順 3: SmartMarkerProcessor をインスタンス化し、マスタ‑デティールモードを有効にする

これでマーカーを読み取りデータを貼り付けるエンジンを呼び出します。`SmartMarkerProcessor` はワークブックをコンストラクタ引数として受け取り、`Options.MasterDetail` フラグにより `#master` と `#detail` マーカーをリンクされたペアとして扱うよう指示します。

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Why enable `MasterDetail`?** このフラグがなければ、プロセッサは `{MasterSheet}#master` と `{DetailSheet}#detail` を独立した操作として扱い、行間の重要な関係が失われます。フラグを設定するだけで、**シートをリンクする方法**が実際に機能するようになります。

## 手順 4: SmartMarker 文字列を定義し、プロセッサを実行する

マーカー文字列は、どのシートがマスターでどのシートが詳細かをSmartMarkerに指示します。構文はシンプルです：`{SheetName}#master;{SheetName}#detail`。追加のマーカー（例：`#header`）も付加できますが、基本的なレポートには不要です。

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

`Process` が実行されると、エンジンは次の処理を行います：

1. ヘッダーの次の最初の空行から始めて、各マスタ行を *MasterSheet* に書き込みます。
2. 各マスタ行について、`Details` コレクションを走査し、`MasterId` がマスタの `Id` と一致する行を選択し、対応するマスタエントリの直下に *DetailSheet* に書き込みます。

## 手順 5: 結果のワークブックを保存またはエクスポートする

この時点で、完全にデータが埋め込まれたワークブックが完成しています。ディスクに保存したり、Webクライアントへストリームで返したり、PDFに変換したりできます。

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

ファイルを開くと、2つのシートが表示されます。*MasterSheet* には `A` と `B` が一覧表示され、*DetailSheet* にはマスタ `1` の下に `Item1`、マスタ `2` の下に `Item2` が表示されます。これが **マスターシートを作成する** と **マスターディテールレポートを生成する** を一度に行う本質です。

## ビジュアル概要

![SmartMarkerProcessor を使用して Excel でシートをリンクする方法を示す図](https://example.com/diagram.png "シートをリンクする方法の図")

この図（代替テキストに主要キーワードが含まれています）は、C# オブジェクト → SmartMarkerProcessor → リンクされた Excel シートへのデータフローを示しています。

## 一般的なエッジケースの処理

### マスタごとの複数の詳細行

マスタ行に複数の関連詳細がある場合、SmartMarker はマスタ行を1回繰り返し、その下に*すべて*の一致する詳細行を書き込みます。追加のコードは不要で、`Details` コレクションにすべての行が含まれていることを確認すれば完了です。

### 詳細がない場合

マスタエントリに一致する詳細行がない場合、詳細シートはそのセクションを単にスキップします。プレースホルダー（例： “No items”）が必要な場合は、テンプレートに計算列を追加し、`=IF(COUNTA(A2:B2)=0,"No items","")` のような Excel 数式を使用できます。

### 大規模データセット

数万行の処理はメモリ集中的になる可能性があります。パフォーマンスを保つために：

- `processor.Options.EnableStreaming = true` を使用する（GcExcel 2025+ で利用可能）。
- データをチャンクに分割し、各チャンクを個別に処理してからワークブックをマージする。

### カスタム列マッピング

プロパティ名が一致しない場合（`MasterKey` と `Id` など）、処理前に `SmartMarkerProcessor.Map` メソッドを使用してエイリアスを作成できます。

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

## 完全な動作例

すべてをまとめると、すぐに実行できる完全なコピー＆ペースト可能なプログラムが以下です。



## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for Java を使用した Excel の外部リンク数式のマスター](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Aspose.Cells を使用した Java の動的 Excel シートのマスター：包括的ガイド](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Aspose.Cells Java を使用した動的 Excel レポートのマスター：名前付き範囲と複雑な数式](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}