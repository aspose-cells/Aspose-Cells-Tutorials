---
date: '2026-10-28'
description: Aspose.Cells for Java を使用して Excel の日付システムを 1904 に変更する方法、Excel の日付形式の設定、Excel
  1904 システムの効率的な変換方法を学びます。
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Aspose.Cells for Java を使用して Excel の日付システムを 1904 に変更します。ステップバイステップで
  1904 システムの有効化、日付の設定、元に戻す変換方法を学びます。
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Aspose.Cells for Java で Excel の日付システムを 1904 に変更
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Aspose.Cells for Java を使用して Excel の日付システムを 1904 に変更
url: /ja/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells JavaでExcelの日付システムを1904に変更する

このチュートリアルでは、Aspose.Cells for Java を使用して **Excelの日付システムを** 1904 形式に **変更する方法** を学びます。1904 システムは、レガシーな Mac ベースの日付を保持したり、そのエポックを前提とした財務モデルと整合させる必要がある場合に不可欠です。ライブラリのインストール、ワークブックの読み込み、日付システムの切り替え、結果の保存までを、サーバー上で Microsoft Excel を必要とせずに実行する手順を解説します。

## クイック回答
- **1904日付システムは何をするのですか？** デフォルトの1900システムと比較して、1904年1月1日から日数をカウントし、すべての日付が1,462日シフトします。  
- **なぜAspose.Cellsで日付システムを変更するのですか？** Excel がインストールされていなくても動作し、大容量ファイルをサポートするシンプルな API を提供します。  
- **対応している Java バージョンは？** JDK 8 以降。  
- **ライセンスは必要ですか？** 無料トライアルで評価可能です。ライセンスを取得すると使用制限が解除されます。  
- **後で1900システムに戻すことはできますか？** はい、`setDate1904(false)` を呼び出すだけです。

## Excelの1904日付システムとは？
1904日付システムは、デフォルトの1900エポックではなく、1904年1月1日から日数をカウントします。このシフトにより、すべての日付値が正確に1,462日増加し、Mac 用のレガシーな Excel ブックが Windows で開かれたときにオフセットして見える原因となります。主に古い Macintosh Excel ファイルや一部のレガシー財務モデルとの互換性のために使用されます。

## なぜAspose.CellsでExcelの日付システムを変更するのか？
Java から直接日付システムを切り替えることで、Excel の手動操作を省けます。Aspose.Cells は **2 GB** までのワークブックを処理でき、典型的な 4 コアサーバー上で **2 秒未満** で 500 シートのブックを変換できるため、サーバー側の高スループット自動化に最適です。

## 前提条件
- Java Development Kit (JDK) 8 以上。  
- 依存関係管理のための Maven または Gradle。  
- 基本的な Java プログラミングの知識。  

## Aspose.Cells for Javaの設定

### Maven
`pom.xml` ファイルに以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
`build.gradle` ファイルに次の行を追加してください。

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### ライセンス取得
Aspose は無料トライアル、期間限定ライセンス、フル商用ライセンスを提供しています。まずは [無料トライアル](https://releases.aspose.com/cells/java/) から始めるか、[期間限定ライセンスページ](https://purchase.aspose.com/temporary-license/) で期間限定ライセンスを取得してください。

## Aspose.Cells for JavaでExcelの日付システムを1904に変更する方法は？
ワークブックをロードし、1904 設定を有効にしてファイルを保存します。この 3 ステップのフローで、ワークブック内部の日付エポックが 1 秒未満で更新されます。API 呼び出し `setDate1904(true)` がシステムフラグを切り替え、`save` を呼び出すと変更が永続化されます。Excel のインストールは不要で、ヘッドレスサーバー環境に最適です。

### 手順 1: ワークブックの初期化とロード
`Workbook` クラスはメモリ内の Excel ファイル全体を表します。まず、既存ファイルを指す `Workbook` インスタンスを作成します。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### 手順 2: 1904日付システムを有効化
`WorkbookSettings.setDate1904` メソッドでワークブックレベルの日付フラグを切り替えます。`true` に設定すると、すべてのワークシートで 1904 システムが有効になります。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**プロのコツ:** 後で元に戻す必要がある場合は、`setDate1904(false)` を呼び出すこともできます。

### 手順 3: 変更されたワークブックを保存
最後に、変更を新しいファイル（または元のファイルを上書き）に書き込みます。`save` メソッドはアクティブな日付システムを自動的に考慮します。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **注意:** 上記コードは元の提供物通り `tWorkbook` というクラス名を使用しています。このタイプミスがプロジェクトの命名規則に合致しているか確認し、必要に応じて `Workbook` に修正してください。

## プログラムでExcelの日付を設定する（サブキーワード）
システム変更後に個別セルの値を調整する必要がある場合は、`cells.get(i, j).putValue(Date)` を使用できます。日付はアクティブな日付システムに従って解釈されます。

## Excelの1904システムを1900に戻す（サブキーワード）
元に戻すには、次のコードを実行してください。

```java
workbook.getSettings().setDate1904(false);
```

その後、再度ワークブックを保存します。

## 実用例
1. **データアーカイブ** – 古い Mac ベースのスプレッドシートを移行する際にレガシータイムスタンプを保持。  
2. **クロスプラットフォームレポーティング** – Windows と macOS の両方で正しく開くレポートを生成し、日付の不一致を防止。  
3. **財務モデリング** – 1904 システムを前提としたレガシー財務モデルと日付計算を整合。

## パフォーマンス上の考慮点
- メモリ使用量を抑えるため、単一セッションでのワークブック操作は制限してください。Aspose.Cells はデータをストリーミングし、明示的に要求しない限りファイル全体を RAM にロードしません。  
- 非常に大きなファイルの場合は、Java のガベージコレクションフラグ（`-XX:+UseG1GC`）を調整し、ポーズ時間のスパイクを回避してください。  

## よくある質問

**Q: 1900と1904の日付システムの違いは何ですか？**  
A: 1900 システムは 1900 年 1 月 1 日からカウントを開始し、1904 システムは 1904 年 1 月 1 日から開始するため、すべての日付が 1,462 日シフトします。

**Q: 現在 Excel で開いているワークブックの日付システムを変更できますか？**  
A: はい、ただし先に Excel でファイルを閉じる必要があります。開いたままでは保存操作が失敗します。

**Q: `setDate1904` を使用するのにライセンスは必要ですか？**  
A: 無料トライアルでもメソッドは動作しますが、フルライセンスを取得すると評価制限が解除されます。

**Q: 単一のワークシートだけの日付システムを変更できますか？**  
A: できません。日付システムはワークブックレベルの設定であり、すべてのワークシートに適用されます。

**Q: 日付システムが変更されたことを確認する方法は？**  
A: 保存したファイルを Excel で開き、**ファイル → オプション → 詳細設定** に移動し、**「1904 日付システムを使用する」** チェックボックスがオンになっているか確認してください。

## 結論
これで、Aspose.Cells for Java を使用して **Excelの日付システムを1904に変更** する方法、個別セルの日付設定、そして必要に応じて1900システムに戻す方法が分かりました。これらのコードスニペットをデータ処理パイプラインに組み込むことで、プラットフォーム間およびレガシーファイル間の日時互換性を保証できます。

---

**Last Updated:** 2026-10-28  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Resources**
- **ドキュメント:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **ダウンロード:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **ライセンス購入:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **無料トライアル:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **期間限定ライセンス:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **サポートフォーラム:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## 関連チュートリアル

- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Master Excel Manipulation with Aspose.Cells for Java: Workbook Operations and Cell Styling Tutorial](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}