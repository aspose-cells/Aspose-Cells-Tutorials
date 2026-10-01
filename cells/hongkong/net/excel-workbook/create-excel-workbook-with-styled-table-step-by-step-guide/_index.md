---
category: general
date: 2026-03-21
description: 建立 Excel 工作簿，將資料表匯入 Excel 並設定欄位樣式，匯出資料至 Excel，並將 Excel 儲存格的日期格式設定為以分鐘為單位。
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: zh-hant
og_description: 快速建立 Excel 活頁簿。學習將資料表匯入 Excel、設定欄位樣式、匯出資料至 Excel，以及在同一指南中格式化 Excel
  儲存格日期。
og_title: 建立 Excel 活頁簿 – 完整樣式與匯出教學
tags:
- C#
- Aspose.Cells
- Excel automation
title: 建立帶樣式表格的 Excel 活頁簿 – 步驟教學
url: /zh-hant/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 – 完整程式教學

有沒有曾經需要 **create excel workbook**，而且直接從程式碼產生的檔案就已經很精緻？也許你正從資料庫抓取資料，想讓日期自動以正確格式顯示，而不必之後再在 Excel 裡手動調整。這是常見的痛點——尤其是當輸出直接寄到客戶的信箱，對方期望檔案一打開就能直接使用。

本教學將一步步示範一個完整、獨立的解決方案，包含 **imports datatable to excel**、套用 **set column style**，最後 **export data to excel** 為一個格式良好的檔案。你將會看到如何 **format excel cells date**，讓試算表看起來像專業報告，並在最後取得完整、可直接執行的範例。沒有遺漏的部份，也不會出現「請參考文件」的捷徑——只有可以直接放入專案的純程式碼。

---

## 你將學會

- 如何使用 Aspose.Cells 函式庫（或任何相容的 API）**create excel workbook**。
- **import datatable to excel** 的最快方法，無需手動逐格迴圈。
- **set column style** 的技巧，包括為特定欄位套用日期格式。
- 如何透過一次 `Save` 呼叫 **export data to excel**。
- 在嘗試 **format excel cells date** 時常見的陷阱以及避免方式。

### 前置條件

- .NET 6 以上（或 .NET Framework 4.6 以上）。  
- 已安裝 Aspose.Cells for .NET（`Install-Package Aspose.Cells`）。  
- 已備妥可匯出的 `DataTable`——你的資料來源可以是 SQL、CSV，或任何能轉成 `DataTable` 的格式。

如果你已經熟悉 C# 且上述項目都已就緒，就可以直接開始。否則，請參考上面的「前置條件」段落，快速檢查所需項目。

---

## 步驟 1 – 建立 Excel 工作簿實例

當你想以程式方式 **create excel workbook** 時，第一件事就是實例化 workbook 物件。可以把它想像成打開一本空白筆記本，之後會在上面寫入資料。

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **為何重要：**  
> `Workbook` 類別是 Aspose.Cells 所有操作的入口。事先建立它能提供一個乾淨的畫布，之後若需要在既有檔案上追加資料，也可以再載入該檔案，而不必從頭開始。

---

## 步驟 2 – 準備要匯入的 DataTable

在能 **import datatable to excel** 之前，我們需要一個 `DataTable`。在實務專案中，這通常來自 `SqlDataAdapter.Fill` 或 `DataTable.Load`。為了說明清楚，我們會寫一個 stub 方法，回傳已備好的表格。

```csharp
// Step 2: Obtain the data to be written – a DataTable with three columns
DataTable dataTable = GetData();   // assume GetData() returns the required table

// Example implementation (you can replace this with your own data source)
DataTable GetData()
{
    DataTable dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Quantity", typeof(int));

    dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
    dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
    dt.Rows.Add(DateTime.Today, "Cherries", 60);
    return dt;
}
```

> **小技巧：** 若你的日期是以字串形式儲存，請先轉成 `DateTime`——否則 **format excel cells date** 步驟將無法如預期運作。

---

## 步驟 3 – 為每個欄位定義樣式（Set Column Style）

接下來就是 **set column style** 的部分。我們會建立一個 `Style` 物件陣列——每個欄位一個。第一欄會使用內建的日期格式（代碼 14），其餘欄位則保留一般格式（代碼 0）。

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **為何使用樣式物件？**  
> 只套用一次樣式並重複使用，比逐格設定格式效率高得多。它也能確保整個欄位遵循相同的 **format excel cells date** 規則，對於在不同語系開啟檔案時保持一致性相當重要。

