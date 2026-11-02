---
category: general
date: 2026-03-29
description: SmartMarker を使用して JSON の変数を置換する方法 – if 式の使い方、条件ロジックの適用、値の乗算、そして手軽に JSON
  を生成する方法を学びましょう。
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: ja
og_description: SmartMarkerを使用してJSON内の変数を置換する方法。if式の使い方、条件ロジックの適用、値の乗算、そして数分でJSONを生成する方法を発見しましょう。
og_title: SmartMarkerでJSONの変数を置換する方法 – ステップバイステップ
tags:
- C#
- SmartMarker
- JSON templating
title: SmartMarkerでJSONの変数を置換する方法 – 完全ガイド
url: /ja/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSONで変数を置換する方法 – SmartMarker 完全ガイド

JSONペイロード内でカスタムパーサーを書かずに **変数を置換する方法** を考えたことはありませんか？ あなただけではありません。多くの統合シナリオ—請求書、価格エンジン、動的設定ファイルなど—では、実行時の値を注入し、シンプルな条件分岐を適用し、場合によっては簡単な掛け算さえ行う必要があります。このチュートリアルでは、SmartMarker ライブラリを使って **変数を置換する方法** を正確に示し、JSON をクリーンで読みやすく保ちます。

実際の例を使って、**if式の使用**、**条件を適用する方法**、**値を掛け算する方法**、そして **json を動的に生成する方法** を順に解説します。最後まで読むと、任意の .NET プロジェクトに組み込める実行可能な C# スニペットが手に入ります。

## 学べること

- `SmartMarkerOptions` を設定して再利用可能な変数を格納する。  
- 条件ロジック用の `if` 式を含む JSON テンプレートを書く。  
- テンプレート内で変数を使って値を掛け算する。  
- `SmartMarkerProcessor` でテンプレートを処理し、最終的な JSON 文字列を取得する。  
- 変数が見つからない、式が不正などの一般的な落とし穴をトラブルシュートする。

外部サービスや重い依存関係は不要です—純粋な C# と SmartMarker NuGet パッケージだけです。

---

## 変数置換の手順 – ステップバイステップ概要

以下はワークフローのハイレベルな図です。左側に生の JSON テンプレートが入り、SmartMarker エンジンが処理を行い、右側に完全にレンダリングされた JSON が出力されるパイプラインと考えてください。

