---
category: general
date: 2026-09-27
description: Aspose.Cells를 사용하여 C#에서 피벗 테이블을 복사하는 방법을 배웁니다. 서식이 포함된 행 복사, 피벗 테이블을
  다른 시트로 복사, 피벗 테이블을 새 워크북으로 내보내기를 포함합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: ko
lastmod: 2026-09-27
og_description: Aspose.Cells를 사용하여 C#에서 피벗 테이블을 복사하는 방법. 서식이 적용된 행을 복사하고, 피벗 테이블을
  다른 시트로 이동하며, 새 워크북으로 내보내는 단계별 가이드를 따라 보세요.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: C#에서 피벗 테이블 복사 방법 – 전체 Aspose.Cells 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Aspose.Cells를 사용하여 C#에서 피벗 테이블 복사하는 방법
url: /ko/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#와 Aspose.Cells를 사용하여 피벗 테이블 복사하는 방법

한 워크시트에서 다른 워크시트로 **피벗 테이블을 복사**해야 할 경우, C#와 Aspose.Cells를 사용한 **피벗 테이블 복사 방법**을 배우면 수작업 시간을 크게 절약할 수 있습니다. 이 방법을 사용하면 **서식이 포함된 행 복사**, 피벗 캐시 보존, 그리고 필요할 때 **피벗 테이블을 새 워크북으로 내보내기**도 할 수 있습니다.

이 튜토리얼에서는 전체 워크플로우를 단계별로 안내합니다:

* 워크북 생성,
* 서식을 유지하면서 피벗 테이블 범위 복사,
* 복사된 데이터를 새 시트에 배치,
* 결과를 별도 파일로 저장.

`CopyRows` 메서드가 **피벗 테이블을 다른 시트로 복사**하는 가장 신뢰할 수 있는 방법인 이유를 확인하고, 숨겨진 행이나 외부 데이터 소스와 같은 엣지 케이스를 처리하는 팁도 얻을 수 있습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

