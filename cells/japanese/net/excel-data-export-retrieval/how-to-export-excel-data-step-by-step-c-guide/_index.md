---
category: general
date: 2026-03-29
description: C# を使用して Excel テーブルをプレーンテキストにエクスポートし、文字列をファイルに書き込み、Excel テーブルを CSV または
  TXT に変換する方法を学びます。完全なコードとヒントが含まれています。
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: ja
og_description: C#でExcelテーブルをテキストファイルにエクスポートする方法。Excelテーブルの変換とTXTファイルの保存に関する完全なソリューション、コード、ベストプラクティスを入手できます。
og_title: Excelデータのエクスポート方法 – 完全C#チュートリアル
tags:
- C#
- Excel
- File I/O
title: Excel データのエクスポート方法 – ステップバイステップ C# ガイド
url: /ja/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel データのエクスポート方法 – 完全 C# ガイド

スプレッドシートを手動で開かずに **Excel データをエクスポート** したいことはありませんか？レガシーシステム向けにテーブルをシンプルなテキストファイルにダンプしたい場合や、データ分析パイプライン用に手早く CSV を出力したい場合に役立ちます。このチュートリアルでは、**文字列を書き込む** 方法を実演しながら、C# を使って **Excel テーブルをデリミテッドテキスト形式に変換** する実践的なエンドツーエンドのソリューションを解説します。

ブックの読み込み、対象テーブルの選択、エクスポートオプションの設定、最終的に `.txt` ファイルとして保存するまでの全工程を網羅します。最後まで読めば、**テーブルを CSV としてエクスポート**（任意の区切り文字も可）でき、**C# で txt ファイルを保存** する際の便利なコツも把握できます。外部ツールは不要—NuGet パッケージと少しのコードだけで完結します。

---

## 必要なもの

- **.NET 6.0+**（または従来版が好きなら .NET Framework 4.7.2）
- **Syncfusion.XlsIO** NuGet パッケージ（`ExportTableOptions` クラスがここにあります）
- 基本的な C# IDE（Visual Studio、VS Code、Rider などお好きなもの）
- 少なくとも 1 つのテーブルが含まれる Excel ブック（例では `ws.Tables[0]` を使用）

> Pro tip: Syncfusion ライブラリがまだ無い場合は、コマンドラインで  
> `dotnet add package Syncfusion.XlsIO.Net.Core` を実行してください。

---

## Step 1 – ワークブックを開き、最初のテーブルを取得  

最初に Excel ファイルを読み込み、テーブルが格納されているワークシートへの参照を取得します。このステップは、**Excel テーブルを変換** する操作が `ITable` オブジェクトに対して行われるため、非常に重要です。

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*ポイント:* `using` でワークブックを開くことで、すべてのアンマネージドリソースが解放され、後で **文字列を書き込む** ときにファイルロックが発生しにくくなります。

---

## Step 2 – エクスポートオプションを設定（プレーンテキスト、ヘッダーなし、セミコロン区切り）  

次に Syncfusion に対して、テーブルのシリアライズ方法を指示します。`ExportTableOptions` でヘッダーの有無、区切り文字、文字列かバイト配列かを選択できます。

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*ポイント:* `IncludeHeaders = false` にすると、列順が既に決まっている下流システムの期待に合致しやすくなります。区切り文字を変更すれば、**テーブルを CSV としてエクスポート** する際にカスタムセパレータを使用できます。

---

## Step 3 – テーブルを文字列へエクスポート  

オプションが整ったら `ExportToString` を呼び出します。このメソッドはテーブル全体（すべての行）を取得し、ファイル出力用の単一文字列を返します。

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*ポイント:* `ExportToString` が Excel グリッドをデリミテッド形式に変換する重い処理を担います。設定した `Delimiter` が反映されるため、余計な加工なしで **テーブルを CSV としてエクスポート** した結果が得られます。

---

## Step 4 – エクスポートしたテキストをファイルに書き込む  

最後に文字列をディスクに保存します。`File.WriteAllText` は **C# で txt ファイルを保存** する最もシンプルな方法で、ファイルが存在しなければ自動的に作成し、既にある場合は上書きします。

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*ポイント:* 文字列を直接書き込むことで、余計な変換ステップを省けます。ファイルの中身は `Value1;Value2;Value3` のような行になり、下流パーサーがすぐに利用できます。

---

## 完全動作サンプル（全ステップを一括で実装）  

以下は、これまで説明した内容をすべて組み合わせた、コピー＆ペースト可能なプログラムです。エラーハンドリングとコメントを含めて分かりやすくしています。

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**期待される出力**（`ExportedTable.txt` の内容）:

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

各行は元の Excel テーブルの 1 行に対応し、値はセミコロンで区切られています。`Delimiter = ","` に変更すれば、従来の CSV ファイルが生成されます。

---

## よくある質問とエッジケース  

### ワークブックに複数のテーブルがある場合は？  
`ws.Tables[0]` を目的のインデックスに変更するか、`ws.Tables` をループすれば対応できます。

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### 列ヘッダーも出力したい場合は？  
`ExportTableOptions` の `IncludeHeaders = true` に設定します。下流システムがヘッダー行を期待しているときに便利です。

### 出力先フォルダーを動的に変更したい場合は？  
`Path.Combine` と `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` などを組み合わせて、ユーザー指定のパスを作成すれば柔軟に対応できます。

### 大容量ファイルはどう扱う？  
巨大テーブルの場合は、文字列全体をメモリに保持せずにストリーミングで出力することを検討してください。

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### .NET Core でも動作する？  
はい。Syncfusion.XlsIO は .NET 5/6/7 をサポートしています。適切な NuGet パッケージを参照すればすぐに利用可能です。

---

## 信頼性の高いエクスポートのためのプロ Tips  

- **ファイルパスを事前に検証** する。ディレクトリが存在しないと `DirectoryNotFoundException` がスローされます。  
- テーブルがメモリに収まるサイズの場合のみ **ExportAsString** を使用し、巨大データセットでは `ExportToStream` を利用してください。  
- **カルチャーに注意**：小数点にカンマが使われているデータの場合は、セミコロン (`;`) やタブ (`\t`) を区切り文字に選んで CSV パースエラーを防ぎましょう。  
- **バージョン固定**：Syncfusion は API シグネチャを変更することがあります。NuGet バージョンをピン留め（例: `<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`）してビルドの再現性を保ちましょう。

---

## 結論  

本ガイドでは、C# を使って **Excel テーブルをプレーンテキストファイルにエクスポート** する方法を実演しました。ワークブックの読み込み、`ExportTableOptions` の設定、テーブルの文字列へのエクスポート、そして **文字列を書き込む** 手順を踏むことで、**Excel テーブルを変換**、**テーブルを CSV としてエクスポート**、**C# で txt ファイルを保存** といったタスクに対する堅牢なパターンが手に入ります。

区切り文字を変えたり、ヘッダーを含めたり、複数テーブルをループしたりして自由に実験してください。同じ手法で CSV レポートの生成やレガシーパサーへのデータ供給、スプレッドシート内容の軽量テキストアーカイブが可能です。

さらにシナリオがありますか？たとえば **非同期で文字列を書き込む**、または出力をリアルタイムで zip 圧縮するなど。次回は *C# の非同期ファイル I/O* と *.NET でのファイル圧縮* に関するチュートリアルをご覧ください。

Happy coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}