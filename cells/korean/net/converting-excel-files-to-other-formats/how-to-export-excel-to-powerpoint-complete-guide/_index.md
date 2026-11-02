---
category: general
date: 2026-07-03
description: Aspose.Cells를 사용하여 편집 가능한 텍스트 상자가 포함된 PowerPoint로 Excel 파일을 내보내는 방법 –
  XLSX를 PPTX로 변환하는 단계별 가이드.
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: ko
og_description: 편집 가능한 텍스트 상자를 포함하여 Excel을 PowerPoint로 내보내는 방법. C#에서 PresentationExportOptions를
  사용해 XLSX를 PPTX로 변환하는 방법을 배워보세요.
og_title: Excel을 PowerPoint로 내보내는 방법 – 완전 가이드
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: Excel을 PowerPoint로 내보내는 방법 – 완전 가이드
url: /ko/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 PowerPoint로 내보내는 방법 – 완전 가이드

Excel 데이터를 편집 가능한 상태로 바로 PowerPoint 슬라이드에 **내보내는 방법**이 궁금하셨나요? 여러분만 그런 것이 아닙니다. 이 튜토리얼에서는 **Excel에서 PowerPoint 만들기**를 실현하면서 텍스트 상자와 도형을 완전히 편집 가능하게 유지하는 실용적인 방법을 보여드립니다.

코드 한 줄 한 줄을 살펴보고, 각 설정이 왜 중요한지 설명한 뒤, 바로 열어보고 수정할 수 있는 PowerPoint 파일을 만들어 드립니다. 최종적으로 **XLSX를 PPTX로 변환**하는 단일 메서드 호출을 수행하고, **프레젠테이션 내보내기 옵션**이 결과에 어떤 영향을 주는지 이해하게 될 것입니다.

## 준비물

시작하기 전에 다음이 준비되어 있는지 확인하세요:

- **.NET 6.0**(또는 최신 .NET 버전) 설치  
- **Aspose.Cells for .NET** 라이선스(무료 체험판으로 테스트 가능)  
- C#에 대한 기본적인 이해—콘솔 앱이나 작은 라이브러리를 만들 수 있는 수준이면 충분합니다.  
- 슬라이드 덱으로 변환하고 싶은 Excel 워크북(`input.xlsx`)

이것만 있으면 됩니다. 별도의 도구나 COM 인터옵 없이 순수 관리 코드만으로 가능합니다.

