---
category: general
date: 2026-03-25
description: 如何使用智慧標記撰寫範本，並學習如何重複列、綁定資料、產生報表，輕鬆建立範本。
draft: false
keywords:
- how to write template
- how to repeat rows
- how to bind data
- how to generate report
- how to create template
language: zh-hant
og_description: 如何使用 Smart Markers 撰寫範本。探索如何重複列、綁定資料、產生報表以及在 C# 中建立範本。
og_title: 如何使用智慧標記編寫模板 – 完整指南
tags:
- Aspose.Cells
- C#
- SmartMarkers
title: 如何使用智慧標記撰寫範本 – 步驟指南
url: /zh-hant/net/smart-markers-dynamic-data/how-to-write-template-with-smart-markers-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Smart Markers 撰寫範本 – 完整教學  

有沒有想過 **how to write template** 能根據您的資料自動展開？您並不孤單——許多開發者在需要動態 Excel 報表時卡住了，卻不知道該使用哪個 API 功能。好消息是？使用 Aspose.Cells Smart Markers，您可以製作單一儲存格範本、綁定階層資料，並讓函式庫自動重複列。在本指南中，我們還會介紹 **how to repeat rows**、**how to bind data**，甚至 **how to generate report** 檔案，而不必手動在工作表中迴圈。

完成本教學後，您將擁有一個完整、可執行的範例，展示 **how to create template** 用於主從（master‑detail）情境，並提供邊緣案例與效能技巧。無需外部文件——所有您需要的資訊都在此。

---

## 我們將建立什麼

我們將產生一個 Excel 活頁簿，列出訂單（主檔）及其明細項目（從檔）。範本位於儲存格 **A1**，Smart Markers 會將其展開成格式良好的表格。最終工作表將如下所示：

```
Order1
   A
   B
Order2
   C
```

這是一個典型的 “how to generate report” 情境，且程式碼相容於 .NET 6+ 與 Aspose.Cells 23.x（或更新版本）。

---

## 前置條件

- .NET 6 SDK（或任何近期的 .NET 版本）  
- Visual Studio 2022 or VS Code  
- Aspose.Cells for .NET (install via NuGet: `Install-Package Aspose.Cells`)  

如果您已具備上述條件，即可開始。

---

## 第 1 步：設定專案並加入 Aspose.Cells  

```csharp
// Create a new console app (run this in a terminal)
// dotnet new console -n SmartMarkerDemo
// cd SmartMarkerDemo
// dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook with a single worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];
```

*Why this matters*：從全新的 `Workbook` 開始，可確保乾淨的畫布。`Worksheet` 物件是我們放置範本的地方。

---

## 第 2 步：撰寫 Smart Marker 範本  

範本使用 `${Master.Name}` 來顯示訂單標題，並使用 `${Detail:Repeat}` 迭代每筆明細項目。

```csharp
            // Step 2: Define a Smart Marker template that repeats detail rows for each master record
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";
            
            // Write the template into cell A1
            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);
```

> **Pro tip**：將範本保留在單一儲存格中；Smart Markers 會自動在列間展開。  

*How this solves the problem*：將 repeat 區塊直接嵌入儲存格，可避免手動插入列——由 Aspose 為您處理。

---

## 第 3 步：建立符合範本的階層資料  

我們的資料必須鏡像範本的結構：一個 `Master` 集合，每個項目包含一個 `Detail` 陣列。

```csharp
            // Step 3: Create hierarchical data matching the template structure
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };
```

*Why we bind data this way*：Smart Markers 使用反射式綁定，因此屬性名稱必須與佔位符完全對應。這就是動態報表 **how to bind data** 的核心。

---

## 第 4 步：處理範本 – 讓 Smart Markers 完成繁重工作  

```csharp
            // Step 4: Process the Smart Markers – the template will be expanded using the data above
            worksheet.SmartMarkerProcessor.Process(orderData);
```

處理完成後，工作表將包含展開的列。無需迴圈，無需手動寫入儲存格。

---

## 第 5 步：儲存活頁簿  

