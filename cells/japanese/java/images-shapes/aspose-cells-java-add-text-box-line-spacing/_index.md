---
"date": "2025-04-08"
"description": "Aspose.Cells for Java を使用して、Excel ブックにテキストボックスを追加し、行間を設定する方法を学びます。スタイル設定されたテキスト図形を使用して、ブックのプレゼンテーションを強化します。"
"title": "Aspose.Cells for Java を使用して Excel にテキスト ボックスを追加し、行間隔を設定する"
"url": "/ja/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells for Java を使用して Excel にテキスト ボックスを追加し、行間隔を設定する

## 導入

動的なExcelレポートを作成するには、特定の行間隔でテキストボックスを追加するなど、テキストの書式設定をカスタマイズする必要があることがよくあります。Aspose.Cells for Javaを使えば、こうした作業が簡単かつ効率的に行えます。このチュートリアルでは、Aspose.Cells for Javaを使用してスタイル付きテキストシェイプを追加し、ワークブックのプレゼンテーションを強化する方法を説明します。

このガイドを読み終えると、次の方法を学習できます。
- 新しい Excel ブックを作成し、そのワークシートにアクセスする
- ワークシートにテキストボックス図形を追加する
- テキスト図形内の行間隔をカスタマイズする
- フォーマットされたワークブックをXLSX形式で保存します

まずは環境の設定から始めましょう。

### 前提条件

始める前に、次のものがあることを確認してください。
- マシンにJava開発キット（JDK）がインストールされている
- Javaコードを書くためのIDEまたはエディタ
- 依存関係を管理するように構成されたMavenまたはGradleビルドシステム

Java プログラミングの基本的な理解と Excel ファイル構造の知識があると役立ちます。

## Aspose.Cells for Java のセットアップ

Maven または Gradle を使用して、プロジェクトの依存関係管理に Aspose.Cells を含めます。

**メイヴン**

次の依存関係ブロックを `pom.xml` ファイル：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**グラドル**

これをあなたの `build.gradle` ファイル：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

次に、無料トライアルを選択するか、一時ライセンスを要求するか、フルライセンスを購入して、Aspose.Cells のライセンスを取得します。

### Aspose.Cells の初期化

ライブラリをプロジェクトに組み込んだら、Java アプリケーション内で初期化します。

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Workbook のインスタンスを初期化します (Excel ファイルを表します)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## 実装ガイド

### ワークブックとアクセスワークシートを作成する

まず、新しいExcelブックを作成し、最初のワークシートにアクセスします。ここにテキストボックスを追加します。

#### 概要

新しいブックを作成すると、必要に応じてデータ、図形、書式を追加するための空白の状態が提供されます。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // 新しいワークブック（Excelファイル）を作成する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### ワークシートにテキストボックスを追加する

次に、選択したワークシートにテキストボックス図形を追加します。この図形には、必要なテキストコンテンツをすべて含めることができます。

#### 概要

テキスト ボックスは、メモや指示などのカスタム テキストを Excel シート内に直接含めることができる多目的ツールです。

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // 新しいワークブック（Excelファイル）を作成する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // ワークシートにテキストボックス図形を追加する
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### 図形内にテキストを設定する

テキスト ボックスが準備できたら、その内容を設定し、その中のテキストの書式を設定します。

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // 新しいワークブック（Excelファイル）を作成する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // ワークシートにテキストボックス図形を追加する
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 図形内にテキストコンテンツを設定する
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### 図形内のテキスト段落にアクセス

テキスト ボックス内の個々の段落にアクセスして、特定の書式を適用できます。

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // 新しいワークブック（Excelファイル）を作成する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // ワークシートにテキストボックス図形を追加する
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 図形内にテキストコンテンツを設定する
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 図形の2番目の段落にアクセスする
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### 段落の行間隔を設定する

行間隔をカスタマイズすると読みやすさが向上します。設定方法は次のとおりです。

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 新しいワークブック（Excelファイル）を作成する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // ワークシートにテキストボックス図形を追加する
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 図形内にテキストコンテンツを設定する
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 図形の2番目の段落にアクセスする
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 行間隔を20ポイントに設定する
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 段落の前後のスペースを設定する
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### ワークブックを保存

最後に、新しく追加されフォーマットされたテキスト ボックスを含むブックを保存します。

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 新しいワークブック（Excelファイル）を作成する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // ワークシートにテキストボックス図形を追加する
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 図形内にテキストコンテンツを設定する
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 図形の2番目の段落にアクセスする
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 行間隔を20ポイントに設定する
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 段落の前後のスペースを設定する
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // ワークブックを保存する
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## 結論

Aspose.Cells for Javaを使用して、Excelブックにテキストボックスを追加し、行間を設定する方法を学習しました。これにより、動的で視覚的に魅力的なレポートを作成できるようになります。

## キーワードの推奨事項
- 「Aspose.Cells for Java」
- 「Excelにテキストボックスを追加する」
- 「Excelで行間隔を設定する」
- 「スタイル付きテキストを含む Excel ワークブック」
- 「Java と Aspose.Cells」


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}