---
title: 割り込みモニタを使用して変換または読み込みを停止する
linktitle: 割り込みモニタを使用して変換または読み込みを停止する
second_title: Aspose.Cells .NET Excel 処理 API
description: 詳細なステップバイステップのチュートリアルを使用して、Interrupt Monitor を使用して Aspose.Cells for .NET でワークブックの変換を停止する方法を学習します。
weight: 26
url: /ja/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 割り込みモニタを使用して変換または読み込みを停止する

## 導入
大きな Excel ファイルの操作には、多くの場合、時間とリソースを浪費する長いプロセスが伴います。しかし、変更が必要だと気付いたときに、変換プロセスを途中で停止できるとしたらどうでしょうか。Aspose.Cells for .NET には、割り込みモニターと呼ばれる機能があり、これを使用すると、ワークブックを PDF などの別の形式に変換するのを中断できます。これは、特に大量のデータ ファイルで作業しているときに非常に役立ちます。このガイドでは、Aspose.Cells for .NET の割り込みモニターを使用して変換プロセスを中断する方法について説明します。
## 前提条件
始める前に、次のものを用意しておいてください。
1.  Aspose.Cells for .NET - ダウンロード[ここ](https://releases.aspose.com/cells/net/).
2. .NET 開発環境 - Visual Studio など。
3. C# プログラミングの基礎知識 - C# 構文に精通していると、理解しやすくなります。
## パッケージのインポート
まず、必要なパッケージをインポートしましょう。インポートするものは次のとおりです。
- Aspose.Cells: Excel ファイルを操作するためのメイン ライブラリ。
- System.Threading: スレッドを管理します。この例では 2 つのプロセスを並列実行します。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
プロセスを詳細な手順に分解してみましょう。各手順は、Excel ブックの変換を管理するために割り込みモニターを設定して使用することの重要性を理解するのに役立ちます。
## ステップ1: クラスを作成し、出力ディレクトリを設定する
まず、関数をカプセル化するクラスと、出力ファイルが保存されるディレクトリが必要です。
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
交換する`"Your Document Directory"` PDF ファイルを保存する実際のパスを入力します。
## ステップ2: 割り込みモニターをインスタンス化する
次に、InterruptMonitor オブジェクトを作成します。このモニターは、任意の時点でプロセスを中断する機能を設定することで、プロセスの制御に役立ちます。
```csharp
InterruptMonitor im = new InterruptMonitor();
```
この割り込みモニターはワークブックに添付され、変換プロセスを管理できるようになります。
## ステップ3: 変換用にワークブックを設定する
ここで、ワークブック オブジェクトを作成し、それに InterruptMonitor を割り当てて、最初のワークシートにアクセスし、サンプル テキストを挿入してみましょう。
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
上記のコードはワークブックを作成し、それに InterruptMonitor を設定し、ファーセルにテキストを配置します (`J1000000`)。このセル位置にテキストを配置すると、ブックの処理に時間がかかり、InterruptMonitor が介入するのに十分な時間が与えられます。
## ステップ4: ワークブックをPDFとして保存し、中断を処理する
さて、ワークブックをPDFとして保存してみましょう。`try-catch`発生する可能性のある中断を処理するためのブロック。
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
プロセスが中断された場合、例外がそれをキャッチし、適切なメッセージを表示します。それ以外の場合、ワークブックは PDF として保存されます。
## ステップ5: 変換プロセスを中断する
ここでの主な機能は、プロセスを中断する機能です。`Thread.Sleep`そして、`Interrupt()` 10 秒後に変換を停止する方法。
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
この遅延により、割り込み信号が送信される前にワークブックが PDF への変換を開始する時間が与えられます。
## ステップ6: スレッドを同時に実行する
すべてをまとめるには、両方の関数を別々のスレッドで開始する必要があります。こうすることで、ワークブックの変換と割り込み待機が同時に発生します。
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
上記のコードは`CreateWorkbookAndConvertItToPdfFormat`そして`WaitForWhileAndThenInterrupt`並列スレッドで実行し、両方のプロセスが終了したら結合します。
## ステップ7: 最終実行
最後に、`Run()`コードを実行する方法。
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
これ`Run`メソッドは、アクションの中断を開始して観察するためのエントリ ポイントです。
## 結論
このチュートリアルでは、Aspose.Cells for .NET で変換プロセスを中断する方法について説明しました。割り込みモニターは、大きな Excel ファイルで作業するときに役立つツールで、完了を待たずにプロセスを停止できます。これは、時間とリソースが貴重で、迅速なフィードバックが必要なシナリオで特に役立ちます。
## よくある質問
### Aspose.Cells for .NET の割り込みモニターとは何ですか?  
割り込みモニターを使用すると、ワークブックの変換または読み込みプロセスを途中で停止できます。
### PDF 以外の形式でも Interrupt Monitor を使用できますか?  
はい、サポートされている他の形式への変換を中断することもできます。
### Thread.Sleep() は割り込みタイミングにどのような影響を与えますか?  
Thread.Sleep() は、割り込みをトリガーする前に遅延を作成し、変換を開始する時間を与えます。
### 10 秒前にプロセスを中断できますか?  
はい、遅延を変更します`WaitForWhileAndThenInterrupt()`より短い時間になります。
### 割り込みプロセスはパフォーマンスに影響しますか?  
影響は最小限であり、長時間実行されるプロセスの管理に非常に役立ちます。
詳細については、[Aspose.Cells for .NET ドキュメント](https://reference.aspose.com/cells/net/)ヘルプが必要な場合は、[サポートフォーラム](https://forum.aspose.com/c/cells/9)または[無料トライアル](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
