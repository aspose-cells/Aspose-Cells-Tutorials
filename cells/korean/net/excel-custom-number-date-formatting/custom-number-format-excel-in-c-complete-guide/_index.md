---
category: general
date: 2026-03-22
description: '사용자 지정 숫자 형식 엑셀 튜토리얼: 데이터테이블을 엑셀로 가져오고, 열 배경색을 설정하고, 열을 통화 형식으로 지정하고,
  워크북을 xlsx로 저장하는 방법.'
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: ko
og_description: 데이터 테이블을 가져오고, 열 배경색을 설정하며, 열을 통화 형식으로 서식 지정하고, 워크북을 xlsx로 저장하는 맞춤
  숫자 형식 엑셀 튜토리얼.
og_title: C#을 사용한 Excel 사용자 지정 숫자 형식 – 단계별 가이드
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: C#에서 Excel 맞춤 숫자 형식 – 완전 가이드
url: /ko/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 맞춤 숫자 형식 Excel – 풀스택 C# 튜토리얼

C#에서 직접 **custom number format excel** 스타일을 적용하는 방법이 궁금했나요? DataTable을 스프레드시트에 덤프했지만 일반 숫자만 보이고 색상이나 통화 서식이 없었을 수도 있습니다. 이해관계자를 위한 깔끔한 보고서가 필요할 때 흔히 겪는 문제입니다.

이 가이드에서는 그 문제를 함께 해결합니다: **import datatable to excel**, **set column background color**, **format column as currency**를 배우고, 마지막으로 **save workbook as xlsx**를 수행하여 숫자를 돋보이게 하는 맞춤 숫자 형식을 적용합니다. 애매한 설명 없이, 프로젝트에 복사‑붙여넣기 할 수 있는 완전한 실행 가능한 솔루션을 제공합니다.

---

## 만들게 될 것

이 튜토리얼이 끝날 때쯤이면 다음과 같은 독립 실행형 C# 콘솔 앱을 갖게 됩니다:

1. `DataTable`을 가져옵니다 (스텁을 직접 쿼리로 교체할 수 있습니다).  
2. Aspose.Cells(또는 호환 라이브러리)를 사용해 새로운 Excel 워크북을 생성합니다.  
3. 첫 번째 열에 파란색 굵은 글꼴을, 두 번째 열에 연노란색 배경을, 세 번째 열에 통화 형식(`$#,##0.00`)을 적용합니다.  
4. 선택한 폴더에 파일을 `DataTableWithStyleArray.xlsx` 이름으로 저장합니다.

각 라인이 최종 Excel 파일에 어떻게 기여하는지 정확히 확인할 수 있으며, 이러한 선택이 유지보수성과 성능에 왜 중요한지 논의합니다.

---

## 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 동작합니다).  
- Aspose.Cells for .NET(무료 체험 또는 라이선스 버전). NuGet을 통해 설치합니다:

```bash
dotnet add package Aspose.Cells
```

- `DataTable` 및 C# 콘솔 애플리케이션에 대한 기본적인 이해.

---

## 단계 1: 소스 데이터를 DataTable로 가져오기

먼저, 내보낼 데이터를 준비해야 합니다. 실제 상황에서는 보통 리포지토리를 호출하거나 SQL 쿼리를 실행합니다. 예시를 위해 메모리 내에 간단한 테이블을 생성합니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Why this matters:** `DataTable`을 사용하면 표 형식의 스키마 인식 소스를 얻어 Excel 행과 열에 깔끔하게 매핑할 수 있습니다. 또한 코드를 다시 작성하지 않고도 모든 데이터셋에 동일한 내보내기 로직을 재사용할 수 있습니다.

---

## 단계 2: 새 워크북을 만들고 첫 번째 워크시트를 가져오기

이제 Excel 워크북을 생성합니다. `Workbook` 클래스는 전체 파일을 나타내며, `Worksheets[0]`은 데이터를 넣을 기본 시트입니다.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** 여러 시트가 필요하면 `workbook.Worksheets.Add("SheetName")`를 호출하고 각 시트마다 스타일링 단계를 반복하면 됩니다.

---

## 단계 3: 열 스타일 정의 – 글꼴, 배경 및 숫자 형식

Aspose.Cells에서 스타일링은 `Style` 객체를 통해 이루어집니다. 각 요소가 DataTable의 열에 해당하는 배열을 만들겠습니다.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Why a style array?** `ImportDataTable`에 배열을 전달하면 한 번의 호출로 각 열에 개별 스타일을 적용할 수 있어 간결하고 성능도 좋습니다. 또한 서식이 데이터 순서와 동기화된 상태를 보장합니다.

---

## 단계 4: 스타일을 적용하면서 DataTable 가져오기

