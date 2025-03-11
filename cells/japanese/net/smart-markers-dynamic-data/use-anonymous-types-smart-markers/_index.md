---
title: スマートマーカーで匿名型を使用する Aspose.Cells
linktitle: スマートマーカーで匿名型を使用する Aspose.Cells
second_title: Aspose.Cells .NET Excel 処理 API
description: .NET で動的な Excel レポートを生成するために、Aspose.Cells でスマート マーカー付きの匿名型を使用する方法を学びます。簡単なガイドに従ってください。
weight: 17
url: /ja/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スマートマーカーで匿名型を使用する Aspose.Cells

## 導入
.NET アプリケーションで動的な Excel レポートを生成する場合、Aspose.Cells は強力なツールとして際立っています。その最も優れた機能の 1 つは、スマート マーカーと匿名型を操作できることです。この概念を初めて知る場合でも心配はいりません。このガイドでは、前提条件から実践的な例まで、知っておく必要のあるすべてのことを、魅力的でわかりやすい内容にまとめています。
## 前提条件
コードに進む前に、このチュートリアルの例をスムーズに実行するために必要なものがすべて揃っていることを確認しましょう。
### 1. .NET環境
ローカル マシンに機能する .NET 環境が設定されていることを確認してください。Visual Studio または任意の他の IDE を使用できます。
### 2. Aspose.Cells ライブラリ
 Aspose.Cellsライブラリが必要です。まだダウンロードしていない場合は、簡単に見つけることができます。[ここ](https://releases.aspose.com/cells/net/)無料トライアルで試してみることもできます。[このリンク](https://releases.aspose.com/).
### 3. C#の基礎知識
C# プログラミングの基礎を理解していれば、チュートリアルをより簡単に進めることができます。クラス、オブジェクト、プロパティなどの用語に慣れていれば、すぐに始めることができます。
## パッケージのインポート
プロジェクトで Aspose.Cells ライブラリを使用するには、関連する名前空間をインポートする必要があります。C# ファイルの先頭に次の using ディレクティブを追加します。
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
これらの名前空間により、後で説明するすべての必要なクラスとメソッドにアクセスできるようになります。
それでは、チュートリアルの本題に入りましょう。カスタム クラスを使用してスマート マーカー付きの Excel ファイルを作成する方法を説明します。心配しないでください。すべてを管理しやすい手順に分解します。
## ステップ1: カスタムクラスを作成する
まず、Excel ファイルに追加するデータを表す簡単なクラスが必要です。このクラスは人物に関する情報を保持します。
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
ここでは、というクラスを定義しています。`Person` 2つの特性を持ち、`Name`そして`Age`コンストラクターはこれらのプロパティを初期化します。 
## ステップ 2: ワークブック デザイナーを設定する
次に、`WorkbookDesigner`クラスは、スマート マーカーを使用して Excel ファイルを設計するために使用します。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ワークブック デザイナー オブジェクトをインスタンス化します。
WorkbookDesigner report = new WorkbookDesigner();
```
交換する`"Your Document Directory"` Excelファイルを保存する実際のファイルパスを入力します。`WorkbookDesigner`クラスはこの操作の中心であり、ここでテンプレートを定義します。
## ステップ3: セルにマーカーを追加する
ここで、ワークシートにスマート マーカーを追加する必要があります。これらのマーカーは、後で入力するデータのプレースホルダーになります。
```csharp
//ワークブックの最初のワークシートを取得します。
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
//セルにいくつかのマーカーを入力します。
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
最初のワークシートを指定して、ヘッダーセルの値を設定します。スマートマーカーには、`&=`これは、これらが後で挿入されるデータのプレースホルダーであることを Aspose に伝えます。
## ステップ4: 人物リストを作成する
それでは、私たちの`Person`スマート マーカーを設定するために使用するクラスです。
```csharp
//カスタム クラスに基づいてリスト コレクションをインスタンス化します。
IList<Person> list = new List<Person>();
//カスタム クラス オブジェクトを使用してマーカーの値を指定します。
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
リストを作成し、インスタンスを追加します`Person`このリストは、Excel テンプレートにデータを入力する際のデータ ソースとして機能します。
## ステップ5: データソースとプロセスマーカーを設定する
リストが準備できたら、それをデータソースとして設定する必要があります。`WorkbookDesigner`インスタンスを作成してからマーカーを処理します。
```csharp
//データソースを設定します。
report.SetDataSource("MyProduct", list);
//マーカーを処理します。
report.Process(false);
```
の`SetDataSource`メソッドは、以前に定義したリストをマーカーにリンクします。`Process`メソッドは、ワークブック内のスマート マーカーをオブジェクトの実際の値に置き換えます。
## ステップ6: Excelファイルを保存する
最後に、変更したワークブックを指定したディレクトリに保存します。
```csharp
// Excel ファイルを保存します。
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
この行は、指定されたファイル パスにブックを保存します。Excel を使用してこのファイルを開き、挿入されたデータを確認できます。
## 結論
これで完了です。独自のカスタム クラスを使用して、Aspose.Cells のスマート マーカーを使用して Excel ファイルを作成できました。この方法により、データ管理がより動的になるだけでなく、コードが整理された状態になります。
したがって、分析、追跡情報、またはその他のデータ関連タスク用のレポートを生成する場合でも、スマート マーカーは Excel レポートをより管理しやすく柔軟にする上で役立ちます。
## よくある質問
### Aspose.Cells のスマート マーカーとは何ですか?
スマート マーカーは、実行時にデータを動的に挿入できる Excel ドキュメント内の特別なプレースホルダーです。
### スマートマーカーに匿名型を使用できますか?
はい。スマート マーカーは、予想されるデータ構造と一致している限り、匿名型を含む任意のオブジェクト タイプで使用できます。
### Aspose.Cells は無料で使用できますか?
Aspose.Cells は有料製品ですが、無料トライアルでその機能を試すことができます。
### Aspose.Cells はどのようなファイル形式をサポートしていますか?
XLS、XLSX、CSV など、幅広いファイル形式をサポートしています。
### Aspose.Cells の詳細情報はどこで入手できますか?
詳細については、[ドキュメント](https://reference.aspose.com/cells/net/)または、[サポートフォーラム](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
