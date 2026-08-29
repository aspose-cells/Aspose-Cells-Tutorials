---
category: general
date: 2026-08-04
description: C#에서 Aspose.Cells를 사용해 Excel 차트를 PowerPoint로 내보내세요. 이 단계별 Excel‑to‑PowerPoint
  변환 가이드를 따라 도형을 편집 가능하게 유지합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: ko
lastmod: 2026-08-04
og_description: C#에서 Aspose.Cells를 사용해 Excel 차트를 PowerPoint로 내보내기. 편집 가능한 PPTX를 만드는
  방법, 차트 데이터를 보존하는 방법, Excel에서 PowerPoint로 변환을 자동화하는 방법을 배워보세요.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: C#를 사용하여 Excel 차트를 PowerPoint로 내보내기 – 전체 Aspose.Cells 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: C#로 Excel 차트를 PowerPoint로 내보내기 – 완전한 Aspose.Cells 가이드
url: /ko/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 Excel 차트를 PowerPoint로 내보내기 – 완전한 Aspose.Cells 가이드

Excel 차트를 PowerPoint로 **내보내야** 하는 경우, 이 튜토리얼에서는 C#에서 Aspose.Cells와 Aspose.Slides를 사용하여 수행하는 방법을 보여줍니다. 차트 데이터와 도형을 보존하는 완전 편집 가능한 PPTX를 얻을 수 있어, 변환 후 추가 디자인 작업이 가능합니다.

Excel에서 PowerPoint로 차트를 내보내는 것은 자동 보고 파이프라인, 영업 프레젠테이션, 교육 자료를 만들 때 흔히 요구되는 작업입니다. 이 가이드에서는 차트 요소를 모두 편집 가능하게 유지하는 **Excel to PowerPoint conversion**을 수행하는 정확한 단계들을 배울 수 있습니다. 수동 복사‑붙여넣기가 필요 없으며, 코드는 .NET 6+와 기존 .NET Framework 모두에서 작동합니다.

## 사전 요구 사항

- 유효한 Aspose.Cells 라이선스(또는 무료 평가 키)  
- 프로젝트에 추가된 Aspose.Slides for .NET(라이브러리는 PPTX 출력을 처리합니다)  
- .NET 6 SDK 이상이 설치됨  
- 하나 이상의 차트를 포함하는 Excel 워크북(`Shapes.xlsx`를 예제로 사용)  

다음 명령을 사용하여 NuGet 패키지를 설치할 수 있습니다:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## 단계 1: Excel 워크북 로드

첫 번째 작업은 내보내려는 차트를 포함하고 있는 워크북을 여는 것입니다. `Workbook` 클래스는 전체 Excel 파일을 나타냅니다.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**왜 중요한가:** 워크북을 로드하면 워크시트, 차트 및 서식에 접근할 수 있습니다. Aspose.Cells는 Microsoft Office가 설치되지 않아도 파일을 읽어 솔루션을 가볍고 서버 친화적으로 유지합니다.

## 단계 2: 워크시트 선택 및 인쇄 영역 정의

워크시트에 여러 차트가 있을 수 있지만 보통 특정 영역만 내보냅니다. `PrintArea`를 설정하면 Aspose.Cells에 어떤 셀(차트 포함)을 렌더링할지 알려줍니다.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**왜 중요한가:** 정의된 인쇄 영역으로 내보내기를 제한하면 불필요한 빈 슬라이드를 방지하고 PPTX 파일 크기를 작게 유지할 수 있습니다. 영역은 차트의 정확한 범위에 맞게 조정할 수 있습니다.

## 단계 3: 편집 가능한 PPTX를 위한 내보내기 옵션 구성

Aspose.Cells는 `ImageOrPrintOptions` 클래스를 사용해 출력 형식과 편집 가능성을 제어합니다. `ImageFormat`을 `ImageFormat.Pptx`로 설정하면 PowerPoint 파일이 생성되고, `ExportEditableShapes = true`는 차트 객체를 편집 가능한 도형으로 보존합니다.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**왜 중요한가:** `ExportEditableShapes` 플래그가 **editable shapes in PowerPoint** 결과의 핵심입니다. 이 옵션이 없으면 차트가 이미지로 래스터화되어 이후 데이터 포인트나 스타일을 수정할 수 없게 됩니다.

## 단계 4: 워크시트를 PowerPoint 프레젠테이션으로 저장

마지막으로 `Workbook` 객체의 `Save` 메서드를 호출합니다. `SaveFormat.Pptx` 열거형은 Aspose.Cells에 PowerPoint 파일을 생성하도록 지시합니다.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

코드 실행이 끝나면 PowerPoint에서 `ShapesExport.pptx`를 엽니다. 원본 Excel 차트가 네이티브 PowerPoint 차트 객체로 포함된 슬라이드를 확인할 수 있습니다. 차트를 더블‑클릭하면 데이터를 편집하고 색상을 변경하거나 애니메이션을 추가할 수 있는데, 이는 PowerPoint에서 직접 차트를 만든 것과 동일합니다.

