---
category: general
date: 2026-04-07
description: C#를 사용하여 Excel 행에 배경 색을 추가합니다. 교차 행 색상을 적용하고, 단색 배경 스타일을 설정하며, 단일 워크플로우에서
  데이터테이블을 Excel로 가져오는 방법을 배웁니다.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: ko
og_description: C#를 사용하여 엑셀 행에 배경색을 추가합니다. 이 가이드는 교차 행 색상을 적용하고, 단색 배경을 설정하며, 데이터테이블을
  효율적으로 엑셀로 가져오는 방법을 보여줍니다.
og_title: Excel에 배경색 추가 – C#에서 교대 행 스타일
tags:
- C#
- Excel
- DataTable
- Styling
title: Excel에 배경색 추가 – C#에서 교대 행 스타일
url: /ko/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에 배경색 추가 – C#에서 교대 행 스타일

Ever needed to **add background color excel** rows but weren't sure how to do it without a thousand lines of fiddly code? You're not alone—most developers hit that wall when they first try to make their spreadsheets look more than just a raw dump of data.  

좋은 소식은? 몇 분만에 **교대 행 색상 적용**, **단색 배경 설정**, 그리고 **import datatable to excel**를 C#의 깔끔하고 재사용 가능한 패턴으로 할 수 있다는 것입니다.  

In this tutorial we’ll walk through the whole process, from pulling data into a `DataTable` to styling each row with a light‑yellow‑white stripe pattern. No external libraries beyond a solid Excel‑handling package (like **ClosedXML** or **GemBox.Spreadsheet**) are required, and you’ll see why this approach is both performant and easy to maintain.  

## 배울 내용

- 데이터를 검색하여 Excel 워크시트에 전달하는 방법.
- **style excel rows**를 교대 배경색으로 스타일링하는 방법.
- `Style` 객체를 사용하여 **set solid background**를 구현하는 메커니즘.
- 행 스타일을 유지하면서 **import datatable to excel**하는 방법.
- 빈 테이블이나 사용자 정의 색상 스키마와 같은 엣지 케이스를 처리하기 위한 팁.

> **Pro tip:** 스타일 생성을 지원하는 라이브러리에서 워크북 객체(`wb`)를 이미 사용하고 있다면, 동일한 `Style` 인스턴스를 여러 워크시트에서 재사용할 수 있습니다—메모리를 절약하고 코드를 깔끔하게 유지합니다.

---

## 1단계: 데이터 가져오기 – DataTable 준비

Before any styling can happen we need a source of rows. In most real‑world scenarios this comes from a database, an API, or a CSV file. For illustration, we’ll just create a simple `DataTable` in‑memory.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** `DataTable`을 사용하면 Excel 라이브러리가 직접 가져올 수 있는 표형식이며 스키마를 인식하는 컨테이너를 제공하므로 셀 단위 루프를 작성할 필요가 없습니다.

---

## 2단계: 행 스타일 만들기 – **Apply alternating row colors**

Now we’ll build an array of `Style` objects—one per row—so that each row can receive its own background. The pattern we’ll use is a classic light‑yellow for even rows and white for odd rows.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()`는 다른 스타일에 영향을 주지 않고 조정할 수 있는 깨끗한 스타일 객체를 제공합니다.  
- 삼항 연산자 `(i % 2 == 0)`는 행이 짝수(연한 노랑)인지 홀수(흰색)인지를 결정합니다.  
- `Pattern = BackgroundType.Solid` 설정은 **set solid background**를 수행하는 핵심 단계이며, 이 설정이 없으면 색상이 무시됩니다.

---

## 3단계: 대상 워크시트 가져오기

Most libraries expose a worksheet collection. We’ll work with the first one, but you can target any index or name you prefer.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

If the workbook is brand new, the library usually creates a default sheet for you. Otherwise, you can add one explicitly:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## 4단계: 행 스타일과 함께 DataTable 가져오기 – **Import datatable to excel**

With the styles ready, the final step is to push the `DataTable` into the sheet while applying the corresponding style to each row.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true`는 메서드가 첫 번째 행에 열 헤더를 기록하도록 지시합니다.  
- `0, 0`은 삽입 지점을 좌상단(A1)으로 지정합니다.  
- `rowStyles`는 각 `Style`을 해당 데이터 행과 맞추어 앞서 준비한 교대 색상을 적용합니다.

---

## 5단계: 워크북 저장

The last piece of the puzzle is persisting the workbook to a file so you can open it in Excel and see the result.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Open the file and you should see a neatly formatted sheet:

- Header row in bold (default library styling).  
- Row 1, 3, 5… with a clean white background.  
- Row 2, 4, 6… with a subtle light‑yellow fill, making it easy to scan.

### 예상 출력 스냅샷

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rows 2, 4, 6, … appear with a light‑yellow background—exactly the **apply alternating row colors** effect we aimed for.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt 텍스트에는 SEO를 위한 주요 키워드가 포함되어 있습니다.)*

---

## 엣지 케이스 및 변형 처리

### 빈 DataTable

If `dataTable.Rows.Count` is zero, the `rowStyles` array will be empty and `ImportDataTable` will still write the header row (if `includeHeaders` is `true`). No exception is thrown, but you might want to guard against generating an almost‑blank file:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### 사용자 정의 색상 스키마

Want a blue/gray stripe instead of yellow/white? Just replace the `Color` values:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Feel free to pull colours from a configuration file so non‑developers can tweak the palette without touching code.

### 여러 워크시트에서 스타일 재사용

If you export several tables into the same workbook, you can generate the style array once and reuse it:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Just be careful that both tables have the same row count, or generate a new array per sheet.

---

## 전체 작업 예제

Putting everything together, here’s a self‑contained program you can copy‑paste into a console app.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Run the program, open `Report.xlsx`, and you’ll see the alternating background exactly as described.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}