---
title: Aspose.Cells を使用して VBAMacro ユーザー フォーム デザイナー ストレージをワークブックにコピーする
linktitle: Aspose.Cells を使用して VBAMacro ユーザー フォーム デザイナー ストレージをワークブックにコピーする
second_title: Aspose.Cells .NET Excel 処理 API
description: 包括的なステップバイステップのチュートリアルを使用して、Aspose.Cells for .NET で VBA マクロ ユーザー フォーム デザイナーを効率的にコピーする方法を学びましょう。Excel の可能性を解き放ちます。
weight: 11
url: /ja/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して VBAMacro ユーザー フォーム デザイナー ストレージをワークブックにコピーする

## 導入
ようこそ! VBA マクロとユーザー フォームを使用して Excel エクスペリエンスを強化したい場合、ここが最適な場所です。このガイドでは、Aspose.Cells for .NET を使用して、VBA マクロ ユーザー フォーム デザイナーを 1 つのワークブックから別のワークブックにシームレスにコピーする方法について詳しく説明します。熟練した開発者でも、初心者でも、重要な手順をすべて順を追って説明します。これは、Excel ファイルをプログラムで処理する技術を習得するためのプレイブックとしてご利用ください。準備はできましたか? さあ、始めましょう!
## 前提条件
コーディングの詳細に入る前に、必要なものがすべて揃っていることを確認しましょう。
1. C# 開発環境: C# 開発用の作業環境を準備しておく必要があります。Visual Studio を強くお勧めします。
2.  Aspose.Cells for .NET ライブラリ: Aspose.Cells ライブラリがプロジェクトに統合されていることを確認してください。[ここからダウンロード](https://releases.aspose.com/cells/net/).
3. VBA と Excel マクロの基礎知識: VBA と Excel マクロの仕組みをよく理解しておくと、このチュートリアルを簡単に進めることができます。
4. ユーザーフォームを含むExcelファイル: ユーザーフォームを含むExcelブックを試用、作成、または入手するには、マクロが有効になっていることが望ましいです（例：`.xlsm`ファイル)。
## パッケージのインポート
C# プロジェクトでは、Aspose.Cells 機能を利用するために、ファイルの先頭に特定の名前空間をインポートする必要があります。手順は次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
これらの名前空間を含めると、Aspose.Cells ライブラリ内に埋め込まれたすべての強力なツールにアクセスできるようになります。 
前提条件とパッケージが揃ったので、次は楽しい部分であるコーディングに移りましょう。ステップごとに説明しましょう。
## ステップ1: ソースディレクトリと出力ディレクトリを定義する
まず、ファイルがどこに保存されているかを確認する必要があります。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
ここで、`"Your Document Directory"`ファイルが保存されている実際のパスを入力します。ここからソース ワークブック (UserForm を含む) が取得され、新しいワークブックが保存されます。
## ステップ2: 空のターゲットワークブックを作成する
次に、ユーザー フォームとマクロをコピーするターゲット ワークブックを作成しましょう。
```csharp
//空のターゲット ワークブックを作成する
Workbook target = new Workbook();
```
このコード行は、データを入力するための新しい空のワークブックを初期化します。傑作を描くための空白のキャンバスと考えてください。
## ステップ3: テンプレートワークブックを読み込む
ユーザー フォームとマクロを含むワークブックを読み込む必要があります。
```csharp
// VBAマクロデザイナーユーザーフォームを含むExcelファイルを読み込みます。
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
必ず変更してください`"sampleDesignerForm.xlsm"`実際のファイル名に置き換えてください。このワークブックはレシピブックのようなもので、ここから材料を取り出すことになります。
## ステップ4: ワークシートをターゲットワークブックにコピーする
それでは、テンプレートから対象のワークブックにワークシートをコピーしてみましょう。
```csharp
//すべてのテンプレート ワークシートをターゲット ワークブックにコピーします
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        //対象ワークシートのセルA2にメッセージを入力します
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
この手順では、テンプレート内の各ワークシートをループし、それらをターゲットのワークブックにコピーします。考えてみると、これは最高のレシピをある料理本から別の料理本に移すようなものです。
## ステップ5: テンプレートからVBAマクロをコピーする
次に、UserForm Designer モジュールを含む VBA マクロを新しいブックにコピーします。
```csharp
// VBAマクロデザイナーのユーザーフォームをテンプレートからターゲットにコピーする
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        //ThisWorkbook モジュール コードをコピーする
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        //他のモジュールのコードとデータをコピーする
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            //ユーザーフォーム（デザイナーストレージ）のデータを取得します
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            //ターゲット Vba プロジェクトにデザイナー ストレージを追加する
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
この膨大なコード チャンクは、テンプレート ファイル内の各 VBA モジュールのチェックを処理します。UserForm デザインとそれに関連するコードをコピーします。これは、おばあちゃんの有名なパイのレシピだけでなく、おばあちゃんの正確な焼き方まで確実に入手できるようなものです。
## ステップ6: ターゲットワークブックを保存する
すべてのコピーが完了したら、苦労して作成したデータを保存します。
```csharp
//対象のワークブックを保存する
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
出力ファイル名は必要に応じて変更してください。保存すると、マクロやユーザー フォームが満載の、自分専用のワークブック バージョンが効果的に作成されます。これはとてもエキサイティングなことではないでしょうか。
## ステップ7: 成功を確認する
最後に、コンソールに成功メッセージを出力します。
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
この小さな行は、プロセスがスムーズに進んだことを保証します。コーディングサンデーの一番上のチェリーのようなものです。
## 結論
おめでとうございます! Aspose.Cells for .NET を使用して、VBA マクロ ユーザー フォーム デザイナーを 1 つのワークブックから別のワークブックにコピーする手順ガイドを完了しました。最初は少し大変に思えるかもしれませんが、練習すればプロのようにワークブックの操作を扱えるようになります。コーディングは練習がすべてです。Excel ファイルでさまざまなことを試してみることをためらわないでください。質問がある場合や問題が発生した場合は、Aspose フォーラムまたはドキュメントでサポートを受けてください。
## よくある質問
### Aspose.Cells はどのバージョンの Excel をサポートしていますか?
Aspose.Cells は、XLSX、XLSM、CSV など、幅広い Excel 形式をサポートしています。
### Aspose.Cells を無料で使用できますか?
はい！無料トライアルから始めて、ライブラリを評価することができます。[無料トライアル](https://releases.aspose.com/).
### このコードを実行するには Visual Studio が必要ですか?
ユーザーフレンドリーな機能を備えているため強く推奨されますが、.NET 開発をサポートしていれば、どの C# IDE でも問題ありません。
### その他の例やドキュメントはどこで見つかりますか?
探索することができます[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)より多くの例と詳細な説明については、こちらをご覧ください。
### Aspose.Cells の使用中に発生した問題を解決するにはどうすればよいですか?
ぜひ訪れてみてください[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9)コミュニティと Aspose サポート スタッフからのサポートを受けてください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
