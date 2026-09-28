---
date: '2026-08-16'
description: Aspose.Cellsを使用してJavaでグローバリゼーションを追加する方法を学び、Excelのエラーメッセージをカスタマイズし、Maven依存関係を設定します。
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Aspose.Cellsを使用してJavaでグローバリゼーションを追加し、Excelのエラーメッセージをカスタマイズし、Maven依存関係を設定する方法を学びます。ステップバイステップのガイドに従ってください。
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: JavaでAspose.Cellsを使用してグローバリゼーションを追加する方法
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: JavaでAspose.Cellsを使用してグローバリゼーションを追加する方法
url: /ja/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# JavaでAspose.Cellsを使用したグローバリゼーションの追加方法

## はじめに

Javaのワークブックにグローバリゼーションを追加すると、エラーメッセージやブール値、その他ロケール固有の文字列をユーザーが期待する言語で表示できます。このチュートリアルではロシア語向けの**グローバリゼーションの追加方法**を学びますが、同じパターンは他の言語でも適用可能です。ガイドの最後までに以下ができるようになります：

- デフォルトのエラーテキストとブール値の表現を上書きする。
- `Workbook` インスタンスにカスタム設定を適用する。
- 一般的な Maven ベースの Java プロジェクトにソリューションを統合する。

Excel ファイルを本格的に多言語対応させる準備はできましたか？まず、開発環境が前提条件を満たしているか確認しましょう。

## クイック回答
- **Aspose.Cells のグローバリゼーションとは何ですか？** ロケール対応の文字列（エラー、ブール値など）のセットで、カスタムテキストに置き換えることができます。  
- **必要な Maven アーティファクトはどれですか？** `com.aspose:aspose-cells:25.3`。  
- **ロシア語以外の言語にも対応できますか？** はい。`GlobalizationSettings` を拡張し、各ロケールに必要なメソッドをオーバーライドします。  
- **開発にライセンスは必要ですか？** 無料トライアルでテスト可能です。永続ライセンスを取得すれば評価用の透かしが除去されます。  
- **このソリューションはスレッドセーフですか？** ワークブックごとに設定を適用します。`GlobalizationSettings` オブジェクトは作成後は不変です。

## Aspose.Cellsにおけるグローバリゼーションとは？

`GlobalizationSettings` は Aspose.Cells の設定オブジェクトで、エラーメッセージ、ブール値、通貨記号、日付パターンなどロケール固有の文字列を制御します。独自のサブクラスを提供することで、各カルチャーで表示するテキストを指定でき、デフォルトの英語文字列をエンドユーザーの言語や地域慣習に合わせた翻訳に置き換えることができます。

## カスタムグローバリゼーションを追加する理由

Aspose.Cells は **50 以上の入力・出力フォーマット**（XLSX、CSV、PDF、ODS など）をサポートし、**最大 200,000 行**のワークブックをファイル全体をメモリに読み込まずに処理できます。グローバリゼーションをカスタマイズすることで、エンドユーザーは母国語でメッセージを確認でき、グローバル展開におけるサポートチケットを **30 %** 程度削減できると推定されています。

## 前提条件

- **Java Development Kit** 8 以上。
- **IDE**（IntelliJ IDEA や Eclipse など）。
- **Aspose.Cells for Java** バージョン 25.3（またはそれ以降）を Maven または Gradle で追加。

### Aspose.Cells for Java の設定

`pom.xml` に Maven 依存関係を追加します：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Gradle を使用する場合は、`build.gradle` に以下を挿入します：

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### ライセンス取得

Aspose では複数のライセンスオプションが用意されています：

- **Free trial** – 30 日間のフル機能評価。  
- **Temporary license** – 無制限の評価（透かしなし）。  
- **Commercial license** – 本番環境向け、優先サポート付き。

ライセンスファイルを取得したら、アプリケーション起動時に一度設定します：

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## ロシア語向けグローバリゼーションの追加方法

