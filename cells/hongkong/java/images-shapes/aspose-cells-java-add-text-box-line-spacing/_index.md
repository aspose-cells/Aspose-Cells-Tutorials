---
"date": "2025-04-08"
"description": "了解如何使用 Aspose.Cells for Java 在 Excel 工作簿中新增文字方塊和設定行距。使用樣式化的文字形狀增強您的工作簿簡報。"
"title": "使用 Aspose.Cells for Java 在 Excel 中新增文字方塊並設定行距"
"url": "/zh-hant/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for Java 在 Excel 中新增文字方塊並設定行距

## 介紹

建立動態 Excel 報表通常需要自訂文字格式，例如新增具有特定行距的文字方塊。使用 Aspose.Cells for Java，這一切變得簡單又有效率。本教學將指導您使用 Aspose.Cells for Java 新增樣式文字形狀來增強您的工作簿簡報。

在本指南結束時，您將學習如何：
- 建立新的 Excel 工作簿並存取其工作表
- 在工作表中新增文字方塊形狀
- 設定文字形狀內的自訂行距
- 將格式化的工作簿儲存為 XLSX 格式

讓我們從設定您的環境開始。

### 先決條件

在開始之前，請確保您已準備好以下內容：
- 您的機器上安裝了 Java 開發工具包 (JDK)
- 用於編寫 Java 程式碼的 IDE 或編輯器
- 配置 Maven 或 Gradle 建置系統來管理依賴項

對 Java 程式設計有基本的了解並熟悉 Excel 文件結構將會很有幫助。

## 設定 Aspose.Cells for Java

使用 Maven 或 Gradle 將 Aspose.Cells 納入專案的依賴管理：

**Maven**

將以下依賴區塊新增到您的 `pom.xml` 文件：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

將其包含在您的 `build.gradle` 文件：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

接下來，透過選擇免費試用、申請臨時許可證或購買完整許可證來取得 Aspose.Cells 的許可證。

### 初始化 Aspose.Cells

一旦該庫包含在您的專案中，請在您的 Java 應用程式中對其進行初始化：

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // 初始化 Workbook 實例（代表一個 Excel 檔案）
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## 實施指南

### 建立工作簿和 Access 工作表

首先建立一個新的 Excel 工作簿並存取其第一個工作表。您可以在此處新增文字方塊。

#### 概述

建立新工作簿可提供一個空白區域，以便根據需要新增資料、形狀和格式。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // 建立新工作簿（Excel 檔案）
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### 將文字方塊新增至工作表

接下來，為您選擇的工作表新增一個文字方塊形狀。此形狀可以包含您需要的任何文字內容。

#### 概述

文字方塊是一種多功能工具，可直接在 Excel 工作表中包含自訂文字（例如註解或說明）。

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // 建立新工作簿（Excel 檔案）
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 在工作表中新增文字方塊形狀
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### 在形狀中設定文本

文字方塊準備好後，設定其內容並格式化其中的文字。

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // 建立新工作簿（Excel 檔案）
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 在工作表中新增文字方塊形狀
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 設定形狀內的文字內容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### 訪問形狀中的文字段落

您可以存取文字方塊中的各個段落以套用特定的格式。

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // 建立新工作簿（Excel 檔案）
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 在工作表中新增文字方塊形狀
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 設定形狀內的文字內容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 訪問形狀中的第二段
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### 設定段落行距

自訂行距可以增強可讀性。設定方法如下：

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 建立新工作簿（Excel 檔案）
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 在工作表中新增文字方塊形狀
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 設定形狀內的文字內容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 訪問形狀中的第二段
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 將行距設定為 20 點
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 配置段落前後的間距
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### 儲存工作簿

最後，使用新新增和格式化的文字方塊儲存您的工作簿。

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // 建立新工作簿（Excel 檔案）
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // 在工作表中新增文字方塊形狀
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // 設定形狀內的文字內容
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // 訪問形狀中的第二段
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // 將行距設定為 20 點
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // 配置段落前後的間距
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // 儲存工作簿
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## 結論

您已成功學習如何使用 Aspose.Cells for Java 在 Excel 工作簿中新增文字方塊和設定行距。這增強了您建立動態、視覺吸引力強的報告的能力。

## 關鍵字推薦
- “ Java 的 Aspose.Cells”
- “在 Excel 中新增文字方塊”
- “在 Excel 中設定行距”
- “帶有樣式文字的 Excel 工作簿”
- “Java 和 Aspose.Cells”


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}