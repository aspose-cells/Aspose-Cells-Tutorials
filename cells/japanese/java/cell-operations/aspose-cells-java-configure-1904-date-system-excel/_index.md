---
date: '2026-02-22'
description: Aspose.Cells for Java を使用して Excel の日付システムを 1904 に変更し、Excel の日付形式を設定し、Excel
  1904 システムを効率的に変換する方法を学びましょう。
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Aspose.Cells JavaでExcelの日付システムを1904に変更する
url: /ja/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java で Excel の日付システムを 1904 に変更する

Excel で過去データを管理するのは、Excel が 2 つの異なる日付システムをサポートしているため困難になることがあります。**このチュートリアルでは Aspose.Cells for Java を使用して Excel の日付システムを 1904 形式に変更する方法を学びます**。これによりレガシー日付の取り扱いが楽になります。ワークブックの初期化、1904 日付システムの有効化、変更の永続化までを順に解説します。

## クイック回答
- **1904 日付システムは何をするものですか？** 1904 年 1 月 1 日から日数をカウントし始め、デフォルトの 1900 システムと比較してすべての日付が 1462 日シフトします。  
- **なぜ Aspose.Cells を使って日付システムを変更するのですか？** Excel がインストールされていなくても動作し、大容量ファイルもサポートするシンプルな API が提供されます。  
- **対応している Java バージョンは？** JDK 8 以降。  
- **ライセンスは必要ですか？** 無料トライアルで評価できます。ライセンスを取得すると使用制限が解除されます。  
- **後で 1900 システムに戻すことはできますか？** はい、`setDate1904(false)` を呼び出すだけです。

## Excel の 1904 日付システムとは？
1904 日付システムは、初期の Macintosh 版 Excel で使用されていたものです。1904 年 1 月 1 日から日数をカウントし、古いスプレッドシートや一部の金融モデルとの互換性を保つのに役立ちます。

## なぜ Aspose.Cells で Excel の日付システムを変更するのか？
- **クロスプラットフォーム互換性** – Windows、Linux、macOS で動作します。  
- **Excel のインストール不要** – サーバーサイド処理に最適です。  
- **高性能** – 大規模なワークブックでもメモリ使用量を最小限に抑えて処理できます。  

## 前提条件
- Java Development Kit (JDK) 8 以上。  
- 依存関係管理のための Maven または Gradle。  
- 基本的な Java プログラミングの知識。  

## Aspose.Cells for Java のセットアップ

### Maven
`pom.xml` ファイルに以下の依存関係を追加します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
`build.gradle` ファイルにこの行を追加します。

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### ライセンス取得
Aspose は無料トライアル、期間限定ライセンス、フル商用ライセンスを提供しています。まずは [無料トライアル](https://releases.aspose.com/cells/java/) から始めるか、[期間限定ライセンスページ](https://purchase.aspose.com/temporary-license/) で一時ライセンスを取得してください。

## Aspose.Cells Java を使用して Excel の日付システムを変更する

以下は実際に **Excel の日付システムを変更** する手順です。各ステップに簡単な説明と、必要なコードを示します。

### 手順 1: ワークブックを初期化してロードする
既存の Excel ファイルを指す `Workbook` インスタンスを作成します。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### 手順 2: 1904 日付システムを有効にする
ワークブック設定を使用して日付システムを切り替えます。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**プロのコツ:** 後で元に戻す必要がある場合は `setDate1904(false)` を呼び出すこともできます。

### 手順 3: 変更したワークブックを保存する
変更を新しいファイル（または元のファイルを上書き）に書き込みます。

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

> **注意:** 上記コードは元のサンプル通りクラス名 `tWorkbook` を使用しています。この綴りがプロジェクトの命名規則に合わない場合は `Workbook` に修正してください。

## プログラムで Excel の日付を設定する（サブキーワード）
システム変更後に個別セルの値を調整する必要がある場合は、`Cells.get(i, j).putValue(Date)` を使用します。日付は現在有効な日付システムに従って解釈されます。

## Excel の 1904 システムを 1900 に戻す（サブキーワード）
元に戻すには次を呼び出します。

```java
workbook.getSettings().setDate1904(false);
```

その後、再度ワークブックを保存します。

## 実用的な活用例
1. **データアーカイブ** – 古い Mac ベースのスプレッドシートを移行する際にレガシータイムスタンプを保持。  
2. **クロスプラットフォームレポーティング** – Windows と macOS の両方で日付のずれなくレポートを生成。  
3. **金融モデリング** – 1904 システムを前提としたレガシー金融モデルと日付計算を整合させる。  

## パフォーマンス上の考慮点
- メモリ使用量を抑えるため、単一セッションでのワークブック操作は必要最低限に制限してください。  
- 非常に大きなファイルの場合は、Java のガベージコレクションチューニングを活用します。  

## よくある質問

**Q: 1900 システムと 1904 システムの違いは何ですか？**  
A: 1900 システムは 1900 年 1 月 1 日からカウントを開始し、1904 システムは 1904 年 1 月 1 日から開始します。その結果、すべての日付が 1462 日シフトします。

**Q: Excel で開いているワークブックの日時システムを変更できますか？**  
A: はい、ただし変更前に Excel でファイルを閉じておく必要があります。開いたままでは保存に失敗します。

**Q: `setDate1904` を使用するのにライセンスは必要ですか？**  
A: 無料トライアルでもメソッドは使用可能ですが、フルライセンスを取得すると評価制限が解除されます。

**Q: 特定のシートだけ日付システムを変更できますか？**  
A: できません。日付システムはワークブックレベルの設定であり、すべてのシートに適用されます。

**Q: 日付システムが変更されたことを確認する方法は？**  
A: 保存したファイルを Excel で開き、**ファイル → オプション → 詳細設定** に移動し、**「1904 日付システムを使用する」** チェックボックスがオンになっているか確認してください。

## 結論
これで Aspose.Cells for Java を使用して Excel の日付システムを 1904 に変更し、Excel の日付形式を設定し、必要に応じて元に戻す方法が分かりました。これらのコードスニペットをデータ処理パイプラインに組み込めば、プラットフォーム間での日付互換性を確実に保てます。

---

**最終更新日:** 2026-02-22  
**テスト環境:** Aspose.Cells 25.3 for Java  
**作者:** Aspose  

**リソース**
- **ドキュメンテーション:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **ダウンロード:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **ライセンス購入:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **無料トライアル:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **期間限定ライセンス:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **サポートフォーラム:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}