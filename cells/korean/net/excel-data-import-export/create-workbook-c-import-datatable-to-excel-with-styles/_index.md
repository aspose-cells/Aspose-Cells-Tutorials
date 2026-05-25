---
category: general
date: 2026-02-28
description: Create Workbook C# 가이드는 DataTable을 Excel로 가져오고, 사용자 정의 스타일을 추가하며, 몇 단계만으로
  서식이 적용된 내보내기를 수행하는 방법을 보여줍니다.
draft: false
keywords:
- create workbook c#
- import datatable to excel
- add custom styles excel
- how to import datatable
- export datatable with formatting
language: ko
og_description: Create Workbook C# 튜토리얼은 DataTable을 Excel로 가져오고, 사용자 정의 스타일을 적용하며,
  서식이 포함된 내보내기를 수행하는 방법을 간결한 가이드로 보여줍니다.
og_title: 워크북 생성 C# – 스타일이 적용된 DataTable을 Excel에 가져오기
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C# 워크북 만들기 – 스타일을 적용하여 DataTable을 Excel에 가져오기
url: /ko/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크북 생성 C# – 스타일이 적용된 DataTable을 Excel로 가져오기

Ever needed to **create workbook c#** and wondered how to get your `DataTable` into Excel with proper formatting? In this guide, we’ll walk through **import datatable to excel**, add custom styles, and export the result with full formatting—all using plain C# code you can drop into any project.

워크북을 **create workbook c#** 해야 할 때, `DataTable`을 적절한 서식으로 Excel에 넣는 방법이 궁금하셨나요? 이 가이드에서는 **import datatable to excel** 과정을 살펴보고, 사용자 정의 스타일을 추가한 뒤 전체 서식이 적용된 결과물을 내보내는 방법을 순수 C# 코드로 설명합니다. 이 코드는 어떤 프로젝트에도 바로 넣어 사용할 수 있습니다.

We’ll cover everything from pulling data out of a database to styling each column with alternating font colors. By the end, you’ll have a reusable snippet that not only **import datatable to excel**, but also shows **how to import datatable** with custom styling, and finally **export datatable with formatting** ready for distribution.

데이터베이스에서 데이터를 가져오는 단계부터 각 열에 교차 색상의 글꼴을 적용하는 스타일링까지 모두 다룹니다. 최종적으로는 **import datatable to excel** 뿐만 아니라 사용자 정의 스타일이 적용된 **how to import datatable** 방법과 배포용으로 준비된 **export datatable with formatting** 코드를 재사용 가능한 스니펫 형태로 제공받게 됩니다.

> **Prerequisites**  
> - .NET 6 or later (the example compiles on .NET Framework 4.7+ as well)  
> - A reference to a spreadsheet library that provides `Workbook`, `Worksheet`, and `Style` classes (e.g., Aspose.Cells, GemBox.Spreadsheet, or ClosedXML).  
> - Basic familiarity with `DataTable` objects.

> **Prerequisites**  
> - .NET 6 이상 (예제는 .NET Framework 4.7+에서도 컴파일됩니다)  
> - `Workbook`, `Worksheet`, `Style` 클래스를 제공하는 스프레드시트 라이브러리에 대한 참조 (예: Aspose.Cells, GemBox.Spreadsheet, ClosedXML).  
> - `DataTable` 객체에 대한 기본적인 이해.

---

