---
title: 資料驗證中的輸入訊息
linktitle: 資料驗證中的輸入訊息
second_title: Aspose.Cells Java Excel 處理 API
description: 了解如何使用 Aspose.Cells for Java 增強 Excel 中的資料驗證。包含程式碼範例的逐步指南，可提高資料準確性和使用者指導。
weight: 18
url: /zh-hant/java/data-validation-rules/input-message-in-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 資料驗證中的輸入訊息


## 資料驗證簡介

資料驗證是 Excel 中的一項功能，它透過限制可以輸入儲存格的資料類型來幫助保持資料的準確性和一致性。它確保用戶輸入有效訊息，減少錯誤並提高數據品質。

## 什麼是 Java 版 Aspose.Cells？

Aspose.Cells for Java 是一個基於 Java 的 API，使開發人員能夠建立、操作和管理 Excel 電子表格，而無需 Microsoft Excel。它提供了以程式設計方式處理 Excel 檔案的廣泛功能，使其成為 Java 開發人員的寶貴工具。

## 設定您的開發環境

在開始之前，請確保您的系統上已設定 Java 開發環境。您可以使用您最喜歡的 IDE（例如 Eclipse 或 IntelliJ IDEA）來建立新的 Java 專案。

## 建立一個新的 Java 項目

首先在您選擇的 IDE 中建立一個新的 Java 專案。為其指定一個有意義的名稱，例如「DataValidationDemo」。

## 將 Aspose.Cells for Java 加入您的專案中

要在專案中使用 Aspose.Cells for Java，您需要新增 Aspose.Cells 函式庫。您可以從網站下載該庫並將其新增至專案的類路徑。

## 將資料驗證新增至工作表

現在您已經設定了項目，讓我們開始在工作表上新增資料驗證。首先，建立一個新的 Excel 工作簿和一個工作表。

```java
//建立新工作簿
Workbook workbook = new Workbook();
//訪問第一個工作表
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 定義驗證標準

您可以定義驗證標準來限制可以輸入儲存格的資料類型。例如，您只能允許 1 到 100 之間的整數。

```java
//定義資料驗證標準
DataValidation validation = worksheet.getValidations().addDataValidation("A1");
validation.setType(DataValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("1");
validation.setFormula2("100");
```

## 用於資料驗證的輸入訊息

輸入訊息為使用者提供有關應輸入的資料類型的指導。您可以使用 Aspose.Cells for Java 將輸入訊息新增至資料驗證規則。

```java
//設定資料驗證的輸入訊息
validation.setInputMessage("Please enter a number between 1 and 100.");
```

## 數據驗證錯誤警報

除了輸入訊息之外，您還可以設定錯誤警報，以便在使用者輸入無效資料時通知使用者。

```java
//設定資料驗證錯誤警報
validation.setShowError(true);
validation.setErrorTitle("Invalid Data");
validation.setErrorMessage("Please enter a valid number between 1 and 100.");
```

## 將資料驗證應用於單元格

現在您已經定義了資料驗證規則，您可以將它們套用到工作表中的特定儲存格。

```java
//將資料驗證應用於一系列單元格
CellArea area = new CellArea();
area.startRow = 0;
area.endRow = 9;
area.startColumn = 0;
area.endColumn = 0;
validation.addArea(area);
```

## 使用不同的資料類型

Aspose.Cells for Java 可讓您使用各種資料類型進行資料驗證，包括整數、小數、日期和文字。

```java
//將資料驗證類型設定為十進位
validation.setType(DataValidationType.DECIMAL);
```

## 自訂資料驗證訊息

您可以自訂輸入訊息和錯誤警報，以便為使用者提供具體的說明和指導。

```java
//自訂輸入訊息和錯誤訊息
validation.setInputMessage("Please enter a decimal number.");
validation.setErrorMessage("Invalid input. Please enter a valid decimal number.");
```

## 驗證日期條目

資料驗證也可用於確保日期條目處於特定範圍或格式內。

```java
//將資料驗證類型設定為日期
validation.setType(DataValidationType.DATE);
```

## 先進的數據驗證技術

Aspose.Cells for Java 提供了先進的資料驗證技術，例如自訂公式和級聯驗證。

## 結論

在本文中，我們探討如何使用 Aspose.Cells for Java 將輸入訊息新增至資料驗證規則。資料驗證是保持 Excel 中資料準確性的一個重要方面，Aspose.Cells 讓您可以在 Java 應用程式中輕鬆實現和自訂這些規則。透過遵循本指南中概述的步驟，您可以增強 Excel 工作簿的可用性和資料品質。

## 常見問題解答

### 如何一次向多個儲存格新增資料驗證？

若要將資料驗證新增至多個儲存格，您可以定義儲存格範圍並將驗證規則套用至該範圍。 Aspose.Cells for Java 可讓您使用下列指令指定儲存格範圍`CellArea`班級。

### 我可以使用自訂公式進行資料驗證嗎？

是的，您可以在 Aspose.Cells for Java 中使用自訂公式進行資料驗證。這允許您根據您的具體要求建立複雜的驗證規則。

### 如何從儲存格中刪除資料驗證？

若要從儲存格中刪除資料驗證，您只需調用`removeDataValidation`細胞上的方法。這將刪除該單元格的任何現有驗證規則。

### 我可以為不同的驗證規則設定不同的錯誤訊息嗎？

是的，您可以在 Aspose.Cells for Java 中為不同的驗證規則設定不同的錯誤訊息。每個資料驗證規則都有自己的輸入訊息和錯誤訊息屬性，您可以自訂這些屬性。

### 在哪裡可以找到有關 Aspose.Cells for Java 的更多資訊？

有關 Aspose.Cells for Java 及其功能的更多信息，您可以訪問文件：[這裡](https://reference.aspose.com/cells/java/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
