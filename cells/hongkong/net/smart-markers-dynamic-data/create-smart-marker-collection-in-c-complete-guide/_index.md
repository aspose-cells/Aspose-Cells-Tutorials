---
category: general
date: 2026-02-23
description: 快速建立智慧標記集合，並學習如何為動態公式定義折扣變數。逐步 C# 範例與完整程式碼。
draft: false
keywords:
- create smart marker collection
- define discount variable
- smart markers Aspose.Cells
- worksheet formulas C#
- dynamic discount calculation
language: zh-hant
og_description: 在 C# 中建立智慧標記集合，並為動態 Excel 公式定義折扣變數。學習完整且可執行的解決方案。
og_title: 建立智慧標記集合 – 完整 C# 教學
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中建立智慧標記集合 – 完整指南
url: /zh-hant/net/smart-markers-dynamic-data/create-smart-marker-collection-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立智慧標記集合 – 完整 C# 教學

是否曾需要在試算表中 **create smart marker collection**，卻不知從何開始？您並非唯一遇到此問題的人——許多開發者在嘗試以程式方式向 Excel 工作表注入變數和公式時，都會碰到相同的障礙。  

好消息是？在本指南中，我們將逐步示範如何 **create smart marker collection**，以及 **define discount variable**，讓您的儲存格即時計算折扣。完成後，您將擁有一個可直接執行的 C# 範例，隨時可放入任何 Aspose.Cells 專案中使用。

## 本教學涵蓋內容

我們將逐步說明每個步驟——從初始化 `MarkerCollection` 到在工作表上套用它。您將了解每行程式碼的意義、如何處理多變數等邊緣情況，以及最終產生的試算表長什麼樣子。無需參考外部文件，所有資訊皆在此。  

先決條件相當簡單：一個較新的 .NET 執行環境（建議 5.0 以上）以及透過 NuGet 安裝的 Aspose.Cells for .NET 套件。若您已有 C# 開發經驗，幾分鐘內即可上手。

---

## 步驟 1：設定專案並加入 Aspose.Cells

### 為何此步驟重要  
在您能 **create smart marker collection** 之前，需要先有一個工作簿物件供標記使用。Aspose.Cells 提供 `Workbook` 與 `Worksheet` 類別，使此過程變得輕鬆。

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Initialize a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
```

> **小技巧：** 若您使用 .NET Core，請在編譯前加入套件：  
> `dotnet add package Aspose.Cells`

### 預期結果  
此時您已擁有一個空的工作表 (`ws`)，可供標記使用。

---

## 步驟 2：建立智慧標記集合

### 為何此步驟重要  
`MarkerCollection` 是保存所有變數與公式標記的容器。可將其視為 Aspose.Cells 稍後會替換成實際值的「佔位符袋」。

```csharp
        // Step 2: Create a collection to hold smart markers
        MarkerCollection markerCollection = new MarkerCollection();
```

現在您已 **created smart marker collection**——所有後續動態內容的基礎。

---

## 步驟 3：定義折扣變數

### 為何此步驟重要  
定義變數可讓您在多個公式中重複使用相同的值。此處我們 **define discount variable** 為 `0.1`（即 10 %）。若折扣變動，只需更新此一項目。

```csharp
        // Step 3: Define a variable marker for Discount (value 0.1)
        markerCollection.Add("var:Discount", "0.1");
```

> **如果折扣是動態的呢？**  
> 您可以將 `"0.1"` 替換為任何十進位字串表示，甚至在加入標記前從資料庫取得。

---

## 步驟 4：加入使用變數的公式標記

### 為何此步驟重要  
公式標記允許您嵌入參照變數的 Excel 公式。在此範例中，儲存格 `A1` 會計算 `B1 * (1 - Discount)`。

```csharp
        // Step 4: Define a formula marker that uses the Discount variable
        markerCollection.Add("A1", "=B1*(1-{{var:Discount}})");
```

當 Aspose.Cells 處理集合時，會將 `{{var:Discount}}` 替換為 `0.1`，最終公式為 `=B1*(1-0.1)`。

---

## 步驟 5：將集合附加至工作表

### 為何此步驟重要  
附加動作告訴工作表哪些標記屬於它。若缺少此連結，`Apply` 呼叫將無可執行的標記。

```csharp
        // Step 5: Attach the marker collection to the worksheet's SmartMarkers
        ws.SmartMarkers.Add(markerCollection);
