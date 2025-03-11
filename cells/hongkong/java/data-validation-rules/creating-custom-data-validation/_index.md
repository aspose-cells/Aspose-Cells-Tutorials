---
title: 建立自訂資料驗證
linktitle: 建立自訂資料驗證
second_title: Aspose.Cells Java Excel 處理 API
description: 了解如何使用 Aspose.Cells for Java 建立自訂資料驗證。帶有原始程式碼的分步指南。
weight: 10
url: /zh-hant/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立自訂資料驗證


## 介紹

資料驗證透過防止使用者在 Excel 電子表格中輸入不正確或無效的資料來幫助維護資料完整性。雖然 Excel 提供內建資料驗證選項，但在某些情況下您需要定義自訂驗證規則。 Aspose.Cells for Java 讓您能夠有效率地實現這一目標。

## 先決條件

在深入研究程式碼之前，請確保您符合以下先決條件：

-  Aspose.Cells for Java：從以下位置下載並安裝該程式庫[這裡](https://releases.aspose.com/cells/java/).

## 第 1 步：設定您的 Java 項目

首先，在您首選的整合開發環境 (IDE) 中建立一個新的 Java 專案。將 Aspose.Cells for Java 函式庫加入到專案的類別路徑中。

## 第 2 步：建立 Excel 工作簿

讓我們先使用 Aspose.Cells for Java 建立一個新的 Excel 工作簿。

```java
//用於建立新 Excel 工作簿的 Java 程式碼
Workbook workbook = new Workbook();
```

## 第 3 步：新增工作表

現在，我們將一個工作表新增到工作簿中，我們將在其中套用自訂資料驗證。

```java
//新增工作表的 Java 程式碼
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 步驟 4：定義自訂驗證標準

在此步驟中，我們將定義資料必須遵守的自訂驗證標準。假設我們要將儲存格中輸入的年齡限制在 18 歲到 60 歲之間。

```java
//用於定義自訂驗證標準的 Java 程式碼
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## 第 5 步：將資料驗證應用於範圍

現在我們已經定義了自訂驗證標準，讓我們將其套用到特定的儲存格範圍。

```java
//將資料驗證套用至範圍的 Java 程式碼
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; //對前十行應用驗證
area.endColumn = 0;

validation.addArea(area);
```

## 步驟 6：儲存 Excel 文件

最後，儲存應用了自訂資料驗證規則的 Excel 檔案。

```java
//用於保存 Excel 檔案的 Java 程式碼
workbook.save("CustomDataValidation.xlsx");
```

## 結論

在本教學中，我們探索如何使用 Aspose.Cells for Java 建立自訂資料驗證規則。透過執行這些步驟，您可以確保 Excel 資料符合特定標準，從而提高資料完整性和準確性。

## 常見問題解答

### 如何下載 Java 版 Aspose.Cells？

您可以從以下網站下載 Aspose.Cells for Java：[這裡](https://releases.aspose.com/cells/java/).

### 我可以將自訂資料驗證套用到同一工作表中的多個範圍嗎？

是的，您可以透過對每個所需範圍重複步驟 5，將自訂資料驗證套用至相同工作表中的多個範圍。

### Aspose.Cells for Java 是否支援其他類型的資料驗證？

是的，Aspose.Cells for Java 支援各種類型的資料驗證，包括整數、小數、日期、時間、文字長度等。

### 如何自訂資料驗證失敗時顯示的錯誤訊息？

您可以透過修改以下內容來自訂錯誤訊息`setErrorMessage`步驟 4 中的方法，您可以在其中定義驗證標準。

### Aspose.Cells for Java 是否可以處理不同格式的 Excel 檔案？

是的，Aspose.Cells for Java 支援多種 Excel 檔案格式，包括 XLS、XLSX、XLSM 等。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