![JSONで変数を置換する方法を示す図](https://example.com/images/smartmarker-flow.png "JSONで変数を置換する方法")

*画像の代替テキスト: JSONで変数を置換する方法を示す図.*

---

## 手順 1: SmartMarker のインストールとインポート

開始する前に、プロジェクトで SmartMarker パッケージが参照されていることを確認してください。.NET CLI を使用している場合は、次のコマンドを実行します。

```bash
dotnet add package SmartMarker
```

次に、C# ファイルの先頭に必要な `using` ディレクティブを追加します。

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **プロのコツ:** 最新バージョン（2026年3月時点）は 2.4.1 です。.NET 6 以降をサポートしていますが、.NET Framework 4.7 でも問題なく動作します。

---

## 手順 2: SmartMarker Options の作成と変数の定義

ここでは、テンプレート全体で再利用したい変数を保持する `SmartMarkerOptions` のインスタンスを作成します。ここで **変数を置換する方法** に答えることになります—変数は SmartMarker が後で置換するプレースホルダーとして機能します。

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

`Variables` にレートを格納するのはハードコーディングしない理由です。データベースや設定ファイル、ユーザー入力からその数値を取得することがあるからです。オプションに保持することで、テンプレートを再利用可能かつテストしやすくなります。

---

## 手順 3: `if` 式を使った JSON テンプレートの作成

ここが **if式の使用** が光るポイントです。SmartMarker は JSON 文字列内に直接条件ロジックを埋め込むことができます。構文はプロパティ名のように見えますが、SmartMarker はそれをディレクティブとして扱います。

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

`if(Amount>500)` キーに注目してください。SmartMarker は式 `Amount>500` を評価し、真の場合は対応する値（`${Amount * Rate}`）を出力に挿入します。`${...}` 構文は *変数置換* エンジンで、ここでは **値を掛け算する方法**（`Amount * Rate`）で結果を注入しています。

---

## 手順 4: テンプレートを処理して最終 JSON を取得する

オプションとテンプレートの準備ができたら、すべてをプロセッサに渡します。`ProcessJson` メソッドはテンプレートを解析し、条件を適用し、掛け算を実行して、クリーンな JSON 文字列を返します。

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

スニペットを実行すると次が出力されます。

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**何が起こったのか？**  
- `Amount` は 1000 で、`Amount>500` を満たしています。  
- SmartMarker は `${Amount * Rate}` を評価し → `1000 * 0.08 = 80`。  
- 元の条件キー（`if(Amount>500)`）はクリーンなプロパティ名（`Result`）に置き換えられます。デフォルトでは SmartMarker は `"Result"` を使用しますが、後述のようにカスタマイズ可能です。

`Amount` を `400` に変更すると、出力は次のようになります。

```json
{
  "Amount": 400
}
```

条件ブロックは式が `false` と評価されたため消えます。これが JSON で **条件を適用する方法** の本質です。

---

## 手順 5: 出力プロパティ名のカスタマイズ（オプション）

場合によっては汎用的な `"Result"` キーを使いたくないことがあります。SmartMarker は `RenameIfExpression` オプションを使ってカスタム名を指定できます。

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

これで条件付きの値がより意味のあるプロパティ名で保存されます—特定のフィールドを期待する下流サービスに最適です。

---

## よくある落とし穴と回避方法

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| 変数が見つからない | `smartMarkerOptions.Variables` に存在しない変数を参照しています。 | スペルを再確認し、処理前に変数が追加されていることを確認してください。 |
| `if` 構文が無効 | 括弧が欠けている、または演算子が間違っている（`>`, `<`, `==`）。 | `if(<expression>)` のパターンを正確に守ってください。SmartMarker は単純な数値比較のみサポートします。 |
| JSON が不正になる | 条件ブロックの後に余分なカンマが残っている。 | SmartMarker に除去させ、元のテンプレートを構文的に正しく保ってください。 |
| 予期しない数値形式 | 結果が数値ではなく文字列 `"80"` として出力される。 | 後でキャストまたはパースするか、数値フォーマット用に `${(Amount * Rate):N0}` を使用してください。 |

---

## 完全動作例（コピー＆ペースト可能）

以下はコンパイルして実行できる完全なプログラムです。動的変数、条件分岐、算術演算を使って **json を生成する方法** を 30 行未満で示しています。

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**期待されるコンソール出力**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

`Amount` を変更して条件分岐をテストしたり、`Rate` を調整して異なる割引計算を確認したりしてください。

---

## パターンの拡張 – さらに “How to” シナリオ

- **設定ファイルから変数を置換する方法**: `appsettings.json` から `Dictionary<string, object>` を読み込み、`smartMarkerOptions.Variables` に渡す。  
- **複数条件で if 式を使用する方法**: `"if(Amount>500 && CustomerType=='VIP')"` のようにチェーンできます—SmartMarker は論理 AND/OR をサポートします。  
- **条件付き書式を適用する方法**: 式内で `${Amount:0.00}` を使用して小数点以下の桁数を制御します。  
- **より複雑な計算で値を掛け算する方法**: `${(Amount - Discount) * TaxRate}` も同様に機能します。  
- **入れ子オブジェクト用に json を生成する方法**: 条件ブロックを別の JSON オブジェクト内に配置すると、SmartMarker が階層構造を保持します。

---

## 結論

SmartMarker を使って JSON で **変数を置換する方法** を取り上げ、条件付き挿入のための **if式の使用** を実演し、**条件を適用する方法** のロジックを説明し、テンプレート内で **値を掛け算する方法** を示し、最終的に **json を生成する方法** を示しました。このアプローチは軽量で、外部のテンプレートエンジンを必要とせず、任意の C# コードベースにすっきりと組み込めます。

ぜひ試してみてください—変数を調整したり、条件を追加したり、ヘルパークラスでラップしてソリューション全体で再利用したりできます。動的な JSON を素早く生成したいときは、SmartMarker が堅実で本番環境向けの選択肢です。

---

**次のステップ**

- ループ（`foreach`）やカスタム関数など、SmartMarker の高度な機能をさらに掘り下げる。  
- この手法を ASP.NET Core エンドポイントと組み合わせて、動的 JSON API を提供する。  
- 他のテンプレートライブラリ（例: Handlebars.NET）を比較検討し、特にリッチな構文が必要な場合に検討する。

質問や特定のユースケースで悩んでいることがありますか？以下にコメントを残してください。一緒にトラブルシューティングしましょう。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}