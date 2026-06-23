---
category: general
date: 2026-06-17
description: C#를 사용해 Excel에서 날짜 형식을 설정하고, 셀 배경을 지정하며, 전경 색상을 적용하고, 가져오기 시 Excel 열에
  색을 입히는 방법을 단계별로 배웁니다.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: ko
og_description: C#를 사용해 Excel에서 날짜 형식을 설정하고 셀 배경을 지정하며 전경 색을 적용하고 가져오기 중에 Excel 열에
  색을 입히는 방법. 전체 튜토리얼.
og_title: C#로 Excel에서 날짜 형식 설정 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: C#로 Excel에서 날짜 형식 설정 – 전체 가져오기 서식 가이드
url: /ko/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용한 Excel 날짜 형식 설정 – 전체 가져오기 서식 가이드

Excel 시트를 C# 코드로 생성하면서 **날짜 형식 설정**을 해야 하고, 동시에 열에 사용자 지정 배경색이나 텍스트 색상을 지정하고 싶었던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 보고 시나리오에서 데이터베이스에서 `DataTable`을 가져와 워크시트에 넣은 뒤, 날짜를 올바르게 표시하고 열을 원하는 색상으로 강조하기 위해 고군분투합니다.  

이 튜토리얼에서는 **날짜 형식 설정**, **셀 배경 색상 지정**, **전경 색상 적용**, 그리고 **Excel 열 색상 지정**까지 포함한 깔끔한 엔드‑투‑엔드 솔루션을 단계별로 살펴봅니다. 끝까지 진행하면 일반적인 시행착오 없이 **excel import formatting**을 처리할 수 있는 재사용 가능한 패턴을 얻게 됩니다.

> **필요한 사항**  
> * .NET 6+ (또는 .NET Framework 4.7+)  
> * Aspose.Cells for .NET (무료 체험판으로 테스트 가능)  
> * `DataTable` 소스 – 아무 ADO.NET 쿼리라도 OK  
> * Visual Studio 또는 선호하는 IDE  

자, 시작해봅시다.

---

## 솔루션 개요

문제를 세 가지 논리적 단계로 나눕니다:

1. **소스 데이터 가져오기** – 내보낼 행이 들어 있는 `DataTable`.  
2. **열별 스타일 생성** – 날짜 열용 스타일 하나, 텍스트 열용 스타일 하나, 그리고 원하는 추가 스타일.  
3. **스타일을 적용해 테이블 가져오기** – `Worksheet.Cells.ImportDataTable`을 사용해 각 열이 준비한 스타일을 상속받도록 합니다.

왜 이런 접근법일까요? Aspose.Cells는 `ImportDataTable` 호출에 `Style` 배열을 직접 연결할 수 있게 해 주어, 서식을 다시 적용하기 위한 두 번째 패스가 필요 없습니다. 더 빠르고, 오류 가능성이 적으며, 코드가 깔끔해집니다.

---

## Step 1: 내보낼 데이터 가져오기

먼저 `DataTable`이 필요합니다. 실제 프로젝트에서는 저장 프로시저를 호출하거나 Entity Framework를 사용해 채우겠지만, 여기서는 날짜와 텍스트 열이 있는 간단한 테이블을 모의합니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **프로 팁:** 소스에 nullable 날짜가 포함돼 있다면 열 타입을 `typeof(DateTime?)`로 지정하세요 – 나중에 지정한 형식이 그대로 적용됩니다.

---

## Step 2: 열당 하나씩 스타일 배열 준비

이제 `DataTable` 열 수와 길이가 같은 `Style[]`를 만들고, 각 항목에 해당 열의 서식을 지정합니다.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 첫 번째 열의 날짜 형식 설정

첫 번째 열(`OrderDate`)은 “MM/dd/yyyy” 형식으로 표시되어야 합니다. Aspose는 짧은 날짜용 내장 숫자 형식 인덱스 14를 사용하지만, 원한다면 사용자 지정 형식 문자열을 제공할 수도 있습니다.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**왜 중요한가:** Excel은 날짜를 일련 번호로 저장합니다. 숫자 형식을 지정하면 Excel이 해당 일련 번호를 사람이 읽을 수 있는 날짜로 렌더링하도록 지시하는 것입니다.

### 2.2 두 번째 열의 셀 배경 색상 설정

