---
category: general
date: 2026-05-23
description: C#でJSONからExcelを素早く生成する。JSONをExcelに読み込む方法、プログラムでExcelブックを作成する方法、ブックをファイルに保存する方法を学びましょう。
draft: false
keywords:
- generate excel from json
- load json into excel
- save workbook to file
- create excel workbook programmatically
language: ja
og_description: C# を使用して JSON から Excel を生成します。このガイドでは、JSON を Excel に読み込む方法、プログラムで
  Excel ワークブックを作成する方法、そしてワークブックをファイルに保存する方法を示します。
og_title: C#でJSONからExcelを生成する – 完全プログラミングチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Generate Excel from JSON in C# quickly. Learn how to load JSON into
    Excel, create Excel workbook programmatically, and save workbook to file.
  headline: Generate Excel from JSON with C# – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- JSON
- Excel Automation
title: C#でJSONからExcelを生成する – 完全ステップバイステップガイド
url: /ja/net/data-loading-and-parsing/generate-excel-from-json-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で JSON から Excel を生成する – 完全ステップバイステップガイド

Excel を手動で開かずに **JSON から Excel を生成** できたらいいなと思ったことはありませんか？ あなただけではありません。多くの開発者が API のレスポンスや設定ファイル、シンプルなデータダンプを、迅速かつ信頼性の高い、ユーザー操作不要のスプレッドシートに変換する必要があります。  

このチュートリアルでは、**JSON を Excel にロード**し、コードだけでブックを作成し、最終的に **ブックをファイルに保存** するクリーンなエンドツーエンドのソリューションを順を追って解説します。最後まで読めば、任意の .NET プロジェクトに貼り付けられる再利用可能なスニペットが手に入ります。

> **Pro tip:** このアプローチは、フラットなテーブルにマッピングできる任意の JSON 形状で機能します。入れ子オブジェクトについては、後述の簡単な回避策をご覧ください。

---

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。  
- **Aspose.Cells for .NET** – 本チュートリアルで使用する Smart Marker エンジンを提供するライブラリ。  
- JSON ペイロード（例では小さな注文リストを使用）。  
- お好みの IDE（Visual Studio、Rider、または VS Code）。  

他のサードパーティーツールは不要です。すべてメモリ上で実行されます。

---

## Step 1 – Excel ブックをプログラムで作成

Excel 自動化の最初のステップは、ブックオブジェクトを作成することです。これは、白紙のキャンバスに例えることができます。

```csharp
using Aspose.Cells;          // Excel manipulation
using Aspose.Cells.Tables;   // Smart Marker support
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();
```

コードでブックを作成する理由は何ですか？ **プログラムからファイルが作成される** ことを保証し、ファイルシステムの競合状態を回避し、UI がなくてもサーバー上でパイプライン全体を実行できるようになるからです。

---

## Step 2 – Smart Marker プレースホルダーを挿入

Smart Markers は、スプレッドシート向けのメールマージ機能に相当する Aspose の機能です。セルに `${Orders:ArrayAsSingle}` のような単一プレースホルダーを配置すると、ライブラリは JSON 配列を自動的に行に展開します。

```csharp
        // Step 2: Put a Smart Marker into cell A1 (first worksheet, first cell)
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");
```

Smart Markers が初めての方は、`${Orders:ArrayAsSingle}` を「*Orders* コレクションの各項目を別々の行として出力せよ」というテンプレートタグと考えてください。

---

## Step 3 – SmartMarkerProcessor を接続

プロセッサはプレースホルダーを読み取り、JSON を解析し、シートにデータを埋め込むエンジンです。

```csharp
        // Step 3: Initialise the processor with the workbook we just prepared
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

なぜすぐに `Workbook.Save` を呼ばないのでしょうか？ データがまだ存在しないからです。プロセッサが生の JSON と Excel レイアウトの橋渡しを行います。

---

## Step 4 – 読み込む JSON データを定義

以下は 2 件の注文を表す小さな JSON 配列です。実際のシナリオでは、REST API から取得したり、ファイルを読み込んだり、動的に生成したりすることになるでしょう。

```csharp
        // Step 4: JSON that will populate the Smart Marker
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";
```

JSON は **フラット** に保っています――各オブジェクトはプリミティブなフィールドのみを持ちます。これが「JSON を Excel にロード」パターンと最も相性が良い形です。入れ子オブジェクトがある場合は、先にフラット化する必要があります（最後の *Advanced Tip* を参照）。

---

## Step 5 – JSON をブックに適用

ここで魔法が起きます。プロセッサが JSON を読み取り、Smart Marker を展開し、各オブジェクトに対して行を生成します。

```csharp
        // Step 5: Apply JSON – the Smart Marker expands automatically
        processor.ApplyJson(jsonData);
