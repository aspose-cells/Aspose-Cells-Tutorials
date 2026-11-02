---
category: general
date: 2026-09-15
description: C#에서 Excel 워크북을 만들고, EXPAND 함수를 사용하여 동적 배열을 스필링하면서 워크북을 PDF로 저장하는 방법을
  배우세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: ko
lastmod: 2026-09-15
og_description: C#에서 Excel 워크북을 만들고, EXPAND 함수를 사용하여 동적 배열을 스필하면서 워크북을 빠르게 PDF로 저장합니다.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: 동적 배열을 사용하여 Excel 워크북을 만들고 PDF로 저장하기
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: 동적 배열을 사용하여 Excel 워크북을 만들고 PDF로 저장
url: /ko/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 동적 배열을 사용하여 Excel 워크북을 만들고 PDF로 저장하기

프로그래밍 방식으로 **Excel 워크북을 생성**하고 **워크북을 PDF로 저장**해야 하는 경우, 이 가이드는 C#에서 완전한 엔드‑투‑엔드 솔루션을 보여줍니다. 또한 VBA 없이 배열을 생성하는 최신 방법인 **EXPAND 함수**를 사용하여 **동적 배열 결과를 스필**하는 방법도 확인할 수 있습니다.  

보고서 서비스, ERP 시스템의 내보내기 기능, 혹은 데이터 기반 대시보드를 구축하든, 아래 단계들을 통해 워크북을 생성하고 스마트‑마커 데이터를 채운 뒤 고급 글꼴 기능을 보존한 PDF를 만들 수 있습니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있어야 합니다:

