---
category: general
date: 2026-09-08
description: Java と Aspose.Cells を使用して Excel を PowerPoint にエクスポートし、PPTX 出力で編集可能なテキストボックスを保持する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- Aspose.Cells Java
- editable text boxes
- ImageOrPrintOptions
- Workbook save
- PowerPoint PPTX export
language: ja
lastmod: 2026-09-08
og_description: Aspose.Cells を使用して Java で Excel を PowerPoint にエクスポートします。このガイドでは、チャートのテキストを編集可能なままに保ち、数分で
  PPTX ファイルを生成する方法を示します。
og_image_alt: Screenshot of Java code exporting an Excel worksheet to a PowerPoint
  slide
og_title: JavaでExcelをPowerPointにエクスポートする – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to export Excel to PowerPoint using Java and Aspose.Cells,
    preserving editable text boxes in the PPTX output.
  headline: How to export Excel to PowerPoint with Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
title: JavaでExcelをPowerPointにエクスポートする方法
url: /ja/java/excel-import-export/how-to-export-excel-to-powerpoint-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を PowerPoint にエクスポートする方法（Java）

If you need to **export Excel to PowerPoint**, this tutorial shows you a clean Java solution. Using **Aspose.Cells Java** you can preserve chart formatting and enable **editable text boxes** in the generated PPTX file.

Excel を PowerPoint にエクスポートする必要がある場合、このチュートリアルではシンプルな Java ソリューションをご紹介します。**Aspose.Cells Java** を使用すると、チャートの書式を保持し、生成された PPTX ファイルで **editable text boxes** を有効にできます。

Exporting a spreadsheet to a presentation is a common requirement when you want to reuse data‑driven charts in slide decks. In this guide you will learn how to:

スプレッドシートをプレゼンテーションにエクスポートすることは、データ駆動型チャートをスライドデッキで再利用したい場合に一般的な要件です。このガイドでは、以下を学びます：

* Load an existing Excel workbook that contains a chart.
* Configure **ImageOrPrintOptions** so the exported slide keeps text boxes editable.
* Save the worksheet as a **PowerPoint PPTX** file in a single method call.
* Run a complete, self‑contained example that you can copy into your own project.

* チャートを含む既存の Excel ワークブックを読み込む。
* **ImageOrPrintOptions** を設定し、エクスポートされたスライドでテキストボックスを編集可能に保つ。
* **PowerPoint PPTX** ファイルとしてワークシートを単一のメソッド呼び出しで保存する。
* 完全な自己完結型サンプルを実行し、プロジェクトにコピーできるようにする。

The only prerequisites are a Java 8 (or newer) runtime and a valid Aspose.Cells for Java license. If you are using the free evaluation version, the output will contain a watermark, but the code works the same.

必要な前提条件は、Java 8（またはそれ以降）のランタイムと有効な Aspose.Cells for Java ライセンスだけです。無料評価版を使用している場合、出力に透かしが入りますが、コードの動作は同じです。

---

## Export Excel to PowerPoint – set up the development environment

## Excel を PowerPoint にエクスポート – 開発環境のセットアップ

Before writing code, make sure you have the following:

コードを書く前に、以下が揃っていることを確認してください：

| Item | Reason |
|------|--------|
| **Java Development Kit (JDK) 8+** | Required to compile and run the example. |
| **Java Development Kit (JDK) 8+** | サンプルをコンパイルおよび実行するために必要です。 |
| **Aspose.Cells for Java** library | Provides the `Workbook`, `ImageOrPrintOptions`, and `SaveFormat` classes used for the conversion. |
| **Aspose.Cells for Java** ライブラリ | 変換に使用される `Workbook`、`ImageOrPrintOptions`、`SaveFormat` クラスを提供します。 |
| **A valid Aspose.Cells license** (optional) | Removes evaluation watermarks and unlocks full functionality. |
| **有効な Aspose.Cells ライセンス**（オプション） | 評価版の透かしを除去し、すべての機能を利用可能にします。 |
| **An Excel file (`chartSheet.xlsx`)** with at least one chart | The source workbook you will export. |
| **Excel ファイル (`chartSheet.xlsx`)**（少なくとも 1 つのチャートを含む） | エクスポート対象となる元のワークブックです。 |

Add the Aspose.Cells JAR to your project’s classpath. If you use Maven, include the dependency:

プロジェクトのクラスパスに Aspose.Cells JAR を追加してください。Maven を使用する場合は、以下の依存関係を含めます：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

---

## Configure ImageOrPrintOptions for editable text boxes

## editable text boxes 用の ImageOrPrintOptions の設定

