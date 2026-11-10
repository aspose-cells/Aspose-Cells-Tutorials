---
category: general
date: 2026-10-26
description: ExportAsStrin을 사용할 때 Custom ExportTableOptions를 사용하면 C#에서 Excel 데이터를
  문자열로 내보낼 수 있습니다. 내보내기를 구성하고 실행하는 단계별 가이드를 따라보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: ko
lastmod: 2026-10-26
og_description: ExportAsStrin이 문자열 전용 Excel 내보내기를 활성화할 때 사용자 지정 ExportTableOptions.
  C#에서 내보내기를 구성하고 실행하는 정확한 단계들을 알아보세요.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: ExportAsString일 때 사용자 지정 ExportTableOptions – C#에서 Excel을 문자열로 내보내기
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel에서 ExportAsString을 사용할 때 사용자 정의 ExportTableOptions
url: /ko/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – C#에서 Excel을 문자열로 내보내기

만약 **Custom ExportTableOptions when ExportAsStrin**을 사용하여 모든 셀 값을 순수 문자열로 가져와야 한다면, 이 가이드는 정확히 어떻게 하는지 보여줍니다. 데이터 가져오기 파이프라인을 구축하거나 깔끔한 CSV 준비 덤프가 필요할 때, 이렇게 옵션을 구성하면 타입 변환에 대한 놀라움을 방지할 수 있다는 것을 알게 될 것입니다.

이 튜토리얼에서는 Aspose.Cells 라이브러리를 사용하여 **how to export excel as string**을 배우고, 완전하고 실행 가능한 코드를 확인하며, 각 설정 뒤에 있는 이유를 이해하게 됩니다. 외부 문서는 필요하지 않습니다 – 필요한 모든 것이 여기 있습니다.

## Prerequisites

* .NET 6.0 SDK 또는 이후 버전이 설치되어 있어야 합니다  
* Visual Studio 2022 (또는 .NET을 지원하는 IDE)  
* Aspose.Cells for .NET 패키지 (NuGet을 통해 설치: `Install-Package Aspose.Cells`)  
* 프로젝트 루트 폴더에 배치된 Excel 워크북 (`sample.xlsx`)  

이 항목들만 의존성이며, 코드는 추가 라이브러리 없이 Windows, Linux, macOS에서 실행됩니다.

## Step 1: Load the workbook you want to export

**Custom ExportTableOptions when ExportAsStrin**을 사용할 때 가장 먼저 해야 할 일은 로드된 워크북에서 `Worksheet` 객체를 가져오는 것입니다. 이 객체를 통해 행, 열 및 내보내기 API에 접근할 수 있습니다.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*왜 중요한가:*  
`Workbook`은 파일을 한 번 읽고 모든 서식 정보를 메모리에 보관합니다. 특정 `Worksheet`를 선택함으로써 내보내기 범위를 제한하고 숨겨진 시트의 불필요한 처리를 방지할 수 있습니다.

## Step 2: Configure ExportTableOptions with ExportAsString = true

**Custom ExportTableOptions when ExportAsStrin**의 핵심은 `ExportTableOptions` 객체입니다. `ExportAsString`을 설정하면 원래 데이터 유형(날짜, 숫자, 불리언 등)에 관계없이 모든 셀을 문자열로 처리하도록 내보내기가 강제됩니다. `PreserveFormatting`을 활성화하면 결과 문자열에 시각적 스타일(예: 통화 기호)이 유지됩니다.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*왜 중요한가:*  
나중에 `ExportDataTable`을 호출하면 라이브러리는 일반적으로 각 열의 .NET 타입을 추론합니다. `ExportAsString = true`이면 이 추론 단계가 생략되어, 다운스트림 CSV 파서가 깨질 수 있는 예기치 않은 `DateTime` 또는 `double` 변환을 방지합니다.

## Step 3: Export a range to a DataTable using the custom options

이제 워크시트에서 직사각형 범위(행 0‑9, 열 0‑4)를 내보낼 수 있습니다. 이 메서드는 모든 필드가 `string`인 `DataTable`을 반환합니다.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*왜 중요한가:*  
`ExportDataTable`은 Excel 데이터를 많은 .NET API가 이미 이해하는 관계형 구조(예: Entity Framework, Dapper)로 이동시키는 가장 편리한 방법입니다. **Custom ExportTableOptions when ExportAsStrin**을 전달함으로써 각 `DataColumn.DataType`이 `typeof(string)`임을 보장합니다.

## Step 4: Verify the result – all values are strings

내보내기가 기대대로 동작했는지 확인하는 것이 좋은 습관입니다. 다음 루프는 각 셀과 해당 런타임 타입을 출력합니다.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**예상 출력**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

각 셀은 타입이 `String`임을 표시하여 **Custom ExportTableOptions when ExportAsStrin**이 올바르게 작동했음을 확인합니다.

## Step 5: Optional – write the DataTable to CSV

궁극적인 목표가 순수 텍스트 파일이라면 `DataTable`을 CSV로 쉽게 직렬화할 수 있습니다:



## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 보여준 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 완전한 동작 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}