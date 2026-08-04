---
category: general
date: 2026-02-09
description: C#에서 연한 파란색 배경을 가진 워크북을 만들고 헤더와 함께 데이터를 가져오는 방법. 연한 파란색 배경을 추가하고 기본 Excel
  스타일을 사용하며 DataTable을 가져오는 방법을 배웁니다.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: ko
og_description: C#에서 연한 파란색 배경의 워크북을 만들고, 헤더가 포함된 데이터를 가져오며, 기본 Excel 스타일을 적용하는 방법—한
  번에 간결하게 안내합니다.
og_title: 워크북 만들기 방법 – 연한 파란색 배경, 데이터 가져오기
tags:
- C#
- Excel
- Aspose.Cells
title: 워크북 만들기 – 연한 파란색 배경, 데이터 가져오기
url: /ko/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크북 만들기 – 연한 파란색 배경, 데이터 가져오기

박스에서 바로 꺼냈을 때 조금 더 예쁘게 보이는 **how to create workbook**을 C#에서 만든 적이 있나요? 데이터베이스에서 `DataTable`을 가져왔는데 기본 흰색 셀에 지치셨다면 이번 튜토리얼에서 새 워크북을 만들고, 열에 연한 파란색 배경을 추가하며, 헤더와 함께 데이터를 가져오는 과정을 기본 Excel 스타일을 사용하면서 단계별로 안내합니다.

또한 null 값을 처리하거나 여러 열을 동시에 커스터마이징하는 등 몇 가지 “what‑if” 시나리오도 함께 살펴볼 것입니다. 최종적으로는 사후 처리 없이 이해관계자에게 바로 전달할 수 있는 완전 스타일이 적용된 Excel 파일을 얻게 됩니다.

## Prerequisites

시작하기 전에 아래 항목들을 준비하세요:

* **.NET 6+** (코드는 .NET Framework 4.6+에서도 동작합니다)  
* **Aspose.Cells for .NET** – `Workbook`, `Style`, `ImportDataTable` 호출을 지원하는 라이브러리입니다. NuGet을 통해 설치하세요:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* `DataTable` 소스 – 예제에서는 가짜 데이터를 만들겠지만, 실제로는 ADO.NET 쿼리로 대체할 수 있습니다.

준비되셨나요? 이제 시작합니다.

## Step 1: Initialize a New Workbook (Primary Keyword)

첫 번째로 해야 할 일은 **how to create workbook**—그대로 워크북을 초기화하는 것입니다. `Workbook` 클래스는 전체 Excel 파일을 나타내며, 생성자를 호출하면 빈 상태의 파일이 생성됩니다.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **왜 중요한가:** 새 `Workbook`으로 시작하면 처음부터 모든 스타일을 직접 제어할 수 있습니다. 기존 파일을 열 경우 원본 작성자가 남긴 스타일을 그대로 물려받게 되어 포맷이 일관되지 않을 수 있습니다.

## Step 2: Prepare the DataTable You’ll Import

예시를 위해 간단한 `DataTable`을 만들어 보겠습니다. 실제 상황에서는 저장 프로시저를 호출하거나 ORM 메서드를 사용하게 될 것입니다.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **팁:** 데이터베이스에 나타나는 컬럼 순서를 정확히 유지하려면 `ImportDataTable`의 `importColumnNames` 매개변수를 `true`로 설정하세요. 이렇게 하면 Aspose.Cells가 자동으로 컬럼 헤더를 작성합니다.

## Step 3: Define Column Styles – Default + Light‑Blue Background

이제 퍼즐의 **add light blue background** 부분을 해결합니다. Aspose.Cells에서는 각 열에 대응하는 `Style` 객체 배열을 전달할 수 있습니다. 첫 번째 항목은 열 0의 스타일, 두 번째는 열 1의 스타일이며, 이렇게 순서대로 매핑됩니다. 스타일 개수가 열보다 적으면 남은 열은 기본 스타일을 사용합니다.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **왜 스타일이 두 개만 있나요?** 예제에서는 네 개의 열이 있지만, 두 번째 열(Name)만 강조하고 싶었습니다. 배열 길이가 컬럼 수와 일치할 필요는 없으며, 누락된 항목은 자동으로 워크북의 기본 스타일을 상속받습니다.

## Step 4: Import the DataTable with Headers and Styles

여기서 **excel import datatable c#**와 **import data with headers**를 결합합니다. `ImportDataTable` 메서드는 컬럼 이름, 행 데이터를 쓰고, 앞서 만든 스타일 배열을 적용하는 역할을 합니다.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Expected Result

프로그램을 실행하면 `workbook`에 아래와 같은 단일 워크시트가 생성됩니다:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* **Name** 열은 연한 파란색 배경이 적용되어 스타일 배열이 정상 작동함을 확인할 수 있습니다.  
* `importColumnNames`를 `true`로 전달했기 때문에 컬럼 헤더가 자동으로 생성됩니다.  
* Null 값은 빈 셀로 표시되며, 이는 Aspose.Cells의 기본 동작입니다.

## Step 5: Save the Workbook (Optional but Useful)

파일을 디스크에 저장하거나 웹 클라이언트에 스트리밍하려면 저장 로직을 사용하면 됩니다:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **프로 팁:** 오래된 Excel 버전을 대상으로 할 경우 `SaveFormat.Xlsx`를 `SaveFormat.Xls`로 변경하면 됩니다. API가 자동으로 변환을 처리합니다.

## Edge Cases & Variations

### Multiple Styled Columns

여러 열에 스타일을 적용하려면 `columnStyles` 배열을 확장하면 됩니다:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

이제 **Name**과 **Salary** 두 열 모두 연한 파란색 배경이 적용됩니다.

### Conditional Formatting Instead of Fixed Styles

값이 특정 임계값을 초과하면 열을 빨간색으로 표시하고 싶다면, **use default style excel**과 조건부 서식을 결합합니다:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importing Without Headers

다운스트림 시스템이 자체 헤더를 제공한다면 `importColumnNames` 인수를 `false`로 전달하면 됩니다. 데이터는 `A1`부터 시작되며, 이후에 사용자 정의 헤더를 직접 작성할 수 있습니다.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}