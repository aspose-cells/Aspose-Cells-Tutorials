---
title: Excel のアドインから関数を登録して呼び出す
linktitle: Excel のアドインから関数を登録して呼び出す
second_title: Aspose.Cells .NET Excel 処理 API
description: 簡単なステップバイステップのチュートリアルで、Aspose.Cells for .NET を使用して Excel のアドインから関数を登録および呼び出す方法を学びます。
weight: 20
url: /ja/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel のアドインから関数を登録して呼び出す

## 導入
アドインから関数を呼び出して Excel エクスペリエンスを強化したいですか? そうであれば、ここが最適な場所です。Excel アドインはスプレッドシートの妖精のゴッドマザーのようなものです。魔法のように機能を拡張し、新しいツールをすぐに使えるようにしてくれます。Aspose.Cells for .NET を使用すると、これらのアドイン関数を登録して使用することがこれまで以上に簡単になります。 
このガイドでは、Aspose.Cells for .NET を使用して Excel アドインから関数を登録して呼び出すプロセスについて説明します。すべてをステップごとに説明するので、すぐにプロになったような気分になれます。
## 前提条件
コーディングの魔法に飛び込む前に、準備しておく必要があるものについて説明しましょう。
1. Visual Studio: マシンに Visual Studio がセットアップされていることを確認してください。ここでコードを記述して実行します。
2.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリをインストールする必要があります。[ダウンロードページ](https://releases.aspose.com/cells/net/).
3. C# の基本知識: C# を少し理解しておくと、スムーズに理解できるようになります。
4.  Excelアドイン: アドインファイル（`.xlam`登録して使用したい関数が含まれている ) を作成します。
5. サンプルExcelアドイン: このチュートリアルでは、次のExcelアドインを使用します。`TESTUDF.xlam`. ぜひこれを利用してみてください!
準備ができたので、袖をまくってコーディングを始めましょう。
## パッケージのインポート
まず、C# ファイルの先頭にいくつかの重要な名前空間をインポートする必要があります。含める必要があるものは次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
これらの名前空間を使用すると、このチュートリアルで使用するクラスとメソッドにアクセスできるようになります。
これを管理しやすいステップに分解してみましょう。このガイドを読み終える頃には、アドイン関数を登録して Excel ブックで使用する方法をしっかりと理解できるようになります。
## ステップ1: ソースディレクトリと出力ディレクトリを設定する
アドインを登録する前に、アドインと出力ファイルを保存する場所を定義する必要があります。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
交換する`"Your Document Directory"`実際の経路で`.xlam`ファイルと出力ファイルが保存されます。これはショーが始まる前にステージを設定するようなものです。
## ステップ2: 空のワークブックを作成する
次に、アドイン関数を試すことができる空のブックを作成します。
```csharp
//空のワークブックを作成する
Workbook workbook = new Workbook();
```
このコード行は、遊び場として機能する新しいワークブックを作成します。これは、創造的なストロークをすぐに実行できる新しいキャンバスだと考えてください。
## ステップ3: アドイン関数を登録する
さて、本題に入りましょう。アドイン関数を登録する時が来ました。手順は次のとおりです。
```csharp
//マクロ対応アドインを関数名とともに登録する
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
この行は、アドイン関数を登録します。`TEST_UDF`見つかった`TESTUDF.xlam`アドインファイル。`false`パラメータは、アドインが「分離」モードで読み込まれないことを意味します。 
## ステップ4: 追加機能の登録（ある場合）
同じアドイン ファイルに複数の関数が登録されている場合は、それらも登録できます。
```csharp
//ファイルにさらに関数を登録する（ある場合）
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
ここでは、同じアドインからさらに機能を追加するのがいかに簡単かがわかります。ビルディング ブロックのように積み重ねていくだけです。
## ステップ5: ワークシートにアクセスする
次に進み、関数を使用するワークシートにアクセスしましょう。 
```csharp
//最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
ワークブックの最初のワークシートにアクセスして、数式を配置します。楽しいことが起こる部屋への扉を開くようなものです。
## ステップ6: 特定のセルにアクセスする
次に、数式に使用するセルを選択する必要があります。 
```csharp
//最初のセルにアクセス
var cell = worksheet.Cells["A1"];
```
ここではセル A1 を指しています。ここに魔法の式を配置します。宝の地図にターゲットをピンで留めるようなものと考えてください。
## ステップ7: 数式を設定する
いよいよお披露目です！登録した関数を呼び出す数式を設定しましょう。
```csharp
//アドインに存在する数式名を設定する
cell.Formula = "=TEST_UDF()";
```
この行では、Excel にセル A1 内の関数を使用するように指示しています。Excel にコマンドを与えて、「これを実行してください」と言っているようなものです。
## ステップ8: ワークブックを保存する
最後になりましたが、私たちの傑作を保存する時が来ました。
```csharp
//ワークブックを XLSX 形式で出力して保存します。
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
ここでは、ワークブックを XLSX ファイルとして保存しています。この最後のステップは、絵画を額縁に入れて展示する準備をするようなものです。
## ステップ9: 実行を確認する
最後に、コンソールに成功メッセージを出力して、すべてを終了しましょう。
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
この行は私たちの勝利の旗の役割を果たします。すべてが順調に進んだことを確認するためのちょっとした素敵なタッチです。
## 結論 
これで完了です。Aspose.Cells for .NET を使用して Excel アドインから関数を登録および呼び出す方法を学習しただけでなく、各手順についての理解も深めました。これで生活が少し楽になりましたね。ぜひご自身で試してみてください。Excel アドインを詳しく調べて、スプレッドシートに新しいレベルのインタラクティブ性と機能性を加えましょう。
## よくある質問
### Excel アドインとは何ですか?  
Excel アドインは、Excel にカスタム機能、関数、またはコマンドを追加して、ユーザーが Excel の機能を拡張できるようにするプログラムです。
### Aspose.Cells をローカルにインストールせずに使用できますか?  
いいえ、.NET アプリケーションで使用するには Aspose.Cells ライブラリをインストールする必要があります。
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?  
訪問することができます[一時ライセンスページ](https://purchase.aspose.com/temporary-license/)詳細についてはこちらをご覧ください。
### つのアドインから複数の関数を呼び出すことは可能ですか?  
はい！同じアドインファイルから複数の関数を登録するには、`RegisterAddInFunction`方法。
### Aspose.Cells に関する詳細なドキュメントはどこで見つかりますか?  
サイトで包括的なドキュメントを閲覧できます[ここ](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
