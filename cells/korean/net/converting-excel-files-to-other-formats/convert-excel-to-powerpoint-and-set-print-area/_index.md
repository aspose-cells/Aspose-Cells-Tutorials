---
category: general
date: 2026-10-10
description: Aspose.Cells를 사용한 C#에서 Excel을 PowerPoint로 변환하고 인쇄 영역을 설정하기 – Excel을 내보내고,
  인쇄 영역을 지정하며, PPTX 파일을 생성하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: ko
lastmod: 2026-10-10
og_description: Aspose.Cells를 사용하여 Excel을 PowerPoint로 변환합니다. 이 튜토리얼에서는 인쇄 영역을 설정하고,
  Excel을 내보내며, C#에서 PPTX 파일을 만드는 방법을 보여줍니다.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Excel을 PowerPoint로 변환하기 – C# 개발자를 위한 전체 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Excel을 PowerPoint로 변환하고 인쇄 영역을 설정
url: /ko/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 PowerPoint로 변환하고 인쇄 영역 설정

Excel을 PowerPoint로 **변환**해야 하는 경우, 이 가이드는 C#에서 정확히 수행하는 방법을 보여줍니다. 먼저 인쇄 영역을 정의하면 각 슬라이드에 표시되는 셀을 제어할 수 있으며, 최종 PPTX 파일이 레이아웃 기대치와 일치합니다. 이 솔루션은 동일한 코드 베이스를 사용하여 “Excel 내보내기 방법” 및 “인쇄 영역 설정 방법”에 대한 답변도 제공합니다.

In this tutorial you will:

* 기존 워크북 로드.
* 워크시트에 인쇄 영역 설정 ( **set print area excel** 단계).
* PowerPoint 출력에 대한 변환 옵션 구성.
* 단일 메서드 호출로 **convert excel to pptx** 파일 생성.

필요한 모든 코드는 포함되어 있으므로 바로 복사하고 붙여넣어 실행할 수 있습니다.

## 사전 요구 사항

시작하기 전에 다음이 준비되어 있는지 확인하십시오:

| 요구 사항 | 중요한 이유 |
|-------------|----------------|
| **.NET 6.0 or later** | 샘플은 .NET 6 이상을 대상으로 하지만, C# 10을 지원하는 모든 .NET 버전에서 작동합니다. |
| **Aspose.Cells for .NET** | 이 라이브러리는 `Workbook`, `ImageOrPrintOptions`, 그리고 `ConvertToPdf`(PPTX에 사용) 메서드를 제공합니다. NuGet을 통해 설치하십시오: `dotnet add package Aspose.Cells` |
| **An input Excel file** | 이 튜토리얼은 `input.xlsx`를 사용합니다. 코드에서 참조할 수 있는 폴더에 배치하십시오. |
| **Write permission to the output folder** | 프로그램은 `output.pptx`를 기록합니다. 디렉터리가 존재하고 쓰기 권한이 있는지 확인하십시오. |

> **Pro tip:** 여러 워크시트를 사용하는 경우, 변환 전에 각 시트에 대해 인쇄 영역 단계를 반복하십시오.

## 단계 1: 새로운 C# 콘솔 프로젝트 만들기

터미널 또는 PowerShell 창을 열고 다음을 실행하십시오:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

이 명령은 **ExcelToPowerPointDemo**라는 새 프로젝트를 생성하고 Aspose.Cells 패키지를 추가합니다. 이 패키지는 **how to export Excel**을 다른 형식으로 내보내기 위한 핵심 종속성입니다.

## 단계 2: 변환 코드 작성

`Program.cs`의 내용을 아래 전체 예제로 교체하십시오. 이 코드는 **convert excel to powerpoint**를 시연하고, **how to set print area**를 보여주며, **convert excel to pptx** 파일을 생성합니다.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### 각 부분이 중요한 이유