### 예상 출력

| 파일 이름                | 슬라이드 내용                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | `Shapes.xlsx`의 차트를 편집 가능한 PowerPoint 차트로 렌더링한 것으로, 축 레이블, 범례 및 데이터 시리즈가 그대로 유지됩니다. |

## 전체 실행 가능한 예제

아래는 복사·붙여넣기 후 바로 실행할 수 있는 전체 프로그램입니다. 필요한 `using` 문, 오류 처리 및 주석이 모두 포함되어 있습니다.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**각 블록 설명**

| 블록 | 목적 |
|-------|---------|
| `using` 지시문 | Aspose.Cells와 Aspose.Slides 네임스페이스를 가져옵니다. |
| `Workbook workbook = new Workbook(excelPath);` | Office가 설치되지 않아도 Excel 파일을 로드합니다. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | 차트가 포함된 영역으로 내보내기를 제한합니다. |
| `ImageOrPrintOptions` | PPTX 출력과 **Aspose.Cells PPTX export**를 편집 가능한 도형과 함께 구성합니다. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | PowerPoint 파일을 디스크에 씁니다. |
| `try / catch` | 파일 누락이나 라이선스 문제와 같은 기본 오류 처리를 제공합니다. |

이 프로그램을 실행하면 Microsoft PowerPoint, Google Slides(변환 후) 또는 기타 호환 뷰어에서 열 수 있는 PowerPoint 슬라이드가 생성됩니다.

## 일반적인 변형 및 엣지 케이스

### 여러 워크시트 내보내기

각 워크시트마다 슬라이드가 필요하면 `workbook.Worksheets`를 순회하면서 각 반복마다 고유 파일 이름으로 `Save`를 호출합니다.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### 슬라이드 레이아웃 제어

Aspose.Slides를 사용하면 내보낸 후 사용자 정의 슬라이드 레이아웃을 추가할 수 있습니다. 새 프레젠테이션을 만들고, 생성된 슬라이드를 가져온 뒤 마스터 테마를 적용합니다.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### 외부 데이터 소스를 사용하는 차트 처리

차트가 정의된 인쇄 영역 밖의 데이터 범위를 참조하는 경우, 해당 셀을 포함하도록 `PrintArea`를 확장합니다. 그렇지 않으면 내보내기 중에 차트가 데이터 시리즈를 잃을 수 있습니다.

### 라이선스 고려 사항

Aspose 라이브러리는 워터마크가 있는 평가 모드로 동작합니다. 워터마크를 제거하려면 API 호출 전에 라이선스를 설정합니다:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

고급 기능을 사용하는 경우 Aspose.Slides에도 동일하게 라이선스를 설정하십시오.

## 전문가 팁

- **내보내기 옵션 재사용:** `ImageOrPrintOptions` 인스턴스를 하나만 생성하고 각 워크시트에 할당하여 코드를 DRY하게 유지합니다.  
- **배치 처리:** 대규모 보고서의 경우 이 내보내기 로직을 백그라운드 워커나 Azure Function과 결합해 필요 시 PPTX 파일을 생성합니다.  
- **성능:** 편집 가능한 차트가 필요 없고 차트 이미지만 필요하면 `ExportEditableShapes = false`로 설정합니다. 이렇게 하면 메모리 사용량이 감소하고 변환 속도가 빨라집니다.  
- **테스트:** 생성된 PPTX를 Windows와 macOS PowerPoint 모두에서 확인하십시오. 일부 렌더링 차이가 플랫폼마다 다를 수 있습니다.  

## 결론

이제 C#을 사용해 **export Excel chart to PowerPoint**를 수행하는 완전한 엔드‑투‑엔드 솔루션을 갖추었습니다. 튜토리얼에서는 워크북 로드, 인쇄 영역 선택, **Aspose.Cells PPTX export**와 **editable shapes in PowerPoint** 구성, 그리고 완전 편집 가능한 PPTX 파일 저장까지 다루었습니다.  

이제 배치 내보내기, 사용자 정의 슬라이드 레이아웃, 웹 API와의 통합 등 추가 **Excel to PowerPoint conversion** 시나리오를 탐색할 수 있습니다. 다양한 차트 유형을 실험하고, 이미지를 추가하거나 여러 워크시트를 하나의 프레젠테이션으로 결합해 비즈니스 요구에 맞게 출력물을 맞춤 설정해 보세요.

보고서 자동화 워크플로를 시작할 준비가 되셨나요? 소스 파일을 교체하고, 인쇄 영역을 조정하고, 코드를 기존 .NET 서비스에 통합해 보세요. 즐거운 코딩 되세요!

## What Should You Learn Next?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Aspose.Cells for .NET를 사용하여 Excel을 PowerPoint로 변환하는 방법: 완전 가이드](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET를 사용하여 Excel 차트를 PDF로 내보내는 방법: 단계별 가이드](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells .NET를 사용하여 Excel 셀을 이미지로 내보내는 방법: 단계별 가이드](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}