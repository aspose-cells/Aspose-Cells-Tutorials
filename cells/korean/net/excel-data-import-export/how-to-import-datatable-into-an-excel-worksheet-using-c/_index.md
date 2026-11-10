---
category: general
date: 2026-10-26
description: C#와 Aspose.Cells를 사용하여 DataTable을 Excel 워크시트에 가져오고, 스타일과 헤더를 유지하면서 몇
  줄의 코드만으로 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: ko
lastmod: 2026-10-26
og_description: C#와 Aspose.Cells를 사용하여 DataTable을 Excel 워크시트에 가져오는 방법. 스타일, 헤더 및 서식을
  보존하는 전체 가이드를 확인하세요.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: DataTable을 Excel 워크시트에 가져오는 방법 – C# 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C#를 사용하여 DataTable을 Excel 워크시트에 가져오는 방법
url: /ko/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 DataTable을 Excel 워크시트에 가져오는 방법

Excel 워크시트에 **DataTable을 가져오는 방법**이 필요하다면, 이 가이드는 C#에서 정확한 단계들을 보여줍니다. 보고서 엔진을 구축하거나 그리드 데이터를 내보낼 때, Aspose.Cells를 사용해 열 헤더와 셀 스타일을 그대로 유지하는 방법을 확인할 수 있습니다. 이 솔루션은 .NET 6+에서 동작하며 몇 줄의 코드만 필요합니다.

DataTable을 가져오는 것은 스프레드시트를 다룰 때 흔히 하는 작업이지만, 개발자들은 스타일 전송을 활성화하거나 헤더 플래그를 올바르게 전달하는 것을 종종 놓칩니다. 이 튜토리얼에서는 **ImportTableOptions**를 구성하고, **ImportDataTableStyle**을 켜며, `ImportDataTable`을 안전하게 호출하는 방법을 배웁니다. 마지막에는 어떤 C# 프로젝트에든 바로 넣어 사용할 수 있는 메서드를 얻게 됩니다.

## 사전 요구 사항

시작하기 전에 다음을 확인하세요:

