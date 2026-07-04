---
category: general
date: 2026-07-03
description: C#를 사용해 데이터테이블을 Excel로 가져올 때 교차 행 색상을 적용하세요. C# 데이터테이블을 Excel로 내보내는 방법,
  스타일이 적용된 테이블을 저장하는 방법, 그리고 워크북 서식을 유지하는 방법을 배워보세요.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: ko
og_description: C#를 사용하여 Excel에서 교대 행 색상을 적용합니다. 이 튜토리얼에서는 데이터테이블을 Excel로 가져오는 방법,
  C# 데이터테이블을 Excel로 내보내는 방법, 그리고 서식이 적용된 워크북을 저장하는 방법을 보여줍니다.
og_title: C#로 Excel에서 교대 행 색상 적용하기 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: C#로 Excel에서 교차 행 색상 적용하기 – 완전 가이드
url: /ko/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 C#을 사용하여 교차 행 색상 적용 – 완전 가이드

C# `DataTable`을 Excel로 내보낼 때 **교차 행 색상 적용**이 필요했던 적 있나요? 당신만 그런 것이 아닙니다—개발자들은 스프레드시트를 수동으로 Excel을 만지지 않고도 깔끔하게 보이게 하는 방법을 지속적으로 묻습니다. 좋은 소식은? 몇 줄의 코드만으로 프로그래밍 방식으로 할 수 있다는 것입니다.

이 튜토리얼에서는 **import datatable to excel**을 단계별로 살펴보고, 스타일이 적용된 테이블로 **export c# datatable to excel**하는 방법을 보여드리며, 마지막으로 서식을 유지한 채 **save styled table excel**하는 방법을 설명합니다. 끝까지 읽으면 **save workbook with formatting**을 수행하여 클라이언트 회의에 바로 사용할 수 있는 파일을 만들 수 있습니다.

## 사전 요구 사항

- .NET 6.0 이상 (샘플은 .NET 6을 사용하지만 최신 버전이면 모두 동작합니다)
- Aspose.Cells for .NET (무료 체험 또는 라이선스 버전) – 이 라이브러리를 사용하면 스타일링이 매우 쉬워집니다
- `DataTable` 소스 (데이터베이스, CSV, 혹은 메모리 컬렉션에서 가져올 수 있음)

> **Pro tip:** 아직 Aspose.Cells가 없으시다면 `dotnet add package Aspose.Cells` 명령으로 NuGet에서 가져올 수 있습니다.

## 단계 1: 프로젝트 설정 및 데이터 로드

