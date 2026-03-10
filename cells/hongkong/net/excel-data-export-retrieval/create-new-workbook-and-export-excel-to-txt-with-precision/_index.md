---
category: general
date: 2026-02-15
description: 建立新工作簿並在設定數值精度的同時將 Excel 匯出為 TXT。學習在 C# 中設定有效位數與限制有效位數。
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: zh-hant
og_description: 建立新工作簿並將 Excel 匯出為 TXT，設定有效位數以確保數值精度。一步一步的 C# 教學。
og_title: 建立新工作簿 – 精準匯出 Excel 為 TXT
tags:
- C#
- Aspose.Cells
- Excel automation
title: 建立新活頁簿並精準匯出 Excel 為 TXT
url: /zh-hant/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立新工作簿 – 將 Excel 匯出為 TXT 並精確設定數值格式

有沒有想過如何在 C# 中 **create new workbook** 物件，並立即將它們匯出為純文字檔？你並不是唯一有此需求的人。在許多資料管道情境下，我們需要 **export Excel to TXT**，同時保持數字易讀，這意味著要限制小數點後出現的位數。  

在本教學中，我們將逐步說明整個流程：從建立全新的工作簿、設定匯出以 **sets significant digits**（亦即限制有效位數），最後將檔案寫入磁碟。完成後，你將擁有一段可直接執行的程式碼片段，符合你的 **numeric precision** 需求——不需額外函式庫，也不需要魔法。

> **Pro tip:** 如果你已經在使用 Aspose.Cells，以下顯示的類別屬於該函式庫。若你使用其他平台，概念仍然適用，只需替換 API 呼叫即可。

---

## 需要的條件

- .NET 6+（此程式碼可在 .NET Core 與 .NET Framework 上編譯）  
- Aspose.Cells for .NET（免費試用版或授權版）——透過 NuGet 安裝：`dotnet add package Aspose.Cells`  
- 任意你喜歡的 IDE（Visual Studio、Rider、VS Code）  

就是這樣。無需額外的設定檔，也沒有隱藏的步驟。

---

## 步驟 1：建立新工作簿

首先要做的就是 **create new workbook**。可以把 `Workbook` 類別想像成一個空的 Excel 檔案，等待加入工作表、儲存格與資料。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Why this matters:** 透過從空白工作簿開始，你可以避免任何可能干擾之後精度設定的隱藏格式。

---

## 步驟 2：設定文字儲存選項 – 設定有效位數

現在我們告訴 Aspose.Cells，在寫入 `.txt` 檔案時希望保留多少 **significant digits**。`TxtSaveOptions` 類別提供 `SignificantDigits` 屬性，正好可以完成此設定。

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Explanation:** `SignificantDigits = 5` 表示匯出時會保留任何數字最重要的五位數，無論小數點位於何處。這是一種方便的方式，可在不手動格式化每個儲存格的情況下 **set numeric precision**。

---

## 步驟 3：將工作簿儲存為純文字檔

當工作簿與選項都已準備好後，我們最終 **export Excel to txt**。`Save` 方法接受檔案路徑以及剛剛設定好的選項物件。

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

執行程式後會產生如下所示的檔案：

```
12346
0.00012346
3.1416
```

請注意，每個數字都遵守了先前設定的 **limit significant digits** 規則。

---

## 步驟 4：驗證結果（可選但建議）

可以在任何編輯器中輕鬆開啟產生的 `numbers.txt`，但你可能想在 CI 流程中自動化驗證步驟。

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

如果主控台顯示上述三行，表示你已成功 **set significant digits**，且匯出如預期運作。

---

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| 數字顯示過多小數位 | `SignificantDigits` 保持預設值 (0) | 明確將 `SignificantDigits` 設為所需的位數 |
| 產生空白檔案 | 在儲存前工作簿未填入任何資料 | Populate cells **before** calling `Save` |
| 檔案路徑拋出 `UnauthorizedAccessException` | 嘗試寫入受保護的資料夾 | 使用你有寫入權限的資料夾（例如 `C:\Temp` 或 `%USERPROFILE%\Documents`） |
| 對於極小數字，精度似乎不正確 | `SignificantDigits` 計算時會包含小數點後的前導零 | 請記住「有效位數」會忽略前導零；0.000123456 以 5 位數顯示會變成 `0.00012346` |

---

## 完整可執行範例（直接複製貼上）

以下是完整、獨立的程式。將它貼到新的主控台專案中，然後點擊 **Run**。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**預期的主控台輸出**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

而 `numbers.txt` 檔案將包含上述的三行內容。

---

## 往後步驟：深入基礎之外

- **Export other formats** – Aspose.Cells 亦支援 CSV、HTML 與 PDF。視需求將 `TxtSaveOptions` 換成 `CsvSaveOptions` 或 `PdfSaveOptions`。  
- **Dynamic precision** – 你可以在執行時根據使用者輸入或設定檔計算 `SignificantDigits`。  
- **Multiple worksheets** – 迭代 `workbook.Worksheets`，將每個工作表匯出為各自的 `.txt` 檔案。  
- **Localization** – 若需符合區域設定，可透過 `CultureInfo` 控制小數點分隔符（`.` 與 `,`）。  

---

## 總結

我們先建立了一個全新的 **create new workbook** 實例，填入資料，並示範如何 **export Excel to TXT** 同時 **setting significant digits** 以限制輸出精度。完整範例可直接執行，說明也闡述了每行程式碼背後的 *why*，讓你能套用到自己的專案中。

歡迎自行實驗——變更 `SignificantDigits` 數值、加入更多工作表，或切換輸出格式。若遇到問題，請參考 Aspose.Cells 文件或在下方留言。祝開發愉快！

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}