---
category: general
date: 2026-09-21
description: Aspose.Cells를 사용하여 편집 가능한 차트와 함께 Excel을 PowerPoint로 내보내세요. 차트를 편집 가능하게
  유지하면서 워크시트를 PPTX로 변환하는 단계별 가이드를 따라보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: ko
lastmod: 2026-09-21
og_description: Aspose.Cells를 사용하여 편집 가능한 차트와 함께 Excel을 PowerPoint로 내보내기. 차트의 완전한
  편집 가능성을 유지하면서 워크시트를 PPTX로 변환하는 방법을 알아보세요.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: 편집 가능한 차트가 포함된 Excel을 PowerPoint로 내보내기 – C# 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: C#에서 편집 가능한 차트를 포함한 Excel을 PowerPoint로 내보내기
url: /ko/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 편집 가능한 차트가 포함된 Excel을 PowerPoint로 내보내기

편집 가능한 차트가 포함된 Excel을 PowerPoint로 내보내는 것은 프레젠테이션에서 스프레드시트 시각 자료를 재사용해야 할 때 흔히 요구되는 작업입니다. 이 가이드는 Aspose.Cells for .NET을 사용하여 차트 편집 가능성을 유지하면서 **export Excel to PowerPoint** 하는 방법을 보여줍니다.

배우게 될 내용:

* 차트와 텍스트 상자가 포함된 기존 워크북을 로드합니다.  
* 차트와 도형이 편집 가능하도록 PPTX 내보내기 옵션을 구성합니다.  
* 특정 워크시트를 Microsoft PowerPoint에서 열고 편집할 수 있는 PowerPoint 파일로 변환합니다.

이 튜토리얼은 기본적인 C# 지식과 최신 .NET 버전(≥ .NET 6)이 있다고 가정합니다. Aspose.Cells에 대한 사전 경험은 필요하지 않습니다.

---

## Excel을 PowerPoint로 내보내기 – 개요

**export Excel to PowerPoint**의 핵심 아이디어는 각 워크시트를 PPTX 슬라이드에 렌더링할 수 있는 이미지 소스로 취급하는 것입니다. `ExportChartAsEditableText`와 `ExportShapeAsEditableText` 플래그를 전환하면 Aspose.Cells는 기본 차트 데이터를 평면 비트맵 대신 PowerPoint 그리기 객체로 기록합니다. 이렇게 하면 결과 슬라이드가 완전히 편집 가능해지며, PowerPoint에서 직접 만든 차트와 동일합니다.

> **왜 편집 가능한 차트를 사용하나요?**  
> 편집 가능한 차트를 사용하면 발표자가 원본 Excel 파일로 돌아가지 않고도 데이터, 색상 또는 레이블을 조정할 수 있어, 마지막 순간의 변경을 빠르게 처리하고 프레젠테이션 워크플로우를 원활하게 유지할 수 있습니다.

## 워크시트를 PowerPoint로 변환 (worksheet to PowerPoint)

아래는 **worksheet to PowerPoint** 변환을 보여주는 완전하고 실행 가능한 예제입니다.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### 각 단계 설명

| 단계 | 코드가 수행하는 작업 | **export excel chart pptx**와 관련된 이유 |
|------|-------------------|----------------------------------------------|
| 1️⃣   | `input.xlsx`를 `Aspose.Cells.Workbook` 객체에 로드합니다. | 워크북은 내보내려는 차트에 대한 접근을 제공합니다. |
| 2️⃣   | `ExportType`을 `Pptx`로 설정하고 `ExportChartAsEditableText`와 `ExportShapeAsEditableText`를 활성화합니다. | 이 플래그들은 **editable charts pptx**의 핵심이며, 라이브러리에게 차트 기하학을 래스터 이미지가 아닌 PowerPoint 그리기 객체로 기록하도록 지시합니다. |
| 3️⃣   | 첫 번째 워크시트에서 `ConvertToImage`를 호출하여 `Worksheet.pptx`를 생성합니다. | 이 메서드는 **export excel to powerpoint** 작업을 수행하고 PowerPoint에서 직접 열 수 있는 PPTX 파일을 기록합니다. |

> **팁:** 여러 워크시트를 내보내야 하는 경우 `workbook.Worksheets`를 반복하고 각 워크시트에 대해 `ConvertToImage`를 호출하세요. 출력 파일 이름을 `Sheet1.pptx`, `Sheet2.pptx` 등으로 지정할 수 있습니다.

