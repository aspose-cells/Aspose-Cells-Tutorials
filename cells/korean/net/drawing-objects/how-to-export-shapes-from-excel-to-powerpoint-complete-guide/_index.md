---
category: general
date: 2026-07-26
description: 몇 단계만으로 Excel 워크시트의 도형을 PowerPoint로 내보내는 방법 – 개발자를 위한 빠른 Excel → PPTX
  내보내기 튜토리얼.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: ko
lastmod: 2026-07-26
og_description: Excel에서 PowerPoint로 도형을 단계별로 내보내는 방법. 이 Excel을 PPTX로 내보내는 튜토리얼을 따라
  하면 워크시트가 편집 가능한 슬라이드로 변환되는 것을 확인할 수 있습니다.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Excel에서 PowerPoint로 도형 내보내는 방법 – 빠르고 쉬운
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Excel에서 PowerPoint로 도형을 내보내는 방법 – 완전 가이드
url: /ko/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 PowerPoint로 도형 내보내기 – 완전 가이드

Excel 파일에서 **도형을 내보내는 방법**을 궁금해 본 적 있나요? 그리고 PowerPoint 데크에서 편집 가능하게 유지하는 방법도요? 당신만 그런 것이 아닙니다. 보고 파이프라인을 구축하든, 단순히 스프레드시트를 프레젠테이션으로 빠르게 변환해야 하든, **워크시트를 PowerPoint로 변환**하면서 도형 편집 가능성을 잃지 않는 기능은 수시간의 수작업을 절약해 줍니다.

이 **excel to powerpoint tutorial**에서는 워크북을 로드하고, 올바른 내보내기 옵션을 구성한 뒤, 텍스트 상자와 기타 그리기 객체가 편집 가능한 상태로 남는 PPTX 파일을 작성하는 완전한 C# 예제를 단계별로 살펴봅니다. 모호한 설명이 아니라 바로 복사·붙여넣기·실행할 수 있는 코드만 제공합니다.

## 배울 내용

- 도형 편집 가능성을 유지하면서 **excel을 pptx로 내보내는** 정확한 단계  
- `Aspose.Cells` 라이브러리의 `PptxSaveOptions`가 내보내기 동작을 제어하는 방법  
- 여러 워크시트, 파일 누락, 사용자 지정 도형 설정을 처리하기 위한 팁  
- 어떤 .NET 프로젝트에도 넣어 사용할 수 있는 완전한 실행 가능한 프로그램  

### 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 작동합니다).  
- **Aspose.Cells for .NET**에 대한 유효한 라이선스 (무료 체험판으로 테스트 가능).  
- 하나 이상의 텍스트 상자 또는 도형을 포함한 Excel 워크북 (예: `ShapesDemo.xlsx`).  
- 개발 환경 — Visual Studio, Rider, 또는 VS Code 중 하나면 충분합니다.  

위 조건을 갖추셨다면, 시작해 봅시다.

## Step 1: 워크북 로드 – 도형 내보내기의 시작점

먼저 편집 가능한 상태로 유지하려는 도형이 들어 있는 Excel 파일을 열어야 합니다.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**왜 중요한가:**  
`Workbook` 객체는 파일 내부의 모든 셀, 차트 및 그리기 객체에 접근할 수 있는 관문입니다. 첫 번째 워크시트(`Worksheets[0]`)를 가져오면 알려진 시트에서 작업한다는 것을 보장하지만, 특정 탭이 필요하면 인덱스를 이름(`workbook.Worksheets["Sheet2"]`)으로 교체할 수 있습니다.

> **팁:** 파일 경로가 잘못되었을 경우 친절한 오류를 제공하도록 `try / catch` 블록으로 로드 호출을 감싸세요.

## Step 2: PPTX 내보내기 옵션 구성 – 도형 내보내기의 핵심

이제 Aspose.Cells에 결과 PPTX에서 도형을 편집 가능하게 유지하도록 지시합니다.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**왜 이러한 플래그인가?**  
- `ExportEditableTextBoxes`는 Excel 텍스트 상자를 PowerPoint 텍스트 자리표시자로 변환하여 더블 클릭으로 편집할 수 있게 합니다.  
- `ExportEditableShapes`는 화살표, 사각형, SmartArt와 같은 도형을 동일하게 변환합니다. 이 플래그가 없으면 객체가 정적 이미지가 되어 **워크시트를 PowerPoint로 변환**하는 목적에 어긋납니다.  

`PptxSaveOptions`를 조정하여 슬라이드 크기, 테마, 글꼴 포함 여부 등을 제어할 수 있습니다—프레젠테이션이 기업 브랜드와 일치해야 할 때 유용합니다.

## Step 3: 워크시트를 PPTX로 저장 – Excel 워크북을 PowerPoint로 내보내는 최종 단계

