---
category: general
date: 2026-06-08
description: Aspose.Words を使用して Word の表の行を削除します。行の削除方法、複数行の削除方法を学び、数分で表編集をマスターしましょう。
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: ja
og_description: Aspose.Words を使用して Word テーブルの行を削除します。このチュートリアルでは、行の削除、複数行の削除方法、テーブルを整頓する方法を示します。
og_title: Wordテーブルの行を削除 – 完全C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: Wordテーブルの行を削除 – 完全C#ガイド
url: /ja/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Word テーブルの行削除 – 完全 C# ガイド

**Word テーブルの行削除** が必要だったけど、どこから始めればいいか分からないことはありませんか？ あなたは一人ではありません。多くの開発者が、生成されたレポートのクリーンアップやデータ駆動テーブルのトリミングでこの問題に直面しています。良いニュースは、C# と Aspose.Words の数行のコードで、単一行でも複数行でも不要な行を簡単に削除できることです。このガイドでは *行の削除方法* を解説し、さらに **Word の複数行削除** のやや高度なケースも一度にカバーします。

必要な情報をすべて網羅します：正確なコード、各ステップの重要性、よくある落とし穴、そしてすぐに実行できるサンプルです。最後まで読めば、ドキュメント構造を壊すことなく任意の Word テーブルから行を削除できるようになります。余計な説明は省き、実践的で実績のあるテクニックだけをご紹介します。

## 前提条件

- **Aspose.Words for .NET**（バージョン 23.12 以降）。NuGet から取得できます：`Install-Package Aspose.Words`。
- .NET 開発環境（Visual Studio、Rider、または C# 拡張機能付き VS Code）。
- ヘッダー行を含む少なくとも 1 つのテーブルがある入力 Word ファイル（`input.docx`）。

以上です—追加のライブラリや COM インターロップは不要、純粋なマネージドコードだけで完結します。

## ステップ 1: Word ドキュメントの読み込み

最初に行うのはドキュメントを開くことです。Aspose.Words は Word ファイルを `Document` オブジェクトとして扱い、セクション、本文、テーブルなどすべてにフルアクセスできます。

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*Why this matters:* ドキュメントを読み込むことでメモリ上に表現が作られ、変更は高速に行われ、明示的に保存するまでファイルシステムには触れません。

## ステップ 2: 対象テーブルを取得

多くの場合、編集したいテーブルは最初のものです。Aspose.Words では `FirstSection` プロパティを使って簡単に取得できます。

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

ドキュメントに複数のテーブルがある場合は、`doc.GetChildNodes(NodeType.Table, true)` をループしてインデックスやカスタムマーカーで目的のテーブルを選択できます。

## ステップ 3: 行の削除 – 単一または複数

### 3.1 行の削除方法（単一行）

単一行を削除するには、`DeleteRows(startIndex, count)` を呼び出します。`startIndex` は 0 から始まるインデックスです。ヘッダー行（インデックス 0）をスキップするのが一般的です。

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 複数行の削除（Word） – バッチ削除

範囲をまとめて削除したい場合（例：行 2‑6）には、開始インデックスと削除する行数を渡します。これが **Word の複数行削除** パターンです。

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*Why use a single call?* 行を一つずつ削除すると、削除ごとにテーブルが再インデックスされ、エラーが起きやすく遅くなります。まとめて削除する方法はテーブル内部の構造を一貫したまま保ちます。

#### エッジケース: テーブルサイズを超える削除

`startIndex + count` が実際の行数を超えると、Aspose.Words は `ArgumentOutOfRangeException` をスローします。防御的にチェックするコード例は次のとおりです。

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

このスニペットは、存在しない行を削除しようとすることを防ぎます。

## ステップ 4: 変更後のドキュメントを保存

行の削除が完了したら、変更を永続化するのはたった一行です。

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

`Save` メソッドはファイル拡張子に基づいてフォーマットを自動選択するため、PDF、HTML、あるいは別の拡張子にすれば ODT などにも出力できます。

## 完全動作例

すべてを組み合わせた、すぐに実行できる完全なプログラムは以下です。

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### 期待される出力

- `output.docx` には元のテーブルから **行 2‑6 が削除された** 状態が保存されます。
- 残りの行は上にシフトし、セルの書式や列幅は保持されます。
- ヘッダー行はそのまま残り、列タイトルが見える状態が保たれます。

## なぜこのアプローチが他の方法より優れているのか

| アプローチ | 長所 | 短所 |
|----------|------|------|
| **Aspose.Words `DeleteRows`** | ワンラインのバルク削除、スタイル保持、COM 依存なし | 商用ライブラリが必要（無料トライアルあり） |
| Office Interop | ネイティブ Word と連携可能 | サーバーに Word が必要、遅い、COM のクリーンアップが面倒 |
| Open XML SDK | 無料・オープンソース | 手動で XML を操作する必要があり、行削除を安全に行うのが手間 |

既に他のドキュメント処理で Aspose.Words を使用している場合、`DeleteRows` を使い続けることでコードベースがシンプルかつ一貫します。

## プロのコツと一般的な落とし穴

- **Pro tip:** ヘッダー行（インデックス 0）は特に理由がない限り削除しないでください。ヘッダーを削除すると、列名を前提とした下流処理が壊れる可能性があります。
- **Watch out for merged cells.** 行に縦方向に結合されたセルがあり、削除対象の行にまたがっている場合、Aspose.Words は自動で結合範囲を調整しますが、見た目を必ず確認してください。
- **Performance note:** 数千行規模の大テーブルでも多数行の削除は高速ですが、数百のドキュメントをループで処理する場合は、可能な限り `Document` オブジェクトを再利用して割り当てオーバーヘッドを削減すると良いでしょう。

## よくある質問

**Q: インデックスではなくセルの内容で行を削除できますか？**  
A: もちろん可能です。`table.Rows` をループし、`row.Cells[i].GetText()` で内容を確認して一致するインデックスを収集します。その後、最小インデックスと総数で `DeleteRows` を呼び出すか、逆順に削除して再インデックスを防ぎます。

**Q: .doc ファイルでも動作しますか？**  
A: はい。Aspose.Words は `.doc` と `.docx` の両方をサポートしています。`Document` コンストラクタと `Save` 呼び出しの拡張子を変更するだけで OK です。

**Q: テーブルがヘッダー/フッター内にある場合はどうすれば？**  
A: `doc.FirstSection.HeadersFooters` コレクションから取得し、同じ `DeleteRows` ロジックを適用してください。

## 結論

これで C# を使った **Word テーブルの行削除** の完全なエンドツーエンドソリューションが手に入りました。サンプルは *行の単体削除* と **Word の複数行削除** を効率的に行う方法を示しています。Aspose.Words を使えば、COM の煩わしさなしにクリーンな API で Word ドキュメントを完全にコントロールできます。

次のチャレンジはどうですか？ 合計を計算した新しい行を追加したり、`Table.ToTxt` を使ってトリミングしたテーブルを CSV にエクスポートしたりしてみましょう。テーブル操作をマスターすれば、可能性は無限です。

Happy coding, and may your Word tables stay tidy!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用できる関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Java 用 Aspose.Cells で Excel の行を削除する方法 | ガイド & チュートリアル](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [Aspose.Cells .NET で Excel の空白行を削除してデータクリーンアップ](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Aspose.Cells for .NET で Excel の行を挿入・削除する包括的ガイド](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}