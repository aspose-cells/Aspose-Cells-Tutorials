---
category: general
date: 2026-03-01
description: C#를 사용하여 서식이 포함된 데이터를 Excel에 가져오기. DataTable을 Excel에 가져오고 셀에 배경색을 추가하는
  방법을 몇 단계만에 배워보세요.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: ko
og_description: C#를 사용하여 서식이 포함된 데이터를 Excel에 가져오기. DataTable을 가져오고 셀에 배경색을 추가하는 방법을
  단계별로 안내합니다.
og_title: 서식이 포함된 데이터를 Excel로 가져오기 – C# 가이드
tags:
- C#
- Excel
- DataTable
- Formatting
title: C#를 사용하여 서식이 포함된 데이터를 Excel에 가져오기
url: /ko/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 서식이 포함된 데이터를 Excel에 가져오기

Excel 워크북에 **서식이 포함된 데이터를 가져오기**가 필요했지만 항상 평범하고 지루한 시트만 나오셨나요? 혼자만 그런 것이 아닙니다. 대부분의 개발자는 기본 가져오기 기능이 원본 데이터에서 정성 들여 설정한 모든 색상과 스타일을 제거한다는 것을 알게 되면서 이 벽에 부딪힙니다.

이 튜토리얼에서는 **DataTable을 Excel에 가져오기**와 동시에 **Excel 셀에 배경색을 추가하기**를 수행하는 완전하고 바로 실행 가능한 솔루션을 단계별로 살펴보겠습니다. 추가적인 후처리가 필요 없습니다—스프레드시트가 바로 원하는 형태로 표시됩니다.

## 배울 내용

- `DataTable`에 데이터를 가져오는 방법.
- 배경색을 포함하는 `Style` 객체 배열을 정의하는 방법.
- 해당 스타일을 사용해 `ImportDataTable`을 호출하여 가져오기 시 서식이 보존되도록 하는 방법.
- 콘솔 앱에 바로 넣어 실행할 수 있는 전체 실행 예제.
- 실제 프로젝트에서 활용할 수 있는 팁, 주의점, 변형 방법.

### 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET Framework 4.6+에서도 동작합니다).
- **GemBox.Spreadsheet** 라이브러리 (데모에는 무료 버전이면 충분합니다).
- C# 및 Excel 개념에 대한 기본적인 이해.

왜 GemBox인지 궁금하시다면, 스타일 배열을 받아들이는 한 줄짜리 `ImportDataTable` 메서드를 제공하기 때문입니다—루프를 작성하지 않고도 **서식이 포함된 데이터를 가져오기**에 정확히 필요한 기능입니다.

---

## 1단계: 프로젝트 설정 및 GemBox.Spreadsheet 추가

시작하려면 새 콘솔 앱을 생성합니다:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **팁:** 무료 버전은 워크시트당 150 k 셀로 제한되며, 데모에는 충분합니다. 제한에 도달하면 업그레이드하거나 EPPlus로 전환하세요, 다만 API가 약간 다르게 보일 수 있습니다.

## 2단계: 소스 데이터를 `DataTable`로 가져오기

먼저 필요한 것은 데이터베이스에서 일반적으로 가져오는 데이터를 모방한 `DataTable`입니다. 메모리에서 생성하는 작은 도우미 코드는 다음과 같습니다:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**왜 중요한가:** 데이터 가져오기를 별도 메서드로 분리하면 SQL, CSV, 웹 서비스 등 어떤 소스든 가져오기 로직을 건드리지 않고 교체할 수 있습니다. 이렇게 하면 코드가 깔끔해지고 튜토리얼 **DataTable을 Excel에 가져오는 방법**을 재사용할 수 있습니다.

## 3단계: 적용할 스타일 정의하기

