---
category: general
date: 2026-03-22
description: Excelブックを作成し、カスタムプロパティを追加し、ワークシート名を設定し、C#でXLSBバイナリファイルとして保存する。
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: ja
og_description: C# を使用して Excel ワークブックを作成し、カスタム プロパティを追加し、ワークシート名を設定し、XLSB バイナリ ファイルとして保存する。
og_title: Excelブックを作成 – カスタムプロパティを追加し、XLSB形式で保存
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excelブックを作成 – カスタムプロパティを追加し、XLSBとして保存
url: /ja/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークブックの作成 – カスタム プロパティの追加と XLSB 形式での保存

プログラムから **Excel ワークブックを作成** しつつ、メタデータを添付したいことはありませんか？たとえば、レポート ID、作成者名、バージョン番号などを各ファイルにタグ付けするレポートエンジンを構築している場合です。そのようなとき、**カスタム プロパティを追加** しながら **ワークシート名を設定** し、最終的に **XLSB 形式で保存** する方法を学んでおくと、手作業の後処理が大幅に削減できます。

このチュートリアルでは、C# を使って **バイナリ Excel ファイルを書き込む** 完全な実行可能サンプルを順を追って解説します。XLSB 形式がカスタム プロパティの転送に最適な理由、よくある落とし穴の回避方法、古い Excel バージョンへの対応方法も併せて紹介します。

---

## 必要なもの

- **.NET 6+**（または .NET Framework 4.6+）。コードは最新のランタイムであればどれでも動作します。  
- **Aspose.Cells for .NET**（無料トライアルまたはライセンス版）。以下で使用する `Workbook`、`Worksheet`、`CustomProperties` クラスを提供します。  
- お好みの IDE – Visual Studio、Rider、あるいは VS Code でも構いません。  
- 生成されたファイルを保存するフォルダーへの書き込み権限。

他のサードパーティ ライブラリは不要です。

---

## 手順 1: Aspose.Cells のインストール

まず、プロジェクトに Aspose.Cells の NuGet パッケージを追加します。

```bash
dotnet add package Aspose.Cells
```

> **プロのコツ:** CI サーバー上で実行する場合は、ライセンスキーを環境変数に保存し、実行時に読み込むようにすると「評価版」透かしが出力に混入するのを防げます。

---

## 手順 2: Excel ワークブックの作成 – 概要

最初の本格的な操作は **Excel ワークブックを作成** することです。このオブジェクトはメモリ上のファイル全体を表し、ワークシート、スタイル、カスタム プロパティへのアクセスを提供します。

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

なぜテンプレートを読み込むのではなく新規 `Workbook` をインスタンス化するのでしょうか？ 空のワークブックは隠れたスタイルや残存するカスタム プロパティがないことを保証し、**バイナリ Excel ファイルを書き込む** 必要がある下流システムに対してクリーンな状態を提供します。

---

## 手順 3: ワークシート名の設定（重要性）

Excel のシートはデフォルトで “Sheet1”、 “Sheet2” と命名されます。シートに意味のある名前を付けることで、Power Query や VBA マクロなどの下流処理が格段に読みやすくなります。

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

重複した名前を割り当てようとすると、Aspose.Cells は `ArgumentException` をスローします。安全策として、リネーム前に `Worksheets.Exists("Data")` で存在チェックを行うとよいでしょう。

---

## 手順 4: カスタム プロパティの追加

カスタム プロパティはワークブック内部の XML に保存され、形式に関係なくファイルと共に搬送されます。`ReportId` や `GeneratedBy` といった情報を埋め込むのに最適です。

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **カスタム プロパティを使う理由**  
> • Excel の “ファイル → 情報 → プロパティ” パネルから直接参照できる。  
> • ワークブックを消費するコードはセル内容を走査せずにプロパティを取得できる。  
> • XLSX ↔ XLSB の形式変換でも保持される。なぜならメタデータの一部として保存されているからです。

日付、ブール値、さらにはバイナリ データも格納できますが、ペイロードは小さめに抑えてください – Excel はデータベースではありません。

---

## 手順 5: XLSB 形式で保存（バイナリ Excel ファイルの書き込み）

XLSB 形式はデータをバイナリ構造で保存するため、ファイルサイズが小さくなり、開く速度も速くなります。本チュートリアルのポイントは、**カスタム プロパティがバイナリ ストリームに組み込まれる** ため、必ずファイルと共に搬送される点です。

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### 期待される結果

プログラムを実行すると、デスクトップに `WithCustomProps.xlsb` が作成されます。Excel で開き、**ファイル → 情報 → プロパティ** に移動すると、*カスタム* 項目の下に `ReportId` と `GeneratedBy` が表示されます。

---

## 手順 6: エッジケースとよくある質問

### 対象フォルダーが読み取り専用の場合は？

`Save` 呼び出しを `try/catch` で囲み、代替として `%TEMP%` など書き込み可能な場所に保存先を切り替えると、権限エラーでアプリがクラッシュするのを防げます。

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### **XLSX** 形式で保存してもカスタム プロパティは保持できますか？

はい。`SaveFormat.Xlsb` を `SaveFormat.Xlsx` に変更すれば OK です。プロパティは同じ XML パートに保存されるため、形式変更後も残ります。ただし、XLSX は XML を ZIP 圧縮したものなのでファイルサイズは大きくなります。一方、XLSB は大規模データセットでのパフォーマンスが優れています。

### 後でカスタム プロパティを読むには？

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

このコードはすべてのカスタム プロパティをコンソールに出力し、下流サービスがファイルの出所を簡単に検証できるようにします。

---

## 完全な動作例

以下は新規コンソール プロジェクトにコピー＆ペーストできる完全プログラムです。`using` 文から最後の `Console.WriteLine` まで、抜け落ちている部分はありません。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

プログラムを実行し、生成されたファイルを開いてカスタム プロパティを確認してください。これが **Excel ワークブックの作成**、**カスタム プロパティの追加**、**ワークシート名の設定**、そして **XLSB 形式で保存** を一連の流れで行う手順です。

---

## 結論

これで **Excel ワークブックを作成** し、シートに明確な **ワークシート名を設定**、有用なメタデータを **カスタム プロパティで埋め込み**、最終的に **XLSB 形式で保存** してコンパクトなバイナリ Excel ファイルを生成する方法が完全に理解できました。このワークフローは信頼性が高く、.NET のバージョンを問わず動作し、1 件のレポートから数千件のレポートまでスケールします。

次のステップは？ “Data” シートにデータテーブルを追加したり、日付やブール値など異なるプロパティ型を試したり、膨大なデータセット向けに **XLSB 形式で保存** に切り替えてみてください。また、ワークブックにパスワード保護を施すことも可能です – Aspose.Cells ならワンライナーで実装できます。

ご質問や実装上の課題があればコメントで教えてください。ご自身のプロジェクトでこのパターンを拡張した事例もぜひ共有してください。Happy coding!  

---  

![Create Excel workbook screenshot](image.png){alt="Create Excel workbook with custom properties"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}