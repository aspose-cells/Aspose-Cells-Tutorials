---
category: general
date: 2026-08-11
description: C#에서 DataTable을 사용해 엑셀 시트를 생성하고 자동 시트 이름 지정으로 DataTable을 엑셀로 내보냅니다. DataTable에
  행을 추가하는 방법과 워크북을 xlsx 형식으로 저장하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: ko
lastmod: 2026-08-11
og_description: C#에서 DataTable을 사용해 Excel 시트를 생성합니다. 이 튜토리얼에서는 DataTable을 Excel로 내보내는
  방법, DataTable에 행을 추가하는 방법, 여러 개의 Excel 시트를 생성하고 워크북을 xlsx 형식으로 저장하는 방법을 보여줍니다.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: C#에서 DataTable을 사용해 엑셀 시트 만들기 – 전체 프로그래밍 가이드
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: C#에서 DataTable을 사용해 엑셀 시트 만들기 – 단계별 가이드
url: /ko/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 DataTable을 사용해 Excel 시트 만들기 – 단계별 가이드

If you need to **create excel sheet** from a `DataTable` in C#, this guide shows you exactly how to do it. You’ll see how to **export datatable to excel**, add rows, handle duplicate sheet names, and finally **save workbook as xlsx**.

C#에서 `DataTable`을 사용해 **excel sheet**을 만들어야 한다면, 이 가이드는 정확한 방법을 보여줍니다. **export datatable to excel** 방법, 행 추가, 중복 시트 이름 처리, 그리고 마지막으로 **save workbook as xlsx** 방법을 확인할 수 있습니다.

The example uses Aspose.Cells, a widely‑used .NET library for Excel automation. The same concepts apply to other libraries that support SmartMarker‑style processing, but the code below works out‑of‑the‑box with Aspose.Cells 22.12 or later.

예제는 Excel 자동화를 위한 널리 사용되는 .NET 라이브러리인 Aspose.Cells를 사용합니다. 동일한 개념은 SmartMarker‑style 처리를 지원하는 다른 라이브러리에도 적용되지만, 아래 코드는 Aspose.Cells 22.12 이상에서 바로 사용할 수 있습니다.

## Prerequisites

## 사전 요구 사항

* .NET 6.0 SDK or later installed  
  * .NET 6.0 SDK 이상이 설치되어 있음
* A reference to the **Aspose.Cells** NuGet package (`Install-Package Aspose.Cells`)  
  * **Aspose.Cells** NuGet 패키지에 대한 참조(`Install-Package Aspose.Cells`)
* Basic familiarity with `DataTable` and C# console applications  
  * `DataTable` 및 C# 콘솔 애플리케이션에 대한 기본적인 이해

These requirements keep the tutorial self‑contained and avoid external tooling.

이 요구 사항은 튜토리얼을 독립적으로 유지하고 외부 도구 사용을 방지합니다.

## Step 1: Create a DataTable that will be exported to Excel

## 단계 1: Excel로 내보낼 DataTable 만들기

The first step is to build a `DataTable` that mirrors the data you want in the worksheet. Here we create a table named **Sheet1**, add an `Id` column, and insert two rows.

첫 번째 단계는 워크시트에 넣고 싶은 데이터를 반영하는 `DataTable`을 만드는 것입니다. 여기서는 **Sheet1**이라는 이름의 테이블을 만들고, `Id` 열을 추가한 뒤 두 개의 행을 삽입합니다.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Why this matters:**  
**왜 중요한가:**  

`DataTable` is a convenient in‑memory representation of tabular data. Naming the table `"Sheet1"` tells Aspose.Cells which sheet to target when processing SmartMarkers.

`DataTable`은 표 형식 데이터를 메모리 내에서 편리하게 표현한 것입니다. 테이블 이름을 `"Sheet1"`으로 지정하면 SmartMarkers를 처리할 때 Aspose.Cells가 대상 시트를 알 수 있습니다.

## Step 2: Add rows to the DataTable (optional expansion)

## 단계 2: DataTable에 행 추가 (선택적 확장)

If your source data is dynamic, you’ll often need to add rows in a loop. The following snippet demonstrates a typical pattern:

소스 데이터가 동적이라면, 루프에서 행을 추가해야 할 경우가 많습니다. 다음 코드 조각은 일반적인 패턴을 보여줍니다:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Tip:**  
**팁:**  

