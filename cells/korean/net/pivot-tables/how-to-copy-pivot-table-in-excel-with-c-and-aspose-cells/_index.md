---
category: general
date: 2026-10-04
description: C#를 사용하여 피벗 테이블을 한 워크북에서 다른 워크북으로 복사하는 방법을 배웁니다. 이 가이드는 행 복사, 피벗 테이블
  복제 및 Excel 범위 효율적인 복사 방법도 다룹니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: ko
lastmod: 2026-10-04
og_description: C#를 사용하여 Excel에서 피벗 테이블 복사하기. Aspose.Cells를 사용하여 피벗 테이블 복제, 행 복사 및
  Excel 범위 복사를 위한 전체 튜토리얼을 따라보세요.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: C#로 Excel에서 피벗 테이블 복사 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#와 Aspose.Cells를 사용하여 Excel에서 피벗 테이블 복사하는 방법
url: /ko/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 C#와 Aspose.Cells를 사용하여 피벗 테이블 복사하는 방법

피벗 테이블을 **복사**해야 할 경우, 이 튜토리얼은 완전하고 실행 가능한 솔루션을 보여줍니다. 소스 파일을 로드하고, 피벗이 포함된 범위를 정의하고, 행(피벗 정의 포함)을 복사한 뒤 결과를 저장하는 과정을 정확히 확인할 수 있습니다. 보고 파이프라인을 자동화하거나 마이그레이션 도구를 구축할 때, 아래 단계만으로 몇 줄의 C# 코드로 피벗 테이블을 복제할 수 있습니다.

