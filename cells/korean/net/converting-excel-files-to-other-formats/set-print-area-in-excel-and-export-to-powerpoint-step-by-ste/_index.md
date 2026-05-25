---
category: general
date: 2026-03-22
description: Excel에서 인쇄 영역을 설정하고 편집 가능한 도형으로 Excel을 PowerPoint로 변환합니다. 제목 행을 반복하는
  방법, Excel에서 PowerPoint를 만드는 방법 및 Excel을 pptx 파일로 내보내는 방법을 배워보세요.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: ko
og_description: Excel에서 인쇄 영역을 설정하고 편집 가능한 도형이 포함된 PowerPoint 슬라이드로 변환합니다. 이 완전한 가이드를
  따라 제목 행을 반복하고 Excel을 pptx 파일로 내보내세요.
og_title: Excel에서 인쇄 영역 설정 – PowerPoint로 내보내기 튜토리얼
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Excel에서 인쇄 영역 설정 및 PowerPoint로 내보내기 – 단계별 가이드
url: /ko/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 인쇄 영역 설정하고 PowerPoint로 내보내기 – 완전 프로그래밍 튜토리얼

Excel 워크시트에서 **인쇄 영역을 설정**하고 그 영역을 PowerPoint 슬라이드로 바꾸고 싶었던 적 있나요? 당신만 그런 것이 아닙니다. 많은 보고 파이프라인에서 깔끔하게 인쇄되는 데이터가 프레젠테이션에도 나타나야 하는 경우가 많으며, 보통 첫 번째 행을 제목으로 반복해서 표시합니다. 좋은 소식은? 몇 줄의 C# 코드만으로 **excel to powerpoint 변환**이 가능하고, 모든 텍스트 상자를 편집 가능하게 유지하며 **제목 행 반복**도 자동으로 할 수 있다는 것입니다.

이 가이드에서는 인쇄 영역을 구성하는 방법부터 PowerPoint에서 바로 편집 가능한 PPTX 파일을 만드는 방법까지 모든 과정을 단계별로 살펴봅니다. 최종적으로 **excel에서 powerpoint 만들기**, **excel을 pptx로 내보내기**를 수행하고, 동일한 코드를 어떤 .NET 프로젝트에서도 재사용할 수 있게 됩니다. 마법은 없습니다, 명확한 단계와 실행 가능한 전체 예제가 전부입니다.

## 준비물

본격적으로 시작하기 전에 아래 항목을 준비하세요:

- **.NET 6.0** 이상 (API는 .NET Framework에서도 동작합니다)
- **Aspose.Cells for .NET** (`Workbook`, `ImageOrPrintOptions` 등을 제공하는 라이브러리)
- 기본 C# IDE (Visual Studio, Rider, 혹은 C# 확장 기능이 설치된 VS Code)
- 내보내고 싶은 데이터가 들어 있는 Excel 파일 (`input.xlsx`)

이것만 있으면 됩니다—Aspose.Cells 외에 추가 NuGet 패키지는 필요 없습니다. 아직 라이브러리를 추가하지 않았다면 다음 명령을 실행하세요:

```bash
dotnet add package Aspose.Cells
```

이제 준비 완료입니다.

## Step 1: Load the Workbook – the Starting Point for Export

첫 번째 단계는 슬라이드로 변환하고자 하는 시트가 들어 있는 워크북을 로드하는 것입니다. 워크북은 원본 문서와 같으며, 이것이 없으면 이후 작업은 의미가 없습니다.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**왜 중요한가:** 워크북을 로드하면 워크시트 컬렉션, 페이지 설정 옵션, 그리고 내보내기 엔진에 접근할 수 있습니다. 이 단계가 없으면 **인쇄 영역**을 설정하거나 행을 반복할 수 없습니다.

> **Pro tip:** 테스트 단계에서는 절대 경로를 사용하고, 프로덕션에서는 상대 경로나 설정 기반 경로로 전환하세요.

## Step 2: Configure Export Options – Keep Text Boxes and Shapes Editable

PowerPoint로 내보낼 때 슬라이드가 편집 가능하도록 하고 싶을 것입니다. Aspose.Cells는 `ImageOrPrintOptions` 로 이를 제어합니다. `ExportTextBoxes`와 `ExportShapeObjects`를 `true` 로 설정하면 해당 객체들이 이미지가 아니라 PowerPoint 고유 요소로 보존됩니다.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**왜 중요한가:** **excel to powerpoint 변환** 후 슬라이드를 수동으로 수정해야 할 경우, 이 설정 덕분에 텍스트 상자를 처음부터 다시 만들 필요가 없습니다. 또한 화살표나 차트 같은 도형도 벡터 객체로 남아 크기 조절이 가능합니다.

