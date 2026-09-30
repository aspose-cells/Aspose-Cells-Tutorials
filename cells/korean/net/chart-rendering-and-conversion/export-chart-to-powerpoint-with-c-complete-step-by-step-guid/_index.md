---
category: general
date: 2026-02-26
description: C#를 사용하여 Excel에서 PowerPoint로 차트를 내보내기. Excel을 PowerPoint로 변환하고, Excel을
  PowerPoint로 저장하며, 도형을 편집 가능하게 유지하는 방법을 배워보세요.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: ko
og_description: C#를 사용하여 Excel에서 PowerPoint로 차트를 내보내기. 이 가이드는 Excel을 PowerPoint로 변환하고,
  워크북을 PPTX 형식으로 저장하며, 도형을 편집 가능하게 유지하는 방법을 보여줍니다.
og_title: C#로 차트를 PowerPoint에 내보내기 – 완전 프로그래밍 튜토리얼
tags:
- Aspose.Cells
- C#
- Office Automation
title: C#로 차트를 PowerPoint에 내보내기 – 완전한 단계별 가이드
url: /ko/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 차트를 PowerPoint로 내보내기 – 완전 프로그래밍 튜토리얼

**차트를 PowerPoint로 내보내기** 할 때 편집 가능성을 유지하고 싶으셨나요? 많은 보고 시나리오에서 슬라이드에 실시간 차트가 필요하지만, 복사‑붙여넣기를 수동으로 하는 것은 번거롭습니다. 좋은 소식은 몇 줄의 C# 코드만으로 프로그래밍 방식으로 구현할 수 있다는 것입니다.

이 가이드에서는 차트와 텍스트 상자가 포함된 Excel 워크북을 로드하고, 텍스트 상자와 도형이 편집 가능하도록 내보내기 옵션을 설정한 뒤, 최종 결과를 **PowerPoint** 파일로 저장하는 전체 과정을 단계별로 살펴봅니다. 끝까지 읽으시면 **Excel을 PowerPoint로 변환하기**, **Excel을 PowerPoint로 저장하기** 방법과 특수 상황을 위한 옵션 조정 방법도 알게 됩니다.

## 준비물

- **Aspose.Cells for .NET** (버전 23.10 이상). 변환을 손쉽게 해주는 라이브러리입니다.
- **.NET 6+** 런타임 – 최신 SDK이면 모두 사용 가능.
- 차트와 텍스트 상자가 최소 하나씩 들어 있는 간단한 Excel 파일 (`ChartWithTextbox.xlsx`).
- Visual Studio 또는 선호하는 IDE.

Aspose.Cells 외에 추가 NuGet 패키지는 필요하지 않으며, C# 기본 문법에 대한 이해가 있으면 도움이 됩니다.

## 차트를 PowerPoint로 내보내기 – 단계별 가이드

아래에서는 솔루션을 이해하기 쉬운 단계로 나누어 설명합니다. 각 단계마다 필요한 정확한 코드와 함께 “왜 이렇게 하는가”에 대한 짧은 설명을 제공합니다.

### 단계 1: 차트가 포함된 Excel 워크북 로드

먼저 원본 파일을 메모리로 불러와야 합니다. Aspose.Cells의 `Workbook`을 사용하면 차트, 이미지, 임베디드 객체를 모두 포함한 전체 스프레드시트를 읽을 수 있습니다.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*왜 중요한가:* 경로를 잘못 지정해 워크북을 열면 `FileNotFoundException`이 발생합니다. 간단한 검증을 통해 나중에 빈 슬라이드가 생성되는 상황을 방지할 수 있습니다.

### 단계 2: 도형을 편집 가능하게 유지하기 위한 프레젠테이션 옵션 설정

Aspose.Cells에서는 텍스트 상자, 도형, 차트 자체를 **편집 가능**하게 유지할지 여부를 선택할 수 있습니다. `ExportTextBoxes`와 `ExportShapes`를 `true`로 설정하면 해당 객체들이 정적 이미지가 아니라 PowerPoint 고유 요소로 보존됩니다.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*왜 중요한가:* 이 플래그를 기본값(`false`) 그대로 두면 결과 슬라이드에 차트가 비트맵 이미지로 삽입되어 시리즈를 수정하거나 캡션을 바꿀 수 없습니다. 두 옵션을 모두 활성화하면 수동으로 만든 차트와 동일하게 완전 편집 가능한 PowerPoint 차트를 얻을 수 있습니다.

### 단계 3: Excel을 PowerPoint로 변환하고 파일 저장

이제 `Save` 메서드를 호출하면서 `SaveFormat.Pptx` 열거형과 앞서 구성한 옵션을 전달합니다. 라이브러리가 Excel 차트 객체를 PowerPoint 차트 도형으로 변환해 줍니다.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*왜 중요한가:* `Save` 호출이 모든 핵심 작업을 수행합니다—Excel 시리즈를 PowerPoint 시리즈에 매핑하고, 축 서식을 보존하며, 연결된 텍스트 상자를 복사합니다. 이 라인이 실행되면 완전 편집 가능한 `.pptx` 파일이 생성되어 Microsoft PowerPoint에서 바로 열 수 있습니다.

### 결과 확인

PowerPoint에서 `Result.pptx`를 열어보세요. 슬라이드에 다음이 표시되어야 합니다:

