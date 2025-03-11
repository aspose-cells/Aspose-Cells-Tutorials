---
title: ワークブック デザイナーに ICellsDataTableDataSource を使用する
linktitle: ワークブック デザイナーに ICellsDataTableDataSource を使用する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET で ICellsDataTableDataSource を使用して Excel シートに動的にデータを入力する方法を学びます。ワークブック内の顧客データを自動化するのに最適です。
weight: 21
url: /ja/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブック デザイナーに ICellsDataTableDataSource を使用する

## 導入
自動化されたデータ統合を備えた高度なスプレッドシートを作成することは、特にビジネスアプリケーションではゲームチェンジャーになる可能性があります。このチュートリアルでは、`ICellsDataTableDataSource`Aspose.Cells for .NET のワークブック デザイナー向けです。Excel ファイルにカスタム データを動的に読み込むための、シンプルで人間が判読できるソリューションの構築手順を説明します。顧客リスト、売上データ、または同様のものを扱っている場合は、このガイドが役に立ちます。
## 前提条件
開始するには、次のものを用意してください。
-  Aspose.Cells for .NETライブラリ – 以下からダウンロードできます。[ここ](https://releases.aspose.com/cells/net/)または無料試用版を入手してください。
- .NET 開発環境 - Visual Studio は最適な選択肢です。
- C# の基本的な理解 - クラスとデータ処理に関する知識があれば、理解しやすくなります。
先に進む前に、開発環境に必要なパッケージが設定されていることを確認してください。
## パッケージのインポート
Aspose.Cells を効果的に使用するには、必須パッケージをインポートする必要があります。以下は、必要な名前空間のクイック リファレンスです。
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## ステップ1: 顧客データクラスを定義する
まず、簡単な`Customer`クラス。このクラスには、次のような基本的な顧客の詳細が保持されます。`FullName`そして`Address`データの「形状」を定義する方法と考えてください。
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## ステップ2: 顧客リストクラスを設定する
次に、`CustomerList`拡張するクラス`ArrayList`このカスタマイズされたリストには、`Customer`各エントリへのインデックスアクセスを許可します。
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
この手順では、Aspose.Cells が認識して処理できる形式にデータをラップします。
## ステップ3: 顧客データソースクラスを作成する
ここからが面白いところです。`CustomerDataSource`クラスの実装`ICellsDataTable`データを Aspose.Cells のワークブック デザイナーと互換性のあるものにするためです。
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
この習慣`CustomerDataSource`クラスにより、Aspose.Cellsは各`Customer`オブジェクトを Excel ファイル内の行として表示します。
## ステップ4: 顧客データを初期化する
次に、リストに顧客を追加してみましょう。ここで、ワークブックに書き込むデータを読み込みます。必要に応じて、自由にエントリを追加してください。
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
この例では、小さなデータセットを使用しています。ただし、データベースや他のソースからデータを読み込むことで、このリストを簡単に拡張できます。
## ステップ5: ワークブックを読み込む
ここで、必要なスマート マーカーを含む既存の Excel ブックを開きます。このブックはテンプレートとして機能し、Aspose.Cells はスマート マーカーを顧客データに動的に置き換えます。
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
確実に`"SmartMarker1.xlsx"`次のようなプレースホルダーが含まれています`&=Customer.FullName`そして`&=Customer.Address`データを入力する必要がある場所。
## ステップ 6: ワークブック デザイナーを設定する
ここで、顧客データ ソースをワークブックのスマート マーカーにリンクするようにワークブック デザイナーを構成します。
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
の`SetDataSource`メソッドは、`CustomerDataSource`ワークブック内のスマートマーカーに追加されます。各マーカーには`&=Customer`Excel 内の対応する顧客データに置き換えられます。
## ステップ 7: ワークブックを処理して保存する
最後に、ワークブックを処理してデータを入力し、結果を保存します。
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
このコードはスマートマーカー処理をトリガーし、すべてのプレースホルダーをデータに置き換え、結果を次のように保存します。`dest.xlsx`.
## 結論
おめでとうございます！実装に成功しました`ICellsDataTableDataSource`Aspose.Cells for .NET を使用するワークブック デザイナー向け。このアプローチは、特に顧客リストや製品在庫などの動的なデータを扱う場合に、スプレッドシートでのデータ入力を自動化するのに最適です。これらのスキルがあれば、Excel ベースのレポート作成を簡単にするデータ駆動型アプリケーションの構築に着手できます。
## よくある質問
### 何ですか`ICellsDataTable` in Aspose.Cells?  
これは、動的なデータ入力のためにカスタム データ ソースを Aspose.Cells Smart Markers にリンクできるようにするインターフェイスです。
### ワークブック テンプレートのデータをカスタマイズするにはどうすればよいですか?  
スマートマーカーと呼ばれるプレースホルダー、例えば`&=Customer.FullName`が使用されます。これらのマーカーは処理中に実際のデータに置き換えられます。
### Aspose.Cells for .NET は無料ですか?  
 Aspose.Cellsは無料トライアルを提供していますが、フルアクセスには有料ライセンスが必要です。[無料トライアル](https://releases.aspose.com/)または[買う](https://purchase.aspose.com/buy)オプション。
### 顧客データを動的に追加できますか?  
もちろんです！`CustomerList`プログラムを実行する前に追加のエントリを入力します。
### 困ったときはどこで助けを得られますか?  
 Asposeには[サポートフォーラム](https://forum.aspose.com/c/cells/9)ユーザーはここで質問したり、コミュニティや Aspose チームから支援を受けることができます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
