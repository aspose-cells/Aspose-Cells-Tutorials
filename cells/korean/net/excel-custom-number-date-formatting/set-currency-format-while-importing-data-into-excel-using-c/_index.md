---
category: general
date: 2026-11-19
description: C#를 사용하여 Excel에서 통화 형식 설정 – Excel 워크시트 가져오기 중에 숫자 형식과 열 스타일을 설정하는 방법을
  배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: ko
lastmod: 2026-11-19
og_description: C#를 사용하여 Excel에서 통화 형식을 설정하고, 엑셀 워크시트 가져오기 중에 숫자 형식을 설정·할당하고, 엑셀 열에
  스타일을 적용하는 방법을 알아보세요.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: C#로 Excel에서 통화 형식 설정 – 완전 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: C#를 사용하여 데이터를 Excel에 가져올 때 통화 형식 설정
url: /ko/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 Excel에 데이터를 가져올 때 통화 형식 설정하기

Excel 워크시트에서 **통화 형식**을 설정해야 하는 경우, 이 가이드는 **숫자 형식**을 설정하고 열에 스타일을 적용하면서 **excel 워크시트 가져오기**를 수행하는 방법을 보여줍니다. `DataTable`의 각 열에 올바른 숫자 형식을 할당하고 원하는 스타일로 데이터를 가져오는 완전하고 실행 가능한 예제를 확인할 수 있습니다.

C#에서 Excel을 다룰 때는 단순히 원시 값을 덤프하는 것 이상이 필요합니다—숫자가 어떻게 표시되는지도 제어해야 합니다. 인보이스, 재무 보고서, 대시보드 등을 생성하든, 통화, 백분율 또는 날짜를 올바르게 포맷하면 출력이 즉시 읽기 쉬워집니다.

## 사전 요구 사항

시작하기 전에 다음이 설치되어 있는지 확인하세요:

* .NET 6.0 (또는 그 이후 버전)
* **Aspose.Cells for .NET**(또는 `Style` 클래스에 `Number` 속성을 제공하는 라이브러리) 참조  
  *NuGet*: `Install-Package Aspose.Cells`.
* `DataTable` 및 C# 컬렉션에 대한 기본 지식
* Visual Studio 2022 또는 VS Code와 같은 IDE

## 1단계: 워크시트에 쓸 데이터를 가져오기

먼저 내보내려는 원시 데이터를 포함한 `DataTable`을 얻습니다. 실제 프로젝트에서는 데이터베이스 쿼리, API 호출, CSV 파서 등에서 가져올 수 있습니다.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **왜 중요한가:** 완전히 채워진 `DataTable`을 가져오면 데이터 검색 로직을 Excel 생성 로직과 분리할 수 있어 테스트 가능성과 유지 보수성이 향상됩니다.

## 2단계: 스타일 배열 만들기 – DataTable의 열당 하나씩

Aspose.Cells는 가져올 열 수와 길이가 일치하는 `Style[]`를 기대합니다. 각 요소는 특정 숫자 형식을 보유할 수 있습니다.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **팁:** 일부 열에만 포맷이 필요하더라도 모든 열에 대해 `Style` 인스턴스를 생성해야 합니다. 그렇지 않으면 가져오기 중 `NullReferenceException`이 발생합니다.

## 3단계: 원하는 열에 숫자 형식 할당하기

내장 스타일 번호는 라이브러리마다 다릅니다. Aspose.Cells에서는:

* `0` → General (정수)  
* `2` → Currency (예: `$#,##0.00`)  
* `3` → Date 등

여기서는 두 열에 **숫자 형식**을 할당합니다: 첫 번째 열(Id)은 정수 그대로 두고, 두 번째 열(Amount)은 통화 형식을 적용합니다.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **숫자 형식 설정 방법:** `Number` 속성을 사용하면 내장 형식을 가장 빠르게 선택할 수 있습니다. 로케일별 통화가 필요하면 적절한 통화 기호를 포함한 사용자 정의 형식 문자열을 사용하는 것을 고려하세요.

## 4단계: 워크시트에 DataTable 가져오기, 열 스타일 적용하기

스타일 배열이 준비되었으니 데이터를 가져옵니다. `ImportDataTable` 메서드는 전달한 스타일을 존중합니다.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### 예상 결과

**FinancialReport.xlsx**를 열면 다음과 같이 표시됩니다:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

* **Amount** 열은 설정한 통화 형식으로 표시되고, **Id**는 정수 그대로 유지됩니다.*

## 추가 시나리오를 위한 숫자 형식 설정 방법

### 날짜 열에 숫자 형식 할당하기

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### 백분율에 사용자 정의 숫자 형식 사용하기

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### 숫자 형식 외 스타일링

같은 `Style` 객체에서 글꼴, 배경색, 정렬 등을 설정할 수도 있습니다:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **왜 작동하나요:** `Style` 객체는 셀의 모든 시각적 속성을 집계합니다. 배열을 `ImportDataTable`에 전달하면 각 셀은 정의된 스타일을 자동으로 상속합니다.

## 흔히 발생하는 함정과 회피 방법

| 함정 | 증상 | 해결책 |
|------|------|--------|
| 각 `Style`을 인스턴스화하지 않음 | 가져오기 시 `NullReferenceException` | 배열을 순회하면서 `CreateStyle()`을 호출해 속성을 설정하기 전에 인스턴스를 만들세요. |
| 잘못된 내장 숫자 인덱스 사용 | 형식이 잘못 표시됨(예: 날짜가 정수로 표시) | 라이브러리 문서를 확인해 올바른 `Number` 상수를 사용하세요. |
| 워크북 저장을 누락 | 파일이 생성되지 않거나 빈 파일 | 가져오기가 끝난 뒤 `workbook.Save(...)`를 호출하세요. |
| 통화 기호 로케일 불일치 | 미국이 아닌 로케일에서도 `$`가 표시 | 적절한 기호가 포함된 사용자 정의 형식 문자열을 사용하세요(예: `"€#,##0.00"`). |

## 전체 실행 가능한 예제



## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 관련 주제를 다룹니다. 각 리소스는 단계별 설명과 완전한 코드 예제를 포함하고 있어 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}