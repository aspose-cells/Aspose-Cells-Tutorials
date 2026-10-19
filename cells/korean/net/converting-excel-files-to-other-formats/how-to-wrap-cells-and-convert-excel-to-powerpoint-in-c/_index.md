---
category: general
date: 2026-09-18
description: Excel 워크북에서 셀을 래핑하고 PowerPoint 파일로 저장하는 방법. WRAPCOLS 사용법, 워크북 워크시트 만들기,
  PPTX로 내보내기 배우기.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: ko
lastmod: 2026-09-18
og_description: C#를 사용하여 Excel에서 셀을 자동 줄바꿈하고 워크북을 편집 가능한 PowerPoint 파일로 내보내는 방법. 단계별
  가이드를 따라 WRAPCOLS와 워크북 워크시트 생성을 마스터하세요.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: C#에서 셀을 자동 줄바꿈하고 Excel을 PowerPoint로 변환하는 방법
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: C#에서 셀을 자동 줄 바꿈하고 Excel을 PowerPoint로 변환하는 방법
url: /ko/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 셀을 래핑하고 Excel을 PowerPoint로 변환하는 방법

Excel 시트에서 **셀을 래핑하는 방법**이 필요하고 그 시트를 PowerPoint 프레젠테이션으로 변환하려면, 이 가이드는 완전하고 바로 실행할 수 있는 솔루션을 보여줍니다. 처음 두 문장이 끝날 때쯤이면 어떤 API 호출이 래핑을 수행하고 어떤 메서드가 파일을 PPTX로 저장하는지 정확히 알게 될 것입니다.

우리는 Microsoft Office가 설치되지 않아도 Excel 워크북을 조작할 수 있는 라이브러리인 Aspose.Cells for .NET을 사용할 것입니다. 이 튜토리얼은 **Excel을 PowerPoint로 변환**을 다루고, **WRAPCOLS 사용 방법**을 시연하며, **워크북 워크시트 생성** 모범 사례를 설명합니다. 외부 도구는 필요 없으며 .NET 개발 환경만 있으면 됩니다.

## 전제 조건

- .NET 6.0 또는 그 이후 버전 (코드는 .NET Framework 4.6+에서도 작동합니다)
- Aspose.Cells for .NET NuGet 패키지 (`Install-Package Aspose.Cells`)
- C# 및 워크시트 개념에 대한 기본적인 이해
- Visual Studio 또는 VS Code와 같은 IDE

> **Pro tip:** 실험 중에는 Aspose.Cells의 무료 평가 라이선스를 사용하고, 실제 운영 전에는 정식 라이선스로 교체하세요.

## 단계 1: 워크북 생성 및 워크시트 추가

먼저 **워크북 워크시트 생성**을 위해 `Workbook` 객체를 인스턴스화해야 합니다. 기본적으로 Aspose.Cells는 하나의 워크시트(인덱스 0)를 생성하며, 이를 데모에 사용할 것입니다.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**왜 중요한가:** 워크북을 초기화하면 깨끗한 캔버스를 얻을 수 있습니다. 기본 워크시트는 이미 `Worksheets` 컬렉션에 포함되어 있으므로 추가 시트가 필요하지 않은 한 `Add()`를 호출할 필요가 없습니다.

## 단계 2: 소스 범위 채우기 (A2:A10)

셀을 **래핑하는 방법**을 수행하기 전에 래핑할 데이터가 필요합니다. 이 단계에서는 A2부터 A10까지의 셀에 샘플 텍스트를 채웁니다.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**예외 상황:** 소스 범위가 비어 있으면 `WRAPCOLS`는 `#VALUE!`를 반환합니다. 범위에 최소 하나 이상의 비어 있지 않은 셀이 포함되도록 항상 확인하세요.

## 단계 3: WRAPCOLS 수식 적용

이제 핵심 질문인 **WRAPCOLS 사용 방법**에 답합니다. 이 수식은 세로 범위를 받아 지정된 열 수에 따라 배열합니다. 우리는 수식을 셀 `A1`에 입력하고, 결과 배열이 인접 셀에 자동으로 채워지게 합니다.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**내부 동작:** `WRAPCOLS`는 소스 범위를 평가하고, 항목을 목표 열에 가능한 한 균등하게 나눈 뒤, 값을 직사각형 블록에 기록합니다. 블록 크기는 동적이므로 대상 범위를 미리 정의할 필요가 없습니다.