* .NET 6 SDK 이상이 설치되어 있어야 합니다.
* **Aspose.Cells for .NET** 라이선스 사본(무료 체험판도 테스트에 사용 가능)
* `DataTable` 및 Excel 개념에 대한 기본 이해
* Visual Studio 2022와 같은 IDE(또는 C#를 지원하는 편집기)

`Aspose.Cells` 외에 추가 NuGet 패키지는 필요하지 않습니다.

## 1단계: 소스 데이터를 DataTable에 가져오기

**DataTable을 가져오는 방법**을 답하기 위해 가장 먼저 해야 할 일은 데이터를 준비하는 것입니다. 실제 상황에서는 `DataTable`이 데이터베이스 쿼리, CSV 파서, 혹은 메모리 컬렉션에서 온다. 아래는 몇 개의 행을 가진 테이블을 만드는 최소 예시입니다:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*왜 중요한가*: 먼저 `DataTable`을 구성하면 열 순서, 데이터 형식, 헤더 이름을 제어할 수 있으며, 이후 Excel 워크시트로 가져올 때 이 모든 정보가 보존됩니다.

## 2단계: ImportTableOptions 생성 및 스타일 가져오기 활성화

**DataTable을 가져오는 방법**에 대한 다음 결정은 소스 `DataTable`에 이미 정의된 시각적 스타일(폰트, 색상, 테두리)을 유지할지 여부입니다. Aspose.Cells는 세밀한 제어를 위해 `ImportTableOptions` 클래스를 제공합니다. `ImportDataTableStyle = true`로 설정하면 스타일 정보가 대상 워크시트에 복사됩니다.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*왜 중요한가*: `ImportDataTableStyle`을 활성화하지 않으면 가져온 셀은 기본 워크시트 스타일을 사용하게 되어, `DataTable`에 적용한 사용자 정의 서식이 사라집니다. 이 플래그는 깔끔한 내보내기에 필수입니다.

## 3단계: 헤더 포함하여 DataTable을 워크시트에 가져오기

이제 **DataTable을 가져오는 방법**에 대한 모든 준비가 끝났습니다. 워크북을 만들고, 워크시트를 선택한 뒤 `ImportDataTable`을 호출합니다. 메서드의 두 번째 인수(`true`)는 Aspose.Cells에게 첫 번째 행에 열 헤더를 기록하도록 지시합니다.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

`ExportDataTableToExcel("Employees.xlsx")`를 실행하면 `Employees.xlsx` 파일이 생성되고, 첫 번째 행에 **Id**, **Name**, **Department**가 들어가며 각 셀은 원본 `DataTable`에 정의된 스타일을 그대로 유지합니다.

### 전체 실행 가능한 예제

아래는 **DataTable을 가져오는 방법**을 보여주는 완전하고 독립적인 콘솔 프로그램입니다. 새 콘솔 프로젝트에 복사‑붙여넣기하고 실행하면 됩니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**예상 출력**  
`Employees.xlsx`를 열면 다음과 같이 표시됩니다:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

모든 셀은 기본 DataTable 스타일(폰트, 정렬)을 유지합니다. 가져오기 전에 `DataTable`에 사용자 정의 스타일을 적용했다면, `ImportDataTableStyle`이 `true`로 설정되어 있기 때문에 워크시트에서도 동일하게 나타납니다.

## 일반적인 함정 및 모범 사례

| 문제 | 발생 원인 | 회피 방법 |
|------|----------|-----------|
| **헤더가 누락됨** | `ImportDataTable`의 두 번째 인수를 `false`로 전달 | 헤더가 필요하면 항상 `true`를 사용하거나, 가져오기 전에 직접 작성 |
| **스타일이 전송되지 않음** | `ImportDataTableStyle`을 활성화하지 않음 | `ImportTableOptions`에서 `ImportDataTableStyle = true` 설정 |
| **대용량 테이블로 성능 저하** | 페이지 처리 없이 수백만 행을 한 번에 가져옴 | 배치로 가져오거나 `startRow` 오버로드를 사용해 스트리밍 |
| **워크시트 참조 오류** | 시트가 하나뿐인데 `workbook.Worksheets[1]` 사용 | `workbook.Worksheets[0]` 사용하거나 `workbook.Worksheets.Add()`로 새 시트 생성 |
| **라이선스 만료** | Aspose.Cells 체험판이 30일 후 워터마크 표시 | `License license = new License(); license.SetLicense("Aspose.Cells.lic");`로 유효한 라이선스 적용 |

**프로 팁**: 가져온 후 사용자 정의 테마를 적용하려면 `ws.Cells.ApplyStyle(style)`을 호출하세요. 여기서 `style`은 한 번 구성하고 여러 행에 재사용할 `Style` 객체입니다.

## 솔루션 확장하기

이제 **DataTable을 가져오는 방법**을 알았으니 다음 시나리오를 탐색해 볼 수 있습니다:

* **여러 테이블 가져오기** – 다른 워크시트에 반복해서 가져오기
* **조건부 서식** – 가져온 뒤 `ws.Cells.ApplyConditionalFormatting`으로 규칙 추가
* **CSV로 내보내기** – 순수 텍스트 형식이 필요하면 `workbook.Save("file.csv", SaveFormat.Csv)` 사용
* **DataTable로 다시 읽어오기** – `ws.Cells.ExportDataTable`로 왕복 무결성 검증

이 모든 확장은 위에서 보여준 핵심 패턴(데이터 가져오기, 옵션 구성, 단일 Aspose.Cells 메서드 호출)을 기반으로 합니다.

## 결론

이제 C#를 사용해 **DataTable을 Excel 워크시트에 가져오는 방법**에 대한 완전하고 프로덕션 수준의 답변을 갖추었습니다. 튜토리얼에서는 소스 데이터 가져오기, `ImportTableOptions`에 `ImportDataTableStyle` 설정, `ImportDataTable` 호출 순서를 다루었습니다. 샘플 코드를 따라 하면 헤더와 스타일이 자동으로 보존되며, 더 큰 데이터셋, 다중 시트, 추가 서식 요구 사항에도 이 패턴을 적용할 수 있습니다.

보고서 자동화를 시작할 준비가 되셨나요? 샘플 `DataTable`을 실제 데이터베이스 쿼리로 교체하고, 사용자 정의 셀 스타일을 실험하며, 기존 서비스 레이어에 메서드를 통합해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 단계별 코드 예제와 상세 설명을 제공합니다.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}