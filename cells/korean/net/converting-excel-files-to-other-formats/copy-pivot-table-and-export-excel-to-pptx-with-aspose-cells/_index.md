---
category: general
date: 2026-09-11
description: Aspose.Cells를 사용하여 피벗 테이블을 복사하고 Excel을 PPTX로 내보냅니다. 편집 가능한 PPTX를 생성하고
  C#에서 워크북을 PPTX로 저장하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: ko
lastmod: 2026-09-11
og_description: Aspose.Cells를 사용하여 C#에서 피벗 테이블을 복사하고 Excel을 PPTX로 내보냅니다. 몇 줄의 코드만으로
  편집 가능한 PPTX를 생성하고 워크북을 PPTX로 저장합니다.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: 피벗 테이블 복사 및 Excel을 PPTX로 내보내기 – 완전한 C# 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Aspose.Cells를 사용하여 피벗 테이블 복사 및 Excel을 PPTX로 내보내기
url: /ko/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 피벗 테이블 복사 및 Aspose.Cells를 사용한 Excel을 PPTX로 내보내기

하나의 워크시트에서 다른 워크시트로 피벗 테이블을 복사한 다음 Excel 파일을 PowerPoint 프레젠테이션으로 내보내야 한다면, 이 가이드가 방법을 보여줍니다. Aspose.Cells를 사용하면 몇 줄의 C# 코드만으로 편집 가능한 PPTX를 생성하고 워크북을 PPTX로 저장할 수 있습니다.

이 튜토리얼은 피벗 테이블을 이동하고 기능을 유지하며 차트와 도형이 편집 가능한 상태로 PPTX 파일을 만드는 모든 단계를 다룹니다. 외부 도구는 필요 없으며 Aspose.Cells 라이브러리와 .NET 개발 환경만 있으면 됩니다.

## 달성할 수 있는 목표

* **Copy pivot table** 소스 시트에서 대상 시트로 복사하면서 모든 데이터 연결을 그대로 유지합니다.  
* **Export Excel to PPTX** 결과 슬라이드를 PowerPoint에서 편집할 수 있도록 합니다.  
* **Generate editable PPTX** 차트, 표, 도형이 이미지로 평탄화되지 않고 편집 가능하도록 생성합니다.  
* **Save workbook as PPTX** 동일한 Aspose.Cells API 호출로 워크북을 PPTX로 저장합니다.  

### 사전 요구 사항

* .NET 6.0 이상 (코드는 .NET Framework 4.6+에서도 작동합니다).  
* Aspose.Cells for .NET (NuGet 패키지 `Aspose.Cells`).  
* C# 콘솔 애플리케이션에 대한 기본 이해.  

> **전문가 팁:** 최신 버전을 보장하려면 CLI를 통해 NuGet 패키지를 설치하세요:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## 워크시트 간 피벗 테이블 복사 방법

첫 번째 작업은 피벗 테이블 정의를 보존하면서 이동하는 것입니다. Aspose.Cells는 `CopyPivotTable` 플래그가 포함된 `CopyOptions` 객체와 함께 `CopyRange` 메서드를 제공합니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**왜 작동하나요:**  
`CopyRange`는 셀 데이터와 서식을 복사하고, `CopyPivotTable`이 true일 경우 피벗 테이블의 캐시와 메타데이터도 복사합니다. 대상 범위는 셀 `A1`(행 0, 열 0)에서 시작하지만 오프셋을 변경하여 피벗 테이블을 다른 위치에 배치할 수 있습니다.

**일반적인 엣지 케이스:** 대상 시트에 동일한 이름의 피벗 테이블이 이미 존재하면 Aspose.Cells가 자동으로 들어오는 피벗 테이블의 이름을 바꿔 충돌을 방지합니다.

## Excel을 PPTX로 내보내고 편집 가능한 PPTX 생성