The `ImageOrPrintOptions` class controls how a worksheet is rendered when exporting. Setting `setExportEditableTextBox(true)` tells Aspose.Cells to keep text elements inside charts as **editable text boxes** in PowerPoint, rather than flattening them into a static image.

`ImageOrPrintOptions` クラスは、エクスポート時にワークシートがどのようにレンダリングされるかを制御します。`setExportEditableTextBox(true)` を設定すると、チャート内のテキスト要素を静的画像にフラット化せず、PowerPoint で **editable text boxes** として保持するよう Aspose.Cells に指示します。

```java
// Create export options for PowerPoint
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);          // Target format is PPTX
exportOptions.setExportEditableTextBox(true);        // Keep chart text editable
```

Why this matters: When you later open the PPTX file in PowerPoint, you can click a chart’s label and edit its content directly, which is essential for presentations that need on‑the‑fly adjustments.

この設定が重要な理由: 後で PowerPoint で PPTX ファイルを開くと、チャートのラベルをクリックして直接内容を編集できるため、プレゼンテーション中に即座に調整が必要な場合に不可欠です。

---

## Load the workbook and export it as a PPTX file

## ワークブックを読み込み、PPTX ファイルとしてエクスポートする

Now load the Excel file, apply the options from the previous step, and call `save`. The `Workbook.save` method accepts the output path and the `ImageOrPrintOptions` instance, handling the conversion internally.

ここで Excel ファイルを読み込み、前ステップで設定したオプションを適用し、`save` を呼び出します。`Workbook.save` メソッドは出力パスと `ImageOrPrintOptions` インスタンスを受け取り、内部で変換を処理します。

```java
// Load the workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

// Export the first worksheet to PowerPoint using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);
```

**Key points**

**重要ポイント**

* `Workbook` represents the entire Excel file. You can also select a specific sheet with `workbook.getWorksheets().get(0)` if you only want to export one sheet.
* `Workbook` は Excel ファイル全体を表します。1 枚のシートだけをエクスポートしたい場合は、`workbook.getWorksheets().get(0)` で特定のシートを選択することもできます。
* The `save` method writes a PPTX file that contains one slide per worksheet by default.
* `save` メソッドは、デフォルトでワークシートごとに 1 スライドを含む PPTX ファイルを書き出します。
* If your workbook contains multiple sheets and you only need the chart sheet, either delete the unwanted sheets before saving or use `ExportOptions.setOnePagePerSheet(false)` to control pagination.
* ワークブックに複数のシートがあり、チャートシートだけが必要な場合は、保存前に不要なシートを削除するか、`ExportOptions.setOnePagePerSheet(false)` を使用してページングを制御してください。

---

## Complete runnable example

## 完全な実行可能サンプル

Below is a minimal, fully runnable Java program that demonstrates the entire flow. Replace `YOUR_DIRECTORY` with an absolute or relative path that points to your files.