When adding many rows, consider disabling constraints (`dataTable.Constraints.Clear()`) to improve performance.

많은 행을 추가할 때는 성능 향상을 위해 제약 조건(`dataTable.Constraints.Clear()`)을 비활성화하는 것을 고려하세요.

## Step 3: Configure SmartMarker options to create multiple excel sheets automatically

## 단계 3: SmartMarker 옵션을 구성하여 여러 Excel 시트를 자동으로 만들기

SmartMarker options let you control how duplicate sheet names are handled. Setting `DetailSheetNewName` to `"Sheet1_{0}"` tells Aspose.Cells to rename subsequent sheets as `Sheet1_1`, `Sheet1_2`, and so on.

SmartMarker 옵션을 사용하면 중복 시트 이름 처리 방식을 제어할 수 있습니다. `DetailSheetNewName`을 `"Sheet1_{0}"`으로 설정하면 Aspose.Cells가 이후 시트들을 `Sheet1_1`, `Sheet1_2` 등으로 자동 이름 변경합니다.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Why this matters:**  
**왜 중요한가:**  

When you process several `DataTable` objects that share the same name, Excel would normally throw an error because sheet names must be unique. The `DetailSheetNewName` pattern eliminates that conflict automatically.

동일한 이름을 가진 여러 `DataTable` 객체를 처리하면 시트 이름은 고유해야 하므로 Excel이 오류를 발생시킵니다. `DetailSheetNewName` 패턴을 사용하면 이러한 충돌을 자동으로 방지합니다.

## Step 4: Process the SmartMarkers and export datatable to excel

## 단계 4: SmartMarkers 처리 및 datatable을 Excel로 내보내기

Now we create a fresh `Workbook`, run `ProcessSmartMarkers`, and let Aspose.Cells populate the worksheet(s) based on the `DataTable`.

이제 새 `Workbook`을 생성하고 `ProcessSmartMarkers`를 실행하여 Aspose.Cells가 `DataTable`을 기반으로 워크시트를 채우게 합니다.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Explanation:**  
**설명:**  

`ProcessSmartMarkers` scans the workbook for markers like `&=Sheet1!A1` (not shown here) and replaces them with the data from `dataTable`. Because we started with an empty workbook, Aspose.Cells creates a new sheet matching the table name and fills it with the rows we added.

`ProcessSmartMarkers`는 워크북에서 `&=Sheet1!A1`와 같은 마커를 스캔(여기서는 표시되지 않음)하고 `dataTable`의 데이터로 교체합니다. 빈 워크북에서 시작했기 때문에 Aspose.Cells는 테이블 이름과 일치하는 새 시트를 만들고 추가한 행들로 채웁니다.

## Step 5: Save workbook as xlsx

## 단계 5: 워크북을 xlsx 형식으로 저장

Finally, write the workbook to disk with the modern OpenXML format (`.xlsx`). You can change the path to suit your environment.

마지막으로 최신 OpenXML 형식(`.xlsx`)으로 워크북을 디스크에 저장합니다. 환경에 맞게 경로를 변경할 수 있습니다.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Result:**  
**결과:**  

| Sheet name | Rows |
|------------|------|
| 시트 이름 | 행 |
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (같은 이름의 다른 DataTable이 처리된 경우) |

The sheet‑renaming logic ensures **create multiple excel sheets** without manual name management.

시트 이름 변경 로직을 통해 **create multiple excel sheets**를 수동으로 이름을 관리하지 않아도 보장합니다.

## Common variations and edge cases

## 일반적인 변형 및 엣지 케이스