| 요구 사항 | 중요한 이유 |
| .NET 6.0 또는 이후 버전 | Aspose.Cells는 .NET 6+를 지원하며 최고의 성능을 제공합니다. |
| Visual Studio 2022 (or any C# IDE) | NuGet 패키지를 복원할 수 있는 편집기가 필요합니다. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | 이 라이브러리는 예제에서 사용된 `CopyRows` API를 제공합니다. |
| 피벗 테이블이 `A1:G20` 범위에 포함된 소스 Excel 파일 (`source.xlsx`) | 코드는 이 특정 범위를 복사합니다; 피벗 테이블이 더 크면 범위를 조정하세요. |

NuGet CLI 또는 패키지 관리자 콘솔을 사용하여 라이브러리를 설치합니다:

```bash
dotnet add package Aspose.Cells
```

## 단계 1: 피벗 테이블이 포함된 워크북 로드

첫 번째 줄은 전체 Excel 파일을 나타내는 `Workbook` 객체를 생성합니다. 파일을 한 번 로드하면 모든 워크시트에 대한 읽기/쓰기 접근 권한을 얻을 수 있습니다.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **이 단계가 중요한 이유** – 워크북을 로드하지 않으면 이후의 `CopyRows` 호출이 원본 데이터나 피벗 캐시를 참조할 수 없습니다.

## 단계 2: 원본 및 대상 워크시트 준비

복사된 피벗 테이블이 위치할 대상 시트가 필요합니다. 아래 코드는 원본 피벗 테이블이 있는 첫 번째 워크시트를 가져오고 **Copy**라는 새 시트를 추가합니다.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **팁:** 대상 시트가 이미 존재한다면 중복 이름을 방지하기 위해 먼저 `Worksheets.RemoveAt(index)`를 호출하세요.

## 단계 3: 피벗 테이블을 포함하는 셀 영역 정의

`CellArea` 객체는 이동하려는 범위의 좌상단 셀과 우하단 셀을 설명합니다. 이 예제에서는 피벗 테이블이 `A1:G20`을 차지합니다. 더 큰 테이블의 경우 좌표를 조정하세요.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## 단계 4: 서식을 포함하여 행 복사 및 피벗 캐시 보존

`CopyRows` 메서드는 원본 시트에서 대상 시트로 **행**을 복사합니다. `CopyOptions.CopyAll`을 전달하면 값, 서식, 차트 및 임베디드 객체 등 피벗 테이블의 모든 요소가 전송됩니다.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### 피벗 테이블에 대해 `CopyRows`가 `Copy`보다 더 잘 작동하는 이유

* `CopyRows`는 내부 피벗 캐시를 존중하므로 복사된 피벗 테이블이 정상적으로 작동합니다.
* 원본 시트에 나타나는 그대로 **서식이 포함된 행 복사**를 보존합니다.
* 단순한 범위 `Copy`와 달리 숨겨진 행과 관련된 슬라이서도 함께 이동합니다.

## 단계 5: 복사된 피벗 테이블이 포함된 워크북 저장

마지막으로 수정된 워크북을 디스크에 기록합니다. 새 파일에는 원본 시트와 원본 피벗 테이블의 완전한 복제본을 담은 **Copy** 시트가 포함됩니다.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### 예상 결과

`pivot_copied.xlsx` 파일을 열면:

* **Sheet1** 시트는 여전히 원본 데이터와 피벗 테이블을 포함합니다.
* **Copy** 시트는 동일한 레이아웃, 필터 및 서식을 가진 동일한 피벗 테이블을 보여줍니다.
* 피벗 캐시가 행과 함께 복사되었기 때문에 모든 수식과 데이터 연결이 그대로 유지됩니다.

## 같은 워크북 내에서 피벗 테이블을 다른 시트로 복사하는 방법

피벗 테이블을 다른 기존 시트(예: “Report”)에만 필요하다면, 대상 시트 생성 단계를 해당 시트에 대한 참조로 교체하면 됩니다:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

이 스니펫은 새 워크시트를 만들지 않고 **피벗 테이블을 다른 시트로 복사**하는 방법을 보여줍니다.

## 피벗 테이블을 새 워크북으로 내보내기

때때로 피벗 테이블을 완전히 별도의 파일에 저장하고 싶을 수 있습니다. 복사 작업 후 복사된 피벗 테이블이 있는 시트를 제외한 모든 워크시트를 제거하고 저장하면 됩니다:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

이제 `pivot_only.xlsx`는 복제된 피벗 테이블이 있는 단일 시트를 포함하며, **피벗 테이블을 새 워크북으로 내보내기** 요구 사항을 충족합니다.

## 서식을 잃지 않고 Excel 행 복사하는 방법

`CopyRows` 호출은 피벗 테이블뿐만 아니라 모든 범위에 적용됩니다. 조건부 서식, 데이터 유효성 검사 또는 병합 셀을 포함한 **Excel 행 복사**가 필요하면 동일한 메서드를 사용하세요:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

`CopyOptions.CopyAll`이 모든 것을 전송하기 때문에 대상 행은 원본 행과 정확히 동일하게 보입니다.

## 일반적인 함정 및 회피 방법

| 함정 | 증상 | 해결 방법 |
|---|---|---|
| 소스 범위가 전체 피벗 테이블을 포함하지 않음 | 복사된 피벗 테이블이 잘려 보입니다. | `CellArea`가 피벗 테이블의 모든 행/열을 포함하는지 확인하세요. |
| 대상 시트에 이미 데이터가 존재함 | 덮어쓴 행으로 인해 데이터 손실이 발생합니다. | 새 시트를 선택하거나 더 높은 행 인덱스에서 복사를 시작하세요. |
| 피벗 테이블이 외부 데이터 소스를 사용함 | 복사 후 연결이 끊깁니다. | 복사 후 `pivotTable.RefreshData()`를 호출하여 연결을 재설정하세요. |
| 숨겨진 행이 누락됨 | 복사본에서 일부 행이 사라집니다. | `CopyRows`는 숨겨진 행을 자동으로 복사합니다; `CopyOptions.CopyValuesOnly`를 사용하고 있지 않은지 확인하세요. |

## 전체 실행 가능한 예제

아래는 새 콘솔 프로젝트에 붙여넣을 수 있는 독립 실행형 프로그램이며, 위에서 논의한 모든 단계를 보여줍니다.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**프로그램을 실행하면** 원본 피벗 테이블 복제본이 **Copy**라는 새 시트에 포함된 `pivot_copied.xlsx` 파일이 생성됩니다.

## 결론

이제 C#를 사용하여 **피벗 테이블 복사 방법**을 알게 되었습니다.

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방법을 탐색하는 데 도움이 됩니다.

- [새 워크북 만들기 – 피벗 테이블이 있는 워크시트 복사 방법](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [C#에서 피벗 테이블 복사 – 완전 단계별 가이드](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [C#에서 피벗 테이블이 포함된 범위 복사 방법 – 완전 가이드](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}