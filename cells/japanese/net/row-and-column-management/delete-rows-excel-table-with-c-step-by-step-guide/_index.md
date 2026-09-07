---
category: general
date: 2026-02-28
description: C#でExcelテーブルの行を素早く削除する。名前付き範囲の追加方法、シート名でのワークシートへのアクセス方法、重複した名前エラーの回避方法を学びましょう。
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: ja
og_description: C# を使用して Excel テーブルの行を削除する。このチュートリアルでは、名前付き範囲の追加方法とシート名でワークシートにアクセスする方法も示します。
og_title: C#でExcelテーブルの行を削除する – 完全ガイド
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: C#でExcelテーブルの行を削除する – ステップバイステップガイド
url: /ja/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel テーブルの行を削除 – 完全プログラミングチュートリアル

ワークブックから **delete rows excel table** を削除したいと思ったことはありませんか？どの API 呼び出しを使えば良いか分からないこともあるでしょう。実は多くの開発者が、プログラムでテーブルを削減しようとしたときに同じ壁にぶつかります。  

このガイドでは、Excel テーブルから行を削除するだけでなく、**add defined name**（別名 *named range*）の追加方法、**access worksheet by name** の方法、そして別シートで重複した名前を追加したときに `InvalidOperationException` がスローされる理由も解説します。  

この記事を読み終えると、以下ができるようになります。

* タブ名でワークシートを取得する。  
* そのシートの最初のテーブルからデータ行を安全に削除する。  
* 特定のアドレスを指す名前付き範囲を作成する。  
* シート間での重複名前の落とし穴を理解する。

外部ドキュメントは不要です。必要な情報はすべてここにあります。

---

## 必要なもの

* **DevExpress Spreadsheet**（または `Workbook`、`Worksheet`、`ListObject`、`Names` オブジェクトを提供する任意のライブラリ）。  
* **.NET 6** 以上を対象とした .NET プロジェクト（コードは .NET Framework 4.8 でもコンパイル可能）。  
* C# の基本的な知識—`foreach` ループが書ければ問題ありません。

> **Pro tip:** 無料の Community Edition を使用している場合でも、以下で使用する API は商用版と同一です。

---

## Step 1 – Access Worksheet by Name

最初にやるべきことは、変更したいテーブルが存在するシートを見つけることです。  
多くの開発者は習慣的に `Worksheets[0]` を使用しますが、これではシートの順序にコードが依存し、タブ名が変更された瞬間に壊れてしまいます。

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*この点が重要な理由:* インデックスではなくシートの **name** を使用することで、ブックの構成が変わっても誤って別シートを編集するリスクを回避できます。  

指定した名前が存在しない場合、ライブラリは `KeyNotFoundException` をスローします。この例外を捕捉してユーザーフレンドリーなエラーメッセージを表示できます。

---

## Step 2 – Delete Rows Excel Table (The Safe Way)

正しいワークシートが取得できたら、最初のテーブルからデータ行を削除しましょう。  
よくあるミスは `DeleteRows(1, rowCount‑1)` を呼び出すことです。**DevExpress 22.2** 以降、このオーバーロードは **禁止** されており `InvalidOperationException` がスローされます。ライブラリはヘッダー行ではなく、テーブルのデータ範囲内で行を削除することを期待しています。

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **テーブルが空の場合はどうなるか？** `if` ガードにより `rowCount = 0` の呼び出しが防がれ、例外が発生しません。

### ビジュアル概要  

![delete rows excel table example](image.png "Excel テーブルから行が削除される様子のスクリーンショット")  

*Alt text: C# コードでの delete rows excel table example*

---

## Step 3 – How to Add Defined Name (Create a Named Range)

テーブルを整理した後、後で特定の範囲を参照したくなることがあります（例: グラフやデータ検証リスト）。そこで **add named range excel** が役立ちます。

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add` メソッドは 2 つのパラメータを受け取ります：識別子と A1 形式のアドレス。  
先ほど **access worksheet by name** を使用したおかげで、アドレス文字列はインデックス変更を気にせず任意のシートを安全に参照できます。

---

## Step 4 – Named Range on Another Sheet – Avoid Duplicate Name Errors

別シートでも同じ識別子を再利用できると思うかもしれませんが、次のように書くと：

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

残念ながら、Excel の名前スコープは **ブック全体** に適用され、シート単位ではありません。上記の呼び出しは `InvalidOperationException` をスローし、メッセージは *“A name with the same identifier already exists.”* となります。  

### 回避策

1. **ユニークな名前**（例: `MyTable_Sheet2`）を選ぶ。  
2. **既存の名前を削除**してから再追加する（本当に置き換えたい場合のみ）。

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## 完全実行可能サンプル

すべてをまとめると、以下のコンソールアプリを Visual Studio に貼り付け、サンプルの `sample.xlsx` に対して実行できます。

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**期待される結果**

* **Sheet1** の最初のテーブルからすべてのデータ行が削除され、ヘッダー行だけが残ります。  
* 名前 **MyTable** は `Sheet1!$A$1:$C$5` を指すようになります。  
* 2 番目の名前 **MyTable_Sheet2** は **Sheet2** 上の範囲を安全に参照し、例外は発生しません。

---

## よくある質問 & エッジケース

| 質問 | 回答 |
|----------|--------|
| *ワークブックに複数のテーブルがある場合は？* | インデックス (`worksheet.ListObjects[1]`) または名前 (`worksheet.ListObjects["MyTable"]`) で正しい `ListObject` を取得します。 |
| *複数シートにまたがるテーブルから行を削除できますか？* | できません。テーブルは単一シートに限定されます。各シートごとに削除ロジックを繰り返す必要があります。 |
| *行の一部だけを削除したい場合は？* | `table.DeleteRows(startRow, count)` を使用します。`startRow` はテーブルのデータ領域内でのゼロベースインデックスです。 |
| *名前付き範囲は保存後も残りますか？* | はい。`SaveDocument` を呼び出すと、名前はブックの XML に組み込まれます。 |
| *ブック内のすべての定義名を列挙するには？* | `foreach (var name in workbook.Names) Console.WriteLine(name.Name);` とします。 |

---

## 結論

C# を使った **delete rows excel table** の手順、**add named range excel** の方法、そして **access worksheet by name** の正しい使い方と重複名前例外の回避策を網羅しました。  

上記のコードスニペットが完全なソリューションです。コピーして自分のファイルで実行し、必要に応じてロジックを拡張して複数テーブルや動的範囲計算、UI との統合などに挑戦してください。

**次のステップ例**

* **named range on another sheet** を利用してチャート系列を駆動する。  
* **ExcelDataReader** と組み合わせて、インポート前にデータをクリーンアップする。  
* `foreach (var file in Directory.GetFiles(...))` ループで数十個のブックに対して一括更新を自動化する。

C# における Excel 自動化でさらに質問がありますか？ コメントで教えてください。会話を続けましょう。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}