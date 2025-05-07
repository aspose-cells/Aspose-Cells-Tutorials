---
"date": "2025-04-08"
"description": "了解如何使用 Aspose.Cells for Java 有效地向 Excel 工作表中填入巢狀資料。本指南涵蓋設定工作簿、實作智慧標記和處理複雜資料集。"
"title": "使用 Aspose.Cells for Java 為 Excel 填入巢狀資料綜合指南"
"url": "/zh-hant/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for Java 向 Excel 填入巢狀數據

## 介紹

在 Excel 中有效管理巢狀資料結構可能具有挑戰性。 **Aspose.Cells for Java** 提供了一個強大的解決方案，可以使用智慧標記動態填充 Excel 工作簿。本教學將引導您完成整個過程，確保您可以輕鬆處理個人及其家庭成員等複雜資料集。

透過遵循本指南，您將學習如何：
- 設定新的工作簿和工作表。
- 實施智慧標記以實現高效的資料填充。
- 在 Java 中建立巢狀物件結構以獲得全面的資料集。
- 使用 Aspose.Cells 的 WorkbookDesigner 類別處理工作簿。

在深入實施之前，讓我們確保您的環境已正確設定並具備所有必要的先決條件。

## 先決條件

在繼續之前，請確保您已：
- **Java 開發工具包 (JDK)**：確保您的系統上安裝了 JDK 8 或更高版本。
- **Aspose.Cells for Java**：使用 Maven 或 Gradle 將 Aspose.Cells 庫新增到您的專案中，如下所述。
- **開發環境**：使用文字編輯器或 IDE，如 IntelliJ IDEA、Eclipse 或 NetBeans。

### 所需的庫和依賴項

要將 Aspose.Cells 包含到您的專案中：

**Maven：**
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradle：**
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### 許可證獲取

要使用 Aspose.Cells，您可以：
- **免費試用**：下載庫並從臨時評估許可證開始。
- **購買**：獲得用於生產的完整許可證。

