---
category: general
date: 2026-09-05
description: Excelで範囲をコピーする方法、ExcelをPowerPointにエクスポートする方法、そしてExcelをpptxに変換する方法を、完全なJava例とともに学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: ja
lastmod: 2026-09-05
og_description: Java を使って範囲をコピーし、Excel を PowerPoint にエクスポートする方法。ステップバイステップのガイドに従って、Excel
  を効率的に PPTX に変換しましょう。
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: JavaでExcelの範囲をコピーしてPowerPointにエクスポートする方法
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Java を使って Excel の範囲をコピーし、PowerPoint にエクスポートする方法
url: /ja/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で Excel の範囲をコピーし、PowerPoint にエクスポートする方法

Excel ブックから **範囲をコピーする方法** を学び、さらに **Excel を PowerPoint にエクスポート** したい方のために、完全に実行可能なソリューションを提供します。このガイドでは、ピボットテーブルを含む範囲のコピー方法、新しいワークシートへの貼り付け、そして単一のメソッド呼び出しで **Excel を PPTX に変換** する手順を詳しく解説します。

範囲のコピーとブックのエクスポートは、レポートやスライドデッキ、ダッシュボードをプログラムで生成する際に頻繁に求められる要件です。このチュートリアルを終える頃には、以下の機能を持つ Java プログラムが完成します。

* 既存の `.xlsx` ファイルを読み込む。
* ピボットテーブルを含む範囲 `A1:H20` を新しいシートへコピーする。
* ワークブックを編集可能な `.pptx` プレゼンテーションとして保存する。

必要なのは Aspose.Cells for Java ライブラリだけです。追加の依存関係は不要です。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* Java 17（またはそれ以降）がインストール済み
* Maven または Gradle による依存関係管理環境
* Aspose.Cells for Java 23.9（または最新バージョン）— 下記の Maven スニペットのようにプロジェクトに追加してください
* コピー対象のデータとピボットテーブルが含まれる Excel ファイル（`input.xlsx`）

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## 手順 1: ファイルからワークブックをロードする

**範囲をコピーする方法** の最初の操作は、ソースワークブックを開くことです。これにより、ワークシート、セル、ピボットテーブルへアクセスできるようになります。

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*なぜこのステップが必要か？*  
ファイルをロードすると、Excel ドキュメントのメモリ上表現が作成され、元ファイルに手を加えることなく内容を操作できます。

## 手順 2: データが格納されているソースワークシートを取得する

通常、最初のシートにコピーしたいデータが入っています。インデックスで取得できます。

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

ワークブックがピボットテーブルを別シートに保持している場合は、`0` を該当するインデックスに置き換えるか、`get("SheetName")` を使用してください。

## 手順 3: コピー先の新しいワークシートを追加する

コピー先シートを作成すると、コピーしたデータが分離され、後のエクスポートがすっきりします。

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

シート名は自由に設定できますが、`Copy` という名前にすると「コピーした範囲がここにある」ことが明確になります。

## 手順 4: ピボットテーブルを含む範囲をコピーする（how to copy range）

ここでコアとなる **範囲をコピーする方法** を実行します。`copyRange` メソッドは値と書式の両方をコピーし、ピボットテーブルの定義も保持します。

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*`CopyOptions` を使う理由*  
`CopyOptions` インスタンスを提供すると、コピー対象（数式、列幅など）を細かく調整できます。デフォルトコンストラクタはすべてをコピーするため、**コピーしたピボットテーブルシート** を完全に再現したい場合に最適です。

## 手順 5: 編集可能な PowerPoint プレゼンテーションとしてエクスポートするオプションを準備する

PowerPoint へのエクスポートは `ImageOrPrintOptions` を使用して行います。保存形式を `SaveFormat.PPTX` に設定すると、Aspose.Cells は画像ではなく PowerPoint ファイルを生成します。

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

カスタムレイアウトが必要な場合は、`pptOptions` でスライドサイズ、DPI、その他のプレゼンテーション設定を調整できます。

## 手順 6: PPTX ファイルとしてワークブックを保存する（convert excel to pptx）

最後に `workbook.save` を PPTX オプションと共に呼び出します。このステップで **Excel をスライドデッキにエクスポート** します。

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

プログラムが完了すると、`output.pptx` に単一スライドが作成され、コピーした範囲が Excel と同じ見た目（ピボットテーブルのコントロールも含む）で表示されます。

### 期待される出力

`output.pptx` を Microsoft PowerPoint または互換ビューアで開くと、`A1:H20` の範囲が 1 枚のスライドに表示され、セルの色、罫線、ピボットテーブルのレイアウトが保持されています。スライドは完全に編集可能で、テーブルの移動・サイズ変更・書式設定が PowerPoint のネイティブコンテンツと同様に行えます。

## 完全な実行可能サンプル

すべての手順をまとめた自己完結型の Java クラスです。

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

IDE から、またはコマンドラインからクラスを実行してください。

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

ファイルが書き込まれたことを示す確認メッセージが表示されます。

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| **非連続範囲をコピーできますか？** | 複数領域を含む名前付き範囲を使用して `copyRange` を呼び出すか、各ブロックごとに `copyRange` を複数回実行してください。 |
| **ソースシートに複数のピボットテーブルがある場合は？** | コピー矩形内にあるすべてのピボットテーブルが転送されます。矩形外のテーブルは別途コピーしてください。 |
| **複数シートを別々のスライドとしてエクスポートするには？** | ワークシートをループし、各シートを一時シートにコピーしてから `workbook.save` を `pptOptions` で呼び出し、`Presentation` API を使って同一 PPTX に追加します。 |
| **生成された PPTX は編集可能ですか？** | はい。エクスポートはネイティブな PowerPoint オブジェクトを生成するため、テキストの変更やテーブルの形状変更、アニメーションの追加が可能です。 |
| **大規模なワークブックの場合は？** | 高精細度が必要な場合は `pptOptions.setDpi(300)` で DPI を上げてください。ただしメモリ使用量が増えるため、必要に応じてシートをバッチ処理してください。 |

## プロのコツ

* **列幅を保持** – 正確な幅が必要な場合は、コピー前に `CopyOptions.setColumnWidth(true)` を設定します。
* **カスタムスライドサイズ** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` で 16:9 プレゼンテーションに合わせます。
* **タイトルスライドを追加** – エクスポート後、Aspose.Slides で PPTX を開き、タイトルと日付のスライドを先頭に挿入します。

## 結論

これで **Excel の範囲をコピーする方法**、**Excel を PowerPoint にエクスポートする方法**、そして Java を使って **Excel を PPTX に変換する方法** が習得できました。上記の 6 ステップに従えば、レポート生成やライブデータからのスライドデッキ作成を自動化でき、ピボットテーブル機能もそのまま保持できます。

### 次にやることは？

* **コピーしたピボットテーブルシート** のバリエーション（例：ピボットキャッシュのみのコピー）を探求する
* このワークフローに **Aspose.Slides** を組み合わせて、カスタムアニメーションやブランディングを追加する
* スケジュールジョブで数十個のワークブックをバッチ処理する自動化を実装する

オプションを試しながら、独自のレポートパイプラインに合わせてコードを調整してみてください。問題が発生した場合は、Aspose.Cells for Java のドキュメントで `CopyOptions` や `ImageOrPrintOptions` の詳細を確認できます。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}