이것이 작업의 핵심입니다: `DataTable`을 워크시트에 넣고, Aspose에 헤더 행을 포함하도록 지시한 뒤, `columnStyles` 배열을 전달합니다.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **What happens under the hood?** Aspose는 각 열을 순회하면서 헤더를 쓰고, 이어서 각 행 값을 씁니다. 이 과정에서 배열에 있는 해당 `Style`을 적용하므로 “Product”는 파란색 헤더, “Quantity”는 노란색 배경, “Revenue”는 깔끔하게 서식이 지정된 열이 됩니다.

---

## 단계 5: 워크북을 XLSX 파일로 저장하기

마지막으로 워크북을 디스크에 저장합니다. `Save` 메서드는 파일 확장자를 기반으로 자동으로 XLSX 형식을 선택합니다.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** 파일을 스트리밍해야 하는 경우(예: 웹 API) 파일 경로 대신 `workbook.Save(stream, SaveFormat.Xlsx)`를 사용하세요.

---

## 전체 작업 예제

아래는 새 콘솔 프로젝트에 붙여넣을 수 있는 전체 프로그램입니다. 그대로 컴파일 및 실행되어 스타일이 적용된 Excel 파일을 생성합니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### 예상 결과

`DataTableWithStyleArray.xlsx`를 열면 다음과 같이 표시됩니다:

| **Product** (파란색, 굵게) | **Quantity** (연노란색) | **Revenue** (통화) |
|----------------------------|--------------------------|--------------------|
| Widget A                   | 120                      | $3,450.75          |
| Widget B                   | 85                       | $2,190.00          |
| Widget C                   | 60                       | $1,580.40          |

지정한 **custom number format excel**(`$#,##0.00`)은 모든 revenue 셀에 달러 기호와 천 단위 구분 기호, 소수점 두 자리 표시를 보장합니다—재무 팀이 기대하는 바로 그 형식입니다.

---

## 자주 묻는 질문 및 엣지 케이스

### 다른 Excel 라이브러리와 함께 사용할 수 있나요?

물론 가능합니다. 열마다 스타일을 생성하고 가져오기 중에 적용하는 개념은 EPPlus, ClosedXML, NPOI에도 적용됩니다. API 호출은 다르지만 패턴은 동일합니다.

### DataTable에 스타일보다 더 많은 열이 있으면 어떻게 되나요?

Aspose는 `columnStyles` 배열에 매칭되는 항목이 없는 열에 기본 스타일을 적용합니다. 예기치 않은 상황을 방지하려면 배열 크기를 `dataTable.Columns.Count`와 맞추거나 루프에서 동적으로 스타일을 생성하세요.

### 날짜에 대한 맞춤 숫자 형식을 어떻게 설정하나요?

`style.Custom = "dd‑mm‑yyyy"`(또는 유효한 Excel 형식 문자열)로 설정하면 됩니다. 동일한 배열 기반 접근 방식은 날짜, 백분율, 과학적 표기에도 적용됩니다.

### 가져온 후 열 자동 크기 조정 방법이 있나요?

네—가져온 후 `worksheet.AutoFitColumns();`를 호출하면 됩니다. 셀 내용에 기반해 빠르게 너비를 계산합니다.

### 대용량 데이터 세트(100k+ 행)는 어떻게 처리하나요?

`ImportDataTable`은 대량 작업에 최적화되어 있지만 메모리 한계에 도달할 수 있습니다. 이 경우 `Cells[i, j].PutValue(...)`로 행을 수동 스트리밍하고, 하나의 `Style` 객체를 재사용하여 오버헤드를 줄이는 방식을 고려하세요.

---

## 전문가 팁 및 흔히 발생하는 실수

- **Avoid hard‑coding paths**: 프로덕션 코드에서 경로를 하드코딩하지 말고 `Environment.GetFolderPath` 또는 설정을 사용하세요.  
- **Dispose of the workbook**: 장기 실행 서비스에서는 `using` 블록으로 감싸 네이티브 리소스를 해제하세요.  
- **Watch out for culture‑specific separators**: 맞춤 형식 `$#,##0.00`은 OS 로케일에 관계없이 소수점 구분자로 마침표를 강제합니다. 이는 재무 보고서에 일반적으로 원하는 동작입니다.  
- **Remember to reference System.Drawing**: 스타일링에 사용되는 색상 구조체를 위해 `System.Drawing`(또는 .NET Core에서는 `System.Drawing.Common`)을 참조하세요.  
- **Test the output on different Excel versions**: 오래된 Excel 버전은 일부 맞춤 형식을 약간 다르게 해석할 수 있으니 테스트하세요.

---

## 결론

우리는 C#에서 **custom number format excel** 파일을 다루는 모든 과정을 다루었습니다: `DataTable`에서 데이터를 가져오고, **import datatable to excel**를 수행하며, **set column background color**를 적용하고, **format column as currency**를 사용한 뒤, 마지막으로 **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}