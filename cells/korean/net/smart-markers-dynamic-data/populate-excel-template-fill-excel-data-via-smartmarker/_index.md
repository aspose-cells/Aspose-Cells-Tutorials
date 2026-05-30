---
category: general
date: 2026-05-30
description: Aspose.Cells SmartMarker를 사용하여 Excel 템플릿을 빠르게 채우고 데이터를 입력하는 방법을 배워보세요.
  실행 가능한 코드가 포함된 완전한 C# 가이드.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: ko
og_description: Aspose.Cells SmartMarker를 사용하여 Excel 템플릿을 채우고 데이터를 입력하세요. 즉시 결과를 얻을
  수 있는 단계별 C# 튜토리얼을 따라보세요.
og_title: Excel 템플릿 채우기 – SmartMarker로 Excel 데이터 입력
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Excel 템플릿 채우기 – SmartMarker로 Excel 데이터 입력
url: /ko/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 템플릿 채우기 – SmartMarker를 사용하여 Excel 데이터 채우기

Excel 템플릿을 **채우는** 것이 필요했지만 자동화 방법을 몰랐던 적이 있나요? 이 튜토리얼에서는 Aspose.Cells SmartMarker를 사용하여 **Excel에 데이터를 채우는** 방법을 보여드리겠습니다—정적 워크북을 동적 보고서 생성기로 변환하는 도구입니다.

미리 디자인된 청구서 시트, 판매 대시보드 또는 반복 가능한 양식이 있다고 상상해 보세요. 값을 수동으로 입력하는 대신 C# 객체를 전달하고 SmartMarker가 무거운 작업을 수행하도록 할 수 있습니다. 이 가이드를 마치면 템플릿을 가져와 행, 합계 및 조건부 서식까지 삽입하는 완전 실행 가능한 프로젝트를 갖게 됩니다—UI를 건드릴 필요 없이.

## 배울 내용

- Excel 템플릿의 마커와 일치하는 데이터 소스를 준비하는 방법.  
- **SmartMarkerProcessor**를 인스턴스화하고 범위 지원을 활성화하는 방법.  
- 주문 항목과 같은 중첩 컬렉션을 사용하여 **Excel 템플릿을 채우는** 방법.  
- 빈 컬렉션이나 사용자 정의 숫자 형식과 같은 엣지 케이스를 처리하기 위한 팁.  

외부 서비스도, VBA 매크로도 없습니다—순수 C#와 Aspose.Cells만 사용합니다. 필요한 것은 .NET 6(이상)과 Aspose.Cells NuGet 패키지뿐입니다.

## 사전 요구 사항

- Visual Studio 2022(또는 선호하는 IDE).  
- .NET 6 SDK 설치.  
- Aspose.Cells for .NET(무료 체험판은 Aspose 웹사이트에서 받을 수 있습니다).  
- SmartMarker 태그가 포함된 기본 Excel 템플릿(잠시 후 만들 예정).

이 중 익숙하지 않은 것이 있더라도 걱정하지 마세요; 아래 단계가 각각의 요구 사항을 안내합니다.

## 단계 1: SmartMarker 태그가 포함된 Excel 템플릿 디자인

먼저 새 워크북을 열고 정적 부분—회사 로고, 헤더 등—을 배치합니다. 그런 다음 동적 데이터가 표시될 위치에 SmartMarker 자리표시자를 삽입합니다.

| Cell | Content |
|------|---------|
| A1   | **청구서** |
| A3   | `{{CompanyName}}` |
| A5   | **주문 상세** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**왜 중요한가:** SmartMarker는 중괄호(`{{...}}`)를 읽어 나중에 전달하는 객체의 속성에 매핑합니다. `Orders.Items` 컬렉션은 엔진에게 목록의 각 항목에 대해 행을 반복하도록 지시합니다.

> **Pro tip:** `RangeSmartMarker` 옵션을 사용하세요(나중에 활성화합니다). 엔진이 범위를 자동으로 확장해야 할 때—테이블이 늘어나거나 줄어들 때 완벽합니다.

