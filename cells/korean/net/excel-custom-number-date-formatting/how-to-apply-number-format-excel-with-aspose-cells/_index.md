---
category: general
date: 2026-10-10
description: DataTable을 가져와 날짜와 통화 형식을 지정하고 헤더 행을 유지하면서 Excel에서 숫자 서식을 한 번에 빠르게 적용합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: ko
lastmod: 2026-10-10
og_description: Aspose.Cells를 사용하여 C#에서 Excel 숫자 서식을 적용합니다. Excel 날짜 서식 설정, 통화 서식
  설정, DataTable을 가져올 때 헤더 행을 유지하는 방법을 배워보세요.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: C#에서 Excel 숫자 서식 적용 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Aspose.Cells를 사용하여 Excel에 숫자 형식 적용하는 방법
url: /ko/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 Excel에서 숫자 서식 적용하기

`DataTable`에서 데이터를 로드하면서 **apply number format excel**을 적용해야 하는 경우, 이 가이드는 정확한 방법을 보여줍니다. 또한 **set date format excel**, **set currency format excel**, 그리고 가져오기 중 **preserve header row excel**을 설정하는 방법도 배울 수 있어, 결과 워크시트가 별도의 후처리 없이도 전문적으로 보입니다.

라이브러리 설치부터 완전한 실행 가능한 코드 스니펫 작성까지 모두 다룹니다. 끝까지 읽으면 `DataTable`을 Excel 워크북으로 가져오고, 숫자 열을 자동으로 서식 지정하며, 헤더 행을 그대로 유지하는 작업을 몇 줄의 C# 코드만으로 수행할 수 있습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* .NET 6.0 이상 (.NET Framework 4.6+에서도 동작)
* Visual Studio 2022 (또는 선호하는 C# IDE)
* **Aspose.Cells for .NET** – NuGet을 통해 설치:

```bash
dotnet add package Aspose.Cells
```

* `DataTable` 소스 – 예제에서는 샘플 데이터를 반환하는 헬퍼 메서드 `GetTable()`을 사용합니다.

> **Pro tip:** Aspose.Cells는 상용 라이브러리이지만, 최대 30일 동안 워터마크가 비활성화되는 무료 평가 모드를 제공합니다.

## Step 1: Create a workbook and access the first worksheet

워크북 객체는 모든 Excel 작업의 진입점입니다. 새 워크북을 만들면 인덱스 0에 기본 워크시트가 자동으로 생성됩니다.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Why this step?*  
`Workbook`은 파일 형식, 계산 엔진, 스타일 저장소를 관리합니다. `Worksheet`에 먼저 접근하면 이후 가져오기 메서드에 대상 시트를 전달하기가 쉬워집니다.

## Step 2: Retrieve the source data as a DataTable

실제 프로젝트에서는 데이터가 데이터베이스 쿼리, CSV 파서, 혹은 API 응답에서 오는 경우가 많습니다. 여기서는 **Product**, **Price**, **ReleaseDate**라는 세 컬럼을 가진 간단한 `DataTable`을 생성합니다.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Why this step?*  
`DataTable`은 Aspose.Cells가 직접 가져올 수 있는 메모리 내 표 형식이며, 컬럼 순서와 데이터 형식을 그대로 유지합니다.

## Step 3: Prepare a `Style` array – one style per column

Aspose.Cells는 `Style` 객체 배열을 전달함으로써 가져오기 시 각 컬럼에 별도 스타일을 적용할 수 있습니다. 배열 길이는 소스 테이블의 컬럼 수와 일치해야 합니다.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Why this step?*  
명시적으로 `CreateStyle()`을 호출하지 않으면 `Number` 속성을 설정할 때 `NullReferenceException`이 발생합니다. 각 `Style`을 초기화하면 이후 할당이 정상적으로 동작합니다.

## Step 4: Assign number formats – currency and date

Excel은 내장 숫자 서식을 ID로 식별합니다.  
* **14** – 통화 (예: `$1,234.00`)  
* **22** – 짧은 날짜 (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Note:** 사용자 정의 서식이 필요할 경우(예: `"¥#,##0.00"`), 내장 ID 대신 `Style.Custom = "¥#,##0.00"`를 사용하세요.

*Why this step?*  
가져오기 시점에 올바른 **number format**을 적용하면 셀을 일일이 순회하며 서식을 바꾸는 두 번째 과정을 생략할 수 있습니다. 또한 **format excel cells date**와 **set currency format excel**이 모든 행에 일관되게 적용됩니다.

## Step 5: Import the DataTable while preserving the header row

`ImportDataTable` 메서드는 데이터를 복사하면서 첫 번째 행을 헤더로 유지하고, 앞서 준비한 컬럼 스타일을 적용할 수 있습니다.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Expected output** – `FormattedReport.xlsx`를 열면 다음과 같이 표시됩니다:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

헤더 행은 그대로 유지되고, **Price** 컬럼에는 통화 기호가, **ReleaseDate** 컬럼에는 짧은 날짜 서식이 적용됩니다—추가 스타일 코드를 작성할 필요가 없습니다.

### Handling common edge cases

| Situation                               | Solution |
|----------------------------------------|----------|
| **More columns than styles**           | `columnStyles.Length`가 `sourceTable.Columns.Count`와 동일하도록 확인하세요. 누락된 항목은 워크북의 기본 스타일이 적용됩니다. |
| **Null values in numeric columns**     | Excel은 `null`을 빈 셀로 처리합니다; 이후 값이 입력되면 숫자 서식이 그대로 적용됩니다. |
| **Custom locale‑specific currency**    | `columnStyles[i].Custom = "\"€\"#,##0.00"`와 `columnStyles[i].Number = -1`을 설정해 내장 ID를 비활성화합니다. |
| **Large tables ( > 100 000 rows )**    | 메모리 부담을 줄이기 위해 `ImportDataTable` 오버로드와 `ImportTableOptions`를 사용해 스트리밍 방식으로 데이터를 가져오는 것을 고려하세요. |
| **Applying the same style to multiple columns** | 배열에 동일 `Style` 인스턴스를 재사용합니다(예: `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Using a custom format string

내장 ID가 요구 사항을 충족하지 못한다면, 사용자 정의 숫자 서식을 정의할 수 있습니다:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

이 방법을 사용하면 **format excel cells date**와 **set currency format excel**을 미리 정의된 ID를 넘어 자유롭게 제어할 수 있습니다.

## Conclusion

이제 Aspose.Cells를 이용해 `DataTable`을 가져올 때 **apply number format excel**을 효율적으로 적용하는 방법을 알게 되었습니다. 컬럼별 `Style` 배열을 만들고, 내장 또는 사용자 정의 숫자 ID를 할당한 뒤, **preserve header row excel** 옵션이 포함된 `ImportDataTable` 오버로드를 사용하면 단 한 번의 작업으로 바로 배포 가능한 워크시트를 생성할 수 있습니다.

### What’s next?

* `"dddd, mmmm dd, yyyy"`와 같은 사용자 정의 패턴으로 **set date format excel**을 탐색해 보세요.  
* **conditional formatting**과 결합해 범위를 벗어난 값을 강조 표시하세요.  
* 피벗 테이블이나 차트에서 **format excel cells date**를 활용해 동적 보고서를 만들세요.

다양한 숫자 ID나 사용자 정의 문자열을 실험해 보면서 조직의 스타일 가이드에 맞는 서식을 적용해 보시기 바랍니다. Happy coding!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 관련 주제를 심도 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하므로, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}