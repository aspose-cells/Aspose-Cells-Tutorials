---
category: general
date: 2026-09-18
description: EXPAND 함수를 사용하여 Excel에서 배열을 확장하는 방법, Excel 템플릿을 채우는 방법, 그리고 C#으로 동적 범위
  Excel 워크시트를 만드는 방법을 배우세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: ko
lastmod: 2026-09-18
og_description: EXPAND 함수를 사용하여 Excel에서 배열을 확장하고, Excel 템플릿을 채우며, C# 코드를 활용해 동적 범위
  Excel 솔루션을 구축하는 방법.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Excel에서 배열을 확장하고 템플릿에 채우는 방법
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Excel에서 배열을 확장하고 템플릿에 채우는 방법
url: /ko/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 배열을 확장하고 템플릿을 채우는 방법

Excel에서 사전 설계된 템플릿을 채우면서 **배열을 확장하는 방법**이 필요하다면, 이 가이드는 완전한 엔드‑투‑엔드 솔루션을 보여줍니다. `EXPAND` 함수와 Aspose.Cells의 Smart Markers를 함께 사용하면 단일 셀 참조를 5 × 5 범위로 전환하고 `{IsActive}`와 같은 마커를 실시간 데이터로 자동 교체할 수 있습니다.

이 튜토리얼에서는 **excel 템플릿을 채우는 방법**, **동적 범위 excel**을 생성하는 방법, 그리고 C# 프로젝트에서 **expand 함수를 올바르게 사용하는 방법**을 확인할 수 있습니다. 튜토리얼이 끝날 때쯤에는 `.xlsx` 파일을 로드하고, 배열 수식을 확장하며, Smart Markers를 적용하고, 결과를 저장하는 실행 가능한 프로그램을 얻게 됩니다.

## 전제 조건

* .NET 6.0 이상 (코드는 .NET Core 3.1+에서도 작동합니다)
* Aspose.Cells for .NET (NuGet 패키지 `Aspose.Cells`)
* 플레이스홀더 수식 셀(예: `B2`)과 `{IsActive}`와 같은 Smart Marker가 포함된 Excel 워크북
* C# 및 Excel 수식에 대한 기본적인 이해

> **Pro tip:** `EXPAND` 함수는 Microsoft 365용 Excel 및 Excel 2021+에서만 사용할 수 있습니다. 이전 버전에서는 `#NAME?` 오류가 반환됩니다.

## 단계 1: EXPAND 함수를 사용하여 배열을 확장하는 방법

첫 번째 단계는 워크북을 로드하고 단일 소스 셀을 더 큰 행렬로 변환하는 `EXPAND` 수식을 작성하는 것입니다.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

이것이 중요한 이유: `EXPAND`는 행과 열에 수식을 수동으로 복사할 필요를 없애줍니다. 소스 셀(`A2`)이 변경되면 전체 5 × 5 블록이 자동으로 업데이트되어 데이터 변경에 반응하는 **dynamic range excel**을 제공합니다.

## 단계 2: Smart Markers를 사용하여 Excel 템플릿 채우기

Smart Markers를 사용하면 템플릿 내부에 플레이스홀더를 삽입하고, 이를 C# 객체의 값으로 교체할 수 있습니다. 이는 셀별 코드를 작성하지 않고 **excel 템플릿을 채우는** 가장 편리한 방법입니다.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

`SmartMarkersProcessor().Apply` 호출은 전체 시트를 스캔하여 `{IsActive}`를 찾고, 불리언 값을 삽입합니다. 그런 다음 수식은 자동으로 `"Active"` 또는 `"Inactive"`로 평가됩니다.

## 단계 3: 확장된 범위와 채워진 결과 확인

`EXPAND` 수식과 Smart Markers를 모두 적용한 후, 몇 개의 셀을 프로그래밍 방식으로 읽어 모든 것이 예상대로 작동했는지 확인할 수 있습니다.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

프로그램을 실행하면 `A2`의 원래 값(또는 배열 결과)과 `IsActive` 플래그에 따라 **Active** 또는 **Inactive**가 출력됩니다.

## 단계 4: 워크북 저장 – 최종 출력

마지막으로 수정된 워크북을 디스크에 저장합니다. 이 단계는 로드, 확장, 채우기, 파일 저장까지의 전체 흐름을 보여줍니다.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

저장된 `output.xlsx`에는 `EXPAND` 수식으로 생성된 5 × 5 매트릭스와 `{IsActive}` 값이 반영된 셀이 포함됩니다. Excel에서 파일을 열어 동적 범위가 작동하는 모습을 확인하세요.

## 엣지 케이스 및 모범 사례

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Excel version does not support `EXPAND`| 클래식 `=OFFSET` 또는 `=INDEX` 수식으로 대체하거나 Office 365로 업그레이드합니다. |
| Need to expand to a variable size      | `EXPAND` 내부에 `ROWS(source)` 및 `COLUMNS(source)`를 사용하여 진정한 동적성을 확보합니다.   |
| Multiple Smart Markers in the same sheet| 복합 데이터 객체와 함께 `SmartMarkersProcessor().Apply`를 한 번 호출합니다.      |
| Large workbooks ( > 10 000 rows)       | 수식을 작성하는 동안 계산을 비활성화합니다 (`workbook.Settings.CheckFormula = false`). |

## 전체 작동 예제

아래는 새 콘솔 프로젝트에 복사‑붙여넣기 할 수 있는 완전하고 독립적인 프로그램입니다.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**프로그램을 실행했을 때 예상 출력** (`A2`에 숫자 `42`가 들어 있다고 가정).

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

`output.xlsx`를 열면 `A2`에서 파생된 값으로 채워진 5 × 5 블록과 **Active**라는 텍스트가 표시된 셀을 확인할 수 있습니다.

## 결론

이제 `EXPAND` 함수를 사용하여 Excel에서 **배열을 확장하는 방법**, Smart Markers로 **excel 템플릿을 채우는 방법**, 그리고 소스 데이터에 자동으로 적응하는 **dynamic range excel**을 구축하는 방법을 알게 되었습니다. 이 예제는 실제 C# 자동화 시나리오에서 **expand 함수를 사용하는 올바른 방법**과 **expand 배열 수식**을 보여줍니다.

다음과 같이 솔루션을 확장해 보세요:

* 고정된 `5,5` 차원을 `ROWS(A2:A10), COLUMNS(A2:E2)`로 교체하여 진정한 가변 범위를 만들기.
* 여러 Smart Markers를 결합하여 전체 보고서(예: 직원 목록, 판매 표)를 생성하기.
* Aspose.Cells의 스타일링 API를 탐색하여 확장된 블록을 자동으로 서식 지정하기.

다양한 소스 배열, 마커 이름 및 워크북 레이아웃을 자유롭게 실험해 보세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접하게 관련된 주제를 다룹니다. 각 리소스에는 단계별 설명과 함께 완전한 코드 예제가 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [C#에서 배열을 사용해 템플릿 채우기: Excel로 데이터 내보내기](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [C#로 Excel에서 배열 만들기 – 단계별 가이드](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Excel에서 배열 함수를 사용한 데이터 처리](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}