템플릿 파일을 `InvoiceTemplate.xlsx`라는 이름으로 프로젝트의 `Resources` 폴더에 저장합니다.

## 단계 2: 템플릿 마커와 일치하는 데이터 소스 준비

이제 마커와 정확히 일치하도록 속성 이름이 맞는 C# 익명 객체(또는 강력 타입 클래스)를 생성합니다. 핵심은 계층 구조를 정확히 그대로 복제하는 것입니다.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**왜 중요한가:** `Orders` 배열에는 단일 주문이 들어 있고, 각 주문은 `Items` 배열을 가지고 있습니다. SmartMarker는 `Items`를 순회하면서 각 요소마다 행을 복제합니다. 나중에 여러 주문이 필요하면 `Orders` 배열에 객체를 추가하기만 하면 코드 변경이 필요 없습니다.

## 단계 3: 템플릿 로드 및 SmartMarkerProcessor 인스턴스 생성

데이터가 준비되면 워크북을 로드하고, 프로세서를 생성한 뒤 범위 마커를 인식하도록 지정합니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**왜 중요한가:** `SmartMarkerProcessor`는 마커를 파싱하고, 범위를 확장하며, 값을 기록하는 엔진입니다. 프로세서를 워크북과 분리함으로써 코드를 깔끔하고 재사용 가능하게 유지할 수 있습니다.

## 단계 4: RangeSmartMarker 활성화하여 워크시트 처리

`Process`를 호출할 때 마법이 일어납니다. `RangeSmartMarker = true`로 설정하면 SmartMarker가 전체 행 범위를 반복 가능한 블록으로 간주하여 필요에 따라 행을 자동으로 삽입하거나 삭제합니다.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

이 시점에서 엔진은 다음을 수행했습니다:

1. `{{...}}` 태그를 찾아 워크시트를 스캔했습니다.  
2. 각 태그를 `data`의 속성에 매핑했습니다.  
3. 테이블 범위(A7:D7)를 감지하고 세 번 복제했습니다—항목당 한 번씩.  
4. 총합 열을 위해 `Price * Qty` 식을 계산했습니다.

## 단계 5: 결과 워크북 저장

마지막으로 채워진 워크북을 디스크에 기록하거나 웹 클라이언트에 스트리밍합니다.

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

`InvoicePopulated.xlsx`를 열면 깔끔하게 채워진 테이블을 확인할 수 있습니다:

| 이름   | 수량 | 가격 | 합계 |
|--------|------|------|------|
| Pen       | 2   | 1.5   | 3.00 |
| Notebook  | 1   | 3.75  | 3.75 |
| Stapler   | 1   | 5.00  | 5.00 |

**Excel 템플릿을 채우는** 단계가 이제 완료되었으며, 행 수에 관계없이 **Excel에 데이터를 채우는** 작업을 성공적으로 수행했습니다.

## 일반적인 엣지 케이스 처리

### 빈 컬렉션

`Items`가 비어 있으면 SmartMarker는 테이블 헤더는 유지하지만 행을 삽입하지 않습니다. 빈 공간을 방지하려면 조건 블록을 추가할 수 있습니다:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### 사용자 정의 숫자 형식

통화 기호나 천 단위 구분 기호가 필요할 때가 있습니다. 처리 후에 프로그래밍 방식으로 스타일을 적용할 수 있습니다:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### 대용량 데이터 세트

수천 개의 행을 처리할 경우 `UseFastMode` 옵션을 활성화하여 성능을 향상시킵니다:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## 전체 작업 예제

아래는 콘솔 앱에 복사·붙여넣기 할 수 있는 완전한 자체 포함 프로그램입니다. 모든 using 지시문, 데이터 준비, 처리 및 저장이 포함되어 있습니다.



## 다음에 배울 내용은?

- [Aspose.Cells와 Smart Markers를 사용하여 Excel에 데이터 채우기](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [.NET용 Aspose.Cells로 Excel 셀 채우기: 단계별 가이드](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [.NET용 Aspose.Cells로 Excel 데이터 내보내기 자동화: 단계별 가이드](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}