```

内部では、Aspose が一時的なデータテーブルを作成し、各プロパティ（`Id`、`Total`）を列にマッピングし、プレースホルダーの直下に行を挿入します。ループや手動でのセル指定は不要で、宣言的な変換だけで完了します。

---

## Step 6 – ブックをファイルに保存

最後に、埋め込まれたブックをディスクに永続化します。

```csharp
        // Step 6: Save the populated workbook to a physical file
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**ブックをファイルに保存** するステップがパズルの最後のピースです。Aspose は内部で Open XML を使用して最終的な `.xlsx` を書き出すため、Excel、Google Sheets、LibreOffice すべてと完全に互換性があります。

---

## 完全動作サンプル（全ステップ統合）

以下はそのままコピー＆ペーストして実行できる完全プログラムです。Aspose.Cells の NuGet パッケージがインストールされていることを確認してください（`dotnet add package Aspose.Cells`）。

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Insert Smart Marker placeholder in cell A1
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");

        // 3️⃣ Initialise SmartMarkerProcessor
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // 4️⃣ JSON data (could come from a file, API, etc.)
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";

        // 5️⃣ Apply JSON – Smart Marker expands automatically
        processor.ApplyJson(jsonData);

        // 6️⃣ Save the workbook to disk
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 期待される出力

`OrdersReport.xlsx` を開くと次のようになります：

| Id | Total |
|----|-------|
| 1  | 99.9  |
| 2  | 45.0  |

列ヘッダーは JSON のプロパティ名から自動生成され、各配列要素が新しい行として追加されます。手動でセルを指定する必要はありません。

---

## Advanced Tip – 大規模または入れ子 JSON の扱い方

JSON に **入れ子オブジェクト**（例：`Order` に `Customer` サブオブジェクトがある場合）が含まれる場合でも、Smart Markers は活用できますが、事前に構造をフラット化する必要があります：

```csharp
// Example flattening using Newtonsoft.Json.Linq
var jArray = JArray.Parse(jsonData);
var flatList = jArray.Select(item => new {
    Id = (int)item["Id"],
    Total = (decimal)item["Total"],
    CustomerName = (string)item["Customer"]["Name"]
}).ToList();
string flatJson = JsonConvert.SerializeObject(flatList);
processor.ApplyJson(flatJson);
```

この手法により、**JSON を Excel にロード**するフローをスムーズに保ちつつ、複雑なデータにも対応できます。

---

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **Aspose.Cells のライセンスがない** | 無料トライアルは透かしが入ります。 | ライセンスファイルを取得し、`License license = new License(); license.SetLicense("Aspose.Cells.lic");` で登録してください。 |
| **プレースホルダーのタイプミス** | Smart Marker タグは大文字小文字を区別します。 | `${Orders:ArrayAsSingle}` の綴りと括弧を再確認してください。 |
| **大きな JSON によるメモリ圧迫** | JSON 全体が RAM にロードされます。 | JSON をストリーム処理するか、バッチで処理し、後でシートをマージしてください。 |
| **日付形式の不一致** | JSON の日付が生のティック値として表示されます。 | `JsonSerializerSettings` で日付をフォーマットするか、処理後にカスタム列書式を追加してください。 |

---

## この方法が手動ループより優れている理由

- **宣言的**：*何を* したいか（テーブル）を記述し、*どうやって* 行を繰り返すかを記述しません。  
- **パフォーマンス**：Smart Markers は内部バッファを最適化しており、素朴な `for` ループより高速になることが多いです。  
- **保守性**：データソース（CSV、DB、API）を JSON 文字列に差し替えるだけで、Excel ロジックの変更は不要です。  
- **スケーラビリティ**：同じテンプレートを使い回して、形状が異なる多数のレポートを生成できます。

---

## 結論

本稿では、**C# で JSON から Excel を生成**する方法を、**JSON を Excel にロード**、**プログラムで Excel ブックを作成**、そして **ブックをファイルに保存**する一連の流れで実演しました。パイプラインはすべてメモリ上で完結し、数行のコードでクリーンな共有可能スプレッドシートが作れます。

さらに踏み込むなら、条件付き書式の追加、チャートの挿入、PDF への直接エクスポートなども同じ `Workbook` オブジェクトで実現可能です。重要なポイントは、Smart Markers がほぼボイラープレートなしで JSON を Excel テーブルに変換してくれることです。

特定の JSON 構造や出力形式の調整について質問があれば、コメントやディスカッションで遠慮なくどうぞ。Happy coding!

---

![Generate Excel from JSON using C# – screenshot of the resulting OrdersReport.xlsx](/images/generate-excel-from-json.png "generate excel from json")

*画像の代替テキスト:* generate excel from json – チュートリアルのビジュアル結果

## 関連チュートリアル

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}