먼저 콘솔 앱(또는任意 C# 프로젝트)을 생성하고 필요한 `using` 문을 추가합니다. 그런 다음 데이터를 `DataTable`에 로드합니다. 예시를 위해 간단한 테이블을 즉석에서 생성합니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**왜 중요한가:** `DataTable`을 미리 준비하면 **import datatable to excel**을 한 번의 호출로 수행할 수 있어 셀을 일일이 삽입하는 수작업을 없앨 수 있습니다.

## 단계 2: 워크북 생성 및 교차 행 스타일 정의

이제 새로운 `Workbook`을 인스턴스화합니다. **apply alternating row colors**를 구현하는 핵심은 `ImportTableOptions.StyleArray`에 있습니다. 기본 제공되는 첫 두 스타일(보통 흰색과 연회색)을 사용하지만 나중에 원하는 대로 커스터마이즈할 수 있습니다.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**설명:** `ImportTableOptions`는 Aspose.Cells에 가져오기 중 각 행을 어떻게 처리할지 알려줍니다. 두 개의 항목으로 구성된 `StyleArray`를 제공하면 라이브러리가 자동으로 홀수 행은 첫 번째 스타일로, 짝수 행은 두 번째 스타일로 색칠합니다—바로 **apply alternating row colors**에 필요한 동작입니다.

## 단계 3: 워크시트에 DataTable 가져오기 (헤더 포함)

워크북과 스타일이 준비되었으니 이제 **import datatable to excel**을 수행합니다. `ImportDataTable` 메서드가 핵심 작업을 수행하는데, 컬럼 헤더를 작성하고, 스타일 배열을 적용하며, 데이터를 셀 A1부터 배치합니다.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**두 번째 인수에 `true`를 포함한 이유:** 메서드가 첫 번째 행에 컬럼 이름을 기록하도록 지정합니다. 이는 전문적인 보고서를 만들기 위해 필수적입니다.

## 단계 4: 테이블 미세 조정 (선택 사항이지만 유용함)

테이블의 열을 자동으로 맞추거나 필터 행을 추가하고 싶다면, 몇 줄의 추가 코드만으로 테이블을 더욱 돋보이게 할 수 있습니다.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

이러한 조정은 교차 색상에는 영향을 주지 않지만 **save styled table excel** 파일의 전반적인 사용자 경험을 향상시킵니다.

## 단계 5: 모든 서식을 유지하면서 워크북 저장

마지막으로 파일을 디스크에 저장합니다. `Save` 메서드는 설정한 모든 스타일을 보존하여 교차 행이 그대로 유지됩니다.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`StyledEmployees.xlsx`를 열면 행이 흰색과 연회색으로 교차되는 깔끔한 테이블을 확인할 수 있습니다—많은 사용자가 가독성을 위해 의존하는 시각적 표시와 정확히 일치합니다.

### 예상 출력

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- 행 1, 3 … → 흰색 배경  
- 행 2, 4 … → 연회색 배경  

이것이 전체 **save workbook with formatting** 과정입니다.

## 일반 질문 및 엣지 케이스

### DataTable에 수천 개의 행이 있는 경우는 어떻게 하나요?

`ImportDataTable` 메서드는 데이터를 효율적으로 스트리밍하지만, 매우 큰 테이블에서는 메모리 제한에 도달할 수 있습니다. 이런 경우에는 내보내기를 여러 워크시트로 나누거나 시작 행과 열을 지정할 수 있는 `ImportDataTable` 오버로드를 사용하는 것을 고려하세요.

### 기본 색상 대신 사용자 정의 색상을 사용할 수 있나요?

물론 가능합니다. `styleWhite`와 `styleGray`의 `ForegroundColor` 할당을 원하는 `System.Drawing.Color`로 교체하면 됩니다—예를 들어 파스텔 블루나 기업 브랜드 색상 등.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### 사용자가 나중에 행을 추가해도 교차 스타일이 유지되도록 하려면 어떻게 해야 하나요?

사용자가 파일을 수동으로 편집하면 원래 스타일 배열이 자동으로 확장되지 않습니다. 간단한 해결책은 가져온 후 범위를 Excel 테이블(`ListObject`)로 변환하는 것입니다. 그러면 Excel이 새로운 행에 대해 패턴을 반복합니다.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

이제 새 행이 추가되면 교차 색상이 자동으로 적용됩니다.

## 전체 작업 예제 (모든 단계 한 곳에 모음)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

프로그램을 실행하고 생성된 파일을 열면 교차 색상이 즉시 적용된 것을 확인할 수 있습니다—수동 포맷팅이 전혀 필요 없습니다.

## 결론

우리는 C#을 사용해 **import datatable to excel**할 때 **apply alternating row colors**를 적용하는 방법을 보여주었습니다. 이 과정은 **export c# datatable to excel**, **save styled table excel**, 그리고 바로 사용할 수 있을 정도로 전문적인 **save workbook with formatting**을 수행하는 모든 단계를 포함합니다.

다음 단계는? 두 스타일을 교체해 맞춤 테마를 시도하거나 범위를 Excel 테이블로 변환해 사용자가 정렬 및 필터링을 할 수 있게 하면서 색상 패턴을 유지해 보세요. 또한 `ConditionalFormattingCollection`을 활용한 조건부 서식을 탐색하면 보다 동적인 시각적 힌트를 제공할 수 있습니다.

특별한 상황이 있나요

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료에는 전체 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET을 사용해 DataTable을 Excel로 가져오는 방법 (단계별 가이드)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Aspose.Cells for .NET을 사용해 Excel에서 색상 및 배경 적용](/cells/english/net/formatting/colors-and-background/)
- [Aspose.Cells .NET을 사용해 Excel 테마 색상 자동화 및 효율적인 서식 지정](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}