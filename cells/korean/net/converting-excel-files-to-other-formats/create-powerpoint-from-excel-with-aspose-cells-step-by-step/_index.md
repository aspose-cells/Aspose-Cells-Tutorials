---
category: general
date: 2026-10-01
description: C#에서 Aspose.Cells를 사용하여 Excel에서 PowerPoint를 생성합니다. Excel을 PowerPoint로
  내보내고 XLSX를 PPTX로 빠르게 변환하는 완전한 코드 예제와 함께 제공합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: ko
lastmod: 2026-10-01
og_description: C#에서 Aspose.Cells를 사용하여 Excel에서 PowerPoint를 생성하세요. 몇 줄의 코드로 Excel을
  PowerPoint로 내보내고 XLSX를 PPTX로 변환하는 방법을 배워보세요.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Aspose.Cells를 사용해 Excel에서 PowerPoint 만들기 – 빠른 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Aspose.Cells로 Excel에서 PowerPoint 만들기 – 단계별 가이드
url: /ko/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 PowerPoint 만들기 (Aspose.Cells 사용) – 단계별 가이드

Excel에서 PowerPoint를 **생성**해야 한다면, 이 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 수행하는 방법을 보여줍니다. **Excel을 PowerPoint로 내보내기**, XLSX 워크북을 PPTX 프레젠테이션으로 변환하고, C# 프로젝트를 떠나지 않고 결과 슬라이드를 사용자 지정하는 방법을 배울 수 있습니다.

이 가이드는 .NET 6 이상에서 코드를 실행하는 데 필요한 모든 사항을 다루며, 프로젝트 설정, 필수 NuGet 패키지, 완전하고 실행 가능한 예제를 포함합니다. 최종적으로 원본 Excel 차트가 워크북에 표시된 그대로 포함된 PowerPoint 파일을 얻을 수 있습니다.

## 필요한 사항

| 전제조건 | 이유 |
|---|---|
| .NET 6 SDK 이상 | C# 콘솔 앱 실행 환경 제공 |
| Visual Studio 2022 (또는 기타 IDE) | 프로젝트 생성 및 디버깅을 쉽게 할 수 있음 |
| Aspose.Cells for .NET NuGet 패키지 | `Workbook` 클래스와 내보내기 API 제공 |
| 하나 이상의 차트가 포함된 Excel 파일(`.xlsx`) | PowerPoint 슬라이드의 원본 데이터 |

> **전문가 팁:** Aspose.Cells는 Windows, Linux, macOS에서 작동하므로 Docker 컨테이너나 CI 파이프라인에서도 동일한 코드를 실행할 수 있습니다.

## 단계 1: 새 콘솔 프로젝트 생성 및 Aspose.Cells 추가

터미널(또는 Visual Studio 패키지 관리자 콘솔)을 열고 다음을 실행합니다:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

`dotnet add package` 명령은 **Aspose.Cells**의 최신 안정 버전을 다운로드하며, 여기에는 이후에 사용할 `ExportPptx` 메서드가 포함됩니다.

## 단계 2: 원본 Excel 워크북 추가

변환하려는 Excel 파일을 프로젝트 폴더에 넣습니다. 이 튜토리얼에서는 첫 번째 워크시트에 단일 차트가 포함된 `ChartOle.xlsx`를 사용합니다.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## 단계 3: **Excel에서 PowerPoint를 생성**하는 코드 작성

`Program.cs`를 열고 내용을 다음 코드로 교체합니다. 예제는 **핵심 내보내기** 작업을 보여주며, 파일 누락 및 지원되지 않는 차트 유형과 같은 일반적인 예외 상황을 처리하는 방법도 포함합니다.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### 작동 원리

* `Workbook`은 포함된 차트, 테이블 및 서식을 포함한 전체 Excel 파일을 읽습니다.
* `ExportPptx`는 현재 워크시트를 PPTX 슬라이드 덱으로 변환합니다. 이 메서드는 Excel 차트를 자동으로 PowerPoint 도형으로 변환하여 시각적 정확성을 유지합니다.
* 코드는 `try/catch` 블록으로 작업을 감싸서 손상된 파일로 인한 **XLSX를 PPTX로 변환** 실패와 같은 오류를 표시합니다.

