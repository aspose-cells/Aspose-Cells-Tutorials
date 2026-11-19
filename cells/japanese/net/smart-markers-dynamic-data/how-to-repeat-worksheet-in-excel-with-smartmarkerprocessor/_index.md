---
category: general
date: 2026-11-19
description: 配列データでExcelに入力しながらシートを繰り返す方法。数ステップで複数のシートを生成し、リストからシートにデータを入力する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: ja
lastmod: 2026-11-19
og_description: SmartMarkerProcessor を使用してワークシートを繰り返す方法。このガイドに従って、配列データで Excel を埋め込み、複数のワークシートを生成し、リストからワークシートを埋め込みます。
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Excelでワークシートを繰り返す方法 – ステップバイステップガイド
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: SmartMarkerProcessor を使用して Excel のワークシートを繰り返す方法
url: /ja/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ExcelでSmartMarkerProcessorを使用してワークシートを繰り返す方法

Excelレポートを生成する際に **how to repeat worksheet** が必要な場合、このガイドでは完全で実行可能なソリューションを示します。チュートリアルの最後までに、SmartMarkerProcessorライブラリを使用して **populate Excel with array** データの **populate worksheet from list**、**generate multiple worksheets** ができるようになります。

部門、地域、または期間ごとに個別のタブが必要になる場合、ワークシートを繰り返すことは一般的な要件です。以下の例では正確な手順を示し、各設定が重要な理由を説明し、空のリストやカスタム命名といったエッジケースもカバーします。

## 前提条件

- .NET 6.0 以降がインストールされていること
- `SmartMarkerProcessor` を含む **GroupDocs.Viewer**（または同等）の NuGet パッケージへの参照
- 繰り返したい行に `${repeat:Dept}` のようなマーカーが配置された Excel テンプレートブック（`.xlsx`）
- C# と LINQ の基本的な知識（任意だがあると便利）

追加のサードパーティライブラリは必要ありません。

## 手順 1: SmartMarkerProcessor インスタンスの作成

プロセッサはマーカー置換とワークシートの複製を調整します。引数なしでインスタンス化するとデフォルトオプションが使用されます。

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

プロセッサを早期に作成すると、データが適用される前にグローバルオプションを設定できます。これは **how to repeat worksheet** を正しく行うための基盤です。

## 手順 2: ワークシートの繰り返しを有効化

デフォルトではプロセッサは現在のシート上のマーカーのみ置換します。`RepeatWorksheet` を `true` に設定すると、データコレクションの各項目に対してシート全体をクローンするようエンジンに指示します。

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

このオプションを有効にすることが **generate multiple worksheets** の鍵となります。プロセッサは `Dept` 配列の各要素に対して新しいタブを作成し、元の書式を保持します。

## 手順 3: データソースを配列またはリストとして準備

SmartMarkerProcessor は任意の列挙可能オブジェクトで動作しますが、**populate worksheet from list** を行いたい場合は配列を使用すると意図が明確になります。ここでは文字列配列を保持する `Dept` プロパティを持つ匿名オブジェクトを作成します。

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

すでに `List<string>` を持っている場合はそのまま渡すことができます。プロセッサは同様に扱います。重要なのはプロパティ名（`Dept`）がテンプレート内のマーカー `${repeat:Dept}` と一致していることです。

## 手順 4: テンプレートワークシートの読み込み

`ExcelPackage`（EPPlus）または `Workbook` オブジェクトを使用していると仮定し、繰り返したいワークシートを取得します。変数 `ws` がそのシートを表します。

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

別のライブラリ（例: ClosedXML）を好む場合でも同様の原則が適用されます。必要なインターフェイスを実装したワークシートオブジェクトを取得してください。

## 手順 5: データでワークシートを処理

データをテンプレートに適用します。プロセッサは各部門ごとにシートをクローンし、`${repeat:Dept}` マーカーを実際の部門名に置換し、シートの残りの部分はそのままにします。

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