---

## 步驟 4 – 使用樣式將 DataTable 匯入工作表

在工作簿已備妥且樣式已定義後，我們現在 **import datatable to excel**。`ImportDataTable` 方法負責主要工作：寫入欄位標題、資料列，並套用我們傳入的樣式。

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **內部運作原理：**  
> - `true` 讓 Aspose.Cells 在第一列加入欄位名稱。  
> - `0, 0` 為起始列與欄的索引（左上角）。  
> - `columnStyles` 使每個欄位對應我們事先準備好的樣式，確保 **format excel cells date** 規則套用於日期欄位。

---

## 步驟 5 – 儲存（匯出）工作簿至實體檔案

最後，我們透過將工作簿儲存至磁碟來 **export data to excel**。你可以自行更改路徑至任意資料夾，甚至直接將檔案串流至 HTTP 回應，以供 Web API 使用。

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **專業小技巧：** 若需在不寫入磁碟的情況下傳送檔案，請使用 `workbook.Save(Stream, SaveFormat.Xlsx)`。

---

## 完整可執行範例（結合所有步驟）

以下是完整、可直接執行的程式。將它貼到 Console 應用程式中，調整輸出路徑，即可在數秒內得到格式良好的 Excel 檔案。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Get the data (replace GetData with your own source if needed)
        DataTable dataTable = GetData();

        // 3️⃣ Prepare column styles – date format for the first column
        Style[] columnStyles = new Style[3];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = workbook.CreateStyle();
            columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date, 0 = general
        }

        // 4️⃣ Import the DataTable with the styles
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 5️⃣ Save the file
        workbook.Save("StyledTable.xlsx");

        Console.WriteLine("Excel workbook created successfully!");
    }

    // Sample data generator – replace with real data source
    static DataTable GetData()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
        dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
        dt.Rows.Add(DateTime.Today, "Cherries", 60);
        return dt;
    }
}
```

**預期輸出：**  
當你開啟 `StyledTable.xlsx` 時，A 欄會顯示類似 `03/19/2026` 的日期（視你的語系而定），而 B、C 欄則分別以純文字/數字顯示商品名稱與數量。無需額外的格式化步驟——你的 **create excel workbook** 已完成。

---

## 常見問答與邊緣案例

### 1️⃣ 如果我的 DataTable 超過三個欄位怎麼辦？

在 `columnStyles` 陣列中加入更多 `Style` 物件，並針對需要特殊格式的欄位（例如貨幣、百分比）調整 `Number` 屬性。`ImportDataTable` 會依照位置對應每個樣式。

### 2️⃣ 我可以使用自訂日期格式取代內建的 14 嗎？

當然可以。將 `columnStyles[i].Number = 14;` 改成：

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ 如何在 Web API 中 **export data to excel** 而不寫入磁碟？

使用 `MemoryStream`：

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ 若使用者的語系需要不同的日期分隔符怎麼辦？

內建的日期格式（ID 14）會遵循工作簿的語系設定。若需要不受語系影響的固定格式，請如上例使用 `Custom` 屬性。

### 5️⃣ 這能在 .NET Core 上使用嗎？

可以——Aspose.Cells 支援 .NET Standard 2.0 及以上版本，故相同程式碼可在 .NET 6、.NET 7 或任何相容的執行環境上執行。

---

## 最佳實踐技巧（Pro Tips）

- **重複使用樣式**：雖然為每個欄位建立樣式成本不高，但對相同欄位重複使用同一樣式物件可節省記憶體。
- **避免逐格迴圈**：`ImportDataTable` 已高度最佳化，手動迴圈較慢且易出錯。
- **提前設定工作簿語系**，若需要在不同環境間保持一致的數字/日期分隔符：

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **匯入前驗證 DataTable**——若有 null 日期，在套用日期樣式時會拋出例外。
- **啟用計算**，若在匯入後加入公式：

```csharp
workbook.CalculateFormula();
```

---

## 結論

現在你已擁有一套完整、端到端的流程，能 **create excel workbook**、**import datatable to excel**、**set column style**、**export data to excel**，以及 **format excel cells date**——全部只需不到十行 C# 程式碼。此方法快速、可靠，且將格式化工作全部寫在程式碼中，讓最終的試算表在使用者打開的瞬間即已準備好供商業使用。

準備好接受下一個挑戰了嗎？試著加入條件格式、插入圖表，或是轉換

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}