以下は、全体のフローを示す最小限の完全実行可能な Java プログラムです。`YOUR_DIRECTORY` をファイルが存在する絶対パスまたは相対パスに置き換えてください。

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook that holds the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

            // 2. Prepare export options for PowerPoint and enable editable text boxes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
            exportOptions.setExportEditableTextBox(true);        // Keep text boxes editable

            // 3. Export the worksheet(s) to a PPTX file
            workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);

            System.out.println("Export completed successfully. Check output.pptx.");
        } catch (Exception e) {
            System.err.println("Error during export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**Expected output**

**期待される出力**

Running the program prints:

プログラムを実行すると次のように出力されます：

```
Export completed successfully. Check output.pptx.
```

When you open `output.pptx` in Microsoft PowerPoint, you will see a slide that mirrors the Excel chart. Double‑click any chart label and you can edit the text directly, confirming that **editable text boxes** are active.

Microsoft PowerPoint で `output.pptx` を開くと、Excel のチャートをそのまま映したスライドが表示されます。チャートのラベルをダブルクリックするとテキストを直接編集でき、**editable text boxes** が有効であることが確認できます。

---

## Handling common variations and edge cases

## 一般的なバリエーションとエッジケースの対処

| Situation | Recommended approach |
|-----------|----------------------|
| **Multiple worksheets** but only one chart sheet should be exported | Use `workbook.getWorksheets().removeAt(index)` to delete unwanted sheets before calling `save`, or set `exportOptions.setOnePagePerSheet(false)` and then manually select the sheet you want to render. |
| **Multiple worksheets** しかしエクスポートすべきは 1 つのチャートシートだけ | `save` を呼び出す前に `workbook.getWorksheets().removeAt(index)` で不要なシートを削除するか、`exportOptions.setOnePagePerSheet(false)` を設定してから手動でレンダリングしたいシートを選択してください。 |
| **Large Excel files** causing memory pressure | Enable streaming mode with `loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` when creating the `Workbook`. |
| **Large Excel files** がメモリ圧迫を引き起こす場合 | `Workbook` 作成時に `loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` を使用してストリーミングモードを有効にします。 |
| **License not set** (evaluation version) | The generated PPTX will contain a watermark. Add `License license = new License(); license.setLicense("Aspose.Cells.lic");` at the start of `main` to remove it. |
| **License not set**（評価版） | 生成された PPTX に透かしが入ります。`main` の冒頭に `License license = new License(); license.setLicense("Aspose.Cells.lic");` を追加して透かしを除去してください。 |
| **Need to export only a specific range** | Create a temporary worksheet, copy the desired range with `worksheet.getCells().copyRange(...)`, and export that temporary sheet. |
| **特定の範囲だけをエクスポートする必要がある場合** | 一時的なワークシートを作成し、`worksheet.getCells().copyRange(...)` で目的の範囲をコピーして、その一時シートをエクスポートします。 |
| **PowerPoint version compatibility** | Aspose.Cells always generates Office Open XML (PPTX) which works with PowerPoint 2007 and later. For older PPT format, change `SaveFormat.PPT` (though editable text boxes are only supported in PPTX). |
| **PowerPoint バージョンの互換性** | Aspose.Cells は常に Office Open XML（PPTX）を生成し、PowerPoint 2007 以降で動作します。古い PPT 形式が必要な場合は `SaveFormat.PPT` に変更してください（ただし editable text boxes は PPTX のみでサポートされます）。 |

---

## Pro tips for production use

## 本番環境でのプロのヒント

* **Batch conversion** – Loop through a directory of Excel files, reusing a single `ImageOrPrintOptions` instance to reduce object creation overhead.
* **バッチ変換** – Excel ファイルが格納されたディレクトリをループし、`ImageOrPrintOptions` インスタンスを1つだけ再利用してオブジェクト生成のオーバーヘッドを削減します。
* **Performance profiling** – Measure the time taken by `workbook.save` for large files; consider increasing the JVM heap (`-Xmx2g`) if you encounter `OutOfMemoryError`.
* **パフォーマンスプロファイリング** – 大きなファイルに対する `workbook.save` の所要時間を測定し、`OutOfMemoryError` が発生した場合は JVM ヒープ（例：`-Xmx2g`）の増加を検討してください。
* **Custom slide layout** – After exporting, you can further manipulate the PPTX using Aspose.Slides for Java to add titles, footers, or apply a master slide.
* **カスタムスライドレイアウト** – エクスポート後、Aspose.Slides for Java を使用して PPTX にタイトルやフッターを追加したり、マスタースライドを適用したりしてさらに操作できます。

---

## Conclusion

## 結論

You now know how to **export Excel to PowerPoint** with Java, preserving chart fidelity and enabling **editable text boxes** via `ImageOrPrintOptions`. The complete example demonstrates loading a workbook, configuring export options, and saving a PPTX file in just three concise steps.  

From here you can explore related topics such as **Aspose.Cells Java chart manipulation**, **PowerPoint PPTX export** with custom templates, or **batch processing multiple spreadsheets**. Experiment with different `SaveFormat` values, combine this approach with Aspose.Slides, and integrate the workflow into your reporting pipeline.

これで、Java を使用して **Excel を PowerPoint にエクスポート** し、チャートの忠実度を保ちつつ `ImageOrPrintOptions` によって **editable text boxes** を有効にする方法が分かりました。完全なサンプルは、ワークブックの読み込み、エクスポートオプションの設定、PPTX ファイルの保存という 3 つの簡潔な手順で実演しています。

ここからは、**Aspose.Cells Java のチャート操作**、カスタムテンプレートを使用した **PowerPoint PPTX エクスポート**、または **複数スプレッドシートのバッチ処理** などの関連トピックを探求できます。さまざまな `SaveFormat` 値を試し、この手法を Aspose.Slides と組み合わせて、レポートパイプラインに統合してください。

---

![Java code exporting Excel to PowerPoint](/images/export-excel-to-powerpoint.png){: .responsive-img alt="Excel を PowerPoint にエクスポートする Java コードのスクリーンショット"}

## What Should You Learn Next?

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [How to Create and Configure Text Boxes in Excel Using Aspose.Cells Java for Enhanced Data Presentation](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
  - Aspose.Cells Java を使用して Excel でテキストボックスを作成および構成する方法（データ表示の強化）
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
  - Aspose.Cells Java を使用して Excel チャートを SVG としてエクスポートする方法（スケーラブルベクターグラフィックス）
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
  - Aspose.Cells Java を使用して Excel ワークシートを PNG にエクスポートする方法

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}