`Process` が完了すると、`ws` は複数のワークシートのうち最初のものになります（部門ごとに1枚）。元のシート名は保持され、複製シートにはインクリメンタルなサフィックスが付与されます（例: “Sheet1 (1)”、 “Sheet1 (2)”）。カスタム命名が必要な場合は、後で名前を変更できます。

### 期待される出力

生成されたブックを開くと、以下のようになっているはずです。

- **Sheet1** – 元のテンプレート（空白のまま、またはマスタとして使用）
- **Sheet1 (1)** – “HR” が入力されたシート
- **Sheet1 (2)** – “IT” が入力されたシート
- **Sheet1 (3)** – “Finance” が入力されたシート

各シートは同じレイアウトですが、`${repeat:Dept}` が出現した場所は部門名に置き換えられています。

## エッジケースの処理

### 空または null の配列

`Dept` が null または空の場合、プロセッサは追加のワークシートを作成しません。完全に空のブックになるのを防ぐために、ガードを追加できます。

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### カスタムワークシート名

デフォルトの命名スキームはすべてのレポート要件に合わないことがあります。処理後にループを使って各シートの名前を変更します。

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### 追加列の入力

単一マーカー以外に **populate excel with array** の値を入力する必要がある場合、データオブジェクトを拡張します。

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

その後、テンプレートマーカーを `${repeat:Dept.Name}` と `${repeat:Dept.Headcount}` に調整します。プロセッサは各部門の行を繰り返し、両方の列にデータを埋め込みます。

## 完全な動作例

以下はテンプレートの読み込みから最終ブックの保存までの全フローを示す、自己完結型のコンソールアプリケーションです。

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explanation of key sections**

- **Processor creation** – マーカーを解釈するエンジンを確立します。
- **RepeatWorksheet option** – *how to repeat worksheet* に答えるコア機能を有効化します。
- **Data source** – **populate excel with array** を満たすために配列 (`new[]`) を使用します。
- **Template loading** – ワークシートオブジェクトを取得する一般的な方法を示します。
- **Processing** – 複製とデータ挿入を一度の呼び出しで実行します。
- **Renaming** – 汎用的な “(1)”、 “(2)” 名を意味のあるタイトルに変換する方法を示します。これは **generate multiple worksheets** 後の典型的な要件です。

このプログラムを実行すると、`Result.xlsx` が生成され、3つの部門別タブが配列から入力された状態で作成されます。

## よくある落とし穴とプロのコツ

- **Marker spelling** – マーカーはプロパティ名と完全に一致する必要があります（`${repeat:Dept}`）。スペルミスは繰り返しを阻止します。
- **Worksheet index** – 処理後、元のシートはインデックス 0 に残り、生成されたシートは順次追加されます。インデックスの取り違えは誤ったタブの名前変更につながります。
- **Large data sets** – 数百枚のワークシートを生成するとファイルサイズが大幅に増加します。パフォーマンスが問題になる場合はレポートを分割するか、単一シートでセクションをグループ化することを検討してください。
- **Thread safety** – `SmartMarkerProcessor` はスレッドセーフではありません。複数のブックを並列処理する場合は、スレッドごとに別々のインスタンスを作成してください。

## 結論

これで SmartMarkerProcessor を使用して Excel で **how to repeat worksheet** を行う方法、**populate excel with array** データの入力方法、**generate multiple worksheets** の作成方法、そして **populate worksheet from list** の効率的な実装方法が分かりました。完全な例はすべての概念を結び付けており、オプションの名前変更ステップにより、クリーンでユーザーフレンドリーなタブ名を生成できます。

次に取り組むべきこととしては：

- 複雑なオブジェクト（入れ子コレクション）を使用した **populate worksheet from list** の活用
- ワークシート複製後の条件付き書式の適用
- 生成されたブックを PDF や CSV にエクスポートして下流システムで利用

コードを自分のレポートシナリオに合わせて自由にカスタマイズし、Excel ワークブックの自動化を自信を持って楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [ワークシートの繰り返し方法 – Excel自動化の完全ガイド](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [アイテムごとにワークシートを作成 – C#でワークシートを繰り返す方法](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Excelで配列を展開しテンプレートに入力する方法](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}