`Workbook` オブジェクトはメモリに読み込まれた Excel ファイルを表し、シート、セル、設定へのアクセスを提供します。ワークブックをロードし、`GlobalizationSettings` のサブクラスを作成してワークブックに適用します。直接的な手順は、**カスタム `GlobalizationSettings` クラスをインスタンス化し、`getErrorValueString` と `getBooleanValueString` をオーバーライドし、`workbook.setGlobalizationSettings(customSettings)` を呼び出す**ことです。この 2 段階のアプローチで、デフォルトのロシア語文字列を独自のものに置き換えます。

### カスタム設定の定義

このガイドで初めて `GlobalizationSettings` に言及する際は、以下の定義に注意してください：

`GlobalizationSettings` は Aspose.Cells がロケール固有の文字列を取得するために使用する基底クラスです。  

次に、ロシア語固有のテキストを返すサブクラスを作成します：

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### 設定をワークブックに適用する

サブクラスを定義したら、任意の `Workbook` インスタンスに適用します：

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## 実用例

- **Financial reporting** – エラーコードを会計担当者の母国語で表示し、誤解を減らす。  
- **Enterprise‑wide tools** – 社内の多数の Excel ベースツールに同一のグローバリゼーションロジックを組み込む。  
- **Automated data pipelines** – 下流システムがロケール対応の値を受け取り、追加の翻訳工程が不要になる。

## パフォーマンス上の考慮点

カスタムグローバリゼーションを有効にしても、Aspose.Cells は同等の高性能で数式や I/O を処理します。メモリ使用量を抑えるために：

- 保存後にワークブック参照を解放します（`wb.dispose()`）。  
- 必要な場合にのみ `CalculationOptions.setEnableIterativeCalculation(true)` を使用します。  
- 100 MB 超のワークブック向けに JVM のヒープ（`-Xmx2g`）を調整します。

## よくある質問

**Q: 同じグローバリゼーション設定を複数のワークブックに同時に適用できますか？**  
A: はい。単一の `RussianGlobalization` インスタンスを作成し、`setGlobalizationSettings` を介して各ワークブックに渡します。

**Q: 右から左へ書くスクリプトを使用する言語をサポートする必要がある場合は？**  
A: サブクラスで `getCurrencySymbol` や `getDatePattern` などの追加メソッドをオーバーライドし、適切な RTL シンボルを返すようにします。

**Q: カスタムグローバリゼーションを使用するためにトライアル版でライセンスは必要ですか？**  
A: いいえ。トライアル版は `GlobalizationSettings` を完全にサポートしており、特定の出力フォーマットでのみ評価用透かしが表示されます。

**Q: 正しくないエラーストリングをデバッグするには？**  
A: オーバーライドしたメソッド内に `System.out.println` を挿入し、入力 `err` 値がスイッチケースと一致しているか確認します。

**Q: これにより数式計算速度に影響がありますか？**  
A: 影響はほとんどありません。ライブラリはセル値をレンダリングする際にのみ文字列を参照し、途中の計算ステップでは参照しません。

## 追加リソース

- **Documentation**: 詳細なガイドは [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/) を参照してください  
- **Download**: 最新リリースは [Aspose Downloads](https://releases.aspose.com/cells/java/) から取得できます  
- **Purchase**: 商用ライセンスは [Aspose Purchase](https://purchase.aspose.com/buy) で購入できます  
- **Free trial**: 無料トライアルは [Aspose Free Trial](https://releases.aspose.com/cells/java/) から開始できます  
- **Temporary license**: 一時ライセンスは [Aspose Temporary License](https://purchase.aspose.com/temporary-license/) で取得できます  
- **Support**: コミュニティからのサポートは [Aspose Support Forum](https://forum.aspose.com/c/cells/9) で受けられます

---

**最終更新日:** 2026-08-16  
**テスト環境:** Aspose.Cells 25.3 for Java  
**作者:** Aspose

## 関連チュートリアル

- [Aspose.Cells Java: Custom Calculation Engine Guide](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven Dependency – Manage Excel Data Connections with Aspose.Cells in Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}