피벗 테이블이 제자리에 배치되면 전체 워크북을 PPTX 파일로 내보낼 수 있습니다. `ImageOrPrintOptions` 클래스에서 `ExportImageFormat = ImageFormat.Pptx`를 지정하면 Aspose.Cells가 출력을 래스터 이미지가 아닌 PowerPoint 프레젠테이션으로 처리합니다.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**왜 작동하나요:**  
`ExportImageFormat`을 `Pptx`로 설정하면 Aspose.Cells가 각 워크시트를 슬라이드로 변환합니다. 도형, 차트, 피벗 테이블은 네이티브 PowerPoint 객체로 기록되므로 PowerPoint에서 더블 클릭하여 기본 데이터를 편집할 수 있습니다.

**대용량 워크북 팁:** 내보낼 필요가 없는 시트가 있다면 `Save` 호출 전에 `workbook.Worksheets.RemoveAt(index)`를 사용해 해당 시트를 제거하세요. 이렇게 하면 PPTX 파일 크기가 감소합니다.

## 전체 실행 가능한 예제

아래는 앞서 설명한 단계를 모두 연결한 완전한 프로그램입니다. `YOUR_DIRECTORY`를 실제 머신의 경로로 교체하세요.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### 예상 출력

프로그램을 실행하면 다음과 같이 출력됩니다:

```
Pivot table copied and workbook exported to PPTX successfully.
```

`output.pptx`를 Microsoft PowerPoint에서 열면 복사된 피벗 테이블이 편집 가능한 차트 형태로 포함된 슬라이드를 확인할 수 있습니다. 차트를 더블 클릭하면 PowerPoint 차트 편집기가 열려 시리즈, 축, 데이터 레이블 등을 Excel로 돌아가지 않고도 수정할 수 있습니다.

## 일반적인 함정 처리

| Issue | Cause | Fix |
|-------|-------|-----|
| 피벗 테이블이 정적 이미지로 표시됨 | `CopyPivotTable` 플래그 누락 또는 `ExportImageFormat`이 `Png`로 설정됨 | `CopyPivotTable = true`와 `ExportImageFormat = ImageFormat.Pptx`를 확인하세요. |
| 대상 시트에 빈 셀만 표시됨 | 원본 범위가 피벗 테이블 전체 영역을 포함하지 않음 | 모든 피벗 필드를 포함하도록 범위를 확장하세요(예: `"A1:H30"`). |
| 내보낸 PPTX 파일이 너무 큼 | 불필요한 워크시트가 포함됨 | `Save` 호출 전에 원하지 않는 시트를 제거하세요. |
| PowerPoint에서 차트를 편집할 수 없음 | PPTX 지원이 없는 오래된 Aspose.Cells 버전 사용 | 최신 Aspose.Cells 버전으로 업그레이드하세요(릴리스 노트 확인). |

## 다음 단계 및 관련 주제

* **Export Excel sheet to PPTX with custom slide layouts** – 슬라이드 모양을 세밀하게 제어하려면 `WorksheetToPdfConverter`를 살펴보세요.  
* **Export Excel to PDF** – `ImageFormat.Pptx`를 `ImageFormat.Pdf`로 교체하면 PDF를 생성할 수 있습니다.  
* **Programmatically modify PPTX after export** – `Aspose.Slides` 라이브러리를 사용해 애니메이션이나 발표자 메모를 추가하세요.  

**copy pivot table**, **export excel to pptx**, **generate editable pptx**를 마스터하면 스프레드시트 데이터를 프레젠테이션 데크로 직접 이동하면서 편집 가능성을 유지하는 엔드‑투‑엔드 보고 파이프라인을 구축할 수 있습니다.

---

## 다음에 배워야 할 내용은 무엇인가요?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접하게 관련된 주제를 다룹니다. 각 리소스에는 단계별 설명과 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [C#에서 피벗 테이블 복사 – Excel을 PPTX로 변환, 범위 복사 및 텍스트 상자 만들기](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [새 Excel 워크북 만들기 – 피벗 테이블 복사 및 복제](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Aspose.Cells for .NET을 사용하여 Excel에서 피벗 테이블 만들기](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}