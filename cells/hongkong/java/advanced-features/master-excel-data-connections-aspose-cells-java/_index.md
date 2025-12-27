---
date: '2025-12-27'
description: 學習如何使用 Aspose.Cells for Java 程式化更改 Excel 資料來源、修改 Excel 資料連接，並自動化您的工作流程。
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: 如何使用 Aspose.Cells for Java 更改 Excel 資料來源
url: /zh-hant/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 更改 Excel 資料來源

## 簡介
在程式中**更改 Excel 資料來源**及修改 Excel 檔案內的資料連接時感到困難嗎？本完整指南專為希望使用強大的 **Aspose.Cells for Java** 函式庫自動化報表流程的開發人員而設。我們將一步步示範如何載入 Excel 活頁簿、更新其外部連接，並儲存變更——全部使用 Java 程式碼。

### 您將學會
- 如何在 Maven 或 Gradle 中設定 Aspose.Cells for Java。  
- **Load Excel workbook Java** – 將現有檔案讀取至記憶體。  
- **Modify Excel data connections** – 更新連接名稱、ODC 路徑與 SQL 指令。  
- **Save Excel workbook Java** – 將更新後的活頁簿寫回磁碟。  

在深入之前，先確保您已備妥所有必需的項目。

## 快速問答
- **主要的函式庫是什麼？** Aspose.Cells for Java。  
- **哪個方法載入活頁簿？** `new Workbook(filePath)`。  
- **如何更新連接字串？** 使用 `DBConnection.setConnectionInfo(...)`。  
- **可以更改 ODC 檔案路徑嗎？** 可以，透過 `ExternalConnection.setOdcFile(...)`。  
- **正式環境需要授權嗎？** 商業授權可移除評估限制。

## 先決條件
開始之前，請確認您具備以下項目：

### 必要函式庫
Aspose.Cells for Java 版本 25.3 或更新版本提供本教學所使用的 API。

### 環境設定
- 已安裝 Java Development Kit (JDK)。  
- 使用 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。

### 知識先備
熟悉 Java、Maven 或 Gradle，以及基本的 SQL 概念，將有助於您順利跟隨本教學。

## 設定 Aspose.Cells for Java
要開始使用 Aspose.Cells，請將函式庫加入您的專案中：

**Maven Setup**  
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle Setup**  
Insert the following line into `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 授權取得步驟
Aspose.Cells 提供免費試用，讓您在購買前評估此函式庫：

- 前往[免費試用頁面](https://releases.aspose.com/cells/java/)下載評估套件。  
- 如需完整功能，請於[購買入口](https://purchase.aspose.com/buy)購買授權。  
- 需要臨時存取嗎？請申請[臨時授權](https://purchase.aspose.com/temporary-license/)。  

完成函式庫引用與授權後，即可開始撰寫程式。

## 實作指南

### 功能 1：從檔案載入活頁簿
**此步驟的作用是什麼？** 它示範如何 **load Excel workbook Java**，讓您能操作其資料連接。

#### Step‑by‑Step Instructions
**Define Your Data Directory** – tell the program where the source file lives:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
請確保該資料夾中有 `DataConnection.xlsx`。

**Load the Workbook** – instantiate the `Workbook` object:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
`Workbook` 實例現在在記憶體中代表您的 Excel 檔案。

### 功能 2：修改活頁簿中的資料連接
**為何要修改？** 更新外部連接可讓您 **change Excel data source**，而無需手動開啟檔案。

#### Step‑by‑Step Instructions
**Access the Data Connection** – retrieve the first connection (you can loop for multiple connections):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()` 會回傳所有連接的集合，讓您能逐一 **modify excel data connections**。

**Modify Connection Properties** – change name, ODC file, command type, and SQL statement:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

Cast to `DBConnection` for database‑specific settings:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
在此您 **update excel external connection** 細節，例如 SQL 查詢與連接字串。

### 功能 3：將活頁簿儲存至檔案
**接下來會發生什麼？** 更新連接後，您需要 **save Excel workbook Java**，以確保變更永久保存。

#### Step‑by‑Step Instructions
**Define Output Directory** – where the modified file will be written:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**Save the Workbook** – write the workbook back to disk:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
`save()` 方法完成 **change excel data source** 的操作。

## 實務應用
以程式方式修改 Excel 資料連接可開啟許多可能：

1. **自動化報告** – 產生永遠從資料庫抓取最新資料的報告。  
2. **資料同步** – 讓活頁簿與即時系統保持同步，無需手動重新整理。  
3. **動態儀表板** – 建立即時反映指標的儀表板。  

將 Aspose.Cells 與 CRM、ERP 或 BI 平台整合，可大幅減少人工工作量。

## 效能考量
處理大型活頁簿或龐大結果集時：

- 分批處理資料，以避免記憶體激增。  
- 優化 SQL 查詢以提升速度。  
- 及時釋放資源；若不再需要物件，請呼叫 `workbook.dispose()`。  

這些做法可確保您的應用程式在 **changing Excel data source** 時保持回應。

## 結論
您現在已學會透過載入活頁簿、**modify excel data connections**，以及使用 **Aspose.Cells for Java** 儲存更新後的檔案，來 **change Excel data source**。此功能讓您能自動化資料驅動的工作流程，並使 Excel 檔案與外部系統保持同步。

### 下一步
- 嘗試使用迴圈遍歷 `workbook.getDataConnections()` 以處理多個連接。  
- 探索其他 Aspose.Cells 功能，例如圖表產生、儲存格樣式設定與樞紐分析表操作。  

準備好提升自動化了嗎？立即實作這些程式碼片段，見證您的生產力飛躍！

## 常見問題

**Q1: How do I handle multiple data connections in a workbook?**  
A1: 使用迴圈內的 `workbook.getDataConnections().get(index)` 逐一存取每個連接。

**Q2: Can I modify other properties of an Excel file using Aspose.Cells Java?**  
A2: 當然可以！Aspose.Cells 支援儲存格格式設定、工作表管理圖表建立等多種功能。

**Q3: What if my SQL command fails to execute?**  
A3: 請確認連接字串、檢查資料庫權限，並檢視例外資訊以找出原因。

**Q4: Where can I get support for Aspose.Cells issues?**  
A4: 前往 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 提問或瀏覽現有解決方案。

**Q5: Are there limitations in the free trial version?**  
A5: 評估版會加入浮水印，且可能限制處理容量。購買授權即可無限制使用。

## 資源
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.Cells Java 25.3  
**Author:** Aspose