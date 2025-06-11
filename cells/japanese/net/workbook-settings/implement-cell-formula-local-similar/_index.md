---
"description": "Aspose.Cells for .NET の範囲数式ローカル機能に似たセル数式を実装する方法を学びます。Excel の組み込み関数名のカスタマイズ方法などについても学習します。"
"linktitle": "範囲式ローカルと同様にセル式ローカルを実装する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "範囲式ローカルと同様にセル式ローカルを実装する"
"url": "/ja/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 範囲式ローカルと同様にセル式ローカルを実装する

## 導入
Aspose.Cells for .NET は、強力で柔軟なスプレッドシート操作 API であり、Excel ファイルをプログラムで作成、操作、変換できます。Aspose.Cells が提供する数多くの機能の一つとして、組み込みの Excel 関数の動作をカスタマイズする機能があります。これには、独自のローカル関数名を作成する機能も含まれます。このチュートリアルでは、Aspose.Cells for .NET の範囲式ローカル機能に似たセル式を実装する手順を説明します。
## 前提条件
始める前に、次のものがあることを確認してください。
1. システムに Microsoft Visual Studio 2010 以降がインストールされていること。
2. プロジェクトにAspose.Cells for .NETライブラリの最新バージョンがインストールされていること。ライブラリは以下からダウンロードできます。 [Aspose.Cells for .NET のダウンロード ページ](https://releases。aspose.com/cells/net/).
## パッケージのインポート
まず、C#プロジェクトに必要なパッケージをインポートする必要があります。コードファイルの先頭に次のusingステートメントを追加してください。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## ステップ1: カスタムグローバリゼーション設定クラスを作成する
最初のステップはカスタム `GlobalizationSettings` Excel関数のデフォルトの動作をオーバーライドできるクラスです。この例では、 `SUM` そして `AVERAGE` 機能する `UserFormulaLocal_SUM` そして `UserFormulaLocal_AVERAGE`、 それぞれ。
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //必要に応じて SUM 関数名を変更します。
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //必要に応じて AVERAGE 関数名を変更します。
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## ステップ2: 新しいワークブックを作成し、カスタムグローバリゼーション設定を割り当てる
次に、新しいワークブックインスタンスを作成し、カスタム `GlobalizationSettings` ワークブックの実装クラス `Settings.GlobalizationSettings` 財産。
```csharp
//ワークブックを作成する
Workbook wb = new Workbook();
//GlobalizationSettings実装クラスを割り当てる
wb.Settings.GlobalizationSettings = new GS();
```
## ステップ3: 最初のワークシートとセルにアクセスする
ここで、ワークブックの最初のワークシートと、そのワークシート内の特定のセルにアクセスしてみましょう。
```csharp
//最初のワークシートにアクセスする
Worksheet ws = wb.Worksheets[0];
//セルにアクセス
Cell cell = ws.Cells["C4"];
```
## ステップ4: 数式を割り当ててFormulaLocalを印刷する
最後に、 `SUM` そして `AVERAGE` セルに数式を入力し、結果を印刷します `FormulaLocal` 価値観。
```csharp
//SUM式を割り当ててそのFormulaLocalを出力する
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//AVERAGE式を割り当て、そのFormulaLocalを出力する
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## 結論
このチュートリアルでは、Aspose.Cells for .NETの範囲式ローカル機能に似たセル式を実装する方法を学びました。カスタムセル式を作成することで、 `GlobalizationSettings` クラスを使用すると、Excel関数のデフォルトの動作をオーバーライドし、ニーズに合わせてローカル関数名をカスタマイズできます。これは、ローカライズまたは国際化されたExcelドキュメントを扱う場合に特に便利です。
## よくある質問
### の目的は何ですか？ `GlobalizationSettings` Aspose.Cells のクラスですか?
その `GlobalizationSettings` Aspose.Cells のクラスを使用すると、ローカル関数名を変更する機能など、組み込みの Excel 関数の動作をカスタマイズできます。
### 関数以外の動作をオーバーライドできますか？ `SUM` そして `AVERAGE`？
はい、Excelの組み込み関数の動作を変更するには、 `GetLocalFunctionName` カスタムメソッド `GlobalizationSettings` クラス。
### 関数名をデフォルト値に戻す方法はありますか?
はい、カスタム名を削除するか、 `GlobalizationSettings` クラスまたは空の文字列を返すことによって `GetLocalFunctionName` 方法。
### この機能を使用して Aspose.Cells でカスタム関数を作成できますか?
いいえ、 `GlobalizationSettings` クラスはExcelの組み込み関数の動作をオーバーライドするものであり、カスタム関数を作成するためのものではありません。カスタム関数を作成する必要がある場合は、 `UserDefinedFunction` Aspose.Cells のクラス。
### この機能は Aspose.Cells for .NET のすべてのバージョンで使用できますか?
はい、 `GlobalizationSettings` クラスと関数名をカスタマイズする機能は、Aspose.Cells for .NET のすべてのバージョンで利用できます。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}