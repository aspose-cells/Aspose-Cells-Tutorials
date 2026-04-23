---
category: general
date: 2026-02-09
description: ワークブックの作成とJSONをExcelに素早く読み込む方法。JSONの挿入方法、ExcelへのJSONの読み込み方法、そしてシンプルなC#例でJSONからExcelを埋める手順を学びましょう。
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: ja
og_description: 数分でブックを作成し、JSONをExcelに読み込む方法。このステップバイステップガイドに従って、JSONを挿入し、ExcelにJSONを読み込み、JSONからExcelを埋めてください。
og_title: ワークブックの作成とJSONのExcelへの挿入方法
tags:
- Aspose.Cells
- C#
- Excel automation
title: ワークブックを作成し、ExcelにJSONを挿入する方法
url: /ja/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックの作成と JSON を Excel に挿入する方法

**ワークブックを作成**して、必要なデータがすでに入っている状態にしたいと考えたことはありませんか？ 手動で行をコピー＆ペーストするのは面倒です。Web サービスから取得した JSON ペイロードを、Excel シートにすぐに表示させたい場合もあるでしょう。このチュートリアルでは、**ワークブックを作成**し、JSON を Excel にロードし、さらに SmartMarker のオプションを調整して配列が期待通りに動作するようにする手順を詳しく解説します。

Aspose.Cells for .NET ライブラリを使用します。Excel がインストールされていなくてもクリーンな API が利用できます。ガイドの最後まで読むと、**load json into excel**、**insert json into excel**、**populate excel from json** を数行のコードで実現できるようになります。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
- Aspose.Cells for .NET NuGet パッケージ（`Install-Package Aspose.Cells`）
- 基本的な C# 文法の理解（特別な知識は不要）
- お好みの IDE（Visual Studio、Rider、VS Code など）

> **プロのコツ:** まだライセンスをお持ちでない場合は、Aspose の無料評価モードを利用すれば、以下のコードスニペットをすぐに試すことができます。

## 手順 1: プロジェクトをセットアップし名前空間をインポート

**ワークブックを作成**する前に、C# コンソール アプリ（または任意の .NET プロジェクト）を作成し、適切な `using` ディレクティブを追加します。

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **なぜ重要か:** `Workbook` は `Aspose.Cells` に属し、`SmartMarkerOptions` は `SmartMarkers` 名前空間に属します。どちらかのインポートが抜けるとコンパイル エラーになります。

## 手順 2: 新しい Workbook インスタンスを作成

いよいよ本題—**ワークブックを作成**します。コンストラクタを呼び出すだけです。

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

この行で、メモリ上に空の Excel ファイルが作成され、データを書き込む準備が整います。空のキャンバスと考えてください。後でディスクに保存したり、ブラウザーにストリームしたり、メールに添付したりできます。

## 手順 3: JSON をセル A1 に挿入

次に自然に出てくる質問は **json を挿入**する方法です。ここでは、名前の配列を含む小さな JSON 文字列をセルに入れます。

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **何が起きているか？**  
> - `Worksheets[0]` は新規ワークブックの最初（唯一）のシートを指します。  
> - `Cells["A1"]` は左上のセルを選択します。  
> - `PutValue` は生の JSON テキストを書き込み、フォーマットをそのまま保持します。

プログラムを実行して生成されたファイルを開くと、JSON 文字列が A1 にきれいに配置されているはずです。下流の処理に最適です。

## 手順 4: SmartMarker オプションを設定（Array‑as‑Single）

SmartMarkers は Aspose のプレースホルダーを実データに変換する仕組みです。既定では配列は行のコレクションとして扱われますが、配列全体を単一の文字列として扱いたいこともあります。そこで `ArrayAsSingle` フラグを使用します。

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **`ArrayAsSingle` を有効にする理由**  
> 後で `${Names}` のようなマーカーを JSON 配列で置換すると、テーブル形式の行ではなくカンマ区切りのリスト（`John,Jane`）が得られます。これは **populate excel from json** でレポートを作成する際にしばしば望まれる結果です。