이제 재미있는 부분입니다: 각각 고유한 `ForegroundColor`를 가진 `Style` 객체 배열을 만들겠습니다. GemBox에서는 `BackgroundPatternColor`(셀 채우기)와 `ForegroundColor`(텍스트 색) 를 설정할 수 있습니다. 이번 데모에서는 첫 두 열에 서로 다른 색을 적용합니다:

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**설명:**  
- `Style` 객체는 가벼운 컨테이너이며, 각 셀마다 새로 만들 필요가 없습니다.  
- 배열 순서를 열 순서와 맞추면 GemBox가 가져오기 시 자동으로 해당 스타일을 적용합니다.  
- 이것이 **서식이 포함된 데이터를 가져오기**의 핵심이며—서식이 데이터와 함께 이동하고, 가져온 뒤에 적용되는 것이 아닙니다.

## 4단계: 스타일과 함께 `DataTable`을 워크시트에 가져오기

데이터와 스타일이 준비되었으니 이제 워크북을 만들고, 첫 번째 워크시트를 선택한 뒤 `ImportDataTable`을 호출합니다. 메서드 시그니처는 다음과 같습니다:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

사용 예시는 다음과 같습니다:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**내부에서 무슨 일이 일어나나요?**  
- `true`는 GemBox에게 첫 번째 행에 열 이름을 기록하도록 지시합니다.  
- `0, 0`은 가져오기를 셀 A1에 위치시킵니다.  
- `importStyles`는 각 열을 앞서 정의한 색상과 연결합니다.  

*Report.xlsx*를 열면 **ID** 열은 연한 파란색, **Name** 열은 연한 초록색으로 색칠되고, **Score** 열은 기본 흰색 그대로임을 확인할 수 있습니다. 이것이 한 번의 호출로 **서식이 포함된 데이터를 가져오기**입니다.

## 5단계: 결과 확인하기 (예상 출력)

생성된 `Report.xlsx`를 열면 다음과 같은 모습이 나타납니다:

| ID (연한 파란색) | Name (연한 초록색) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- **ID** 열 셀은 연한 파란색 배경을 가지고 있습니다.  
- **Name** 열 셀은 연한 초록색 배경을 가지고 있습니다.  
- **Score** 열은 기본 흰색 배경을 유지합니다.

![Excel sheet showing import data with formatting – ID column light blue, Name column light green](excel-screenshot.png "서식이 포함된 데이터 가져오기 예시")

*이미지 alt 텍스트에는 SEO를 위한 주요 키워드가 포함됩니다.*

## 일반적인 질문 및 엣지 케이스

### 배경색 외에도 다른 서식을 적용할 수 있나요?

물론 가능합니다. `Style`을 사용하면 글꼴, 테두리, 숫자 형식, 심지어 조건부 서식까지 설정할 수 있습니다. 예를 들어, 점수가 90점 이상인 경우 굵게 빨간색으로 표시하려면:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### DataTable에 스타일보다 더 많은 열이 있으면 어떻게 되나요?

GemBox는 배열에 매칭되는 항목이 있는 열에만 스타일을 적용합니다. 추가 열은 기본 스타일을 사용하며 오류가 발생하지 않습니다.

### 대용량 데이터셋에서도 작동하나요?

예, 하지만 무료 버전의 셀 제한(150 k 셀)을 유의하세요. 대규모 보고서의 경우 유료 라이선스를 고려하거나 `worksheet.Cells[row, col].Value = …`와 같이 행‑열 단위로 데이터를 스트리밍할 수 있지만, 한 줄 호출의 편리함은 사라집니다.

### 기존 Excel 템플릿에서 서식이 포함된 데이터를 가져오려면 어떻게 해야 하나요?

먼저 템플릿 워크북을 로드할 수 있습니다:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

이를 통해 헤더 로고, 푸터 및 기존 스타일을 유지하면서 동적 부분에 대해서는 **서식이 포함된 데이터를 가져오기**를 수행할 수 있습니다.

## 전체 작업 예제 (복사‑붙여넣기 준비 완료)

다음은 전체 코드 예제입니다:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

프로그램을 실행(`dotnet run`)하고 생성된 *Report.xlsx*를 열면 색상이 즉시 적용된 것을 확인할 수 있습니다.

## 결론

이제 견고하고 완전한, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}