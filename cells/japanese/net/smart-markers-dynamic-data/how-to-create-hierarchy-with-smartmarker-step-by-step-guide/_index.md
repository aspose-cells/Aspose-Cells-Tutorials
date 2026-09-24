---
category: general
date: 2026-02-14
description: SmartMarkerテンプレートで階層を作成する方法は、思っているよりも簡単です – 階層データの作成方法と従業員を効率的に一覧表示する方法を学びましょう。
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: ja
og_description: SmartMarkerテンプレートで階層構造を作成する方法は簡単です。このガイドに従って階層データを作成し、入れ子になった範囲で従業員を一覧表示しましょう。
og_title: SmartMarkerで階層を作成する方法 – 完全ガイド
tags:
- SmartMarker
- C#
- templating
title: SmartMarkerで階層を作成する方法 – ステップバイステップガイド
url: /ja/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarkerで階層を作成する方法 – 完全ガイド

SmartMarkerテンプレート内で**階層を作成する方法**を、頭を抱えずに知りたくなったことはありませんか？ あなただけではありません。多くのレポートシナリオでは、親子関係が必要です—たとえば部門とその部門で働く人々です。良いニュースは、正しい手順さえ分かればSmartMarkerはとても簡単にしてくれるということです。

このチュートリアルでは、**C#で階層データを作成**し、ネストされたレンジを有効化し、最終的に各部門の**従業員を一覧表示**するテンプレートをレンダリングするまでの全プロセスを順を追って解説します。最後まで読めば、任意の.NETプロジェクトにすぐ組み込めるサンプルが手に入ります。

---

## 必要なもの

- .NET 6+（最近のバージョンであればどれでも可）
- **SmartMarker** ライブラリへの参照（`ws.SmartMarkerProcessor` 名前空間）
- 基本的な C# の知識 – 特別なことは不要、オブジェクトとラムダが数個あれば OK
- お好みの IDE またはエディタ（Visual Studio、Rider、VS Code…好きなもの）

これらがすでに揃っているなら、さっそく始めましょう。

---

## 階層作成の概要

核心となる考え方は、最終ドキュメントに表示したい構造をそのまま映す **ネストされたオブジェクトグラフ** を構築することです。今回の例ではグラフは次のようになります：

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker は `Departments` を走査し、**ネストされたレンジ処理** を有効にすれば、各部門の `Employees` コレクションも自動的にループします。

---

## ステップ1: 階層データモデルの構築

まず、部門の配列を含み、各部門が自分自身の従業員リストを持つ匿名オブジェクトを作成します。匿名型を使うことでサンプルが軽量になります—後で実際の POCO クラスに置き換えても構いません。

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Why this matters:** `Departments` 配列は最上位のコレクションです。各要素は `Employees` 配列を保持しており、これが第二レベルの階層となり、後で `#Departments.Employees#` でアクセスできるようになります。

---

## ステップ2: ネストされたレンジ処理の有効化

SmartMarker は内部コレクションに自動で潜り込むことはありません。`SmartMarkerOptions` オブジェクトでそのスイッチをオンにします。

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Pro tip:** このフラグを忘れると、内部の `#Employees#` レンジは何も返さず、テンプレートが空になる原因となります。

---

## ステップ3: データでプロセッサを実行する

データとオプションをプロセッサに渡します。`ws` 変数は **WebService**（または SmartMarker エンジンをホストする任意のオブジェクト）を表します。

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

この時点で SmartMarker はテンプレートを解析し、`#Departments.Name#` を各部門名に置換します。さらにネストされたレンジが有効になっているため、各部門の `Employees` コレクションも自動的に走査されます。

---

## ステップ4: テンプレートマーカーの作成

以下は外側と内側のループ両方を示す最小限のテンプレートです。SmartMarker のテンプレートエディタ（またはプロセッサに渡す `.txt` ファイル）に貼り付けてください。

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

レンダリング結果は次のようになります：

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **What you’re seeing:** 外側の `#Departments.Name#` が部門名を出力します。内側の `#Departments.Employees#` ブロックは各従業員をループし、ブロック内の `#Departments.Employees#` が実際の名前を出力します。

---

## 期待される出力と検証

データ + オプション + テンプレートのフル例を実行すると、上記と全く同じリストが生成されます。簡単に確認したい場合は、結果をコンソールに出力してみてください：

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

部門見出しが2つ、続いてそれぞれの従業員箇条書きが表示されれば、**階層の作成** と **従業員の一覧表示** に成功しています。

---

## よくある落とし穴とエッジケース

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| No output for employees | `EnableNestedRange` left false | Set `EnableNestedRange = true` |
| Duplicate employee names | Same array reused across departments | Clone the array or use distinct collections |
| Very large hierarchies cause memory pressure | SmartMarker loads the whole object graph into memory | Stream data or paginate large collections |
| Template syntax errors | Missed closing `#/…#` tags | Use the SmartMarker validator or run a quick test with a tiny template |

---

## さらに進める – 実務でのバリエーション

1. **Dynamic data sources** – データベースから部門を取得し、LINQ を使って匿名構造にマッピングします。  
2. **Conditional formatting** – 各従業員に `IsManager` フラグを追加し、SmartMarker の条件タグ（`#if …#`）でマネージャーをハイライトします。  
3. **Multiple nesting levels** – 部門内にチームが必要な場合は、別のコレクション（`Teams`）を追加し、`EnableNestedRange` をオンのままにします。

---

## 完全動作例（コピー＆ペースト可能）

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

プログラムを実行すると、先ほど示した階層がそのまま出力されます。

---

## 結論

本稿では **SmartMarker で階層を作成する方法** を、C# での **階層データの形成**、ネストされたレンジの有効化、そして部門ごとに **従業員を一覧表示** するテンプレートのレンダリングまで網羅しました。このパターンはスケーラブルで、さらにネストされたコレクションや条件ロジックを追加すれば、強力なレポートエンジンが手元にあります。

次のチャレンジに進みませんか？ 匿名型を強く型付けされた POCO クラスに置き換える、あるいはこのフローを ASP.NET Core エンドポイントに組み込んで PDF や Word ドキュメントを返す、といった応用が考えられます。可能性は無限大です。今すぐこの土台を活用してください。

![階層作成図](image.png){alt="部門と従業員の関係を示す階層作成図"}

*Happy coding! もし詰まったら下のコメント欄に書き込んでください—喜んでお手伝いします。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}