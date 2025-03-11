---
title: Excel でギア型スマート アートからテキストを抽出する
linktitle: Excel でギア型スマート アートからテキストを抽出する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel のギア型 SmartArt からテキストを抽出する方法を学びます。ステップバイステップのガイドとコード例が含まれています。
weight: 10
url: /ja/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel でギア型スマート アートからテキストを抽出する

## 導入
Excel で作業しているときに、視覚的に魅力的な方法でメッセージを伝えるのに役立つ SmartArt グラフィックに遭遇することがあります。これらのグラフィックの中で、歯車型の SmartArt は階層的かつ方向性のあるフローが特徴で、プロジェクト管理やシステム モデリングでよく使用されます。しかし、これらの図形からプログラムでテキストを抽出する必要がある場合はどうすればよいでしょうか。ここで Aspose.Cells for .NET が役立ちます。このブログ記事では、Aspose.Cells for .NET を使用して Excel の歯車型の SmartArt 図形からテキストを抽出する方法をステップ バイ ステップで説明します。
## 前提条件
始める前に、準備しておく必要のある重要な前提条件がいくつかあります。心配しないでください。簡単なので、手順を説明します。
### .NET 環境
コンピューターに .NET 開発環境が設定されていることを確認してください。Visual Studio または .NET 開発をサポートする任意の IDE を使用できます。
### .NET 用 Aspose.Cells
次に、Aspose.Cellsライブラリをインストールする必要があります。これはExcelファイルをシームレスに操作できるようにする強力なツールです。ダウンロードは以下から行えます。[Aspose リリース ページ](https://releases.aspose.com/cells/net/)まずは探検したいなら、[無料トライアル](https://releases.aspose.com/).
### C#の基礎知識
このチュートリアルを進めるには、C# プログラミングの基本的な知識が必要です。初心者でも心配はいりません。できるだけ初心者に優しい手順を設計します。
### サンプル Excel ファイル
このチュートリアルでは、ギアタイプの SmartArt 図形を含むサンプル Excel ファイルも必要です。簡単に作成したり、オンラインでテンプレートを見つけたりできます。ただし、SmartArt にギアタイプの図形が少なくとも 1 つ含まれていることを確認してください。
## パッケージのインポート
コーディングを始めるには、必要なパッケージをインポートする必要があります。手順は次のとおりです。
### 新しいプロジェクトを作成する
1. .NET IDE を開きます。
2. 新しいプロジェクトを作成します。たとえば、.NET オプションで「コンソール アプリケーション」を選択します。
3. プロジェクトに名前を付け、必要なフレームワークを設定します。 
### 参照を追加
Aspose.Cells を使用するには、プロジェクトにライブラリ参照を追加する必要があります。
1. ソリューション エクスプローラーでプロジェクト名を右クリックします。
2. 「NuGet パッケージの管理」を選択します。
3. 「Aspose.Cells」を検索してインストールします。
インストールしたら、コーディングの準備は完了です。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
それでは、テキストを抽出するために使用するコードを分解してみましょう。ステップごとに実行していきます。
## ステップ1: ソースディレクトリを設定する
まず、Excel ファイルが配置されているディレクトリを定義します。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
```
必ず交換してください`"Your Document Directory"`Excel ファイルへの実際のパスを入力します。
## ステップ2: Excelワークブックを読み込む
次に、Excel ブックを読み込みます。その内容にアクセスするには、次の操作を行います。
```csharp
//ギアタイプのスマートアートシェイプを含むサンプル Excel ファイルを読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
この部分ではサンプルの Excel ワークブックを読み込みます。
## ステップ3: 最初のワークシートにアクセスする
ワークブックを読み込んだので、SmartArt が存在する最初のワークシートにアクセスしてみましょう。
```csharp
//最初のワークシートにアクセスします。
Worksheet ws = wb.Worksheets[0];
```
これにより、最初のワークシートが取得され、さらに操作できるようになります。
## ステップ4: 最初の図形にアクセスする
次に、ワークシート内の最初の図形にアクセスする必要があります。これにより、SmartArt グラフィック内を移動できるようになります。
```csharp
//最初の図形にアクセスします。
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
ここでは、必要な SmartArt であると想定される最初の図形に焦点を当てています。
## ステップ5: グループシェイプを取得する
図形が完成したら、次は SmartArt 表現の結果を取得します。
```csharp
//ギア型スマートアートシェイプの結果をグループシェイプの形式で取得します。
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
これにより、ギア タイプの SmartArt がグループ化された図形として取得されます。
## ステップ6: 個々の図形を抽出する
次に、SmartArt を構成する個々の図形を抽出します。
```csharp
//グループ シェイプを構成する個々のシェイプのリストを取得します。
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
この配列には、ループ処理する必要があるすべての個別の図形が保持されます。
## ステップ7: テキストを抽出して印刷する
最後に、図形の配列をループして、任意のギアタイプの図形からテキストを抽出します。
```csharp
//ギア型図形のテキストを抽出し、コンソールに印刷します。
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
このループでは、図形の種類をチェックし、歯車型の図形の場合はテキストを出力します。
## ステップ8: 実行の確認
最後に、プロセスが正常に完了したら確認メッセージを追加することもできます。
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
これで抽出が完了し、コンソールにテキスト出力が表示されます。
## 結論
おめでとうございます！Aspose.Cells for .NET を使用して Excel のギア型 SmartArt 図形からテキストを抽出する方法を学習しました。この便利なテクニックは、視覚的なデータ表現に依存するレポートやドキュメントの自動化への扉を開きます。熟練した開発者でも、始めたばかりの開発者でも、SmartArt から情報を制御および抽出することで、ワークフローを合理化し、効率を高めることができます。詳細な内容もぜひご覧ください。[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)さらなる機能のために。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、開発者が Excel ファイルを簡単に作成および操作できるようにする .NET ライブラリです。
### Aspose.Cells を他の言語で使用できますか?
はい！Aspose.Cells は、Java や Python を含む複数のプログラミング言語で利用できます。
### Aspose.Cells for .NET を購入する必要がありますか?
 Aspose.Cellsは無料トライアルを提供していますが、長期間使用するには購入が必要です。購入オプションは以下をご覧ください。[ここ](https://purchase.aspose.com/buy).
### Aspose.Cells ユーザー向けのサポートはありますか?
もちろんです！コミュニティサポートは[Aspose.Cells フォーラム](https://forum.aspose.com/c/cells/9).
### この方法を使用して他の種類の SmartArt を抽出できますか?
はい、コード内の条件を少し変更するだけで、さまざまな SmartArt 図形からテキストを抽出できます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
