---
category: general
date: 2026-08-20
description: Java を使用して、Excel を TXT にエクスポートし、小数点以下の桁数を制限しながら有効数字を保持し、ブックを TXT として保存する方法を学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: ja
lastmod: 2026-08-20
og_description: Aspose.Cells を使用して Excel を TXT にエクスポートします。このガイドでは、小数点以下の桁数を制限し、有効数字を保持し、Java
  でブックを TXT として保存する方法を示します。
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: JavaでExcelをTXTにエクスポート – 小数点以下の桁数と有効数字を制御
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Aspose.Cells を使用して Excel を TXT にエクスポートし、小数点以下の精度を制御する方法
url: /ja/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して Excel を TXT にエクスポートし、小数点以下の精度を制御する方法

**Excel を TXT にエクスポート** し、出力が特定の小数点以下桁数を保持するようにしたい場合、本ガイドが完全なソリューションを提供します。小数点以下桁数の制限、 有効数字の保持、 そして Aspose.Cells for Java を使用した **ワークブックの TXT 形式での保存** 方法を確認できます。

このチュートリアルでは、ワークブックの作成、 高精度の値の挿入、 TXT 保存オプションの設定、 ファイルへの書き込みまでを順に解説します。最終的に、手動での後処理なしに、必要な精度を正確に持つテキストファイルを生成できるようになります。

## 必要な環境

- Java 17（またはサポートされている任意の JDK）
- Aspose.Cells for Java 23.10 以降
- IDE またはビルドツール（Maven/Gradle）での依存関係管理
- 出力ディレクトリへの書き込み権限

## 手順 1: ワークブックを作成し、最初のワークシートにアクセスする

**Excel を TXT にエクスポート** する際の最初のステップはワークブックの作成です。`Workbook` クラスは Excel ファイル全体を表し、`Worksheet` はセルへのアクセスを提供します。

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*重要性*：ワークブックオブジェクトはすべてのデータ、スタイル、メタデータを保持します。新規ワークブックから開始することで、隠れた書式設定がテキストエクスポートに干渉することを防げます。

## 手順 2: 数値を追加し、小数点以下桁数を制限する

多数の小数点以下桁を持つ数値を挿入し、エクスポート時に **小数点以下桁数を制限** できることを示します。

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*重要性*：Excel はフル精度で値を保持しますが、エクスポート時に切り捨てや丸めが必要になることがあります。`limit decimal places` 設定がこれを自動的に処理します。

## 手順 3: 有効数字を保持するために TXT 保存オプションを構成する

Aspose.Cells は `TxtSaveOptions` を提供します。`significantDigits` を設定すると、先頭のゼロを除いた必要な有効数字だけを保持するようエクスポーターに指示できます。

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*重要性*：**有効数字を保持** オプションにより、出力ファイルは予測可能な精度を持つようになり、固定幅数値形式を期待する下流システムにとって重要です。

## 手順 4: ワークブックを TXT として保存する

最後に、ワークブックをテキストファイルに書き出します。`save` メソッドは構成したオプションを尊重するため、結果のファイルは制限された小数表現を含みます。

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*重要性*：**save workbook as txt** を事前に設定した `TxtSaveOptions` と共に使用することで、エクスポートされたファイルが前ステップで設定した精度制約と一致することが保証されます。

### `SignificantDigits.txt` の期待される内容

```
0.00012346
```

この値は丸め後に 5 桁の有効数字（`12346`）を示し、先頭のゼロは TXT 形式に従って保持されます。

## バリエーションとエッジケース

| シナリオ | 調整方法 |
|----------|----------|
| **有効数字の数を変更する** | `txtOptions.setSignificantDigits(n)` を呼び出し、`n` に 1‑15 のいずれかを指定します。 |
| **シート全体ではなく範囲をエクスポートする** | 保存前に `txtOptions.setExportRange("A1:B10")` を使用します。 |
| **列区切り文字を保持する** | タブ区切り出力の場合は `txtOptions.setSeparator('\t')` を設定します。 |
| **大規模なワークシート** | `OutOfMemoryError` を回避するために `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` を増やします。 |

## よくある落とし穴とプロのコツ

- **有効数字と小数点以下桁数を混同しない**。先頭のゼロは有効数字にカウントされません。意味のある精度が必要な場合は `setSignificantDigits`、小数点以下の固定桁数が必要な場合は `setDecimalPlaces` を使用してください。
- IDE から実行する際は **絶対パスの出力先を必ず指定** し、権限エラーを回避します。
- **生成されたファイルを検証** するために、`java.nio.file.Files.readAllLines(Paths.get(outputPath))` を呼び出して内容が期待通りか確認し、下流プロセスに渡す前にチェックしましょう。

## 参考用フルソースコード

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

プログラムを実行すると `SignificantDigits.txt` が生成され、単一行 `0.00012346` が書き込まれます。これにより **export excel to txt** プロセスが **limit decimal places** と **keep significant digits** の両要件を満たすことが実証されます。

## まとめ

Aspose.Cells for Java を使用して **Excel を TXT にエクスポート** しながら数値精度を制御する方法が分かりました。`TxtSaveOptions` を設定することで **小数点以下桁数を制限**、**有効数字を保持**、そして追加の後処理なしで **ワークブックを txt として保存** できるようになります。

次に試してみると良いこと：

- 複数シートを個別の TXT ファイルにエクスポート（シートごとに `save workbook as txt`）
- `setSeparator` を使用して CSV 互換の出力を作成
- 大量データセット向けにバッチ変換を自動化

プロジェクトの正確な要件に合わせて桁数や区切り文字を自由に調整し、ぜひ実験してみてください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}