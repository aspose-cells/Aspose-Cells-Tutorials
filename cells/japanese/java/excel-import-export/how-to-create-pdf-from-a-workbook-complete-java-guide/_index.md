---
category: general
date: 2026-03-01
description: Aspose.Cells for Java を使用して PDF を作成し、ブックを PDF として保存し、Excel を HTML にエクスポートし、expand
  関数を利用する方法。ステップバイステップのコードを含む。
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: ja
og_description: Aspose.Cells for Java を使用してワークブックから PDF を作成する方法。ワークブックを PDF として保存し、Excel
  を HTML にエクスポートし、EXPAND 関数を使用する方法を学びます。
og_title: ワークブックからPDFを作成する方法 – Javaチュートリアル
tags:
- Aspose.Cells
- Java
- PDF generation
title: ワークブックからPDFを作成する方法 – 完全なJavaガイド
url: /ja/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックからPDFを作成する方法 – 完全なJavaガイド

サードパーティのコンバータを使わずに、Excelワークブックから直接 **PDFを作成する方法** を考えたことはありませんか？ あなたは一人ではありません。多くの開発者は、迅速なPDFエクスポート、HTMLプレビュー、または高度な配列数式が一度に必要になると壁にぶつかります。  

このチュートリアルでは、まさにそれを実現する単一の自己完結型Javaプログラムを順を追って解説します。**ワークブックをPDFとして保存**し、凍結行を保持したまま **ExcelをHTMLにエクスポート**する方法を示し、ワークシート内で **EXPAND関数を使用**する方法をデモします。最後まで実行可能なプロジェクトが手に入り、任意のMavenまたはGradleビルドに組み込むことができます。

> **Pro tip:** 以下のコードはすべて Aspose.Cells 23.10（またはそれ以降）で動作します。古いバージョンを使用している場合、メソッド名が若干異なることがあります。

---

## 前提条件

- **Java 17**（または任意のLTSバージョン）をインストールし、設定済みであること。
- **Aspose.Cells for Java** ライブラリ。`pom.xml` に以下のMaven依存関係を追加してください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- お好みのIDEまたはテキストエディタ（IntelliJ IDEA、VS Code、Eclipse など）。

外部APIやWebサービスは不要です。純粋なJavaとAspose.Cells SDKだけで完結します。

---

## ソリューションの概要

実装は **7つの論理的ステップ** に分割します：

1. ワークブックを作成し、**EXPAND** 関数をデモする。  
2. フォントバリエーションセレクタを有効にし、**ワークブックをPDFとして保存**する。  
3. 同じワークブックをHTMLにエクスポートし、凍結行を保持する。  
4. `IF` パラメータ付きのSmart Markerを使用して条件付きテキストを挿入する。  
5. 階層データ用のマスタ‑ディテールSmart Markerを適用する。  
6. Base‑64エンコードされた画像を含むMarkdownファイルをロードする。  
7. GridJsオプションを設定し、データを挿入する。

各ステップは独自のメソッドにラップされており、`main` メソッドをすっきり保ちつつ、**何を** 行うかだけでなく **なぜ** それを行うのかを示します。

---

## Step 1 – ワークブックを作成し、EXPAND 関数を使用

**EXPAND** 関数は Office 365 で導入された新しい動的配列数式です。セルを手動でコピーせずに、範囲をより大きな領域へ「スピル」させることができます。

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**この重要性:**  
- `EXPAND` は結果を自動的に空白で埋めるため、後で **ワークブックをPDFとして保存** するときに、PDF がきれいな長方形のテーブルとして表示されます。  
- `calculateFormula()` を呼び出すことで、エクスポート前に数式エンジンが実行されます。

---

## Step 2 – フォントバリエーションセレクタを有効にし、**ワークブックをPDFとして保存**

高度なタイポグラフィ（例: 絵文字やCJKバリエーションセレクタ）をサポートする必要がある場合、保存 **前に** この機能をオンにする必要があります。

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**重要ポイント:** 主要キーワード **how to create pdf** の答えはここにあります。設定を行った後に `workbook.save(..., SaveFormat.PDF)` を呼び出すことで実現します。

---

## Step 3 – **ExcelをHTMLにエクスポート**し、凍結行を保持

ステークホルダーが迅速なWebプレビューを求めることがよくあります。Aspose.Cells はHTMLへのエクスポートをサポートしており、`setPreserveFrozenRows(true)` を使用すると Excel と同様のスクロール体験が保たれます。

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**なぜ重要か:** 凍結行はユーザビリティ向上のための便利機能です。これがないと、ページをスクロールした際にヘッダー行が消えてしまいます。

---

## Step 4 – IF パラメータ付き Smart Marker

Smart Marker を使うと、ループを書かずにデータをテンプレートにマージできます。`if` パラメータはマーカー内に直接条件ロジックを組み込むことができます。

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

出力されるPDFは **「VIP Customer: Acme Corp」** と表示されます（`IsVIP` が `true` のため）。フラグを `false` に変更すると **「Regular Customer: Acme Corp」** が出力され、追加コードは不要です。

---

## Step 5 – 階層範囲を使用したマスタ‑ディテール Smart Marker

親子データ（例: 注文と明細行）がある場合、マスタ‑ディテールマーカーを使うと手動で行を挿入する手間が省けます。

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**得られる効果:** エンジンが各注文ごとにマスタ行を展開し、明細行を自動的にその下にネストします。請求書や購買レポートに最適です。

---

## Step 6 – 埋め込み Base‑64 画像付き Markdown ドキュメントのロード

ソースデータが Markdown にある場合（ドキュメントパイプラインで一般的）、Aspose.Cells はそれを直接ワークブックにレンダリングできます。

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**エッジケースの注意:** Base‑64 文字列が不正な場合、Aspose は画像をスキップしますが、ドキュメントの残りの部分は引き続き処理され、クラッシュは起きません。

---

## Step 7 – GridJs オプションを設定しデータを挿入

GridJs は軽量な JavaScript グリッドで、Aspose はそれをHTMLにレンダリングできます。数値の右揃えや罫線の適用は可読性を向上させます。

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**なぜ重要か:** 適切な配置と罫線により、生成されたHTMLは洗練されたスプレッドシートのように見え、ダッシュボードでの利用に適しています。

---

## 全体をまとめる – `main` メソッド

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}