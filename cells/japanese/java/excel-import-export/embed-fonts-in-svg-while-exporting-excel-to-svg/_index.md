---
category: general
date: 2026-08-14
description: Aspose.Cells を使用して Excel を SVG にエクスポートする際に、SVG にフォントを埋め込む。印刷範囲の設定、印刷オプションの設定、WRAPCOLS
  関数の使用方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: ja
lastmod: 2026-08-14
og_description: Aspose.Cells を使用して Excel を SVG にエクスポートする際に、SVG にフォントを埋め込みます。このガイドでは、印刷範囲の設定、印刷オプションの構成、そして
  WRAPCOLS 関数の適用方法を示します。
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: ExcelをSVGにエクスポートする際にフォントをSVGに埋め込む – ステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: ExcelをSVGにエクスポートする際にフォントをSVGに埋め込む
url: /ja/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を SVG にエクスポートする際のフォント埋め込み

Excel を SVG にエクスポートする際に **フォントを SVG に埋め込む** 必要がある場合、このチュートリアルでは Aspose.Cells for Java を使用した具体的な手順を示します。また、**印刷範囲の設定**、**印刷オプションの設定**、そして **WRAPCOLS 関数の使用** によってレイアウトを失わずにデータを整形する方法もカバーします。

既存のブックブックを読み込み、`WRAPCOLS` 関数を適用し、SVG 固有の画像オプションを構成し、印刷領域を定義し、最後にフォントが埋め込まれた SVG として保存する、完全な実行可能サンプルを順に確認できます。外部ドキュメントは不要です—コードをコピーして実行し、生成された SVG を確認してください。

## SVG にフォントを埋め込む – ImageOrPrintOptions の設定

フォントを埋め込むことで、元のフォントがインストールされていないマシンでも、SVG が Excel 上の表示と全く同じようにレンダリングされます。

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Why this matters*: `setEmbedFonts(true)` を有効にすると、Aspose.Cells はフォントデータを SVG の `<defs>` セクションに直接書き込みます。その結果、ブラウザやプラットフォームを問わず同一の外観を保つ自己完結型ファイルが生成されます。

## Excel を SVG にエクスポート – フルワークフロー

以下の手順は、ブックブックの読み込みから SVG ファイルの保存までのエンドツーエンドのプロセスを示しています。

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Expected output**: `output.svg` が `YOUR_DIRECTORY` に作成されます。ブラウザで開くと、すべてのフォントが埋め込まれたワークシートが表示され、`WRAPCOLS` によりデータが 3 列に折り返され、`A1:H30` 内のセルだけが描画されます。

## ワークシートの印刷範囲を設定する

印刷範囲を定義すると、エクスポートされる SVG が特定の範囲に限定され、ファイルサイズが削減され、閲覧者は関連データに集中できます。

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tip*: 範囲は Excel の A1 形式で指定します。動的な範囲が必要な場合は、`ws.getCells().getMaxDisplayRange()` を使用してプログラムから取得できます。

## SVG 出力の印刷オプションを設定する

印刷オプションは、Aspose.Cells がワークシートを画像に変換する方法を制御します。フォント埋め込みに加えて、解像度、スケーリング、ページレイアウトなどを調整できます。

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Why you should set print options*: 明示的にオプションを設定しない場合、Aspose.Cells はデフォルト設定を使用し、フォント埋め込みが省略されたり、不要なスケーリングが適用されたりして、ぼやけた、またはスタイルが崩れた SVG が生成される可能性があります。

## WRAPCOLS 関数を使用して列データを折り返す

`WRAPCOLS` は、縦方向の範囲を指定した列数に分配する Excel の数式です。長いリストをコンパクトなグリッドで表示したいときに便利です。

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

ブックブックを保存すると、Aspose.Cells が数式を評価し、定義された印刷領域内に 3 列のレイアウトを生成します。この手法は任意のサイズの範囲で機能します—第 2 引数を希望する列数に変更するだけです。

## 完全な実行可能サンプル

以下は任意の IDE に貼り付けて使用できる完全な Java プログラムです。クラスパスに Aspose.Cells for Java ライブラリが含まれていることを確認してください。

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Verification steps**

1. プログラムを実行します。  
2. `output.svg` をウェブブラウザで開きます。  
3. テキストが元の Excel ファイルと同じフォントで表示されていることを確認します（フォントが埋め込まれています）。  
4. `A1:H30` 内のセルだけが表示され、`A2:A10` のデータが 3 列に折り返されていることを検証します。

## よくある落とし穴と回避策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| SVG でフォントが欠落している | `setEmbedFonts(false)` もしくはフォントファイルにアクセスできない | `setEmbedFonts(true)` を設定し、コード実行マシンにフォントがインストールされていることを確認 |
| WRAPCOLS が評価されない | 計算エンジンが無効化されている | エクスポート前に `workbook.calculateFormula()` を呼び出すか、保存時に Aspose.Cells に評価させる |
| エクスポートされた SVG が空白になる | 印刷範囲にデータが含まれていない | `setPrintArea` に渡す範囲を再確認 |
| SVG ファイルが巨大になる | スケーリングが適用されず、解像度が高すぎる | `imgOptions.setResolution(96)` などで DPI を調整 |

## プロのコツ: 複数シートで ImageOrPrintOptions を再利用する

ブックブックに同一の SVG 設定が必要なシートが複数ある場合、単一の `ImageOrPrintOptions` インスタンスを作成し、各シートの `PageSetup` に割り当てます。これによりメモリ使用量が削減され、すべてのエクスポートファイルでフォント埋め込みが一貫します。

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## 次のステップ

* **他のベクターフォーマットへのエクスポート** – `ImageFormat.SVG` を `ImageFormat.PDF` に変更して高品質 PDF を生成。  
* **バッチ処理** – フォルダー内の `.xlsx` ファイルをループし、SVG を自動生成。  
* **カスタムフォント処理** – システムフォントが不足している場合、`FontSettings` を使用して特定ディレクトリからフォントをロード。

**embed fonts in SVG**、**export excel to svg**、**set print area**、**set print options**、**use WRAPCOLS function** をマスターすれば、Excel データからレポート、ダッシュボード、ウェブ可視化用の高忠実度 SVG を自動生成できます。Happy coding!

## 次に学ぶべきことは？

本ガイドで示した手法を基に、以下のチュートリアルで密接に関連するトピックを学べます。各リソースは完全な動作コード例とステップバイステップの解説を含み、追加の API 機能習得や独自プロジェクトでの代替実装アプローチの探索に役立ちます。

- [Aspose.Cells for .NET を使用した Excel の印刷範囲の設定方法](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Aspose.Cells Net で Excel の印刷範囲を設定する](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Aspose.Cells Net で Excel の印刷範囲を設定する](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}