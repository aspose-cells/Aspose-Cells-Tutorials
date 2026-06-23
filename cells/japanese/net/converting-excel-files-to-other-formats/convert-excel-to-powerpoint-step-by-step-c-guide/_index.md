---
category: general
date: 2026-03-01
description: C#でExcelをPowerPointに素早く変換。Aspose.Cells を使用して、Excelブックから数行のコードでPowerPointを生成する方法を学びましょう。
draft: false
keywords:
- convert excel to powerpoint
- generate powerpoint from excel
- convert xlsx to pptx
- how to convert excel
- create pptx from excel
language: ja
og_description: C#でExcelをPowerPointに変換する。このガイドでは、Aspose.Cells を使用して Excel ファイルから PowerPoint
  を生成する方法を、完全なコードとヒントとともに紹介します。
og_title: Excel を PowerPoint に変換 – 完全 C# チュートリアル
tags:
- C#
- Aspose.Cells
- Excel
- PowerPoint
title: Excel を PowerPoint に変換 – ステップバイステップ C# ガイド
url: /ja/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を PowerPoint に変換 – ステップバイステップ C# ガイド

Excel を PowerPoint に **変換したい**けれど、どこから始めればいいか分からないことはありませんか？ あなたは一人ではありません。多くの開発者が、データが豊富なスプレッドシートをプレゼンテーション用のスライドに変換しようとして壁にぶつかります。  

良いニュースは、数行の C# コードさえ書けば、**Excel から PowerPoint を自動生成**でき、手動でコピー＆ペーストする必要がなくなるということです。このチュートリアルでは、`.xlsx` ファイルの読み込みから、Microsoft PowerPoint や互換ビューアで開ける洗練された `.pptx` の保存まで、全工程を順を追って解説します。

> **得られるもの:** Excel ブックを読み込み、PowerPoint の保存オプションを設定し、PowerPoint ファイルを書き出す実行可能なプログラム—すべて Aspose.Cells ライブラリを使用しています。

## 必要なもの

- **.NET 6.0** 以降（コードは .NET Framework 4.7+ でも動作します）  
- **Aspose.Cells for .NET** – NuGet から取得できます（`Install-Package Aspose.Cells`）  
- C# の基本的な知識（特別なことは不要、通常の `using` 文さえあれば OK）  
- スライドデッキに変換したい Excel ファイル（`input.xlsx`）  

以上です。追加のサードパーティツールは不要、COM インターロップも不要、面倒な PowerPoint 自動化も不要です。さっそく始めましょう。

![Convert Excel to PowerPoint workflow](convert-excel-to-powerpoint.png "Convert Excel to PowerPoint")

*Alt text: Convert Excel to PowerPoint workflow diagram*

## Aspose.Cells を使った Excel から PowerPoint への変換

### Step 1 – Load the Excel Workbook

最初に行うべきことは、スプレッドシートをメモリに読み込むことです。Aspose.Cells では `Workbook` コンストラクタにファイルパスを渡すだけで簡単に実現できます。

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the Excel workbook
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
```

**Why this matters:** ワークブックを読み込むことで、すべてのワークシート、チャート、埋め込み画像にアクセスできるようになります。ここから、変換前に保持するものや除外するものを選択できます。

### Step 2 – Set Up Presentation Save Options

Aspose.Cells は複数の出力形式に対応しており、PowerPoint 用には `PresentationSaveOptions` を使用します。このオブジェクトで `SaveFormat.Pptx` を指定したり、マクロの埋め込みや元の列幅の保持など、便利な設定を調整できます。

```csharp
            // Step 2: Set up presentation save options for PowerPoint format
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                // Optional: keep the original Excel formatting as much as possible
                // (true by default, but we set it explicitly for clarity)
                KeepOriginalFormatting = true
            };
```

**Why this matters:** 設定が適切でないと、スライドがつぶれたりスタイルが失われたりします。Aspose.Cells に本物の PPTX ファイルを生成するよう指示することで、Excel のレイアウトが正しく保持されます。

### Step 3 – Save the Workbook as a PowerPoint Presentation

いよいよ魔法の瞬間です。`Save` メソッドを一度呼び出すだけで、ワークブックの最初のワークシート（またはライブラリのバージョンによってはすべてのシート）を鏡写しにした `.pptx` が生成されます。多くのシナリオでは最初のシートだけで十分ですが、後で試してみても構いません。

```csharp
            // Step 3: Save the workbook as a PowerPoint presentation
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"Success! '{outputPath}' has been created.");
        }
    }
}
```

**What you’ll see:** `output.pptx` を PowerPoint で開くと、各ワークシートがスライドに変換されていることが確認できます。テキストセルはテキストボックスに、チャートは PowerPoint のネイティブチャートに、画像は元の解像度を保ったまま表示されます。

## Excel から PowerPoint を生成 – プロジェクト設定のポイント

- **NuGet Install:** プロジェクトフォルダーで `dotnet add package Aspose.Cells` を実行します。これにより最新の安定版（2026年3月時点でバージョン 23.10）が取得されます。  
- **Target Platform:** .NET Core を使用している場合は、`csproj` に `<TargetFramework>net6.0</TargetFramework>` が含まれていることを確認してください。  
- **File Paths:** クロスプラットフォームの安全性を確保するため、特に Linux コンテナ上で実行する場合は `Path.Combine` を使用しましょう。  

```csharp
using System.IO;