## PPTX에서 편집 가능한 차트 활성화 (export excel chart pptx)

`ExportChartAsEditableText`가 `true`로 설정되면 Aspose.Cells는 각 차트를 PPTX XML 내부의 `<a:graphic>` 요소 컬렉션으로 기록합니다. PowerPoint는 이러한 요소들을 기본 차트 객체로 인식하며, 더블 클릭하면 차트 편집기를 열 수 있습니다.

**일반적인 함정**

* **Aspose.Cells 라이선스 누락** – 라이선스가 없으면 라이브러리가 출력에 워터마크를 추가합니다. 프로그램 초기에 라이선스를 등록하세요 (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **지원되지 않는 차트 유형** – 대부분의 2D 차트(컬럼, 라인, 파이)는 완전히 편집 가능하지만, 일부 복잡한 3D 또는 콤보 차트는 이미지로 대체될 수 있습니다. 완전한 편집 가능성에 의존한다면 특정 차트 유형을 테스트하세요.  
* **큰 워크시트** – 매우 큰 워크시트를 내보내면 메모리를 많이 사용할 수 있습니다. 변환되는 영역을 제한하려면 `ImageOrPrintOptions`에서 `ExportMaxRows` 또는 `ExportMaxColumns`를 사용하는 것을 고려하세요.

## 차트를 편집 가능하게 유지하기 위한 팁 (editable charts pptx)

1. **차트 데이터 범위 유지** – 차트 데이터 소스가 내보내는 워크시트와 동일한 시트에 있는지 확인하세요. 시트 간 참조는 PPTX에서 정적 값으로 변환됩니다.  
2. **최신 Aspose.Cells 버전 사용** – 새로운 릴리스는 추가 차트 기능 지원을 개선하고 PPTX 내보내기와 관련된 특수 버그를 수정합니다.  
3. **출력 검증** – 변환 후 PowerPoint에서 생성된 PPTX를 열어 차트 제목, 시리즈 및 축 레이블을 편집할 수 있는지 확인하세요. 요소가 이미지로 표시되면 `ExportChartAsEditableText`가 활성화되어 있는지와 차트 유형이 지원되는지 다시 확인하세요.  
4. **배치 처리** – 자동화 시나리오(예: 여러 Excel 보고서에서 슬라이드 덱 생성)에서는 변환 로직을 `Workbook`, `int worksheetIndex`, `string outputPath`를 매개변수로 받는 메서드로 감싸세요. 이렇게 하면 **export excel to powerpoint** 워크플로우가 분리되어 재사용 가능해집니다.

## 전체 작업 예제 요약

모든 내용을 종합하면, 새 .NET 콘솔 프로젝트에 복사‑붙여넣기 할 수 있는 최소 프로그램은 다음과 같습니다:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**예상 결과**

* `YOUR_DIRECTORY`에 `Worksheet.pptx` 파일이 생성됩니다.  
* Microsoft PowerPoint에서 파일을 열면 원본 차트와 모든 텍스트 상자를 포함한 슬라이드가 표시됩니다.  
* 차트를 더블 클릭하면 PowerPoint 차트 편집기가 열려 시리즈 값, 색상 또는 축 제목을 변경할 수 있으며, **editable charts pptx** 기능이 의도대로 작동함을 확인할 수 있습니다.

## 결론

이제 차트를 편집 가능하게 유지하는 **export Excel to PowerPoint**에 대한 완전한 솔루션을 갖추었습니다. `ImageOrPrintOptions`에 `ExportChartAsEditableText`와 `ExportShapeAsEditableText`를 설정하면 변환 과정에서 차트가 PowerPoint에서 직접 만든 것처럼 동작하는 기본 PPTX 파일이 생성됩니다.

이후 할 수 있는 일:

* 각 워크시트에 대해 **worksheet to PowerPoint**를 적용하도록 코드를 확장합니다.  
* 슬라이드 제목 추가나 이미지 삽입 등 다른 Aspose.Cells 기능과 내보내기를 결합합니다.  
* 맞춤 테마를 사용한 **export Excel chart PPTX** 또는 전체 슬라이드 덱 생성 파이프라인 자동화와 같은 관련 주제를 탐색합니다.

다양한 차트 유형을 실험하고, 데이터 레이블을 추가하거나, 이 워크플로우를 더 큰 보고 시스템에 통합해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}