피벗 테이블 복사는 셀 값만 복사하는 것이 아니라, 기본 캐시와 필드 설정도 함께 이동해야 합니다. 예제에서는 **Aspose.Cells** 라이브러리를 사용합니다. 이 라이브러리는 피벗 메타데이터를 자동으로 처리해 주므로 캐시를 수동으로 재구성할 필요가 없습니다. 이 가이드를 끝까지 따라 하면 **피벗 복사 방법**, **Excel 범위 복사**, **행 복사 방법**을 안전하게 수행할 수 있게 됩니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- .NET 6.0 이상이 설치되어 있어야 합니다(코드는 .NET Framework 4.7+에서도 동작합니다).
- 유효한 Aspose.Cells for .NET 라이선스 또는 임시 평가 라이선스.
- 두 개의 Excel 파일: 피벗 테이블이 포함된 `Source.xlsx`와 `CopyWithPivot.xlsx`가 저장될 빈 폴더.
- Visual Studio 2022(또는 C#를 지원하는 다른 IDE).

## Step 1: Set up the project and add Aspose.Cells

새 콘솔 프로젝트를 만들고 Aspose.Cells NuGet 패키지를 추가합니다:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

패키지는 아래 코드에서 사용할 `Workbook`, `Worksheet`, `CellArea` 클래스를 제공합니다.

## Step 2: Load the source workbook that contains the pivot table

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Why this matters:** 워크북을 로드하면 모든 워크시트와 숨겨진 피벗 캐시가 메모리에 표현됩니다. 파일을 로드하지 않으면 피벗 범위를 참조할 수 없습니다.

## Step 3: Define the cell area that covers the pivot table

피벗에 포함되는 행과 열을 Aspose.Cells에 알려줘야 합니다. `CellArea` 구조체를 사용하면 직사각형 블록을 지정할 수 있습니다.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Tip:** 정확한 크기를 모를 경우 Excel에서 소스 파일을 열고 피벗을 선택한 뒤 이름 상자에 표시되는 범위(예: `A1:K31`)를 확인하세요. Excel 좌표를 0 기반 인덱스로 변환하여 코드에 사용합니다.

## Step 4: Create a new destination workbook and get its first worksheet

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Why this step is required:** 행을 복사하려면 대상 워크북이 먼저 존재해야 합니다. Aspose.Cells는 기본 워크시트를 자동으로 생성하며, 이를 대상 워크시트로 사용합니다.

## Step 5: Copy the rows (including the pivot table) from source to destination

`CopyRows` 메서드는 셀 값과 기본 피벗 캐시를 모두 복사합니다.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **How this works:**  
> - `CopyRows`는 소스 워크시트, 시작 행, 복사할 행 수를 받습니다.  
> - 또한 대상 워크시트와 복사가 시작될 행을 받습니다.  
> - 소스 범위에 피벗 테이블이 포함되어 있기 때문에 메서드는 피벗의 캐시, 필드 목록, 레이아웃을 그대로 전달합니다. 이것이 **피벗 복사 방법**의 핵심이며 기능 손실 없이 복사할 수 있습니다.

### Edge case: copying a pivot that spans multiple worksheets

피벗의 원본 데이터가 피벗 자체와 다른 시트에 있더라도 캐시는 워크북에 저장되므로 복사 시 함께 이동합니다. 하지만 대상 워크북에 동일한 원본 데이터 범위가 존재해야 합니다. 그렇지 않으면 피벗이 `#REF!` 오류를 표시합니다. 이런 경우 먼저 원본 데이터 범위를 복사한 뒤 피벗 행을 복사하세요.

## Step 6: Save the workbook that now contains the copied pivot table

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

프로그램을 실행하면 `CopyWithPivot.xlsx`가 생성되고, 원본 피벗 테이블과 동일한 복제본(슬라이서, 필터, 계산된 필드 포함)이 저장됩니다.

### Expected output

`CopyWithPivot.xlsx`를 열면:

- 피벗 테이블이 `Source.xlsx`와 동일한 위치(예: A1:K31)에 나타납니다.
- 모든 행·열 레이블, 합계, 서식이 보존됩니다.
- 피벗을 새로 고치면 원본과 동일한 데이터가 표시되어 캐시가 올바르게 복사됐음을 확인할 수 있습니다.

## How to copy rows without a pivot (copy excel range)

피벗 데이터 없이 **Excel 범위 복사**만 필요하다면 동일한 `CopyRows` 메서드를 사용하되 피벗이 포함되지 않은 범위를 지정하면 됩니다. 예시:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

이는 **행 복사 방법**을 일반 데이터에 적용하는 예시이며, 동일 API의 다재다능함을 보여줍니다.

## Duplicate pivot table in the same workbook (alternative approach)

때때로 새 파일을 만들지 않고 **같은 워크북 내에서 피벗 테이블 복제**가 필요할 수 있습니다. 이 경우 행을 다른 위치로 복사하면 됩니다:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

저장 후 워크북에는 두 개의 동일한 피벗이 포함되어 있어 나란히 비교하거나 백업 사본을 만들 때 유용합니다.

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Pivot shows `#REF!` after copy | Source data range not present in destination workbook | Copy the source data range first, or use `CopyRows` on the source data sheet before copying the pivot |
| Formatting lost | Only values were copied (e.g., using `Copy` instead of `CopyRows`) | Always use `CopyRows` which preserves style, formatting, and pivot metadata |
| Unexpected row offset | Destination start row mismatched with source start row | Verify that `destWorksheet.Cells` start row matches the intended location |
| Large workbooks cause memory pressure | `CopyRows` loads entire worksheets into memory | Process the copy in chunks or use streaming APIs if working with >100,000 rows |

## Full, runnable example

아래는 `Program.cs`에 붙여넣고 바로 실행할 수 있는 전체 프로그램입니다(`YOUR_DIRECTORY`를 실제 경로로 바꾸세요).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

`dotnet run`으로 프로그램을 실행합니다. 실행 후 `CopyWithPivot.xlsx`를 열어 피벗 테이블이 원본 파일과 정확히 동일하게 나타나는지 확인하세요.

## Conclusion

이제 C#와 Aspose.Cells를 사용해 한 Excel 워크북에서 다른 워크북으로 **피벗 테이블 복사**하는 방법을 알게 되었습니다. 이 가이드는 소스 파일 로드, 피벗 셀 영역 정의, 행 복사, 대상 워크북 저장까지 전체 흐름을 다루었습니다. 또한 **행 복사 방법**, **Excel 범위 복사**, **같은 파일 내 피벗 테이블 복제**와 일반적인 함정 및 모범 사례도 배웠습니다.

다음 단계가 준비되셨나요? 복사된 피벗을 프로그래밍 방식으로 새로 고치는 코드를 추가하거나 Aspose.Cells를 사용해 피벗을 PDF로 내보내는 것을 시도해 보세요. 다양한 원본 범위를 실험하면서 .NET에서 Excel 자동화를 빠르게 마스터할 수 있습니다.

---


## What Should You Learn Next?


다음 튜토리얼은 이 가이드에서 다룬 기술을 기반으로 한 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 API 기능을 추가로 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}