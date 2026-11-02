---
category: general
date: 2026-09-11
description: Aspose.Cells を使用して新しいワークシートを作成し、Excel の範囲をコピーします。ピボットテーブルを保持したまま、シート間で範囲をコピーする方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: ja
lastmod: 2026-09-11
og_description: Aspose.Cells を使用して新しいワークシートを作成し、Excel の範囲をコピーします。このチュートリアルでは、シート間で範囲をコピーし、ピボットテーブルをそのまま保持する正確な手順を示します。
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: 新しいワークシートを作成し、Excel範囲をコピーする – Aspose.Cells ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Aspose.Cells を使用して新しいワークシートを作成し、Excel の範囲をコピーする
url: /ja/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して新しいワークシートを作成し、Excel 範囲をコピーする

Excel ファイル内でデータを移動し、**create new worksheet** が必要な場合、Aspose.Cells はシンプルに実行できます。このガイドでは、範囲内のピボットテーブルを保持したまま、あるシートから別のシートへ Excel 範囲をコピーする方法を正確に示します。

このガイドでは、**copy excel range** の方法、**copy range between sheets** の方法、そして Aspose.Cells の `copy` メソッドがピボットテーブル定義をそのまま保持する理由を学びます。外部ツールは不要で、Aspose.Cells ライブラリを使用した Java プロジェクトだけで完了します。

## 前提条件

- Java 17 以降がインストールされていること
- Aspose.Cells for Java（バージョン 23.12 以降）をプロジェクトのクラスパスに追加していること
- コピーしたい範囲にピボットテーブルが含まれるソース ワークブック（`input.xlsx`）
- Java の構文と Maven/Gradle の依存関係管理に関する基本的な知識

## ステップ 1: プロジェクトを設定し、Aspose.Cells をインポートする

シンプルな Maven プロジェクト（または好みで Gradle）を作成し、Aspose.Cells の依存関係を追加します。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

次に、Java ソースファイルで必要なクラスをインポートします。

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Why this step matters*: 正しいクラスをインポートすることで、`Workbook`、`Worksheet`、`Range`、および範囲転送を処理する `copy` メソッドにアクセスできるようになります。

## ステップ 2: ソース ワークブックをロードする

コピーしたいデータが含まれるワークブックを開きます。以下のコードは、指定したディレクトリから `input.xlsx` をロードします。

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explanation*: `Workbook` は Excel ファイル全体を表します。1 回ロードすれば、すべてのシートとセル コレクションに対して読み書きアクセスが可能になります。

## ステップ 3: ピボットテーブルを含むソース範囲を特定する

ピボットテーブルが配置されているワークシートを選択し、コピーしたい正確なセルブロックを定義します。この例ではセル A1 から D20 をコピーします。

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Why this matters*: `Range` オブジェクトを作成することで、Aspose.Cells に対し、どのセル（ピボットテーブルなどの埋め込みオブジェクトを含む）を複製すべきか正確に指示できます。

## ステップ 4: コピーされたデータを受け取る **Create new worksheet** を作成する

ここで同じワークブックに新しいシートを追加します。ここが主要キーワードが登場するポイントです。

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explanation*: 新しいシートを追加することでコピーされたデータが分離され、元のシートに影響を与えずに **copy excel range** 操作が成功したことを簡単に確認できます。

## ステップ 5: 範囲をコピー – ピボットテーブルは自動的に保持される

`copy` メソッドを使用して、ソースシートから宛先シートへ範囲を移動します。Aspose.Cells は数式、書式設定、ピボットテーブル定義をコピーします。

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Why this works*: `copy` メソッドはソースセルのディープコピーを実行します。単に値をコピーするだけでなく、ピボットキャッシュを含むセル構造全体を複製します。そのため、**copy range aspose.cells** を使用しても、新しいシートに機能するピボットテーブルが表示されます。

## ステップ 6: 新しいワークシートを含むワークブックを保存する

最後に、変更されたワークブックを書き込みます。

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Result*: `output.xlsx` には元のシートに加えて、**Copy** という名前の新しいシートが含まれ、同一の範囲とピボットテーブルが保持されています。

## 完全な動作例

すべての要素を組み合わせた、完全で実行可能なプログラムは以下の通りです。

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected output**: Excel で `output.xlsx` を開くと、**Copy** というシートが表示され、セル A1:D20 に元と同じデータ、書式設定、そして同一のアクティブなピボットテーブルが含まれています。

## よくある質問とエッジケース

- **What if the source range contains merged cells?**  
  `copy` メソッドは結合情報もコピーするため、結合されたセルは宛先シートでも変更されずに表示されます。

- **Can I copy to a different workbook?**  
  はい。2 つ目の `Workbook` インスタンスをロードし、そのブック内に宛先範囲を作成して `sourceRange.copy(destinationRange)` を呼び出します。このメソッドはブック間のコピーを自動的に処理します。

- **What if the destination sheet already has data?**  
  コピー操作は、宛先範囲と重なる既存のセルを上書きします。データ損失を防ぐには、宛先領域が空であることを確認するか、別の開始セル（例: `"B2"`）を使用してください。

- **Is the pivot cache duplicated?**  
  Aspose.Cells は元のピボットキャッシュを再利用するため、新しいピボットテーブルは同じソースデータにリンクしたままです。独立したキャッシュが必要な場合は、コピー後にピボットテーブルを再作成する必要があります。

## ヒントとベストプラクティス

- **Pro tip**: コピーしたブロック外のデータに依存する数式が範囲に含まれる場合、保存前に `Workbook.setForceFormulaRecalculation(true)` を使用してください。

- **Watch out for** 大きな範囲: 大規模なシートをコピーすると大量のメモリを消費する可能性があります。`OutOfMemoryError` が発生した場合は、より小さなチャンクに分割してコピーすることを検討してください。

- **Performance tip**: 非常に大きなファイルを扱う際は、画面更新を無効に（`workbook.getSettings().setCalculateFormulaOnOpen(false)`）してコピー処理を高速化してください。

## 結論

これで、Aspose.Cells を使用してシート間で **create new worksheet** と **copy excel range** を行い、ピボットテーブルやすべてのセル属性を保持する方法が分かりました。この手法により、データブロックをプログラムで複製したり、レポートテンプレートを作成したり、手動のコピー＆ペーストなしでワークブックを再構築したりできます。

次に、クロスブック操作のための **copy range aspose.cells**、ピボットテーブルの自動更新、コピーしたシートの PDF へのエクスポートなど、関連トピックを探求してください。さまざまなソース範囲やシート名を試して、特定の自動化シナリオに合わせてみましょう。Happy coding!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}