![Create Workbook C# example showing styled Excel export](https://example.com/images/create-workbook-csharp.png)

## Step 1: Create Workbook C# – Initialize the Spreadsheet Object

## 1단계: 워크북 생성 C# – 스프레드시트 객체 초기화

First things first. We need a fresh workbook instance that will become the container for our Excel file.

우선 가장 먼저 해야 할 일은 Excel 파일의 컨테이너가 될 새로운 워크북 인스턴스를 만드는 것입니다.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using Aspose.Cells;           // Replace with your library if different

// Initialize a new workbook
Workbook workbook = new Workbook();               // assume a new workbook for this example
Worksheet worksheet = workbook.Worksheets[0];    // Grab the first (default) worksheet
```

**Why this matters:**  
**왜 중요한가:**  
Creating the workbook is the equivalent of opening a blank Excel file. The `Worksheet` object gives us a grid where we’ll later drop the `DataTable`. If you skip this step, there’s nowhere to import the data, and the library will throw a null‑reference exception.

워크북을 만드는 것은 빈 Excel 파일을 여는 것과 동일합니다. `Worksheet` 객체는 이후에 `DataTable`을 삽입할 그리드를 제공합니다. 이 단계를 건너뛰면 데이터를 가져올 위치가 없으며, 라이브러리는 null‑reference 예외를 발생시킵니다.

> **Pro tip:** If you already have a template file (maybe with a logo or pre‑defined columns), load it with `new Workbook("Template.xlsx")` instead of a brand‑new instance.

> **Pro tip:** 이미 로고나 미리 정의된 열이 포함된 템플릿 파일이 있다면, 새 인스턴스를 만들지 말고 `new Workbook("Template.xlsx")` 로 로드하세요.

## Step 2: Prepare the Source Data – Retrieve a DataTable

## 2단계: 원본 데이터 준비 – DataTable 가져오기

Next, we need the data we’re about to export. In real‑world apps this often comes from a database, but for illustration we’ll build a simple table in‑memory.

다음으로, 내보낼 데이터를 준비해야 합니다. 실제 애플리케이션에서는 보통 데이터베이스에서 가져오지만, 여기서는 메모리 내에 간단한 테이블을 만들어 보겠습니다.

```csharp
// Step 2: Retrieve the source data as a DataTable
DataTable GetData()
{
    DataTable table = new DataTable("Employees");

    // Define columns
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));
    table.Columns.Add("HireDate", typeof(DateTime));

    // Populate rows
    table.Rows.Add(1, "Alice Johnson", "Finance", new DateTime(2018, 4, 12));
    table.Rows.Add(2, "Bob Smith", "Engineering", new DateTime(2020, 7, 23));
    table.Rows.Add(3, "Carol White", "HR", new DateTime(2019, 11, 5));
    table.Rows.Add(4, "David Brown", "Marketing", new DateTime(2021, 1, 30));

    return table;
}

DataTable dataTable = GetData();   // Call the method to obtain the DataTable
```

**Why this matters:**  
**왜 중요한가:**  
A `DataTable` is a versatile, in‑memory representation of tabular data. It mirrors the rows and columns you’d eventually see in Excel, making the **how to import datatable** step straightforward.

`DataTable`은 표 형식 데이터를 메모리 내에서 표현하는 다목적 객체입니다. Excel에서 최종적으로 보게 될 행과 열을 그대로 반영하므로 **how to import datatable** 단계가 간단해집니다.

## Step 3: Define Column‑Level Styles – Add Custom Styles Excel

## 3단계: 열 수준 스타일 정의 – Excel에 사용자 정의 스타일 추가

Now we get to the fun part: styling. We’ll create an array of `Style` objects—one for each column—so that every column can have its own visual treatment. In this example we’ll alternate font colors between blue and green.

이제 재미있는 부분인 스타일링을 진행합니다. 각 열마다 `Style` 객체 배열을 만들어 열마다 고유한 시각적 처리를 적용합니다. 이 예시에서는 글꼴 색상을 파란색과 녹색으로 교차시킵니다.

```csharp
// Step 3: Prepare a style for each column in the DataTable
Style[] columnStyles = new Style[dataTable.Columns.Count];

for (int columnIndex = 0; columnIndex < columnStyles.Length; columnIndex++)
{
    // Create a new style instance for the current column
    columnStyles[columnIndex] = workbook.CreateStyle();

    // Step 4: Assign alternating font colors for visual distinction
    columnStyles[columnIndex].Font.Color = (columnIndex % 2 == 0) ? Color.Blue : Color.Green;
}
```

**Why this matters:**  
**왜 중요한가:**  
Applying styles column‑wise gives you fine‑grained control over the final look. Instead of a single blanket style, each column can convey meaning—think “blue for IDs, green for names.” This is the core of **add custom styles excel**.

열 단위로 스타일을 적용하면 최종 모습에 대한 세밀한 제어가 가능합니다. 하나의 전체 스타일 대신 각 열이 의미를 전달하도록 할 수 있습니다—예를 들어 “ID는 파란색, 이름은 녹색”처럼. 이것이 **add custom styles excel**의 핵심입니다.

> **Watch out:** Some libraries require you to also set `StyleFlag` properties (e.g., `styleFlag.FontColor = true`) before the style takes effect. Check your library’s docs if colors don’t appear.

> **Watch out:** 일부 라이브러리는 스타일이 적용되기 전에 `StyleFlag` 속성(예: `styleFlag.FontColor = true`)을 설정해야 합니다. 색상이 나타나지 않으면 라이브러리 문서를 확인하세요.

## Step 4: Import the DataTable – How to Import DataTable into the Worksheet

## 4단계: DataTable 가져오기 – Worksheet에 DataTable을 가져오는 방법

With data and styles ready, we finally import the table. The `ImportDataTable` method copies rows, columns, and optionally the column headers.

데이터와 스타일이 준비되었으니 이제 테이블을 가져옵니다. `ImportDataTable` 메서드는 행, 열 및 선택적으로 열 머리글을 복사합니다.

```csharp
// Step 5: Import the DataTable into the worksheet, applying the column styles
bool includeColumnNames = true;   // true to write column headers
int startRow = 0;                 // zero‑based index; 0 = first row
int startColumn = 0;              // zero‑based index; 0 = first column

