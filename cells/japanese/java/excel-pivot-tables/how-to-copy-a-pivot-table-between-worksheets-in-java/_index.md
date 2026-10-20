---
category: general
date: 2026-10-16
description: Aspose.Cells を使用した Java でのピボットテーブルのコピー方法 – 範囲を別シートにコピーし、ワークシート間で効率的に範囲をコピーする方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: ja
lastmod: 2026-10-16
og_description: Aspose.Cells を使用した Java でのピボットテーブルのコピー方法。このチュートリアルでは、範囲を別のシートにコピーする方法と、ワークシート間で範囲をコピーする方法を、完全なコードとともに示します。
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Javaでワークシート間のピボットテーブルをコピーする方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Javaでワークシート間のピボットテーブルをコピーする方法
url: /ja/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークシート間でピボットテーブルをコピーする方法（Java）

同じブック内でシート間で **ピボットテーブルをコピーする方法** が必要な場合、このガイドは完全な、すぐに実行できるソリューションを提供します。ピボットテーブルを含むソース範囲のコピー方法、機能を保持する方法、結果の検証方法を、すべて Aspose.Cells for Java を使用して確認できます。

ピボットテーブルのコピーは、プログラムでレポートを生成する際によくある作業で、正しく行うことでピボットキャッシュの喪失や数式の破損を防げます。このチュートリアルの最後までに、**範囲を別シートにコピー** および **シート間で範囲をコピー** を手動の手順なしで実行できるようになります。

## 学習内容

* ピボットテーブルを含む既存の Excel ファイルをロードする。
* ピボットテーブルが格納されているソース範囲を定義する。
* 別のワークシート上の宛先範囲を定義する。
* `CopyOptions` を使用してピボットテーブルをそのまま保持する。
* コピーされたピボットテーブルが期待通りに動作することを検証する。

**前提条件**

* Java 17 以降。
* Aspose.Cells for Java（バージョン 23.12 以上）。  
* 最初のシートにピボットテーブルが含まれる Excel ファイル（`input.xlsx`）。

---

## Aspose.Cells を使用したピボットテーブルのコピー方法

この操作の核心は4ステップのプロセスです：ブックをロードし、ソース範囲を特定し、宛先範囲を設定し、コピーを実行します。以下で各ステップを詳細に説明します。

### 手順 1: ブックをロードする

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*このステップの目的は？*  
ブックをロードすると、ファイル全体がメモリに読み込まれ、ワークシート、セル、ピボットキャッシュにアクセスできるようになります。Aspose.Cells はファイル形式を自動的に読み取るため、`.xls` と `.xlsx` を意識する必要はありません。

### 手順 2: ピボットテーブルを含むソース範囲を特定する

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*このステップの目的は？*  
ピボットテーブルは、非表示のキャッシュも参照するセルブロックに格納されています。正確な範囲（この例では `A1:G20`）を選択することで、コピー時にキャッシュがリンクされたままになることを保証します。

### 手順 3: 別シート上の宛先範囲を定義する

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*このステップの目的は？*  
別のワークシート上に宛先を選択することで、**範囲を別シートにコピー** できます。左上のセル（`A1`）は一般的な開始位置ですが、アドレスを変更すれば任意の場所に配置できます。

### 手順 4: ピボットテーブルを保持しながらソース範囲をコピーする

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*このステップの目的は？*  
`CopyOptions` は転送される内容を制御します。`PasteType.PASTE_ALL` を使用すると、ピボットテーブル、その書式設定、基になる数式がすべて複製されることが保証されます。これらのオプションを指定しない場合、コピーされるのは生の値だけになる可能性があり、ピボット機能が壊れます。

### 手順 5: ブックを保存し、結果を検証する

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

`output.xlsx` を Excel で開き、以下を確認します：

* 2 番目のシートに、元と同一の完全に機能するピボットテーブルが含まれていること。
* ピボットテーブルを更新（リフレッシュ）するとデータが更新され、キャッシュが保持されていることが証明されること。

---

## Java を使用して範囲を別シートにコピーする

ピボットテーブルなしで単に **範囲を別シートにコピー** することが目的であれば、同じコードが通常のセル範囲でも機能します。唯一の変更点はソースアドレスです。`CopyOptions` の設定は同じままで、数式と書式が保持されます。

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

このスニペットは、ピボットシナリオと非ピボットシナリオの両方に対する API の柔軟性を示しています。

---

## シート間で範囲をコピーして数式を失わない方法

**シート間で範囲をコピー** すると、他のシートを参照する数式は相対参照が変わると壊れる可能性があります。これを防ぐには：

1. 数式だけが必要な場合は `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` を使用します。
2. 宛先シートを同じブック内に保ち、内部参照が有効なままにします。
3. コピー後に `workbook.calculateFormula();` を呼び出して再計算を強制します。

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

これらの追加手順により、コピーされた範囲は元の範囲と全く同じ動作をし、複数シートにまたがる場合でも正しく機能します。

---

## プロのコツと一般的な落とし穴

| Situation | Tip |
|-----------|-----|
| **ピボットキャッシュが更新されない** | コピー後に `destSheet.getPivotTables().get(0).refresh();` を呼び出してキャッシュを更新します。 |
| **別のブックへのコピー** | `Workbook destWorkbook = new Workbook();` を使用し、次に `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);` を実行します。必要に応じてピボットキャッシュを別途コピーすることを忘れないでください。 |
| **大規模なピボットテーブル** | コピー中に `OutOfMemoryError` が発生しないよう、Java ヒープサイズ（`-Xmx2g`）を増やします。 |
| **スタイルの保持** | `copyOptions.setPasteType(PasteType.PASTE_ALL)` を設定します。設定しない場合、値だけがコピーされます。 |

---

## 期待される出力

プログラム全体を実行すると `output.xlsx` が生成されます。Excel で開くと：

* **Sheet2!A1:G20** は **Sheet1!A1:G20** と同じピボットテーブルを表示します。
* ピボットフィールドリスト、行/列ラベル、データ値がソースと一致します。
* ピボットを更新すると数値が更新され、キャッシュが機能していることが確認できます。

```
Pivot table copied successfully.
```

---

## 結論

このチュートリアルでは、Aspose.Cells for Java を使用して、あるワークシートから別のワークシートへ **ピボットテーブルをコピーする方法** を学びました。ブックをロードし、正しいソース範囲を選択し、宛先を定義し、`CopyOptions` を設定することで、すべてのピボット機能を保持したまま **範囲を別シートにコピー** および **シート間で範囲をコピー** を確実に実行できます。  

次に検討できること：

* コピーしたピボットテーブルを PDF や HTML にエクスポートする。
* 複数ブックにわたるピボットテーブルの自動リフレッシュ。
* `CopyOptions` を使用して特定の要素（例：値、書式）だけをコピーする。

さまざまな範囲アドレスやブック構造、さらにはブック間コピーを試してみてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Java で範囲をコピーする方法 – Aspose.Cells を使用したピボットテーブルのコピー](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Java でピボットテーブルをコピーする方法 – 完全な Aspose.Cells ガイド](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Excel のピボットテーブルコピー – Java を使用したステップバイステップガイド](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}