## 단계 4: 워크북을 편집 가능한 PowerPoint 파일로 저장

마지막으로 **Excel을 PowerPoint로 변환** 및 **Excel을 PowerPoint로 저장**을 다룹니다. Aspose.Cells는 워크시트를 직접 PPTX로 내보낼 수 있으며, 레이아웃을 편집 가능한 도형으로 보존합니다.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**왜 PPTX인가?** 생성된 PowerPoint는 래핑된 셀을 테이블로 표시한 단일 슬라이드를 포함합니다. Microsoft PowerPoint에서 파일을 열어 텍스트를 편집하고, 스타일을 변경하거나, 추가 슬라이드를 삽입할 수 있으며—모든 것이 완전히 편집 가능하게 유지됩니다.

### 예상 출력

- **Excel 측:** 셀 `A1`은 원래 긴 문자열을 3열 배열로 보여주며, 각 열은 대략 동일한 행 수를 포함합니다.
- **PowerPoint 측:** `ChartEditable.pptx`를 열면 래핑된 레이아웃을 반영한 테이블이 있는 슬라이드가 표시됩니다. 테이블은 선택, 크기 조정, 편집이 가능하며 일반 PowerPoint 객체와 동일하게 동작합니다.

## 일반적인 변형 및 주의 사항

| Scenario | Adjustment |
|----------|------------|
| **더 많은 열로 래핑** | 두 번째 인수를 `WRAPCOLS`에 변경합니다. 예: `=WRAPCOLS(A2:A10,5)`. |
| **다른 범위 래핑** | 수식 참조를 업데이트합니다. 예: `=WRAPCOLS(B2:B15,2)`. |
| **시트의 일부만 내보내기** | `Worksheet.ExportDataTable`을 사용해 `DataTable`을 추출한 뒤, `Presentation` API를 이용해 맞춤형 PPTX를 생성합니다. |
| **대형 워크시트 ( > 10 000 행 )** | 성능 병목을 피하기 위해 내보내기를 여러 슬라이드로 분할하는 것을 고려하세요. |

> **Watch out for:** 워크북에 차트가 포함된 경우 기본 PPTX 내보내기는 워크시트를 단일 이미지로 렌더링합니다. `WRAPCOLS`를 사용하면 데이터가 테이블 형태로 유지되어 편집 가능하게 됩니다.

## 빠른 복사‑붙여넣기를 위한 전체 소스 코드

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

`Program.cs` 파일로 저장하고, NuGet 패키지를 복원한 뒤 실행합니다:

```bash
dotnet run
```

콘솔에 내보내기가 완료되었다는 메시지가 표시되고, 지정된 폴더에 PPTX 파일이 생성됩니다.

## 결론

이제 Excel 워크시트에서 **셀을 래핑하는 방법**, **WRAPCOLS 사용 방법**, 그리고 Aspose.Cells를 사용해 **Excel을 PowerPoint로 변환**하고 **Excel을 PowerPoint로 저장**하는 정확한 단계들을 알게 되었습니다. 전체 솔루션은 **워크북 워크시트 생성**을 시연하고, 래핑 수식을 적용하여 프레젠테이션 수정을 바로 할 수 있는 편집 가능한 PPTX 파일을 생성합니다.

### 다음 단계

- 내보내기 전에 다른 Excel 함수(예: `TRANSPOSE`, `FILTER`)를 탐색합니다.
- 루프를 사용해 여러 워크시트를 결합하여 다중 슬라이드 PowerPoint 데크를 만듭니다.
- 내보낸 후 Aspose.Slides를 통합해 맞춤형 슬라이드 제목이나 브랜딩을 추가합니다.

다양한 열 수, 소스 범위 등을 자유롭게 실험하거나 차트와 테이블을 동일 PPTX에 결합해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 단계별 설명과 함께 완전한 동작 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [Aspose.Cells for .NET을 사용하여 Excel을 PowerPoint로 변환하는 방법&#58; 완전 가이드](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET을 사용하여 Excel에서 텍스트 래핑하는 방법 | 포맷팅 튜토리얼](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Aspose.Cells for .NET을 사용하여 Excel 워크북 및 워크시트 속성을 HTML로 내보내기](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}