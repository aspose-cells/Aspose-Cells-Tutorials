---
category: general
date: 2026-02-15
description: 新しいブックを作成し、数値精度を設定しながらExcelをTXTにエクスポートします。C#で有効数字を設定し、桁数を制限する方法を学びます。
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: ja
og_description: 新しいブックを作成し、ExcelをTXTにエクスポートして数値の有効数字を設定します。ステップバイステップのC#ガイド。
og_title: 新規ワークブック作成 – 正確にExcelをTXTにエクスポート
tags:
- C#
- Aspose.Cells
- Excel automation
title: 新規ワークブックを作成し、Excelを正確にTXTにエクスポート
url: /ja/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新しいワークブックの作成 – 正確な数値書式で Excel を TXT にエクスポート

C# で **create new workbook** オブジェクトを作成し、すぐにプレーンテキストファイルへダンプしたいと思ったことはありませんか？ あなただけではありません。多くのデータパイプラインシナリオでは、**export Excel to TXT** しつつ数値を読みやすく保つ必要があり、つまり小数点以下に表示される桁数を制限することが求められます。

このチュートリアルでは、フレッシュなワークブックを作成し、**significant digits**（有効桁数）を設定してエクスポートを構成し、最終的にディスクへ書き込むまでの全工程を解説します。最後まで読めば、**numeric precision** 要件を満たす実行可能なコードスニペットが手に入ります—追加ライブラリ不要、マジックも不要です。

> **Pro tip:** すでに Aspose.Cells を使用している場合、以下に示すクラスはそのライブラリの一部です。別のプラットフォームを使用している場合でも概念は同じなので、API 呼び出しを置き換えるだけで利用できます。

---

## 必要なもの

- .NET 6+（コードは .NET Core と .NET Framework のどちらでもコンパイル可能）  
- Aspose.Cells for .NET（無料トライアルまたはライセンス版） – NuGet でインストール: `dotnet add package Aspose.Cells`  
- お好みの IDE（Visual Studio、Rider、VS Code など）  

以上です。追加の設定ファイルや隠れた手順は不要です。

---

## 手順 1: 新しいワークブックを作成

最初にやるべきことは **create new workbook** です。`Workbook` クラスは、シートやセル、データがまだ入っていない空の Excel ファイルと考えてください。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** クリーンなワークブックから始めることで、後で精度設定に影響を与える可能性のある隠れた書式設定を回避できます。

---

## 手順 2: テキスト保存オプションを構成 – 有効桁数を設定

次に、Aspose.Cells に対して `.txt` ファイルに書き出す際の **significant digits** の数を指示します。`TxtSaveOptions` クラスの `SignificantDigits` プロパティがこれを実現します。

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` は、数値の小数点位置に関係なく、最も重要な 5 桁を保持することを意味します。各セルを個別に書式設定せずに **numeric precision** を設定できる便利な方法です。

---

## 手順 3: ワークブックをプレーンテキストファイルとして保存

ワークブックとオプションの準備ができたら、いよいよ **export Excel to txt** です。`Save` メソッドにファイルパスと先ほど構成したオプションオブジェクトを渡します。

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

プログラムを実行すると、以下のようなファイルが生成されます：

```
12346
0.00012346
3.1416
```

各数値が先に設定した **limit significant digits** ルールに従っていることが確認できます。

---

## 手順 4: 結果を検証 (任意だが推奨)

生成された `numbers.txt` を任意のエディタで開くこともできますが、特に CI パイプラインでは検証ステップを自動化したいでしょう。

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

コンソールに上記の 3 行が表示されれば、**significant digits** が正しく設定され、エクスポートが期待通りに機能していることが確認できます。

---

## よくある落とし穴と回避策

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| 数字が小数点以下多数の桁で表示される | `SignificantDigits` がデフォルト (0) のまま | 必要な桁数を明示的に `SignificantDigits` に設定 |
| 空ファイルが作成される | 保存前にワークブックにデータが入っていない | `Save` を呼び出す **前に** セルにデータを入力 |
| ファイルパスで `UnauthorizedAccessException` が発生 | 保護されたフォルダへ書き込もうとしている | 書き込み権限のあるフォルダを使用 (例: `C:\Temp` や `%USERPROFILE%\Documents`) |
| 非常に小さい数値で精度がずれる | 有効桁数は小数点以下の先頭のゼロを除外してカウントするため | 「有効桁数」は先頭のゼロを無視することを覚えておく; 例: 0.000123456 を 5 桁にすると `0.00012346` になる |

---

## 完全動作サンプル (コピー＆ペースト可能)

以下は単体で動作する完全なプログラムです。新しいコンソールプロジェクトに貼り付けて **Run** をクリックしてください。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**期待されるコンソール出力**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

`numbers.txt` ファイルには上記と同じ 3 行が書き込まれます。

---

## 次のステップ: 基礎を超えて

- **他フォーマットへのエクスポート** – Aspose.Cells は CSV、HTML、PDF もサポートしています。必要に応じて `TxtSaveOptions` を `CsvSaveOptions` や `PdfSaveOptions` に置き換えてください。  
- **動的な精度設定** – ユーザー入力や設定ファイルに基づいて実行時に `SignificantDigits` を算出できます。  
- **複数シートの処理** – `workbook.Worksheets` を列挙し、各シートを個別の `.txt` ファイルにエクスポートします。  
- **ローカリゼーション** – `CultureInfo` を使って小数点区切り文字（`.` と `,`）を制御し、地域設定に合わせられます。  

これらの拡張もすべて、ここで学んだ **create new workbook**、エクスポート設定、**numeric precision** のコア概念に基づいています。

---

## まとめ

新しく **create new workbook** インスタンスを作成し、データを入力したうえで、**export Excel to TXT** しながら **significant digits** を設定して出力精度を制限する方法を紹介しました。完全なサンプルはすぐに実行可能で、各行の解説により *なぜ* そのコードが必要かが理解できるので、プロジェクトに合わせて自由にカスタマイズできます。

ぜひ `SignificantDigits` の値を変えてみたり、シートを増やしたり、出力フォーマットを切り替えてみてください。問題が発生したら Aspose.Cells のドキュメントを参照するか、下のコメント欄で質問してください。Happy coding!

---

![Create new workbook example](/images/create-new-workbook.png "C# IDE で create new workbook コードを表示しているスクリーンショット")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}