* **Loading the workbook** – 이는 모든 **how to export Excel** 시나리오에서 첫 번째 단계입니다. `Workbook`은 파일을 메모리로 읽어 시트, 셀 및 서식에 대한 전체 접근 권한을 제공합니다.
* **Setting the print area** – `PageSetup.PrintArea`를 지정함으로써 Aspose.Cells에 렌더링할 셀을 알려줍니다. 이는 **set print area excel**의 핵심이며, 이를 설정하지 않으면 전체 시트가 내보내져 크고 읽기 어려운 슬라이드가 생성될 수 있습니다.
* **Choosing `SaveFormat.Pptx`** – `ImageOrPrintOptions` 객체를 사용하면 출력 형식을 전환할 수 있습니다. `SaveFormat`을 `Pptx`로 설정하면 **convert excel to pptx** 파이프라인이 시작됩니다.
* **Calling `ConvertToPdf`** – 메서드 이름과 달리 `SaveFormat`이 `Pptx`일 때 라이브러리는 PowerPoint 파일을 출력합니다. 이는 단일 호출로 **convert excel to powerpoint**를 수행하는 권장 방법입니다.

## 단계 3: 프로그램 실행

프로젝트 폴더에서 다음을 실행하십시오:

```bash
dotnet run
```

모든 설정이 올바르게 구성되었다면, 다음과 유사한 콘솔 출력이 표시됩니다:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

`output.pptx`를 Microsoft PowerPoint 또는 호환 가능한 뷰어에서 열어보십시오. 각 슬라이드는 정의한 범위에 제한된 워크시트의 인쇄 페이지와 대응합니다.

## 여러 워크시트 처리

워크북에 여러 시트가 포함되어 있고 각 시트를 별도의 슬라이드 데크로 만들고 싶다면, 컬렉션을 반복하십시오:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

이 패턴은 **how to export Excel** 데이터를 시트별로 내보내면서도 개별적으로 **setting print area**를 설정하는 방법을 보여줍니다.

## 엣지 케이스 및 모범 사례 팁

| 상황 | 권장 접근 방식 |
|-----------|----------------------|
| **Very large worksheets** | 인쇄 영역을 축소하거나 `HorizontalResolution`/`VerticalResolution`을 늘려 PPTX 크기를 관리 가능한 수준으로 유지하십시오. |
| **Different page orientations** | 변환 전에 `sheet.PageSetup.Orientation = PageOrientationType.Landscape;`를 설정하십시오. |
| **Custom slide size** | `conversionOptions.OnePagePerSheet = false;`를 사용하고 `conversionOptions.Width` / `conversionOptions.Height`를 조정하십시오. |
| **Missing input file** | 로드 코드를 `try { … } catch (FileNotFoundException)` 블록으로 감싸 명확한 오류 메시지를 제공하십시오. |
| **Non‑ASCII characters** | 워크북이 UTF‑8 인코딩으로 저장되었는지 확인하십시오; Aspose.Cells는 유니코드를 자동으로 처리합니다. |

## 참고용 전체 소스 코드

아래는 `using` 지시문과 주석을 포함한 전체 프로그램입니다. **Step 1**에서 만든 프로젝트 내부에 `Program.cs`로 저장하십시오.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## 예상 출력

프로그램을 실행하면 다음을 포함하는 PowerPoint 파일(`output.pptx`)이 생성됩니다:

* 워크시트의 인쇄 페이지당 하나의 슬라이드.
* 각 슬라이드에 **A1:G30** 범위의 셀만 표시됩니다.
* Excel에 표시된 대로 서식(글꼴, 색상, 테두리)이 유지됩니다.

PowerPoint에서 파일을 열어 레이아웃이 정의한 인쇄 영역과 일치하는지 확인하십시오.

## 결론

이제 Aspose.Cells를 사용한 C#에서 **convert Excel to PowerPoint**를 수행하면서 정확히 **set print area excel**하는 방법을 알게 되었습니다. 이 튜토리얼은 **how to export Excel**을 다루고, **how to set print area**를 시연했으며, 전체 **convert excel to pptx** 과정을 보여주었습니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 단계별 설명과 함께 완전한 작동 코드 예제를 제공하여 추가 API 기능을 마스터하고 자체 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET를 사용하여 Excel에서 인쇄 영역 설정 방법](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Excel에서 인쇄 영역 설정 및 PowerPoint로 내보내기 – 단계별 가이드](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Excel 인쇄 영역 설정 Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}