![How to export excel to PowerPoint diagram](https://example.com/placeholder.png "Diagram showing the flow of how to export excel data into PowerPoint")

## 단계 1: Aspose.Cells 설치 및 프로젝트 설정

**Excel을 내보내는 방법**을 구현하려면 먼저 해당 라이브러리를 설치해야 합니다. 프로젝트 폴더에서 터미널을 열고 다음을 실행하세요:

```bash
dotnet add package Aspose.Cells
```

이 명령은 NuGet에서 최신 Aspose.Cells 패키지를 가져옵니다. 라이브러리는 **프레젠테이션 내보내기 옵션**에 필요한 모든 기능을 포함하고 있어 Office Interop 어셈블리를 별도로 참조할 필요가 없습니다.

> **Pro tip:** .NET Framework를 대상으로 하는 경우 호환성 문제를 피하기 위해 적절한 NuGet 버전(예: `Aspose.Cells.NET`)을 사용하세요.

## 단계 2: Excel 워크북 로드

라이브러리가 준비되었으니 이제 원본 파일을 로드합니다. `Workbook` 클래스는 전체 Excel 문서를 나타냅니다.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*왜 중요한가:* 워크북을 로드하는 것은 **XLSX를 PPTX로 변환** 워크플로의 첫 단계입니다. `Workbook` 객체는 시트, 차트, 셀 서식 등을 보관하고 있으며, 이후 PowerPoint 객체와 매핑될 수 있습니다.

## 단계 3: 프레젠테이션 내보내기 옵션 설정 (편집 가능한 텍스트 상자)

여기가 핵심입니다. 기본적으로 Aspose.Cells는 도형을 정적 이미지로 내보냅니다. **편집 가능한 텍스트 상자**를 유지하려면 올바른 플래그를 활성화해야 합니다.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **`ExportEditableObjects`를 활성화하는 이유**  
> 이 속성이 `true`이면 Aspose.Cells는 각 Excel 도형을 PowerPoint 고유 도형으로 변환합니다. 따라서 결과 `.pptx` 파일을 PowerPoint에서 열어 텍스트를 직접 편집하고, 상자의 크기를 조절하거나 색상을 변경할 수 있습니다—즉 **Excel에서 PowerPoint 만들기** 시 기대하는 바로 그 동작입니다.

## 단계 4: 워크북을 PowerPoint로 내보내기

워크북을 로드하고 옵션을 설정했으니, 마지막 줄에서 파일을 PowerPoint 프레젠테이션으로 저장합니다.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*예상 결과:* `output.pptx` 파일은 기본적으로 워크시트당 하나의 슬라이드를 포함합니다. 각 슬라이드는 원본 시트 레이아웃을 그대로 반영하며, Excel에 배치한 모든 텍스트 상자는 이제 PowerPoint에서 **편집 가능한 텍스트 상자**가 됩니다.

## 단계 5: 결과 확인 및 필요 시 조정

Microsoft PowerPoint에서 `output.pptx`를 엽니다:

1. 워크시트에서 생성된 슬라이드로 이동합니다.  
2. 텍스트 상자를 클릭하면 바로 텍스트를 편집할 수 있음을 확인합니다.  
3. 도형의 크기나 색을 조정해 보세요; 변경 내용이 그대로 유지됩니다.

문제가 있다면 다음과 같은 조정을 고려해 보세요:

- **특정 시트만 내보내기:** 저장하기 전에 `workbook.Worksheets.RemoveAt(index)` 사용  
- **슬라이드 레이아웃 제어:** `exportOptions.ExportAllSheetsAsSlide = false` 로 설정하고 슬라이드를 수동으로 추가  
- **차트 서식 유지:** 내보내기 전에 차트를 시트에 배치하면 자동으로 PowerPoint 차트로 변환됩니다

## 흔히 발생하는 문제와 해결 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| 도형이 이미지로 변환됨 | `ExportEditableObjects`가 기본값(`false`)인 상태 | 단계 3에서 `ExportEditableObjects = true` 로 설정 |
| 워크시트 누락 | 원하지 않는 시트를 제거하기 전에 `Save` 호출 | 내보내기 전에 필요 없는 시트를 제거하거나 숨김 처리 |
| 파일 크기 과다 | 도형과 함께 고해상도 이미지가 삽입됨 | 필요에 따라 `exportOptions.ImageResolution = 150` 로 DPI 낮추기 |
| PowerPoint 호환성 경고 | 오래된 Aspose.Cells 버전 사용 | 최신 NuGet 패키지로 업그레이드( PPTX 2016+ 지원 ) |

## 전체 작업 예제

아래는 콘솔 앱에 복사‑붙여넣기 할 수 있는 완전한 프로그램 예제입니다. 모든 단계, 오류 처리, 주석이 포함되어 있습니다.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**콘솔에 출력되는 예상 내용:**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

생성된 `output.pptx`를 열어 보면 각 워크시트가 슬라이드로 변환되고, Excel에 추가한 모든 도형이 이제 **편집 가능한 텍스트 상자**가 되어 자유롭게 수정할 수 있습니다.

## 요약: Excel을 빠르고 깔끔하게 내보내는 방법

우리는 **Excel을 내보내는 방법** 전체 과정을 다루었습니다—Aspose.Cells 설치, **프레젠테이션 내보내기 옵션** 구성, 그리고 완전 편집 가능한 콘텐츠와 함께 **XLSX를 PPTX로 변환**까지. 핵심 포인트는 다음과 같습니다:

- `PresentationExportOptions.ExportEditableObjects = true` 로 설정해 도형을 편집 가능하게 유지  
- `Workbook.Save` 메서드가 핵심 작업을 수행하므로 COM 인터옵이 전혀 필요 없음  
- 이미지 해상도, 시트 선택 등 선택 옵션을 조정해 결과물을 미세 조정

## 다음 단계는?

스프레드시트를 슬라이드로 변환하는 작업이 마음에 든다면 다음 주제도 살펴보세요:

- **차트를 네이티브 PowerPoint 차트**로 내보내기 (`exportOptions.ExportChartAsShape = false`)  
- **맞춤 슬라이드 마스터** 적용해 기업 브랜딩에 맞추기  
- **배치 변환 자동화**—`foreach` 루프를 사용해 수십 개 파일을 한 번에 처리  

위 모든 내용은 방금 다룬 기본 원리를 기반으로 하므로 이미 탄탄한 기반을 갖추고 있습니다.

---

궁금한 점이 있거나 진행 중에 어려움이 발생하면 댓글로 알려 주세요. 여러분만의 프로젝트에 이 패턴을 어떻게 확장했는지 공유해 주셔도 좋습니다. 즐거운 코딩 되시고, Excel과 PowerPoint 사이의 매끄러운 연결을 만끽하세요!


## 다음에 배워야 할 내용은?


다음 튜토리얼들은 이번 가이드에서 다룬 기술을 기반으로 하여 연관된 주제를 깊이 있게 다룹니다. 각 리소스에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Add and Access Text Boxes in Excel using Aspose.Cells .NET | Step-by-Step Guide](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}