// Example of safe path building
string baseDir = AppDomain.CurrentDomain.BaseDirectory;
string inputPath = Path.Combine(baseDir, "input.xlsx");
string outputPath = Path.Combine(baseDir, "output.pptx");
```

## Xlsx から Pptx への変換 – 複数シートの取り扱い

デフォルトでは Aspose.Cells は **アクティブなシートのみ** を変換します。シートごとにスライドが必要な場合は、コレクションをループして個別に保存できます。

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet sheet = workbook.Worksheets[i];
    sheet.IsSelected = true; // Make this sheet the active one
    string slidePath = Path.Combine(baseDir, $"Slide_{i + 1}.pptx");
    workbook.Save(slidePath, saveOptions);
}
```

**Pro tip:** 各イテレーションの後で `workbook.Worksheets[i].IsSelected = false` を呼び出すと、同じ `Workbook` オブジェクトを他の操作に再利用する際に便利です。

## Excel の変換方法 – 大容量ファイルへの対処

サイズが数百メガバイトに達する大規模ブックはメモリを圧迫しがちです。以下のテクニックで処理をスムーズに保ちましょう。

1. **Enable Streaming:** `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` を設定すると、Aspose.Cells は RAM にすべて読み込む代わりに一時ファイルを使用します。  
2. **Skip Empty Rows/Columns:** `saveOptions.IgnoreEmptyRows = true` とすれば、不要な空行・空列がスライドに現れなくなります。  
3. **Resize Images:** Excel に高解像度画像が含まれている場合は、`ImageResizeOptions` を使って変換前に縮小できます。  

```csharp
workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;
saveOptions.IgnoreEmptyRows = true;
saveOptions.ImageResizeOptions = new ImageResizeOptions
{
    Width = 1024,
    Height = 768,
    ResizeMode = ResizeMode.Proportional
};
```

## Excel から Pptx を作成 – 結果の検証

`Save` 呼び出しが完了したら、生成されたファイルが正しく利用できるか確認しましょう。

```csharp
if (File.Exists(outputPath))
{
    var fileInfo = new FileInfo(outputPath);
    Console.WriteLine($"File size: {fileInfo.Length / 1024} KB");
    // Optionally launch PowerPoint automatically (Windows only)
    System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
    {
        FileName = outputPath,
        UseShellExecute = true
    });
}
else
{
    Console.Error.WriteLine("Something went wrong – the PPTX was not created.");
}
```

ファイルを開くと、元のスプレッドシートのレイアウトを忠実に再現したスライドデッキが表示され、チャート、テーブル、埋め込み画像がすべて含まれているはずです。

## よくある質問 & エッジケース

| 質問 | 回答 |
|----------|--------|
| *Excel のマクロを保持できますか？* | できません。PowerPoint は Excel の VBA マクロをサポートしていません。必要な自動化は PowerPoint 側で再作成する必要があります。 |
| *セルのコメントはどうなりますか？* | スライド上の別個のテキストボックスとして表示されますが、`saveOptions.IncludeCellComments = false` に設定すれば非表示にできます。 |
| *数式は評価されますか？* | はい。Aspose.Cells は変換前に数式を評価するため、スライドには計算結果が表示され、数式そのものは表示されません。 |
| *スライドのデザインをカスタマイズする方法はありますか？* | 変換後に Aspose.Slides の `Presentation` クラスを使って PowerPoint テンプレートを適用し、生成されたスライドをそのテンプレートにコピーすることで実現できます。 |

## 完全動作サンプル（コードをすべて一箇所にまとめたもの）

```csharp
using Aspose.Cells;
using System;
using System.IO;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build safe file paths
            string baseDir = AppDomain.CurrentDomain.BaseDirectory;
            string inputPath = Path.Combine(baseDir, "input.xlsx");
            string outputPath = Path.Combine(baseDir, "output.pptx");

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Optional: improve memory usage for huge files
            workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;

            // Configure PowerPoint save options
            PresentationSaveOptions saveOptions = new PresentationSaveOptions(SaveFormat.Pptx)
            {
                KeepOriginalFormatting = true,
                IgnoreEmptyRows = true,
                ImageResizeOptions = new ImageResizeOptions
                {
                    Width = 1024,
                    Height = 768,
                    ResizeMode = ResizeMode.Proportional
                }
            };

            // Save as PowerPoint
            workbook.Save(outputPath, saveOptions);

            // Verify the result
            if (File.Exists(outputPath))
            {
                Console.WriteLine($"Success! '{outputPath}' created ({new FileInfo(outputPath).Length / 1024} KB).");
                // Open the file automatically (Windows only)
                System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            else
            {
                Console.Error.WriteLine("Failed to create the PowerPoint file.");
            }
        }
    }
}
```

プログラムを実行すれば、次のクライアントミーティングや取締役会プレゼンテーション、社内ブリーフィングで使える新しい `.pptx` がすぐに手に入ります。

## 結論

これで **Excel を PowerPoint に変換する方法** を C# と Aspose.Cells を使ってマスターしました。基本的な手順は、ワークブックを読み込み、`PresentationSaveOptions` を設定し、`Save` を呼び出すだけとシンプルです。また、本チュートリアルでは **Excel から PowerPoint を生成** する際のメモリ管理などの細かなポイントもカバーしました。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}