| Situation | How to handle it |
|-----------|------------------|
| 상황 | 처리 방법 |
| **Very large tables** (≥ 100 000 rows) | **매우 큰 테이블** (≥ 100 000 행) | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` before processing to keep memory usage low. | 처리 전에 `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized`를 설정하여 메모리 사용량을 낮게 유지합니다. |
| **Custom column order** | **사용자 지정 열 순서** | Reorder `DataColumn` objects in the `DataTable` before calling `ProcessSmartMarkers`. | `ProcessSmartMarkers` 호출 전에 `DataTable`의 `DataColumn` 객체 순서를 재정렬합니다. |
| **Multiple DataTables with different names** | **다른 이름을 가진 여러 DataTable** | Call `ProcessSmartMarkers` for each table; Aspose.Cells will create a separate sheet for each name automatically. | 각 테이블마다 `ProcessSmartMarkers`를 호출하면 Aspose.Cells가 자동으로 각 이름에 해당하는 별도 시트를 생성합니다. |
| **Need a header row with styling** | **스타일이 적용된 헤더 행이 필요할 경우** | After processing, access `Worksheet.Cells["A1"]` and apply `Style` properties (font, background). | 처리 후 `Worksheet.Cells["A1"]`에 접근하여 `Style` 속성(폰트, 배경 등)을 적용합니다. |
| **Saving to a stream instead of a file** | **파일 대신 스트림에 저장** | Replace `workbook.Save(outputPath, SaveFormat.Xlsx)` with `workbook.Save(stream, SaveFormat.Xlsx)`. | `workbook.Save(outputPath, SaveFormat.Xlsx)`를 `workbook.Save(stream, SaveFormat.Xlsx)`로 교체합니다. |

**Pro tip:** Always wrap file‑system operations in `try…catch` blocks to surface permission issues early.

**Pro tip:** 파일 시스템 작업은 항상 `try…catch` 블록으로 감싸서 권한 문제를 조기에 발견하도록 합니다.

## Full source code (ready to copy)

## 전체 소스 코드 (복사 준비 완료)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Expected output

### 예상 출력

Running the program prints:

프로그램을 실행하면 다음과 같이 출력됩니다:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Opening `DuplicateSheets.xlsx` shows a sheet named **Sheet1** with the `Id` column containing the values `1, 2, 3, 4, 5`. If you later process another `DataTable` named `"Sheet1"` in the same workbook, Aspose.Cells will create **Sheet1_1**, **Sheet1_2**, etc., automatically.

`DuplicateSheets.xlsx`를 열면 **Sheet1**이라는 시트가 나타나며 `Id` 열에 `1, 2, 3, 4, 5` 값이 들어 있습니다. 동일 워크북에서 나중에 `"Sheet1"`이라는 이름의 다른 `DataTable`을 처리하면 Aspose.Cells가 자동으로 **Sheet1_1**, **Sheet1_2** 등을 생성합니다.

## Conclusion

## 결론

You now know how to **create excel sheet** from a `DataTable` in C#, **export datatable to excel**, **add rows to datatable**, generate **create multiple excel sheets** with automatic naming, and **save workbook as xlsx**. The complete, runnable example demonstrates the end‑to‑end workflow and provides practical tips for large data sets and custom styling.

이제 C#에서 `DataTable`을 사용해 **create excel sheet**을 만들고, **export datatable to excel**, **add rows to datatable** 방법, 자동 이름 지정으로 **create multiple excel sheets**를 생성하며, **save workbook as xlsx**하는 방법을 알게 되었습니다. 완전하고 실행 가능한 예제가 전체 흐름을 보여 주며 대용량 데이터와 사용자 지정 스타일링에 대한 실용적인 팁을 제공합니다.

### What’s next?

### 다음 단계는?

* Explore **cell formatting** (fonts, colors, borders) by accessing `Worksheet.Cells` after `ProcessSmartMarkers`.  
  * **cell formatting**(폰트, 색상, 테두리)을 `ProcessSmartMarkers` 후 `Worksheet.Cells`에 접근하여 탐색합니다.  
* Use **SmartMarker loops** to generate master‑detail reports in a single workbook.  
  * **SmartMarker loops**를 사용해 단일 워크북에서 마스터‑디테일 보고서를 생성합니다.  
* Switch to **CSV export** by changing `SaveFormat.Csv` if you need a plain‑text representation.  
  * 텍스트 형태가 필요하면 `SaveFormat.Csv`로 변경하여 **CSV export**로 전환합니다.  

Feel free to adapt the code to your own data sources—whether it’s a database query, an API response, or an in‑memory collection. Happy coding!

데이터베이스 쿼리, API 응답, 메모리 컬렉션 등 자신의 데이터 소스에 맞게 코드를 자유롭게 적용하세요. 즐거운 코딩 되세요!

## What Should You Learn Next?

## 다음에 배워야 할 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET을 사용하여 Excel 워크북을 ODS로 만들고 저장하는 방법](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Aspose.Cells for Java를 사용하여 Excel 워크북을 SVG로 만들고 저장하는 방법](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Aspose.Cells Java를 사용하여 Excel을 HTML로 만들고 내보내는 방법 | 워크북 작업 가이드](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}