---
category: general
date: 2026-11-19
description: Aspose.Cells에서 CopyOptions를 사용해 범위를 복사하는 방법을 배우고, 서식을 유지하면서 피벗 테이블을 보존하며
  서식이 적용된 Excel 범위를 복사합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: ko
lastmod: 2026-11-19
og_description: Aspose.Cells에서 CopyOptions를 사용하여 범위를 복사하면 전체 서식과 피벗 테이블이 보존된 상태로 Excel
  데이터를 복제할 수 있어 신뢰할 수 있는 워크북 조작이 가능합니다.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Aspose.Cells에서 CopyOptions를 사용하여 범위 복사 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells에서 CopyOptions를 사용하여 범위 복사하는 방법
url: /ko/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells에서 CopyOptions를 사용하여 범위 복사하는 방법

Aspose.Cells에서 **CopyOptions를 사용하여 범위 복사**가 필요할 때, 이 가이드는 서식과 포함된 피벗 테이블을 그대로 유지하면서 셀 블록을 복제하는 방법을 정확히 보여줍니다. 워크시트 간에 데이터를 이동할 때 스타일을 보존하는 데 어려움을 겪는 개발자들이 많으며, `CopyOptions` 클래스가 추가적인 수동 작업 없이 이 문제를 해결합니다.

이 튜토리얼을 통해 배우게 될 내용:

* Excel 워크북에서 원본 및 대상 영역 정의하기.  
* `CopyOptions`를 사용하여 셀 서식, 열 너비 및 피벗 테이블 유지하기.  
* 결과를 새로운 파일에 저장하여 이후 처리에 활용하기.

예제는 모든 `.xlsx` 파일에서 동작하며 Aspose.Cells for .NET 라이브러리만 필요합니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* .NET 6.0 이상이 설치되어 있음.  
* 유효한 Aspose.Cells for .NET 라이선스(또는 무료 평가 키).  
* Visual Studio 2022 또는 선호하는 C# IDE.  

`Aspose.Cells` 외에 추가 NuGet 패키지는 필요하지 않습니다.

## 1단계: 프로젝트 설정 및 네임스페이스 가져오기

새 콘솔 애플리케이션을 만들고 Aspose.Cells 참조를 추가합니다:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

`using Aspose.Cells;` 지시문을 통해 `Workbook`, `CellArea`, `CopyOptions`에 접근할 수 있습니다.

## 2단계: 수정할 워크북 로드하기

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook`은 전체 Excel 파일을 나타냅니다. `YOUR_DIRECTORY`를 소스 파일이 들어 있는 폴더 경로로 바꾸세요.

## 3단계: 원본 및 대상 범위 정의하기

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea`는 좌상단 셀 주소와 우하단 셀 주소를 기반으로 직사각형 영역을 생성합니다. 복사하려는 블록 크기에 맞게 좌표를 조정하면 됩니다.

## 4단계: 서식 및 피벗 테이블을 보존하면서 범위 복사하기

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions` 객체는 Aspose.Cells에게 어떤 요소를 유지할지 정확히 알려줍니다. `CopyPivotTables = true` 설정이 **CopyOptions를 사용하여 범위 복사**할 때 피벗 테이블이 포함된 경우 핵심입니다. 다른 플래그들은 **서식을 포함한 Excel 범위 복사**가 자동으로 이루어지도록 하며, 복사 후 스타일을 다시 적용할 필요가 없습니다.

### `CopyOptions`가 중요한 이유

* **성능** – 셀을 하나씩 복사하는 대신 내부에서 한 번에 처리합니다.  
* **정확성** – 글꼴, 색상, 테두리 등 모든 시각적 요소가 그대로 유지되어 보고서의 시각적 일관성이 유지됩니다.  
* **신뢰성** – 피벗 테이블의 캐시와 원본 참조가 복제되므로 기능이 그대로 작동합니다.

## 5단계: 수정된 워크북 저장하기

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

`Save`를 호출하면 `output.xlsx` 파일에 원본 데이터와 복제된 블록이 대상 위치에 함께 저장되며, 서식과 피벗 테이블이 그대로 유지됩니다.

## 전체 소스 코드 (참고용)

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

프로그램을 실행하면 다음과 같이 출력됩니다:

```
Range copied successfully. Output saved to output.xlsx
```

`output.xlsx`를 Excel에서 열면 A1:H30 블록이 A35:H64에 복제된 것을 확인할 수 있으며, 모든 셀 색상, 테두리, 숫자 형식 및 피벗 테이블이 그대로 유지됩니다.

## 흔히 묻는 질문 및 예외 상황 처리

### 대상 영역이 원본과 겹치는 경우는 어떻게 하나요?

Aspose.Cells는 `ArgumentException`을 발생시킵니다. 겹치지 않는 위치를 계산하거나 다른 워크시트로 복사하세요:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### 서로 다른 워크북 간에 복사하려면?

대상 파일용 두 번째 `Workbook` 인스턴스를 만들고 동일한 `CopyOptions` 객체를 사용합니다:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions`가 병합 셀도 복사하나요?

예. `CopyStyle` 플래그에 병합 셀 정보가 포함됩니다. 더 세밀한 제어가 필요하면 `options.CopyMergedCells = true`(신버전에서 사용 가능)를 설정하세요.

### 매우 큰 범위(수천 행)인 경우는?

작업은 메모리 효율적이지만, 매우 큰 파일에서는 `WorkbookSettings`의 `MemorySetting`을 `MemorySetting.MemoryPreference`로 높이는 것이 좋습니다.

## 전문가 팁

* **동일한 `CopyOptions` 인스턴스를 여러 복사 작업에 재사용**하면 객체 할당 오버헤드를 줄일 수 있습니다.  
* **복사 전에 범위 검증**: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))`와 같이 검사하면 오타로 인한 오류를 초기에 잡을 수 있습니다.  
* **대량 데이터 복사 시 계산 모드 끄기** (`workbook.Settings.CalcMode = CalculationMode.Manual`) 로 속도를 높이고, 복사 후 필요하면 `workbook.CalculateFormula()`를 호출해 최신 결과를 얻으세요.

## 결론

이제 Aspose.Cells에서 **CopyOptions를 사용하여 범위 복사**하는 방법을 알게 되었으며, **서식을 포함한 Excel 범위 복사**를 피벗 테이블 및 기타 고급 기능을 유지하면서 수행할 수 있습니다. 이 접근 방식은 수동 스타일 재적용을 없애고 Excel 자동화의 견고함과 유지 보수성을 높여줍니다.

다음 단계로 시도해 볼 내용:

* `CopyOptions`를 사용해 전체 워크시트를 복제하기.  
* `WorksheetCollection.AddCopy`와 결합해 템플릿 기반 보고서 생성하기.  
* 코드를 ASP.NET Core API에 통합해 실시간 Excel 변환 서비스를 제공하기.

다양한 원본/대상 좌표를 실험해 보고, 결과를 댓글로 공유해 주세요!

## 다음에 배울 내용은?

아래 튜토리얼들은 이번 가이드에서 다룬 기술을 확장하여 추가 API 기능을 마스터하고, 프로젝트에 다양한 구현 방식을 적용할 수 있도록 도와줍니다.

- [Excel Aspose Cells .NET 복사 범위 데이터](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET 복사 범위 데이터](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET 복사 범위 데이터](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}