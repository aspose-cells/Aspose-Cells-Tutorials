---
category: general
date: 2026-02-21
description: 將 Excel 儲存為 txt，精確控制有效位數。使用 C# 匯出 Excel 為 txt，輕鬆設定有效位數。
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: zh-hant
og_description: 快速將 Excel 儲存為 txt。學習如何使用 C# 匯出 Excel 為 txt、設定有效位數，並控制文字輸出。
og_title: 將 Excel 儲存為 txt – 在 C# 中匯出具有效位數的數字
tags:
- C#
- Aspose.Cells
- Excel automation
title: 將 Excel 另存為 txt – 完整 C# 指南：匯出具有效位數的數字
url: /zh-hant/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 Excel 儲存為 txt – 完整 C# 指南：匯出具有效位數的數字

有沒有曾經需要 **save Excel as txt** 但擔心數字會失去精度？你並不孤單。許多開發者在嘗試 export Excel to txt 時會卡住，結果要麼小數位過多，要麼被四捨五入成一團糟。  

在本教學中，我們將示範一個直接且簡單的方式來 **export Excel to txt**，同時 **setting significant digits**，讓輸出結果完全符合你的需求。完成後，你將擁有一段可直接執行的 C# 程式碼，能將活頁簿儲存為文字檔、匯出數字至 txt，並完整掌控數值格式。

## 您將學會

- 如何建立新的工作簿並寫入數值資料。
- 使用 `TxtSaveOptions` 正確 **set significant digits** 的方法。
- 如何 **save workbook as text** 並驗證結果。
- 邊緣案例處理（大數字、負值、語系問題）。
- 進一步微調輸出的快速提示（分隔符變更、編碼）。

### 前置條件

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.6 以上執行）。
- **Aspose.Cells** NuGet 套件（`Install-Package Aspose.Cells`）。
- 對 C# 語法有基本了解——不需要深入的 Excel interop 知識。

> **專業提示：** 若您使用 Visual Studio，請啟用 *nullable reference types*（`<Nullable>enable</Nullable>`）以提前捕捉可能的 null 錯誤。

---

## Step 1: Initialize the Workbook and Write a Number

首先，我們需要一個 workbook 物件。它相當於 Excel 檔案的記憶體表示。

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**為什麼這很重要：**  
以程式方式建立工作簿可避免 COM interop 的額外負擔，且 `PutValue` 會自動偵測資料類型，確保儲存格被視為數字而非字串。

---

## Step 2: Configure TxtSaveOptions to Control Significant Digits

`TxtSaveOptions` 類別正是關鍵所在。透過設定 `SignificantDigits`，你告訴 Aspose.Cells 在寫入檔案時要保留多少個有意義的位數。

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**為什麼要設定它：**  
在 **export numbers to txt** 時，常需要一個簡潔的表示（例如報表系統只接受特定精度）。`SignificantDigits` 屬性保證不論原始數字長度如何，都能以一致的四捨五入方式呈現。

---

## Step 3: Save the Workbook as a Text File

現在使用剛剛定義的選項將工作簿寫入磁碟。

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**你會看到的結果：**  
開啟 `Numbers.txt`，會得到一行：

```
12350
```

原本的 `12345.6789` 已被四捨五入為 **四個有效位數**，正如需求所示。

---

## Step 4: Verify the Output (Optional but Recommended)

自動化測試是好習慣。以下提供一段簡易檢查程式，可在儲存後立即執行：

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

執行此區塊若一切正確，會印出綠色勾勾，讓你確信 **save excel as txt** 操作如預期運作。

---

## Common Variations & Edge Cases

### Exporting Multiple Cells or Ranges

如果需要 **export excel to txt** 整個範圍，只要在儲存前多寫入儲存格即可：

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

相同的 `TxtSaveOptions` 會對每個值套用 4 位數規則，產生：

```
12350
0.0001235
-98800
```

### Changing the Delimiter

有些下游系統要求以 Tab 分隔值。只要這樣調整分隔符：

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

現在每列的儲存格會以 Tab 分開。

### Handling Locale‑Specific Decimal Separators

若使用者慣用逗號作為小數點，請設定文化資訊：

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

輸出會遵循該語系，將 `12350` 轉為 `12 350`（法文中的千位空格）。

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**預期的 `Numbers.txt` 內容（預設分隔符、4 個有效位數）：**

```
12350	0.0001235	-98800
```

範例中保留了預設的 Tab（`\t`）作為分隔符；若想要 CSV，可改為逗號。

---

## Conclusion

現在你已完全掌握 **how to save Excel as txt**，同時能控制有效位數。只要依序執行：建立工作簿、設定 `TxtSaveOptions.SignificantDigits`、儲存，即可可靠地 **export excel to txt**。  

接下來你可以：

- **Export numbers to txt** 用於更大的資料集。
- 調整分隔符、編碼或文化設定，以符合任何下游系統。
- 在匯出前結合 Aspose.Cells 其他功能（樣式、公式）一起使用。

試著改變 `SignificantDigits` 為 2 或 6，觀察輸出如何變化。**Save workbook as text** 的彈性，使其成為任何資料交換流程中的好幫手。

---

### Related Topics You Might Explore Next

- **Export Excel to CSV** with custom column ordering.
- **Read txt files back into a workbook** (`Workbook.Load` with `LoadOptions`).
- **Batch processing** multiple worksheets and consolidating them into one txt file.
- **Performance tuning** for large‑scale exports (streaming vs. in‑memory).

如有任何問題，歡迎留言討論，或分享你在專案中自訂匯出的經驗。祝開發順利！

---  

*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*  
*Alt text: “Numbers.txt file displaying 12350, 0.0001235, and -98800 after saving Excel as txt with 4 significant digits.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}