- 원본 차트가 그대로 남아 데이터와 연결됨(더블 클릭하면 시리즈 편집 가능).
- Excel 시트에 있던 텍스트 상자가 이제 PowerPoint 텍스트 상자로 변환됨.
- 슬라이드 레이아웃이 자동으로 선택됨(보통 빈 슬라이드).

요소가 누락된 경우, 원본 워크북에 실제로 보이는 객체가 있었는지와 `ExportTextBoxes` / `ExportShapes`가 `true`로 설정되었는지 다시 확인하세요.

### Excel을 PowerPoint로 변환: 여러 워크시트 처리

워크북에 여러 시트가 있고 각각 차트가 있는 경우가 많습니다. 기본적으로 Aspose.Cells는 **모든** 워크시트의 **모든** 차트를 개별 슬라이드로 내보냅니다. 일부만 필요하면 저장 전에 필터링할 수 있습니다.

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*팁:* `chart.IsVisible = false` 로 설정하면 차트를 완전히 삭제하지 않아도 되며, 원본 파일을 수정하지 않고 포함 여부를 토글할 수 있어 비용 효율적입니다.

### Excel을 PowerPoint로 저장 – 슬라이드 크기 맞춤

PowerPoint 기본 슬라이드 크기는 10인치 × 5.63인치입니다. 차트가 좁게 보인다면 `PresentationOptions` 객체를 통해 슬라이드 크기를 조정할 수 있습니다.

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

이제 내보낸 차트에 여유 공간이 생기고, 텍스트 상자도 원래 레이아웃을 유지합니다.

### Excel을 PPT로 변환: 숨겨진 객체 처리

숨겨진 행, 열, 도형이 내보내기 과정에 포함될 수 있습니다. 저장 전에 간단히 정리하면 이러한 문제를 방지할 수 있습니다.

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

필수 단계는 아니지만, 최종 슬라이드에 예상치 못한 빈 공간이 생기는 것을 막아줍니다.

### 워크북을 PPTX로 저장 – 전체 작동 예제

모든 단계를 하나로 합친 콘솔 프로그램 예제입니다. 바로 실행해 볼 수 있습니다.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

이 프로그램을 실행하면 **워크북을 pptx로 저장**했을 때와 동일하게 편집 가능한 차트와 텍스트 상자가 포함된 `Result.pptx`가 생성됩니다.

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – editable slide")

## 자주 묻는 질문 및 엣지 케이스

**Excel 파일에 외부 데이터 소스와 연결된 차트가 포함되어 있으면 어떻게 되나요?**  
Aspose.Cells는 현재 데이터 값을 PowerPoint 차트에 복사합니다. 외부 연결은 보존되지 않으며, PowerPoint는 동일한 방식으로 Excel 데이터 연결을 참조할 수 없습니다. 실시간 업데이트가 필요하면 원본 Excel 파일을 OLE 객체로 PPTX에 삽입하는 방법을 고려하세요.

**사용자 정의 테마가 적용된 차트를 내보낼 수 있나요?**  
가능합니다. 라이브러리는 Excel 테마 색상을 PowerPoint 테마 슬롯에 매핑하려 시도합니다. 매우 특수한 팔레트인 경우, PowerPoint API(예: Aspose.Slides)를 사용해 색상을 추가로 조정해야 할 수도 있습니다.

**차트 개수에 제한이 있나요?**  
실질적인 제한은 없습니다. Aspose.Cells는 데이터를 스트리밍하므로 수십 개의 차트가 있는 워크북도 정상적으로 내보낼 수 있지만, 결과 PPTX 파일 크기는 차트 수에 비례해 증가합니다.

**Aspose.Cells 라이선스가 필요합니까?**  
무료 평가판을 사용할 수 있지만 첫 슬라이드에 워터마크가 삽입됩니다. 프로덕션 환경에서는 정식 라이선스를 구매해 워터마크를 제거하고 전체 성능을 활용하세요.

## 요약

C#을 사용해 **차트를 PowerPoint로 내보내는** 방법을 살펴보았습니다. Excel 워크북 로드, 텍스트 상자와 도형을 편집 가능하게 유지하는 `PresentationOptions` 설정, 그리고 `.pptx` 파일로 저장하는 전체 흐름을 정확한 코드와 함께 제공했습니다. 또한 **Excel을 PowerPoint로 변환하기**, **Excel을 PowerPoint로 저장하기**, 그리고 “**Excel을 ppt로 변환하는 방법**”에 대한 완전한 실행 예제도 확인했습니다.

## 다음 단계

- **워크북을 PPTX로 저장**하면서 여러 슬라이드 만들기: 각 워크시트를 순회하며 `PresentationOptions`를 사용해 `Save` 호출.
- 생성된 PPTX를 추가로 수정하려면 **Aspose.Slides**를 탐색해 보세요(전환 효과, 발표자 메모 등 추가 가능).
- **피벗 차트** 또는 **3‑D 차트** 내보내기 시도 – 동일 옵션이 적용되지만 축 서식 조정이 필요할 수 있습니다.

문제가 발생하면 아래에 댓글을 남기거나 최신 API 변경 사항은 공식 Aspose.Cells 문서를 참고하세요. 즐거운 코딩 되시고, 몇 줄의 C# 코드만으로 Excel 차트를 깔끔한 PowerPoint 프레젠테이션으로 변환해 보세요!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}