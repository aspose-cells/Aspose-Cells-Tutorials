---
"description": "Aspose.Cells for .NET の汎用リストとスマートマーカーをマスターすれば、動的な Excel レポートを簡単に作成できます。開発者向けの簡単なガイドです。"
"linktitle": "スマートマーカーAspose.Cellsで汎用リストを使用する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "スマートマーカーAspose.Cellsで汎用リストを使用する"
"url": "/ja/net/smart-markers-dynamic-data/generic-list-smart-markers/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# スマートマーカーAspose.Cellsで汎用リストを使用する

## 導入
動的なレポートやデータ駆動型アプリケーションの作成は、今日のテクノロジー環境において不可欠なスキルです。.NETやExcelファイルを扱っている方なら、Excelスプレッドシートをプログラム的に操作するために特別に設計された強力なライブラリ、Aspose.Cellsについてご存知でしょう。この包括的なガイドでは、Aspose.Cellsのスマートマーカー付き汎用リストの活用方法を段階的に解説し、アプリケーションにおけるデータ処理を最適化するためのアプローチを段階的に示します。
## 前提条件
コードに進む前に、必要なものを簡単に確認しましょう。
### C#の基礎知識
C#の基礎知識と、クラスやオブジェクトの扱い方を理解している必要があります。オブジェクト指向プログラミングに精通しているなら、すでに正しい道を歩んでいると言えるでしょう。
### Aspose.Cells for .NET がインストール済み
.NETプロジェクトにAspose.Cellsがインストールされていることを確認してください。ライブラリは以下からダウンロードできます。 [Aspose ウェブサイト](https://releases。aspose.com/cells/net/). 
### Visual Studio 環境
Visual Studio をマシンにインストールしておくことは非常に重要です。Visual Studio は、C# コードを書く最も一般的な開発環境です。
### テンプレートファイル
このチュートリアルでは、事前に設定できるシンプルなExcelテンプレートを使用します。デモ用に空白のワークブックのみが必要です。
## パッケージのインポート
基本的な準備が整ったので、必要なパッケージをインポートすることから始めましょう。目安としては、以下の名前空間を含めるのが良いでしょう。
```csharp
using System.IO;
using Aspose.Cells;
using System;
using System.Drawing;
using System.Collections.Generic;
```
これらの名前空間は、Excel ファイルの操作やセルのスタイル設定に必要な機能を提供します。
## ステップ1: クラスを定義する
まずは最初に！ `Person` そして `Teacher` クラス。やり方は以下のとおりです。
### Personクラスを定義する
その `Person` クラスは名前や年齢などの基本属性を保持します。
```csharp
public class Person
{
    int _age;
    string _name;
    
    public int Age
    {
        get { return _age; }
        set { _age = value; }
    }
    
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
    
    public Person(string name, int age)
    {
        _age = age;
        _name = name;
    }
}
```
### 教師クラスを定義する
次は `Teacher` クラスは、 `Person` クラス。このクラスはさらに生徒のリストをカプセル化します。
```csharp
public class Teacher : Person
{
    private IList<Person> m_students;
    public IList<Person> Students
    {
        get { return m_students; }
        set { m_students = value; }
    }
    
    public Teacher(string name, int age) : base(name, age)
    {
        m_students = new List<Person>();
    }
}
```
## ステップ2: ワークブックを初期化してデザイナーを作成する
クラスの準備ができたので、次はワークブックを初期化します。
```csharp
string dataDir = "Your Document Directory"; // ドキュメントディレクトリを指定する
Workbook workbook = new Workbook(); // 新しいワークブックインスタンス
Worksheet worksheet = workbook.Worksheets[0];
```
## ステップ3: ワークシートにスマートマーカーを設定する
Excel ワークシートにスマート マーカーを設定し、動的な値が配置される場所を示します。
```csharp
worksheet.Cells["A1"].PutValue("Teacher Name");
worksheet.Cells["A2"].PutValue("&=Teacher.Name");
worksheet.Cells["B1"].PutValue("Teacher Age");
worksheet.Cells["B2"].PutValue("&=Teacher.Age");
worksheet.Cells["C1"].PutValue("Student Name");
worksheet.Cells["C2"].PutValue("&=Teacher.Students.Name");
worksheet.Cells["D1"].PutValue("Student Age");
worksheet.Cells["D2"].PutValue("&=Teacher.Students.Age");
```
## ステップ4: プレゼンテーションを強化するためにスタイルを適用する
優れたレポートは見た目も魅力的であるべきです！ヘッダーにスタイルを適用してみましょう。
```csharp
Range range = worksheet.Cells.CreateRange("A1:D1");
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
StyleFlag flag = new StyleFlag();
flag.All = true;
range.ApplyStyle(style, flag);
```
## ステップ5: 教師と生徒のインスタンスを作成する
さて、インスタンスを作成しましょう `Teacher` そして `Person` クラスを作成してデータを入力します。
```csharp
System.Collections.Generic.List<Teacher> list = new System.Collections.Generic.List<Teacher>();
// 最初の教師オブジェクトを作成する
Teacher h1 = new Teacher("Mark John", 30);
h1.Students = new List<Person>
{
    new Person("Chen Zhao", 14),
    new Person("Jamima Winfrey", 18),
    new Person("Reham Smith", 15)
};
// 2番目の教師オブジェクトを作成する
Teacher h2 = new Teacher("Masood Shankar", 40);
h2.Students = new List<Person>
{
    new Person("Karishma Jathool", 16),
    new Person("Angela Rose", 13),
    new Person("Hina Khanna", 15)
};
// リストに追加
list.Add(h1);
list.Add(h2);
```
## ステップ6: デザイナーのデータソースを設定する
ここで、準備したワークシートにデータをリンクする必要があります。 
```csharp
WorkbookDesigner designer = new WorkbookDesigner();
designer.Workbook = workbook;
designer.SetDataSource("Teacher", list);
```
## ステップ7：マーカーを処理する
次のステップでは、先ほど配置したすべてのスマート マーカーを処理します。
```csharp
designer.Process();
```
## ステップ8: 列を自動調整してワークブックを保存する
すべてがプロフェッショナルに見えるように、列を自動調整してワークブックを保存しましょう。
```csharp
worksheet.AutoFitColumns();
designer.Workbook.Save(dataDir + "output.xlsx"); // 指定されたディレクトリに保存する
```
## 結論
これで完了です！Aspose.Cells for .NETの汎用リストとスマートマーカーを活用し、Excelワークシートを動的に作成できました。このスキルを習得すれば、複雑なレポートを簡単に作成し、アプリケーションにデータドリブンな機能を組み込むことができます。学校のレポート、ビジネス分析、その他あらゆる動的コンテンツの作成など、このガイドで紹介するテクニックは、ワークフローを大幅に効率化するのに役立ちます。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、Microsoft Excel をインストールしなくても Excel ファイルを作成および管理するための .NET ライブラリです。
### Aspose.Cells を他のファイル形式で使用できますか?
はい！Aspose は PDF、Word、その他の形式用のライブラリを提供しており、多目的にドキュメントを管理できます。
### Aspose.Cells を使用するにはライセンスが必要ですか?
無料トライアルから始めることができます [ここ](https://releases.aspose.com/)ただし、実稼働環境で使用する場合は有料ライセンスが必要です。
### スマートマーカーとは何ですか?
スマート マーカーは Excel テンプレート内のプレースホルダーであり、Aspose.Cells によって処理されるときに実際のデータに置き換えられます。
### Aspose.Cells は大規模なデータセットに適していますか?
もちろんです! Aspose.Cells はパフォーマンスが最適化されており、大規模なデータセットを効率的に処理できます。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}