```csharp
            // Save the result to an XLSX file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

開啟產生的檔案，您會看到與前述相同的主從版面配置。這就是使用單行處理程式碼 **how to generate report** 的方式。

---

## 視覺概覽  

![Smart Markers 產生的 Excel 報表 – 如何撰寫範本](/images/smart-marker-report.png "如何撰寫範本")

*Alt text*：「如何撰寫範本」– 顯示最終 Excel 檔案的螢幕截圖，展示每筆訂單的重複列。

---

## 深入探討：為何 Smart Markers 是顛覆性工具  

### 如何在不使用迴圈的情況下重複列  

傳統的 Excel 自動化需要您計算最後一列、插入新列並複製樣式——這些都是容易出錯的工作。Smart Markers 以宣告式 `${Detail:Repeat}` 區塊取代這些步驟。引擎會解析該區塊，為集合中的每個元素克隆列並注入值。此方法即 **how to repeat rows** 的高效實作。

### 綁定複雜物件  

您可以綁定巢狀物件、集合，甚至 DataTable。只要屬性名稱對應，處理器就會遍歷物件圖。這正是 **how to bind data** 的核心：您提供給處理器一個普通的 CLR 物件（或如同我們所示的匿名型別），讓它自動映射。

### 產生不同格式  

雖然本例儲存為 XLSX，您只需一行程式碼即可改為 `SaveFormat.Pdf` 或 `SaveFormat.Csv`。這提供了在不修改範本的情況下，快速實作 **how to generate report** 為多種格式的途徑。

### 重複使用範本  

如果您需要 **how to create template** 用於其他工作表，只要將儲存格內容複製到另一張工作表或存入字串資源即可。相同的處理器呼叫在任何地方皆可使用，讓您的程式碼保持 DRY 且易於維護。

---

## 常見問題與邊緣案例  

| Question | Answer |
|----------|--------|
| *如果主檔沒有明細列呢？* | `${Detail:Repeat}` 區塊將被跳過，只留下主檔名稱。不會產生空白列。 |
| *我可以為重複的列設定樣式嗎？* | 可以——在處理前對範本列套用格式（字型、邊框等）。該樣式會複製到每一生成的列。 |
| *我需要釋放 workbook 嗎？* | `Workbook` 實作了 `IDisposable`。在正式程式碼中建議使用 `using` 區塊包住，但在簡短的 console 示範中可選擇性使用。 |
| *資料規模可以有多大？* | Smart Markers 記憶體使用效率高，但若集合極大（數十萬筆）可能需要分頁或串流處理。 |
| *我可以使用 JSON 檔案取代物件嗎？* | 當然可以——將 JSON 反序列化為符合範本的 POCO，然後傳遞給 `Process`。 |

---

## 完整可執行範例（直接複製貼上）  

```csharp
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize workbook
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // Define template
            string smartMarkerTemplate = @"${Master.Name}
${Detail:Repeat}
   ${Detail.Item}
${/Detail}";

            worksheet.Cells["A1"].PutValue(smartMarkerTemplate);

            // Prepare data
            var orderData = new
            {
                Master = new[]
                {
                    new
                    {
                        Name = "Order1",
                        Detail = new[]
                        {
                            new { Item = "A" },
                            new { Item = "B" }
                        }
                    },
                    new
                    {
                        Name = "Order2",
                        Detail = new[]
                        {
                            new { Item = "C" }
                        }
                    }
                }
            };

            // Process template
            worksheet.SmartMarkerProcessor.Process(orderData);

            // Save file
            workbook.Save("SmartMarkerReport.xlsx", SaveFormat.Xlsx);
            System.Console.WriteLine("Report generated: SmartMarkerReport.xlsx");
        }
    }
}
```

執行程式 (`dotnet run`) 並開啟 *SmartMarkerReport.xlsx* ——您會看到整齊排列的主從列。

---

## 重點回顧  

我們已說明如何使用 Aspose.Cells Smart Markers **how to write template**，示範 **how to repeat rows**，展示如何以階層物件 **how to bind data**，以及如何在 XLSX（或其他支援格式）中 **how to generate report**。相同的模式讓您能 **how to create template** 用於發票、庫存或任何您能想像的主從版面配置。

---

## 接下來可以做什麼？  

- **Style the output**：在處理前對範本列套用儲存格樣式。  
- **Export to PDF**：將 `SaveFormat.Xlsx` 改為 `SaveFormat.Pdf` 以產生可列印的報表。  
- **Dynamic headers**：加入 `${Headers}` 佔位符，即時產生欄位標題。  
- **Multiple sheets**：在其他工作表上重複此流程，以建立多區段報表。  

歡迎自行嘗試——更換資料來源、加入更多巢狀層級，或結合公式。Smart Markers 的彈性讓您減少編寫迴圈的時間，將更多精力投入於提供價值。

*祝程式開發順利！若遇到任何問題，歡迎在下方留言或在 Stack Overflow 上使用 `aspose-cells` 標籤聯絡我。讓我們持續交流。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}