---
category: general
date: 2026-03-18
description: 新しいブックを作成し、数値の精度を保ったままExcelをTXTにエクスポートします。ワークシートをTXTとして保存する方法と、ワークシートを効率的にTXTに変換する方法を学びましょう。
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: ja
og_description: 新しいブックを作成し、Excel を正確に TXT にエクスポートします。このチュートリアルでは、ワークシートを TXT として保存する方法と、C#
  を使用してワークシートを TXT に変換する方法を示します。
og_title: 新しいブックを作成 – ExcelをTXTにエクスポートするガイド
tags:
- Aspose.Cells
- C#
- Excel automation
title: 新しいブックを作成 – 完全精度でExcelをTXTにエクスポート
url: /ja/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新しいワークブックの作成 – Excel を TXT にエクスポート（完全精度）

C# で **新しいワークブックを作成** し、データをプレーンテキストファイルにダンプしたことはありませんか？レガシーシステムからレポートを取得し、下流ツールが `.txt` フィードしか受け付けない場合などです。朗報です！数値の精度を犠牲にする必要はなく、CSV 文字列を手作業で作成する必要もありません。

このガイドでは **excel を txt にエクスポート** する全プロセスを解説します。ワークブックの初期化から、**ワークシートを txt として保存** する際に末尾のゼロを保持する方法まで網羅しています。最後には、任意の .NET プロジェクトにそのまま貼り付けられる実行可能なスニペットが手に入ります。

## 必要なもの

- **ASP.NET / .NET 6+**（コードは .NET Framework 4.6+ でも動作します）  
- **Aspose.Cells for .NET** – `Workbook`、`Worksheet`、`TxtSaveOptions` クラスを提供するライブラリです。NuGet で `Install-Package Aspose.Cells` として取得できます。  
- C# の基本的な知識（`using` 文が書ければ問題ありません）。  

以上です—Excel の Interop や COM オブジェクトは不要、手動で文字列を結合する必要もありません。

---

## 手順 1: 新しいワークブックを初期化する（主要キーワード）

最初にやるべきことは **新しいワークブックを作成** することです。ワークブックは、後で数値やテキスト、数式を貼り付けるための空白キャンバスと考えてください。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **なぜ重要か:** ファイルをロードせずに `Workbook` をインスタンス化すると、真っ白な状態からデータをプログラムで追加できます。これは既存の `.xlsx` がない **ワークシートを txt に変換** シナリオに最適です。

---

## 手順 2: セルにデータを入力 – 末尾のゼロを保持

数値をテキストにダンプする際の一般的な落とし穴は、末尾のゼロが失われることです（例: `123.45000` が `123.45` になる）。下流システムが固定幅フィールドを要求する場合、このロスは致命的です。

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **プロのコツ:** `PutValue` は自動的にデータ型を推測します。数値に見える文字列が必要な場合は `PutValue("123.45000")` のように文字列として渡してください。

---

## 手順 3: TXT 保存オプションを設定 – 数値精度を保持

ここが魔法の部分です。`PreserveNumericPrecision` をオンにすることで、Aspose.Cells に入力した正確な値（不要な末尾のゼロを含む）を書き出すよう指示できます。

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **なぜ有効にするのか:** **excel を txt として保存** すると、既定では不要な小数点以下が削除されます。`PreserveNumericPrecision = true` を設定すると、出力がセルに表示されている値と完全に一致し、財務レポートや科学データで特に重要です。

---

## 手順 4: ワークシートを TXT として保存 – 最終エクスポート

いよいよ **ワークシートを txt として保存** します。書き込み権限がある任意のパスを指定できます。例では相対フォルダー `output` を使用しています。

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **期待される出力**（`num-preserve.txt`）:

```
123.45000
```

末尾のゼロがそのまま残っていることが確認できます。これが求めていた結果です。

---

## 手順 5: 結果を検証 – 簡易チェック

プログラム実行後、任意のテキストエディタで `num-preserve.txt` を開きます。単一行の `123.45000` が表示されていれば成功です。`123.45` と表示された場合は、`PreserveNumericPrecision` が `true` になっているか、Aspose.Cells のバージョンが v23.10 以上かを再確認してください。

---

## よくあるバリエーションとエッジケース

### 複数セルまたは範囲をエクスポート

全範囲を **excel を txt にエクスポート** したい場合は、保存前にさらにセルを埋めれば OK です。

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

デフォルトでは各セルが新しい行として書き出されます。`txtSaveOptions.Separator` で区切り文字（タブ、カンマなど）を変更できます。

### エンコーディングを変えてワークシートを TXT に変換

下流システムが UTF‑8 BOM や ASCII を要求することがあります。その場合は次のようにエンコーディングを指定します。

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### 大規模ワークブックの取り扱い

数十万行規模のシートを処理する場合は、出力をストリーミングすることを検討してください。

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## プロのコツと落とし穴

- **出力ディレクトリを事前に作成** することを忘れないでください。作成していないと `DirectoryNotFoundException` が発生します。  
- **ロケール固有の小数点記号に注意**。環境がカンマ（`1,23`）を使用している場合は、`txtSaveOptions.DecimalSeparator = '.'` と設定してドットを強制してください。  
- **バージョン互換性**: `PreserveNumericPrecision` フラグは Aspose.Cells 20.6 で導入されました。古いバージョンを使用している場合はフラグが存在せず、保存前にセルをテキスト形式にフォーマットする必要があります。

---

![新しいワークブックの例](excel-to-txt.png "新しいワークブック")

*画像代替テキスト: 「新しいワークブックを作成し、数値精度を保持したまま Excel を TXT にエクスポート」*

---

## まとめ – カバーした内容

- Aspose.Cells を使った **新しいワークブックの作成**。  
- 末尾ゼロを含む数値をセルに入力。  
- `TxtSaveOptions.PreserveNumericPrecision = true` を設定して **excel を txt として保存** し、精度を失わない方法。  
- ファイルを書き出し、出力が元の値と一致することを検証。  

これで 50 行未満の C# コードで **ワークシートを txt に変換** するフルワークフローが完了です。

---

## 次のステップと関連トピック

**excel を txt にエクスポート** の精度が確保できたら、以下も検討してみてください。

- カスタム区切り文字付き **CSV エクスポート**（`TxtSaveOptions.Separator`）。  
- TSV など他のプレーンテキスト形式への **保存**（`SaveFormat.TabDelimited`）。  
- `Directory.GetFiles` を使ったフォルダー内複数ワークブックの **バッチ処理**。  
- Azure Functions と統合し、クラウド上でオンデマンド変換を実現。

いずれも同じ `Workbook` → `Worksheet` → `TxtSaveOptions` パターンなので、すぐに慣れるはずです。

---

### 最後に

この手順を踏めば、**新しいワークブックを作成**し、データを入力し、**ワークシートを txt として保存** する際に、必要なすべての小数点以下を保持できるようになります。コードは小さくても、レガシーパイプラインがプレーンテキスト入力を要求するという意外に多い課題を解決します。

ぜひ試してみて、オプションを調整しながらデータを思い通りに流してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}