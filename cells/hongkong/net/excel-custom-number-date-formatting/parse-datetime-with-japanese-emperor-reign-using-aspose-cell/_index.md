---
category: general
date: 2026-09-24
description: 使用 Aspose.Cells 在 C# 中解析帶有日本天皇年號的 DateTime。啟用日本紀元曆，寫入年號字串，並取得精確的 DateTime
  值。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: zh-hant
lastmod: 2026-09-24
og_description: 使用 Aspose.Cells 在 C# 中解析帶有日本天皇年號的 DateTime。本教程說明如何啟用日本年號曆、寫入年號字串，並正確讀取
  DateTime。
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: 使用 Aspose.Cells 解析含日本天皇在位期間的日期時間 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: 使用 Aspose.Cells 解析含日本天皇年號的日期時間
url: /zh-hant/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 解析帶有日本天皇年號的 DateTime

如果您需要在 .NET 應用程式中 **解析帶有日本天皇年號的 DateTime**，本指南將一步步示範如何使用 Aspose.Cells 完成。只要啟用日本年號曆、寫入帶年號的字串，並讀取產生的 `DateTime` 值，即可取得可靠且符合文化的日期，無需自行處理字串。

在金融、政府及仍以「令和3年5月10日」等格式儲存日期的舊系統中，處理日本年號日期相當常見。本教學涵蓋完整工作流程，從專案設定到取得可用於計算、記錄或 UI 顯示的 `DateTime` 物件。

## 您將學會

- 如何將 Aspose.Cells NuGet 套件加入 C# 專案。  
- 如何透過 `Workbook.Settings` 開啟 **日本年號曆**。  
- 如何將日本年號日期字串寫入儲存格，讓 Aspose.Cells 自動解析。  
- 如何使用 `DateTimeValue` 屬性讀取解析後的 `DateTime`。  

**先備條件**  
- .NET 6.0 或更新版本（此程式碼亦支援 .NET Framework 4.7+）。  
- 具備 C# 與 Visual Studio（或任意 IDE）的基本知識。  
- 可連網下載 Aspose.Cells 套件。

---

## 步驟 1：安裝 Aspose.Cells

在終端機或 NuGet 套件管理員主控台中開啟專案資料夾，執行：

```bash
dotnet add package Aspose.Cells
```

或在 Visual Studio 中，右鍵點擊專案 → **Manage NuGet Packages** → 搜尋 **Aspose.Cells** 並點擊 **Install**。  
此操作會加入 `Aspose.Cells` 程式庫，提供我們所需的 `Workbook`、`Worksheet` 以及解析功能。

## 步驟 2：啟用日本年號曆

Aspose.Cells 預設會停用日本年號解析。必須透過 `Workbook.Settings.UseJapaneseEraCalendar` 旗標將其開啟。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

將 `UseJapaneseEraCalendar` 設為 `true` 後，函式庫會依官方日本曆法規則，解讀包含年號名稱（`令和`、`平成`、`昭和` 等）的字串。

## 步驟 3：將日本年號日期字串寫入儲存格

接著，取得第一個工作表，並將日本年號日期字串寫入 **A1** 儲存格。

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**為什麼會這樣運作：**  
當 `UseJapaneseEraCalendar` 為啟用狀態時，`PutValue` 會檢查字串、偵測年號前綴（`令和`），並在內部將其轉換為對應的公曆年份（2021）。函式庫隨後將此值存為真正的 `DateTime` 物件，而非純文字。

## 步驟 4：取得解析後的 `DateTime` 值

現在讀取儲存格的 `DateTimeValue`。Aspose.Cells 會自動回傳公曆日期。

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

執行程式後會印出：

```
Parsed Gregorian date: 2021-05-10
```

輸出證實 **Parse DateTime with Japanese Emperor Reign** 正確將「令和3年5月10日」轉換為 2021 年 5 月 10 日。

## 步驟 5：處理邊緣情況與常見變形

### 多種年號格式
Aspose.Cells 能辨識以下幾種年號表示方式：

| 時代（日本） | 公曆年份範圍 |
|--------------|--------------|
| 明治 (Meiji) | 1868‑1912 |
| 大正 (Taishō) | 1912‑1926 |
| 昭和 (Shōwa) | 1926‑1989 |
| 平成 (Heisei) | 1989‑2019 |
| 令和 (Reiwa) | 2019‑present |

即使來源資料混用全形字元、空格，或使用漢字「年」「月」「日」等，解析器仍能正確處理。例如，`"平成31年4月30日"` 會被轉換為 `2019-04-30`。

### 無效字串
當字串無法解析（例如 `"令和99年13月40日"`）時，`DateTimeValue` 會回傳 `DateTime.MinValue`。您可以這樣檢查：

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### 停用功能
若之後需要保留原始年號字串而不做轉換，只需將旗標設回 `false`：

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### 效能小技巧
啟用年號曆會在每次涉及字串的 `PutValue` 呼叫時增加少量開銷。若只需解析少數儲存格，建議在操作前開啟旗標，完成後立即關閉，以降低影響。

## 完整可執行範例

以下提供完整程式碼，您可以直接複製、貼上並立即執行。

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**預期輸出**

```
Parsed Gregorian date: 2021-05-10
```

此程式示範了使用 Aspose.Cells 進行 **Parse DateTime with Japanese Emperor Reign** 的端對端流程，從建立工作簿到取得可用的 `DateTime` 物件。

---

## 結論

您現在已掌握在 C# 中 **Parse DateTime with Japanese Emperor Reign** 的步驟：

1. 安裝 **Aspose.Cells**。  
2. 透過 `Workbook.Settings` 啟用 **日本年號曆**。  
3. 將帶年號的字串寫入儲存格。  
4. 讀取產生的 `DateTimeValue`。  

此方法省去自行撰寫解析程式碼，遵循官方年號界限，且能無縫整合至現有 .NET 日期處理程式碼。

**後續建議**  
- 探索 Aspose.Cells 其他文化特定功能，例如 **C# date parsing** 用於伊斯蘭曆或泰國佛教曆。  
- 結合 `Workbook Settings` 如 `CalcEngine`，評估引用年號日期的公式。  
- 在報表、資料庫儲存或需要公曆日期的 UI 元件中使用解析後的 `DateTime`。

歡迎嘗試不同的年號字串、處理無效輸入，並將此解決方案整合至更大型的資料匯入管線。祝開發順利！

## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您對相關 API 功能的掌握，並提供其他實作方式的範例說明。

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}