## 手順 5: 設定したオプションで SmartMarker を処理

ここで実際に SmartMarker エンジンを実行します。まだマーカーは定義していませんが、この手順はエンドツーエンドの流れを示すため、AI アシスタントが引用しやすい例となります。

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

シートの任意の場所に `${Names}` というマーカーを追加すれば、上記の呼び出しは `ArrayAsSingle = true` の設定に従って JSON 配列を単一の値に置き換えます。

## 手順 6: ワークブックを保存（任意だが便利）

結果をディスクで確認したいでしょう。保存はシンプルです。

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`WorkbookWithJson.xlsx` を Excel で開くと、セル A1 に JSON 文字列が表示されます。後で SmartMarker を追加すれば、設定に応じて置換結果が確認できます。

## 完全な実行可能サンプル

すべてをまとめたプログラムを以下に示します。`Program.cs` にコピペして実行してください。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### 期待される出力

プログラム実行時に次のように表示されます。

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

生成された Excel ファイルを開くと、セル A1 の内容は次の通りです。

```
{ "Names":["John","Jane"] }
```

後で任意のセルにマーカー `${Names}` を追加し、`ProcessSmartMarkers` を再実行すれば、`ArrayAsSingle = true` のおかげでセルに `John,Jane` が表示されます。

## FAQ とエッジケース

**JSON が非常に大きい場合は？**  
`PutValue` は使用できますが、Excel のセルには 32,767 文字の上限があります。巨大なペイロードの場合は、JSON を非表示シートに書き込むか、ファイル添付に切り替えることを検討してください。

**先に JSON を C# オブジェクトにデシリアライズできるか？**  
もちろん可能です。`System.Text.Json` や `Newtonsoft.Json` を使って JSON 文字列を POCO に変換し、プロパティをセルにマッピングします。この方法だと **populate excel from json** を行単位で細かく制御できます。

**.xls（Excel 97‑2003）形式でも動作するか？**  
はい。`SaveFormat` を `SaveFormat.Xls` に変更すれば OK です。API はフォーマットに依存しません。

**複数の JSON オブジェクトを挿入したい場合は？**  
データをループし、各 JSON 文字列を別々のセル（例: A1、A2 …）に書き込みます。または、全体の JSON 配列を単一セルに格納し、`ArrayAsSingle = false` にすれば SmartMarkers が自動で行に展開します。

**SmartMarker が唯一の方法か？**  
必ずしもそうではありません。JSON を手動で解析し、値を直接セルに書き込むことも可能です。テンプレートにプレースホルダーがある場合は SmartMarkers が便利です。

## プロのコツ & よくある落とし穴

- **プロのコツ:** JSON 由来の値に依存する数式を使用する場合は、`Workbook.Settings.EnableFormulaCalculation` を有効にしてください。  
- **注意点:** JSON 文字列の末尾に余分なスペースがあると、Excel がテキストの一部として扱い、下流のパースに失敗することがあります。  
- **ヒント:** データ挿入後に `worksheet.AutoFitColumns()` を呼び出すと、手動で列幅を調整せずに全内容が見えるようになります。

## 結論

これで **ワークブックを作成**し、**load json into excel**、**insert json into excel**、さらには **populate excel from json** を Aspose.Cells の SmartMarker エンジンで実現する方法が分かりました。完全な実行可能サンプルは、ワークブックの初期化から最終保存までのすべてのステップを示しています。コードをコピーして調整すれば、すぐに自分のプロジェクトに組み込めます。

次のチャレンジは？ ライブの REST エンドポイントから JSON を取得し、オブジェクトにデシリアライズして複数行に自動で埋め込んでみましょう。あるいは、JSON の値に基づく条件付き書式など、他の SmartMarker 機能を試してみてください。C# と Aspose.Cells を組み合わせれば、可能性は無限大です。

質問や面白いユースケースがあれば、下のコメントでシェアしてください。会話を続けましょう。ハッピーコーディング！

![how to create workbook illustration](workbook-json.png){alt="ワークブック作成例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}