---
"date": "2025-04-08"
"description": "了解如何使用 Aspose.Cells for Java 有效地管理和提取嵌入在 Excel 檔案中的 OLE 物件。請按照本逐步指南實現無縫整合。"
"title": "使用 Aspose.Cells Java 從 Excel 中提取並保存 OLE 物件&#58;完整指南"
"url": "/zh-hant/java/ole-objects-embedded-content/aspose-cells-java-extract-save-ole-objects/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells Java 從 Excel 中提取並保存 OLE 物件：完整指南

## 介紹

管理 Excel 檔案中嵌入的 OLE（物件連結和嵌入）物件對於軟體開發人員和資料分析師來說是一項至關重要的任務。本教學提供了使用 Aspose.Cells for Java 有效提取和保存這些物件的全面指南，透過多種檔案格式簡化您的工作流程。

**您將學到什麼：**
- 使用 Aspose.Cells 初始化 Excel 工作簿
- 從工作表中提取 OLE 對象
- 以各種格式儲存擷取的檔案（DOCX、XLSX、PPTX、PDF）
- 處理特殊情況，例如儲存為新的 Excel 文件

在本指南結束時，您將能夠使用強大的資料處理功能來增強您的 Java 應用程式。

## 先決條件

在繼續之前，請確保您已：

**所需庫：**
- Aspose.Cells for Java（版本 25.3 或更高版本）
- 與適合運行 Aspose.Cells 的 JDK 版本相容

**環境設定要求：**
- 對 Java 和 Maven/Gradle 建置工具有基本的了解
- 整合開發環境 (IDE)，例如 IntelliJ IDEA 或 Eclipse

**知識前提：**
- 熟悉 Java 中的檔案處理
- 了解 Excel 中的 OLE 對象

## 設定 Aspose.Cells for Java

首先，使用以下配置將 Aspose.Cells 包含在您的專案中：

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 許可證獲取

Aspose.Cells提供多種授權選項：
- **免費試用**：下載試用版來測試功能。
- **臨時執照**：取得擴展評估許可證。
- **購買**：取得用於生產的永久許可證。

訪問 [購買頁面](https://purchase.aspose.com/buy) 或請求 [臨時執照](https://purchase.aspose.com/temporary-license/) 根據您的需要。

### 基本初始化

以下是在 Java 應用程式中初始化 Aspose.Cells 的方法：
```java
import com.aspose.cells.Workbook;

public class InitializeWorkbook {
    public static void main(String[] args) {
        Workbook workbook = new Workbook("path/to/excel/file.xlsx");
        // 根據需要繼續使用工作簿對象
    }
}
```

## 實施指南

### 功能1：從Excel中提取OLE對象

**概述：** 初始化工作簿並從第一個工作表中提取嵌入的物件。

#### 步驟 1：初始化工作簿
設定資料目錄路徑並建立 `Workbook` 實例：
```java
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/oleFile.xlsx");
```

#### 步驟2：提取OLE對象
存取第一個工作表中的 OLE 物件集合：
```java
import com.aspose.cells.OleObjectCollection;

OleObjectCollection oleObjects = workbook.getWorksheets().get(0).getOleObjects();
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    // 在這裡處理每個對象
}
```

#### 步驟3：保存提取的對象
根據文件類型保存每個提取的 OLE 物件：
```java
import com.aspose.cells.FileFormatType;
import java.io.FileOutputStream;

String outDir = "YOUR_OUTPUT_DIRECTORY";
for (int i = 0; i < oleObjects.getCount(); i++) {
    OleObject object = oleObjects.get(i);
    String fileName = outDir + "/object" + i + ".";

    switch (object.getFileFormatType()) {
        case FileFormatType.DOCX:
            fileName += "docx";
            break;
        case FileFormatType.XLSX:
            fileName += "xlsx";
            break;
        // 根據需要新增其他格式
    }

    if (object.getFileFormatType() == FileFormatType.XLSX) {
        byte[] bytes = object.getObjectData();
        Workbook oleBook = new Workbook(new java.io.ByteArrayInputStream(bytes));
        oleBook.getSettings().setHidden(false);
        oleBook.save(fileName);
    } else {
        try (FileOutputStream fos = new FileOutputStream(fileName)) {
            fos.write(object.getObjectData());
        }
    }
}
```

### 功能 2：將 OLE 物件儲存為 Excel 文件
**概述：** 示範如何將擷取的 OLE 物件具體儲存為 Excel 檔案。

#### 步驟 1：檢索 OLE 數據
假設你有 `byte[] bytes` 來自 `OleObject`：
```java
import com.aspose.cells.Workbook;
import java.io.ByteArrayInputStream;

Workbook oleBook = new Workbook(new ByteArrayInputStream(bytes));
oleBook.getSettings().setHidden(false);
oleBook.save("YOUR_OUTPUT_DIRECTORY/object.xlsx");
```

## 實際應用

- **數據整合：** 從Excel中提取各種文件類型並集中儲存。
- **自動報告產生：** 直接從您的應用程式整合並儲存不同格式的報告。
- **資料遷移工具：** 使用擷取的資料進行系統之間的遷移過程。

## 性能考慮

- 透過有效管理大物件（可能透過串流方法）來優化記憶體使用量。
- 利用 Aspose.Cells 的設定來動態管理工作簿的可見度和大小。
- 實施有效的文件處理實務以防止資源洩漏。

## 結論

透過遵循本指南，您可以使用 Aspose.Cells for Java 有效地提取和保存 OLE 物件。這些功能顯著增強了您的資料管理流程。

**後續步驟：**
考慮探索 Aspose.Cells 的其他功能，如圖表操作或進階 Excel 檔案轉換，以進一步擴展您的 Java 應用程式。

## 常見問題部分

1. **如何處理不支援的 OLE 物件格式？**
   - 對於未知物件使用預設格式（如 JPG）。
2. **我可以從多張表中提取 OLE 物件嗎？**
   - 是的，遍歷工作簿中的每個工作表並重複提取過程。
3. **如果 OLE 物件無法正確保存怎麼辦？**
   - 檢查檔案權限並確保輸出目錄路徑正確。
4. **Aspose.Cells 是否支援所有 Excel 版本？**
   - Aspose.Cells 支援多種 Excel 格式，包括 XLS 等傳統格式。
5. **處理大檔案時如何優化效能？**
   - 考慮分塊處理或使用檔案流技術來有效管理記憶體使用情況。

## 資源
- [文件](https://reference.aspose.com/cells/java/)
- [下載 Aspose.Cells](https://releases.aspose.com/cells/java/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用版下載](https://releases.aspose.com/cells/java/)
- [臨時許可證申請](https://purchase.aspose.com/temporary-license/)
- [社群支援論壇](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}