## 단계 4: 프로그램 실행 및 출력 확인

애플리케이션을 실행합니다:

```bash
dotnet run
```

콘솔에 다음 메시지가 표시됩니다:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

`Exported.pptx`를 Microsoft PowerPoint 또는 호환 뷰어에서 엽니다. 첫 번째 슬라이드에 `ChartOle.xlsx`에 있던 차트가 그대로 표시됩니다. 이는 **Excel에서 PowerPoint를 성공적으로 생성**했음을 확인하는 것입니다.

## 단계 5: 고급 – 여러 워크시트 내보내기 또는 사용자 정의 슬라이드 레이아웃

기본 예제는 첫 번째 워크시트만 내보냅니다. 실제 상황에서는 다음이 필요할 수 있습니다:

* **여러 워크시트 내보내기**를 통해 각각을 별도 슬라이드로 만들기.
* **슬라이드 크기 제어** 또는 제목 플레이스홀더 추가.
* **숨겨진 워크시트 포함** 변환.

아래는 모든 워크시트를 순회하며 각각을 별도 슬라이드로 추가하는 간결한 스니펫입니다:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **참고:** 고급 스니펫은 **Aspose.Slides for .NET** 라이브러리가 필요합니다. 단순히 한 시트만 변환하면 된다면 이전의 `ExportPptx` 호출만으로 충분합니다.

## 흔히 발생하는 문제와 해결 방법

| 문제 | 원인 | 해결책 |
|---|---|---|
| 내보낸 후 빈 슬라이드 | 워크시트에 보이는 객체가 없음 | `ExportPptx` 호출 전에 최소 하나의 차트, 테이블 또는 도형이 존재하도록 합니다. |
| PowerPoint에서 폰트 누락 | PPTX를 여는 머신에 폰트가 설치되지 않음 | 필요한 폰트를 Excel 워크북에 포함시키거나 대상 시스템에 설치합니다. |
| 예상치 못한 스케일링 | 큰 차트가 슬라이드 크기를 초과 | 내보내기 전에 워크시트의 `PageSetup.Zoom` 속성을 조정합니다. |
| `convert XLSX to PPTX`가 `NotSupportedException`을 발생 | Aspose.Cells에서 지원하지 않는 차트 유형(예: 3D 지도) | 지원되는 유형으로 차트를 교체하거나 먼저 시트를 이미지로 내보냅니다. |

이러한 예외 상황을 처리하면 프로덕션 환경에서 신뢰할 수 있는 **Excel을 PowerPoint로 내보내기** 워크플로를 보장할 수 있습니다.

## 결론

이제 Aspose.Cells for .NET을 사용해 **Excel에서 PowerPoint를 생성**하는 방법을 알게 되었습니다. 튜토리얼에서는 다음을 다루었습니다:

* 프로젝트 설정 및 NuGet 설치
* Excel 워크북 로드 및 `ExportPptx` 호출
* 코드 실행 및 생성된 PPTX 확인
* 다중 워크시트 및 사용자 정의 레이아웃을 처리하도록 솔루션 확장
* 일반 변환 문제 회피를 위한 실용적인 팁

이 지식을 활용하면 보고서 자동화, 프레젠테이션 파이프라인 구축, 혹은 Excel‑to‑PowerPoint 변환을 모든 C# 애플리케이션에 통합할 수 있습니다. 다양한 차트 유형을 실험하고, 슬라이드 제목을 추가하거나, Aspose.Slides와 결합해 전체 기능을 갖춘 프레젠테이션을 만들어 보세요.

--- 

*더 알아보고 싶으신가요? **Excel을 PDF로 변환**, **Excel 데이터를 Word에 삽입**, 또는 **Aspose.Slides를 사용해 프로그래밍 방식으로 PPTX 파일 편집**과 같은 관련 주제를 확인해 보세요.*

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접하게 관련된 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}