```

---

## 步驟 6：填入工作表並套用標記

### 為何此步驟重要  
我們至少需要為 `B1` 提供一個輸入值，才能讓公式產生結果。設定 `B1` 後，呼叫 `Apply()` 讓 Aspose.Cells 替換標記並計算公式。

```csharp
        // Provide a base price in B1 (e.g., $100)
        ws.Cells["B1"].PutValue(100);

        // Step 6: Apply the smart markers to populate the worksheet cells
        ws.SmartMarkers.Apply();

        // Save the workbook to verify the outcome
        wb.Save("SmartMarkerResult.xlsx");
    }
}
```

### 預期輸出
- 儲存格 **B1** 包含 `100`。
- 儲存格 **A1** 包含公式 `=B1*(1-0.1)`。
- **A1** 的計算結果為 `90`（即套用 10 % 折扣）。

開啟 `SmartMarkerResult.xlsx`，您會看到折扣已自動套用——無需手動編輯。

---

## 處理多變數與邊緣情況

### 新增更多變數
若需要額外參數，只需持續使用 `var:` 前綴呼叫 `Add`：

```csharp
markerCollection.Add("var:TaxRate", "0.07"); // 7 % tax
markerCollection.Add("B2", "=A1*(1+{{var:TaxRate}})"); // Total with tax
```

### 變數命名規則
- 僅能使用英數字元與底線。
- 以 `var:` 為前綴，告訴 Aspose.Cells 這是變數而非儲存格參照。

### 如果變數遺失會怎樣？
Aspose.Cells 會保留未替換的佔位符，這有助於在除錯時發現設定問題。

---

## 完整範例（結合所有步驟）

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Initialize workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Create the smart marker collection
        MarkerCollection markerCollection = new MarkerCollection();

        // Define discount variable (10 % discount)
        markerCollection.Add("var:Discount", "0.1");

        // Optional: define tax variable (7 % tax)
        markerCollection.Add("var:TaxRate", "0.07");

        // Formula for discounted price in A1
        markerCollection.Add("A1", "=B1*(1-{{var:Discount}})");

        // Formula for total price with tax in B2
        markerCollection.Add("B2", "=A1*(1+{{var:TaxRate}})");

        // Attach collection to worksheet
        ws.SmartMarkers.Add(markerCollection);

        // Input base price
        ws.Cells["B1"].PutValue(100); // $100

        // Apply markers and evaluate formulas
        ws.SmartMarkers.Apply();

        // Save the file
        wb.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook saved. Check SmartMarkerResult.xlsx.");
    }
}
```

執行此程式會產生以下試算表：

| 儲存格 | 數值 | 說明 |
|------|-------|-------------|
| B1   | 100   | 基礎價格 |
| A1   | 90    | 套用 10 % 折扣 |
| B2   | 96.3  | 折扣後價格 + 7 % 稅金 |

---

## 常見問題與解答

**Q: 這能用於現有的工作表嗎？**  
A: 當然可以。您可以載入既有工作簿 (`new Workbook("template.xlsx")`)，然後將相同的標記集合套用至任意工作表。

**Q: 我可以使用複雜的 Excel 函數嗎？**  
A: 可以。任何 Excel 支援的函數——`VLOOKUP`、`IF`、`SUMIFS`——皆可放入標記字串中。必要時請記得轉義大括號。

**Q: 若需在執行時變更折扣該怎麼做？**  
A: 在呼叫 `Apply()` 前更新變數：  
```csharp
markerCollection["var:Discount"] = newDiscount.ToString();
ws.SmartMarkers.Apply();
```

**Q: 大量標記會影響效能嗎？**  
A: 套用標記的時間複雜度為 O(N)，N 為標記數量。若有上千筆資料，可採用批次更新或串流工作簿以降低記憶體使用量。

---

## 結論

現在您已了解如何在 C# 中 **create smart marker collection**，以及 **define discount variable**，以在 Excel 工作表中驅動動態計算。完整且可執行的範例示範了整個工作流程——從設定工作簿到儲存已評估公式的最終檔案。  

準備好進一步了嗎？試著根據折扣後價格加入條件格式，或從 JSON 設定檔取得折扣率。探索這些變化將深化您對 Aspose.Cells 智慧標記的掌握，讓 Excel 自動化更具彈性。  

祝程式開發愉快，盡情嘗試吧——使用智慧標記的自動化沒有任何限制！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}