訪問 [Aspose 購買](https://purchase.aspose.com/buy) 了解有關獲取許可證的更多資訊。如需免費試用，請訪問 [Aspose 版本](https://releases。aspose.com/cells/java/).

## 設定 Aspose.Cells for Java

首先按照先決條件部分中的說明將 Aspose.Cells 依賴項新增至您的專案中。一旦包含了該庫，請在 Java 應用程式中對其進行初始化。

以下是基本設定：
```java
import com.aspose.cells.Workbook;

public class AsposeCellsSetup {
    public static void main(String[] args) {
        // 初始化一個新的 Workbook 物件。
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java is set up and ready to use!");
    }
}
```

此程式碼片段示範了開始使用 Aspose.Cells 是多麼簡單。在執行任何進一步的程式碼之前，請確保您的環境能夠識別該程式庫。

## 實施指南

讓我們將實作分解為易於管理的部分，每個部分都專注於 Aspose.Cells for Java 的特定功能。

### 使用初始資料設定工作簿

#### 概述

本節涉及初始化新工作簿並使用智慧標記在第一個工作表中設定初始標題。

**實施步驟：**
1. **初始化工作簿和工作表**：
   - 建立一個實例 `Workbook`。
   - 從工作簿存取第一個工作表。
2. **設定列標題**：
   - 定義 A、B、C 和 D 列的標題。
3. **實施智能標記**：
   - 使用智慧標記來準備資料佔位符。

**程式碼實作：**
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class InitializeWorkbook {
    public static void main(String[] args) throws Exception {
        // 初始化一個新的工作簿並取得第一個工作表。
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 設定 A、B、C 和 D 列的標題。
        worksheet.getCells().get("A1").putValue("Person Name");
        worksheet.getCells().get("B1").putValue("Person Age");
        worksheet.getCells().get("C1").putValue("Wife Name");
        worksheet.getCells().get("D1").putValue("Wife Age");

        // 為資料填充設定智慧標記。
        worksheet.getCells().get("A2").putValue("&=Individual.Name");
        worksheet.getCells().get("B2").putValue("&=Individual.Age");
        worksheet.getCells().get("C2").putValue("&=Individual.Wife.Name");
        worksheet.getCells().get("D2").putValue("&=Individual.Wife.Age");

        // 用於保存工作簿的佔位符路徑。
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        workbook.save(outDir + "/UsingNestedObjects-out.xlsx");
    }
}
```

### 為資料來源建立嵌套物件列表

#### 概述

此步驟涉及建立 Java 類別來表示巢狀資料結構，這些類別將用作 Excel 工作簿中的資料來源。

**實施步驟：**
1. **定義類別結構**：
   - 創造 `Individual` 和 `Person` 課程。
   - 包括必要的字段和建構函數。
2. **建立資料列表**：
   - 實例化物件 `Individual`，每個都包含一個嵌套的 `Person`。

**程式碼實作：**
```java
import java.util.ArrayList;

// 為個人和人員定義類別結構。
class Individual {
    String name;
    int age;
    Person wife;

    public Individual(String name, int age, Person wife) {
        this.name = name;
        this.age = age;
        this.wife = wife;
    }
}

class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// 建立帶有嵌套妻子詳細資料的個人物件清單。
public class CreateDataList {
    public static void main(String[] args) {
        ArrayList<Individual> individuals = new ArrayList<>();
        individuals.add(new Individual("John", 23, new Person("Jill", 20)));
        individuals.add(new Individual("Jack", 25, new Person("Hilly", 21)));
        individuals.add(new Individual("James", 26, new Person("Hally", 22)));
        individuals.add(new Individual("Baptist", 27, new Person("Newly", 23)));

        System.out.println("Data list created successfully!");
    }
}
```

### 使用智慧標記和資料來源處理工作簿

#### 概述

在這裡，你將會利用 `WorkbookDesigner` 使用智慧標記和資料來源處理您的工作簿。

**實施步驟：**
1. **初始化 WorkbookDesigner**：
   - 建立一個實例 `WorkbookDesigner`。
2. **分配資料來源**：
   - 將個人清單設定為處理智慧標記的資料來源。
3. **處理工作簿**：
   - 使用 `process` 方法用巢狀資料填入工作簿。

**程式碼實作：**
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookDesigner;

public class ProcessWorkbook {
    public static void main(String[] args) throws Exception {
        // 設定一個WorkbookDesigner來處理工作簿。
        Workbook workbook = new Workbook("YOUR_OUTPUT_DIRECTORY/UsingNestedObjects-out.xlsx");
        WorkbookDesigner designer = new WorkbookDesigner();
        designer.setWorkbook(workbook);

        // 假設「個人」已根據前面的步驟填充
        ArrayList<Individual> individuals = new ArrayList<>();
        individuals.add(new Individual("John", 23, new Person("Jill", 20)));
        individuals.add(new Individual("Jack", 25, new Person("Hilly", 21)));
        individuals.add(new Individual("James", 26, new Person("Hally", 22)));
        individuals.add(new Individual("Baptist", 27, new Person("Newly", 23)));

        // 將個人清單指定為智慧標記的資料來源。
        designer.setDataSource("Individual", individuals);

        // 使用帶有智慧標記的設定資料來源來處理工作簿。
        designer.process();

        // 將處理後的工作簿儲存到文件中。
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        workbook.save(outDir + "/PopulatedUsingNestedObjects.xlsx");
    }
}
```

## 結論

透過遵循本指南，您將學習如何使用 Aspose.Cells for Java 有效地管理和填入包含巢狀資料的 Excel 工作簿。這種方法不僅簡化了複雜資料集的處理，而且還增強了資料管理流程的靈活性。

為了進一步探索，請考慮深入研究 Aspose.Cells 的更多進階功能或嘗試不同類型的資料結構。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}