worksheet.Cells.ImportDataTable(dataTable, includeColumnNames, startRow, startColumn, columnStyles);
```

**Why this matters:**  
**왜 중요한가:**  
This single call does the heavy lifting of **import datatable to excel**. It respects the `columnStyles` array, so each column’s font color is applied as soon as the data lands in the sheet. If you ever need to skip headers, just flip `includeColumnNames` to `false`.

이 한 번의 호출이 **import datatable to excel**의 핵심 작업을 수행합니다. `columnStyles` 배열을 인식하므로 데이터가 시트에 들어오는 즉시 각 열의 글꼴 색상이 적용됩니다. 머리글을 제외하고 싶다면 `includeColumnNames`를 `false`로 바꾸면 됩니다.

## Step 5: Save the Workbook – Export DataTable with Formatting

## 5단계: 워크북 저장 – 서식이 적용된 DataTable 내보내기

The final piece is persisting the workbook to a file (or a memory stream). This is where **export datatable with formatting** becomes visible to the end user.

마지막 단계는 워크북을 파일(또는 메모리 스트림)로 저장하는 것입니다. 여기서 **export datatable with formatting**이 최종 사용자에게 보여집니다.

```csharp
// Step 6: Save the workbook to an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "Employees.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved successfully to {outputPath}");
```

**Why this matters:**  
**왜 중요한가:**  
Saving as `Xlsx` preserves all style information. If you choose CSV, all formatting would be lost. The resulting file can be opened in Excel, Google Sheets, or any modern spreadsheet app, showing the alternating blue/green fonts we defined earlier.

`Xlsx` 형식으로 저장하면 모든 스타일 정보가 보존됩니다. CSV를 선택하면 모든 서식이 사라집니다. 생성된 파일은 Excel, Google Sheets 또는 최신 스프레드시트 앱에서 열 수 있으며, 앞서 정의한 파란색/녹색 교차 글꼴이 표시됩니다.

### Expected Output

### 예상 출력

When you open `Employees.xlsx`, you’ll see:

`Employees.xlsx`를 열면 다음과 같이 표시됩니다:

| Id | Name          | Department | HireDate   |
|----|---------------|------------|------------|
| 1  | Alice Johnson | Finance    | 4/12/2018 |
| 2  | Bob Smith     | Engineering| 7/23/2020 |
| 3  | Carol White   | HR         | 11/5/2019 |
| 4  | David Brown   | Marketing  | 1/30/2021 |

- **Id** and **HireDate** columns appear in **blue** font.  
- **Name** and **Department** columns appear in **green** font.  
- Column headers are bold (default style from the library) and included because we set `includeColumnNames` to `true`.

- **Id**와 **HireDate** 열은 **파란색** 글꼴로 표시됩니다.  
- **Name**과 **Department** 열은 **녹색** 글꼴로 표시됩니다.  
- 열 머리글은 굵게 표시됩니다(라이브러리 기본 스타일) 그리고 `includeColumnNames`를 `true`로 설정했기 때문에 포함됩니다.

---

## Common Variations & Edge Cases

## 일반적인 변형 및 엣지 케이스

### 1. Using a Template File

### 1. 템플릿 파일 사용

If you have a pre‑styled template (company logo, frozen panes, etc.), load it instead of creating a blank workbook:

사전에 스타일이 적용된 템플릿(회사 로고, 고정 창 등)이 있다면 빈 워크북을 만들지 말고 이를 로드하세요:

```csharp
Workbook workbook = new Workbook("Template.xlsx");
Worksheet worksheet = workbook.Worksheets[0];
```

The `ImportDataTable` call works the same way, and the styles you define will blend with the template’s existing formatting.

`ImportDataTable` 호출은 동일하게 동작하며, 정의한 스타일은 템플릿에 이미 존재하는 서식과 결합됩니다.

### 2. Styling Rows Instead of Columns

### 2. 열이 아닌 행 스타일링

Sometimes you want alternating row colors rather than column colors. Swap the loop logic:

때때로 열 색상이 아니라 행 색상을 교차시키고 싶을 때가 있습니다. 루프 로직을 바꾸면 됩니다:

```csharp
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    Style rowStyle = workbook.CreateStyle();
    rowStyle.Font.Color = (rowIndex % 2 == 0

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}