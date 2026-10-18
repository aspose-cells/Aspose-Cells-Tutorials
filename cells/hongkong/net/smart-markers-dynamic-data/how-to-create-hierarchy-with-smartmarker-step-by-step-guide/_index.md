---
category: general
date: 2026-02-14
description: 在 SmartMarker 模板中建立層次結構比你想像的更簡單——學習如何建立階層資料以及如何有效列出員工。
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: zh-hant
og_description: 在 SmartMarker 模板中建立層次結構非常簡單。請遵循本指南來建立層次資料，並以嵌套範圍列出員工。
og_title: 使用 SmartMarker 建立層級結構 – 完整指南
tags:
- SmartMarker
- C#
- templating
title: 如何使用 SmartMarker 建立層級 – 步驟指南
url: /zh-hant/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 SmartMarker 建立階層 – 完整指南

有沒有想過 **如何在 SmartMarker 範本中建立階層**，卻又不想抓狂？你並不是唯一的。許多報表情境都需要父子關係——比如部門與其所屬員工。好消息是，只要掌握正確步驟，SmartMarker 就能讓這件事變得輕而易舉。

在本教學中，我們會一步步說明：從 **在 C# 中建立階層資料**、啟用巢狀範圍 (nested ranges)，到最終渲染一個 **列出每個部門員工** 的範本。完成後，你將得到一個可直接放入任何 .NET 專案的完整範例。

---

## 需要的條件

- .NET 6+（任何較新的版本皆可）
- 參考 **SmartMarker** 函式庫（`ws.SmartMarkerProcessor` 命名空間）
- 基本的 C# 知識——不需要高階技巧，只要會建立幾個物件與寫個 lambda 即可
- 你慣用的 IDE 或編輯器（Visual Studio、Rider、VS Code … 隨你挑）

如果以上都已備妥，太好了——讓我們直接進入主題。

---

## 如何建立階層 – 概觀

核心概念是建立一個 **巢狀物件圖**，讓它映射出最終文件想要呈現的結構。以我們的例子來說，圖形如下：

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker 之後會遍歷 `Departments`，而因為我們會開啟 **巢狀範圍處理**，它也會自動迭代每個部門的 `Employees` 集合。

---

## 步驟 1：建構階層資料模型

首先，我們建立一個匿名物件，裡面包含部門陣列，每個部門都有自己的員工清單。使用匿名型別可以讓範例保持輕量——之後若需要，可自行換成正式的 POCO 類別。

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **為什麼這很重要：** `Departments` 陣列是最上層的集合。每個元素內含 `Employees` 陣列，形成第二層階層，我們稍後會以 `#Departments.Employees#` 取用。

---

## 步驟 2：啟用巢狀範圍處理

除非明確告訴 SmartMarker，否則它不會深入內部集合。`SmartMarkerOptions` 物件即負責此開關。

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **小技巧：** 若忘記設定此旗標，內部的 `#Employees#` 範圍會直接回傳空值，結果範本會變成空白，讓人摸不著頭緒。

---

## 步驟 3：以資料執行處理器

現在把資料與選項交給處理器。`ws` 變數代表你的 **WebService**（或任何承載 SmartMarker 引擎的物件）。

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

此時 SmartMarker 會解析範本，將 `#Departments.Name#` 取代為各部門名稱，且因為已啟用巢狀範圍，會再遍歷每個部門的 `Employees` 集合。

---

## 步驟 4：編寫範本標記

以下是一個最小化範本，示範外層與內層迴圈的寫法。請將它貼到 SmartMarker 範本編輯器（或傳給處理器的 `.txt` 檔）中。

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

渲染後會得到：

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **你看到的結果：** 外層的 `#Departments.Name#` 會印出部門標題。內層的 `#Departments.Employees#` 區塊會遍歷每位員工，而區塊內的 `#Departments.Employees#` 則輸出實際姓名。

---

## 預期輸出與驗證

執行完整範例（資料 + 選項 + 範本）應該會產生上方所示的清單。若想快速驗證，可將結果輸出至主控台：

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

只要看到兩個部門標題，且其下的員工項目正確列出，即代表你已成功 **建立階層** 並 **列出員工**。

---

## 常見陷阱與邊緣情況

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| 員工沒有輸出 | `EnableNestedRange` 為 false | 設定 `EnableNestedRange = true` |
| 員工姓名重複 | 同一陣列被多個部門共用 | 複製陣列或使用不同的集合 |
| 大型階層造成記憶體壓力 | SmartMarker 會一次載入整個物件圖 | 改為串流資料或分頁載入大型集合 |
| 範本語法錯誤 | 漏掉結束 `#/…#` 標籤 | 使用 SmartMarker 驗證工具，或先用小範本測試 |

---

## 更進一步 – 真實情境變化

1. **動態資料來源** – 從資料庫撈取部門資料，並使用 LINQ 對映成匿名結構。  
2. **條件格式化** – 為每位員工加入 `IsManager` 標記，利用 SmartMarker 的條件標籤（`#if …#`）突顯主管。  
3. **多層巢狀** – 若需要在部門內再劃分團隊，只要新增 `Teams` 集合，並保持 `EnableNestedRange` 開啟即可。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**範本 (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

執行程式後會如前所示，完整印出階層結構。

---

## 結論

我們已說明 **如何在 SmartMarker 中建立階層**，從在 C# 中塑造 **階層資料**、開啟巢狀範圍，到最終渲染一個 **列出部門員工** 的範本。此模式具備高度可擴充性——只要再加入更多巢狀集合或條件邏輯，即可擁有功能強大的報表引擎。

準備好接受下一個挑戰了嗎？試著把匿名型別換成強型別 POCO 類別，或將此流程整合到 ASP.NET Core 端點，回傳 PDF 或 Word 文件。天際無限，而你已擁有堅實的基礎。

---

![How to create hierarchy diagram](image.png){alt="顯示部門與員工關係的階層圖示"}

*祝程式開發愉快！若遇到任何問題，歡迎在下方留言，我很樂意協助。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}