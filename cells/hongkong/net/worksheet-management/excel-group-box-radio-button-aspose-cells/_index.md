---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中新增互動式群組框和單選按鈕，從而提高資料輸入效率。"
"title": "使用 Aspose.Cells for .NET 在 Excel 中實作群組框和單選按鈕控制項"
"url": "/zh-hant/net/worksheet-management/excel-group-box-radio-button-aspose-cells/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for .NET 在 Excel 中實作群組框和單選按鈕控制項

在 Excel 中建立互動式表單可以透過允許使用者進行結構化輸入來顯著提高資料輸入效率。使用 Aspose.Cells for .NET，您可以將群組框控制項和單選按鈕無縫新增至 Excel 工作表。本綜合指南將引導您完成使用 C# 的整個過程。

## 您將學到什麼：
- 在 Excel 工作表中建立 Group Box 控制項
- 在群組框中新增多個單選按鈕
- 將形狀分組以便更好地管理和展示
- 這些控制項在現實場景中的實際應用

讓我們先了解一下您在深入研究之前需要了解的基本知識。

### 先決條件
在開始之前，請確保您具備以下條件：
- **所需庫**：從下載最新版本的 Aspose.Cells for .NET [Aspose 網站](https://releases。aspose.com/cells/net/).
- **環境設定要求**：本教學假設在 Windows 環境中安裝了 Visual Studio。
- **知識前提**：對 C# 程式設計有基本的了解，並熟悉 Excel 檔案操作。

### 設定 Aspose.Cells for .NET
若要將 Aspose.Cells 整合到您的專案中，請按照以下安裝步驟操作：

#### .NET CLI
```bash
dotnet add package Aspose.Cells
```

#### 套件管理器控制台
```powershell
PM> Install-Package Aspose.Cells
```

**許可證獲取**：從 [免費試用](https://releases.aspose.com/cells/net/) 或取得臨時許可證以無限制探索所有功能。如需長期使用，請考慮從 [Aspose購買頁面](https://purchase。aspose.com/buy).

### 實施指南
我們將把實作分為三個主要部分：建立群組框、新增單選按鈕和分組形狀。

#### 建立組框控件
組框作為相關控件的容器。以下介紹如何將其新增至 Excel 工作表：

**步驟 1**：初始化您的工作簿並存取第一個工作表。
```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;

string outputDir = "/YOUR_OUTPUT_DIRECTORY";
Workbook excelbook = new Workbook();
Worksheet sheet = excelbook.Worksheets[0];
```

**第 2 步**：向工作表新增具有指定尺寸的分組框。
```csharp
GroupBox box = sheet.Shapes.AddGroupBox(1, 0, 300, 250);
box.Text = "Age Groups";
box.Placement = PlacementType.FreeFloating;
box.Shadow = false;

excelbook.Save(outputDir + "/GroupBoxControl.xls");
```

**解釋**： 這 `AddGroupBox` 方法將一個群組框放置在指定的行和列索引處，寬度為 300 個單位，高度為 250 個單位。放置設定為自由浮動，允許獨立移動。

#### 新增單選按鈕
單選按鈕可用於從群組框中的多個選項中選擇一個選項。

**步驟 1**：在工作表中建立單選按鈕。
```csharp
RadioButton radio1 = sheet.Shapes.AddRadioButton(3, 0, 30, 110);
radio1.Text = "20-29";
radio1.LinkedCell = "A1"; // 連結到儲存格 A1 以進行資料檢索
radio1.Shadow = true;
radio1.Line.Weight = 4;
radio1.Line.DashStyle = MsoLineDashStyle.Solid;

RadioButton radio2 = sheet.Shapes.AddRadioButton(6, 0, 30, 110);
radio2.Text = "30-39";
radio2.LinkedCell = "A1";

RadioButton radio3 = sheet.Shapes.AddRadioButton(9, 0, 30, 110);
radio3.Text = "40-49";
radio3.LinkedCell = "A1";

excelbook.Save(outputDir + "/RadioButtons123.xls");
```

**解釋**： 每個 `AddRadioButton` 呼叫在指定位置建立一個新按鈕。這 `LinkedCell` 屬性將單選按鈕與單元格綁定，從而可以輕鬆提取資料。

#### 分組形狀
將形狀分組可以使工作表中的操作和組織更加容易。
```csharp
Shape[] shapeobjects = new Shape[] { box, radio1, radio2, radio3 };
GroupShape group = sheet.Shapes.Group(shapeobjects);

excelbook.Save(outputDir + "/GroupedShapes.xls");
```

**解釋**：透過使用 `sheet.Shapes.Group`，您可以將多個形狀組合成一個實體。這對於維持控制之間的空間關係特別有用。

### 實際應用
以下是這些功能在現實生活中的一些應用場景：
1. **資料收集表**：使用分組框和單選按鈕在調查中收集使用者的結構化資料。
2. **配置面板**：在 Excel 工作表中建立互動式配置面板以進行自訂設定。
3. **庫存管理**：實作允許使用者有效選擇庫存類別的表格。

### 性能考慮
為了獲得最佳性能：
- 盡量減少添加到工作表的形狀數量。
- 使用輕量級控制並避免形狀設計中不必要的複雜性。
- 透過在不再需要時處置資源來有效地管理記憶體。

### 結論
透過遵循本指南，您已經學會如何使用 Aspose.Cells for .NET 透過互動式群組框和單選按鈕來增強您的 Excel 工作表。此功能可大幅改善使用者在資料輸入任務及其他方面的體驗。

**後續步驟**：嘗試不同的配置並探索 Aspose.Cells 的附加功能以進一步自訂您的 Excel 應用程式。

### 常見問題部分
1. **如何將單選按鈕連結到不同的儲存格？**
   - 變更 `LinkedCell` 屬性到您想要的目標儲存格。
2. **我可以更改組框的顏色嗎？**
   - 是的，探索 `FillFormat` GroupBox 類別內的屬性用於自訂。
3. **形狀分組有哪些常見問題？**
   - 分組之前，請確保所有形狀都位於同一張工作表上並且正確對齊。
4. **是否可以根據使用者輸入動態新增這些控制項？**
   - 當然，您可以透過程式設計來確定何時何地放置控制項。
5. **如何在 Aspose.Cells 中處理這些形狀的事件？**
   - 目前，Aspose.Cells 專注於創建和操作；事件處理超出了它的範圍。

### 資源
- [Aspose.Cells文檔](https://reference.aspose.com/cells/net/)
- [下載 Aspose.Cells](https://releases.aspose.com/cells/net/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用版下載](https://releases.aspose.com/cells/net/)
- [臨時許可證申請](https://purchase.aspose.com/temporary-license/)
- [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}