## Step 3: Set Print Area and Repeat the Title Row

이제 튜토리얼의 핵심인 **인쇄 영역 설정**과 첫 번째 행을 모든 페이지(또는 여기서는 내보낸 슬라이드)에서 반복하도록 하는 작업을 합니다. 인쇄 영역은 Excel이 인쇄하거나 내보낼 셀 범위를 지정합니다.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**왜 중요한가:** `A1:G20` 으로 내보내기를 제한하면 불필요한 빈 영역을 제외할 수 있어 변환 속도가 빨라지고 슬라이드가 깔끔해집니다. `PrintTitleRows` 라인은 첫 번째 행을 헤더처럼 동작하게 하여 프레젠테이션에서 **제목 행 반복**을 구현합니다.

> **Edge case:** 데이터가 2행부터 시작한다면 범위를 적절히 조정하세요 (예: `PrintTitleRows = "$2:$2"`).

## Step 4: Save the Worksheet as a PowerPoint File

마지막으로 슬라이드를 디스크에 저장합니다. `Save` 메서드는 대상 파일명과 앞서 구성한 옵션을 인수로 받습니다. 결과물은 편집 가능한 텍스트 상자와 도형을 포함한 PPTX 파일이며, PowerPoint에서 바로 열 수 있습니다.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**결과 확인:** `SheetWithEditableShapes.pptx` 를 PowerPoint에서 열면 첫 번째 행이 제목으로 표시되고, `A1:G20` 범위의 모든 셀이 렌더링되며, Excel에서 추가한 도형도 그대로 이동·편집이 가능합니다. 래스터 이미지가 아니라 PowerPoint 고유 객체입니다.

## Full Working Example – All Steps Combined

아래는 복사‑붙여넣기만 하면 바로 실행 가능한 전체 프로그램입니다. 콘솔 앱으로 실행하거나 더 큰 솔루션에 포함시켜 사용하세요.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**예상 출력:** 프로그램 실행 후 콘솔에 성공 메시지가 표시되고, 지정한 위치에 PPTX 파일이 생성됩니다. 파일을 열면 선택된 범위와 편집 가능한 텍스트 상자, 원본 도형이 포함된 단일 슬라이드가 나타납니다.

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **Does this work with multiple worksheets?** | Yes. Loop through `workbook.Worksheets` and repeat the same steps for each sheet, changing the output filename each time. |
| **What if I need to export more than one slide?** | Call `workbook.Save` multiple times with different `ImageOrPrintOptions` objects, each configured with a different `PageSetup` if needed. |
| **Can I change the slide size?** | Use `exportOptions.ImageFormat` to set DPI, or adjust `sheet.PageSetup.PaperSize` before saving. |
| **Is Aspose.Cells free?** | It offers a free evaluation with watermarks. For production, a license is required. |
| **What about Excel formulas?** | The exported values are the **calculated results** at the time of export. If you need live formulas in PowerPoint, you’ll need a different approach. |

## Tips for a Smooth Workflow

- **Pro tip:** Set `Workbook.Settings.CalcMode = CalculationModeType.Automatic` before export to guarantee all formulas are up‑to‑date.
- **Watch out for:** Very large ranges can cause memory pressure. Trim the print area to the smallest necessary range.
- **Performance tip:** Reuse a single `ImageOrPrintOptions` instance if you’re exporting many sheets; creating a new one each time adds overhead.
- **Version note:** The code above targets Aspose.Cells 23.10 (released November 2023). Later versions keep the same API, but always double‑check the release notes for breaking changes.

## Conclusion

우리는 Excel 워크시트에서 **인쇄 영역을 설정**하고 첫 번째 행을 제목으로 반복한 뒤, **excel을 pptx로 내보내기**하면서 텍스트 상자와 도형을 편집 가능하게 유지하는 방법을 다뤘습니다. 요약하면, 몇 줄의 C# 코드만으로 **excel to powerpoint 변환**, **제목 행 반복**, **excel에서 powerpoint 만들기**를 신뢰성 있게 수행할 수 있게 되었습니다.

다음 단계가 준비되셨나요? 수십 개의 보고서를 일괄 변환하도록 자동화하거나, 내보낸 후 PowerPoint SDK를 사용해 맞춤 슬라이드 레이아웃을 추가해 보세요. 가능성은 무한합니다—실험하고, 깨고, 프로그래밍 문서 생성의 힘을 즐기세요.

이 튜토리얼이 도움이 되었다면 공유하고, 여러분만의 팁을 댓글로 남기거나 **excel을 pptx로 내보내기**와 관련된 다른 가이드를 살펴보세요. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}