`CustomerName` 열에 연한 파란색 배경을 적용해 보겠습니다. 여기서 **set cell background**가 사용됩니다.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **참고:** `Pattern`을 `Solid`로 설정하지 않으면 전경 색상이 표시되지 않는데, 기본 패턴이 “None”이기 때문입니다.

### 2.3 전경(텍스트) 색상 적용 – 선택적 추가

텍스트 자체를 대비되는 색상으로 바꾸고 싶다면 같은 스타일을 조금 수정하면 됩니다:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

이렇게 하면 **apply foreground color** 요구 사항을 충족하면서 열의 배경은 그대로 유지됩니다.

---

## Step 3: 정의한 스타일로 DataTable 가져오기

스타일을 준비했으면, 이제 한 줄로 데이터를 가져오면서 열별 스타일을 적용합니다.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**동작 원리:** Aspose는 `columnStyles` 배열을 읽어 각 `Style`을 해당 열 인덱스에 매핑합니다. 헤더 행은 별도 스타일을 제공하지 않는 한 기본 스타일을 상속받습니다.

### 3.1 워크북 저장

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

프로그램을 실행하고 *FormattedReport.xlsx* 파일을 열면 다음과 같이 표시됩니다:

- **OrderDate** 열이 날짜 형식(예: `06/15/2026`)으로 표시됩니다.  
- **CustomerName** 열이 연한 파란색 채우기와 진한 파란색 텍스트를 가집니다.  

이것이 30줄 이하의 C# 코드로 구현한 전체 **excel import formatting** 워크플로우입니다.

---

## Step‑by‑Step Recap (with Why)

| 단계 | 수행 내용 | 왜 중요한가 |
|------|-------------|----------------|
| **데이터 가져오기** | `GetData()`를 호출해 `DataTable`을 채웁니다. | Aspose가 직접 ingest할 수 있는 구조화된 소스를 제공합니다. |
| **스타일 배열 생성** | 열 수에 맞게 `Style[]`를 할당합니다. | 한 번의 가져오기 호출로 열별 스타일을 적용할 수 있습니다. |
| **날짜 형식 설정** | `columnStyles[0].Number = 14;` | Excel에서 날짜가 올바르게 렌더링됩니다. |
| **배경 색상 설정** | `ForegroundColor = LightBlue; Pattern = Solid;` | 열을 강조하여 **set cell background** 요구를 만족합니다. |
| **전경 색상 적용** | `Font.Color = DarkBlue;` | 가독성을 높이고 **apply foreground color**를 충족합니다. |
| **스타일 적용 가져오기** | `ImportDataTable(..., columnStyles);` | 모든 서식을 한 번에 적용하는 단일 패스 가져오기입니다. |
| **워크북 저장** | `wb.Save(...);` | 최종 결과를 파일로 저장해 downstream 사용자가 활용합니다. |

---

## 엣지 케이스 및 자주 묻는 질문

### 열이 두 개 이상이면 어떻게 하나요?

`columnStyles` 배열을 확장하고 필요한 인덱스마다 `Style`을 할당하면 됩니다. 할당하지 않은 인덱스는 기본 스타일을 사용하므로 문제 없습니다.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### 열을 통화 형식으로 표시하려면?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### 헤더 행 스타일을 별도로 바꾸고 싶나요?

가져온 뒤 첫 번째 행을 선택해 별도 스타일을 적용할 수 있습니다:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### DataTable에 null 날짜가 포함돼 있으면?

Aspose는 해당 셀을 빈칸으로 둡니다. “N/A” 같은 플레이스홀더를 원한다면 테이블을 미리 처리하세요:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

그 후 스타일을 조정해 sentinel 값에 대해 “N/A”를 표시하도록 커스텀 형식을 지정합니다.

---

## 전체 작업 예제

아래는 복사‑붙여넣기만 하면 되는 완전한 프로그램입니다. 콘솔 앱으로 실행하면 깔끔하게 서식이 적용된 Excel 파일이 생성됩니다.



## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 추가 API 기능을 마스터하고 다양한 구현 방식을 탐색할 수 있도록 완전한 코드 예제와 단계별 설명을 제공합니다.

- [Aspose.Cells for .NET을 사용한 Excel 셀의 글꼴 색상 설정](/cells/english/net/formatting/setting-font-color/)
- [Aspose.Cells를 이용한 .NET Excel에서 글꼴 색상 설정](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Aspose.Cells for .NET을 사용해 픽셀 단위로 Excel 열 너비 설정 | 단계별 가이드](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}