* .NET 6.0 이상 (.NET Framework 4.8에서도 동작)
* 최신 버전의 **Aspose.Cells for .NET** (v25.8 이상) – `Workbook`, `PdfSaveOptions`, `SmartMarkerProcessor` 제공
* Visual Studio 2022 같은 IDE (C#을 컴파일할 수 있는 편집기면 모두 가능)

프로젝트에 NuGet 패키지를 추가합니다:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Step 1: Create Excel workbook and set up the first worksheet

첫 번째 작업은 **Excel 워크북을 생성**하고 기본 워크시트에 대한 참조를 얻는 것입니다. 이 워크시트가 동적 배열과 스마트 마커 템플릿을 호스팅합니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*왜 중요한가*: `Workbook`을 인스턴스화하면 내부 워크북 구조가 할당되고, `Worksheets[0]`에 접근하면 수동으로 시트를 추가하지 않아도 바로 사용할 수 있는 시트를 얻을 수 있습니다.

## Step 2: Spill dynamic array using the EXPAND function

Excel의 **EXPAND 함수**는 정적 배열 리터럴을 원하는 크기의 스필 범위로 변환할 수 있습니다. 여기서는 `{1,2,3}`을 `A1`부터 시작하는 5행 × 1열 범위로 확장하도록 요청합니다.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*왜 중요한가*: `EXPAND`를 사용하면 C#에서 수동 루프를 작성할 필요가 없습니다. 엔진이 스필 범위를 계산하고 값을 워크시트에 직접 저장하므로 이후 PDF에 그대로 반영됩니다.

## Step 3: Save workbook as PDF while preserving font variation selectors

**워크북을 PDF로 저장**할 때 Aspose.Cells v25.8부터 지원되는 글꼴 변형 선택자와 같은 고급 타이포그래피 기능을 활성화할 수 있습니다. 이를 통해 복잡한 스크립트가 올바르게 렌더링됩니다.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*왜 중요한가*: `FontVariationSelectors`를 `true`로 설정하면 글리프 변형이 필요한 언어(예: 중국어, 일본어, 이모지)에서 정확한 표시가 보장됩니다. 생성된 PDF는 화면상의 Excel 뷰와 동일하게 보입니다.

## Step 4: Insert a Smart Marker template that references a nested data source

스마트 마커를 사용하면 워크시트에 바로 플레이스홀더를 삽입할 수 있습니다. 아래 템플릿은 주문 목록과 해당 항목들을 생성합니다.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*왜 중요한가*: 템플릿을 `A1`에 배치하면 Aspose.Cells가 데이터를 어디서부터 확장할지 알게 됩니다. `:` 구문(`Items:ItemName`)은 중첩 컬렉션을 반복하도록 프로세서에 지시합니다.

## Step 5: Define the nested data source (orders containing items)

각 주문이 자체 아이템 컬렉션을 포함하는 익명 배열을 생성합니다. 이는 일반적인 마스터‑디테일 시나리오를 반영합니다.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*왜 중요한가*: 중첩 구조는 VBA나 수동 셀 루프 없이 스마트 마커를 통해 **Excel에서 동적 배열을 만드는 방법**을 보여줍니다.

## Step 6: Process the Smart Markers and save the final Excel file

이제 워크북과 데이터 소스를 `SmartMarkerProcessor`에 전달합니다. 처리 후 플레이스홀더가 실제 행으로 교체되고 결과를 일반 `.xlsx` 파일로 저장합니다.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*왜 중요한가*: `SmartMarkerProcessor`는 템플릿을 자동으로 확장하고 필요한 행을 생성한 뒤 데이터를 채워 넣습니다. 최종 워크북을 Excel에서 열어 각 주문과 항목이 올바르게 표시되는지 확인할 수 있습니다.

## Expected output

* **VarSelector.pdf** – 1‑3 숫자가 5행으로 스필되는 모습을 보여주며, 활성화한 OpenType 글꼴 변형이 적용된 PDF 파일
* **NestedSmartMarker.xlsx** – `A1`부터 시작하는 다음 행들을 포함하는 Excel 파일:

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF 버전은 워크시트 상태가 스마트 마커 처리 전에 저장되었기 때문에 동일한 숫자 스필을 유지합니다. 필요에 따라 처리 후에도 PDF 저장을 반복하면 최종 데이터를 PDF로 얻을 수 있습니다.

## Pro tips and common pitfalls

| Tip | Explanation |
|-----|-------------|
| **Reuse the same `PdfSaveOptions`** | 옵션 객체를 한 번만 생성하고 재사용하면 렌더링 차이(예: 변형 선택자 누락)와 같은 미묘한 차이를 방지할 수 있습니다. |
| **Call `ws.Calculate()` after setting formulas** | 명시적인 계산을 수행하지 않으면 스필 범위가 비어 있어 프로그램matically 워크북을 검사할 때 값이 보이지 않을 수 있습니다. |
| **Place Smart Marker templates on a clean sheet** | 기존 데이터와 템플릿을 혼합하면 예상치 못한 행 삽입이 발생할 수 있습니다. 가능하면 전용 시트를 사용하세요. |
| **Mind the file paths** | `Path.Combine(Environment.CurrentDirectory, "output.pdf")`와 같이 경로를 결합하면 머신마다 하드코딩된 디렉터리를 피할 수 있습니다. |
| **Version check** | `FontVariationSelectors`는 버전 25.8부터 제공됩니다; 이전 버전에서는 속성이 무시되고 예외가 발생하지 않습니다. |

## Next steps

이제 **Excel 워크북을 생성**, **동적 배열을 스필**, **워크북을 PDF로 저장**하는 방법을 알았으니 다음을 탐색해 보세요:

* PDF 변환 전에 차트나 이미지를 추가하기
* `Save` 오버로드를 사용해 동일 워크북을 HTML, CSV 등 다른 형식으로 내보내기
* **스마트 마커 식**(`${Orders.Total:SUM(Items.Price)}`)을 활용해 실시간 집계 계산하기
* 이 코드를 ASP.NET Core API에 통합해 사용자가 웹 엔드포인트에서 바로 생성된 PDF를 다운로드하도록 만들기

---

**Summary** – 이 튜토리얼에서는 **Excel 워크북을 생성**, **EXPAND 함수를 사용해 동적 배열을 스필**, **중첩 데이터 소스를 활용하는 스마트 마커**를 삽입하고, 마지막으로 **고급 글꼴 기능을 보존하면서 워크북을 PDF로 저장**하는 전체 과정을 보여주었습니다. 완전한 실행 가능한 예제는 어떤 C# 프로젝트에도 복사해 넣어 사용할 수 있으며, 필요에 따라 자체 데이터 구조에 맞게 조정하면 됩니다. 즐거운 코딩 되세요!


## What Should You Learn Next?


다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하여 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}