옵션을 설정했으면 저장은 간단합니다.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**내부에서 무슨 일이 일어나나요?**  
Aspose.Cells는 시트의 모든 그리기 객체를 순회하면서 해당 PowerPoint 도형 클래스로 매핑하고 PowerPoint가 읽는 XML을 작성합니다. 편집 가능한 플래그를 활성화했기 때문에 XML은 각 도형을 `Picture`가 아닌 `Shape`로 표시하여 PowerPoint가 이를 실시간 객체로 취급합니다.

## Step 4: 내보내기 확인 – 사용자에게 빠른 피드백 제공

작은 콘솔 메시지가 프로세스가 성공했음을 알려줍니다.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

프로그램을 실행해 메시지가 표시되면 PowerPoint에서 `ShapesEditable.pptx`를 엽니다. 텍스트 상자를 클릭하면 직접 텍스트를 편집할 수 있고, 도형을 드래그하면 기본 PowerPoint 객체처럼 이동합니다.

## Step 5: 실제 시나리오 처리

아래에 **excel to powerpoint tutorial**을 진행하면서 마주칠 수 있는 일반적인 변형 사례를 소개합니다.

### 여러 워크시트

여러 시트를 하나의 PPTX로 내보내야 한다면 `workbook.Worksheets`를 순회하면서 동일한 `pptxOptions`로 `worksheet.Save`를 호출합니다. Aspose.Cells는 각 시트마다 자동으로 새 슬라이드를 추가합니다.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### 사용자 지정 슬라이드 레이아웃

`pptxOptions.SlideSize`(예: `SlideSizeType.Widescreen`)를 지정하여 기업 프레젠테이션 크기에 맞출 수 있습니다.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### 파일 누락 또는 권한 문제

`Main` 메서드 전체를 `try` 블록으로 감싸세요:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

이렇게 하면 **export excel workbook powerpoint** 프로세스가 프로덕션 파이프라인에서도 견고해집니다.

## 전체 작업 예제

지금 바로 컴파일할 수 있는 전체 프로그램입니다. `ExportEditableShapes.cs`로 저장하고 파일 경로를 조정한 뒤 `dotnet run`을 실행하세요.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

프로그램 실행 시 **예상 출력**:

```
Exported worksheet with editable shapes.
```

생성된 `ShapesEditable.pptx`를 열면 각 Excel 도형이 완전히 편집 가능한 PowerPoint 객체로 표시됩니다—**how to export shapes**를 검색했을 때 원했던 바로 그 결과입니다.

## 자주 묻는 질문

- **이것이 오래된 Excel 형식(.xls)에서도 작동하나요?**  
  네. `Workbook`은 `.xls`, `.xlsx`, 그리고 CSV 파일도 열 수 있습니다. 도형 내보내기는 동일하게 작동합니다.  

- **차트를 편집 가능하게 유지하려면 어떻게 해야 하나요?**  
  차트는 이미 기본 PowerPoint 차트로 내보내지므로 추가 플래그가 필요 없습니다.  

- **PPTX 대신 PDF로 내보낼 수 있나요?**  
  물론입니다—`SaveFormat.Pptx`를 `SaveFormat.Pdf`로 바꾸고 `PptxSaveOptions`를 생략하면 됩니다.  

## 결론

이제 Excel에서 편집 가능한 PowerPoint 데크로 **도형을 내보내는** 완전한 솔루션을 갖추었습니다. `Aspose.Cells`의 `PptxSaveOptions`를 활용하면 모든 텍스트 상자와 그리기 객체를 보존하여 정적인 스프레드시트를 최소한의 노력으로 동적인 프레젠테이션으로 변환합니다.

다음 도전에 준비가 되셨나요? 사용자 지정 슬라이드 마스터 추가, 이미지 프로그래밍 삽입, 혹은 이 내보내기를 CI/CD 파이프라인에 연결해 주간 영업 자료를 자동 생성해 보세요. **export excel workbook powerpoint** 세계는 무한히 열려 있습니다—탐험해 보세요!

--- 

*이 **excel to powerpoint tutorial**이 도움이 되었다면 GitHub에 별표를 달거나 여전히 스프레드시트를 슬라이드에 복사‑붙여넣는 동료와 공유하세요. 즐거운 코딩 되세요!*

## 다음에 배울 내용

다음 튜토리얼은 이 가이드에서 보여준 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 완전한 작업 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Aspose.Cells Java를 사용하여 Excel 워크시트를 PNG로 내보내는 방법](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Aspose.Cells for Java를 사용하여 Excel 셀을 이미지로 내보내는 방법](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [Aspose.Cells Java를 사용하여 Excel 차트를 SVG(확장 가능한 벡터 그래픽)로 내보내는 방법](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}