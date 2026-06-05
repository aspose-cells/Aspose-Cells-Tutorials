---
category: general
date: 2026-06-05
description: Aspose.Cells SmartMarkerProcessor에서 중첩 범위 옵션을 활성화하여 계층형 Excel 데이터를 손쉽게
  처리하십시오. 스마트 마커, 중첩 범위 및 모범 사례를 배우세요.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: ko
og_description: Aspose.Cells SmartMarkerProcessor에서 중첩 범위 옵션을 활성화하여 계층형 데이터와 함께 작업합니다.
  코드, 팁 및 함정이 포함된 완전한 가이드.
og_title: Aspose.Cells SmartMarker에서 중첩 범위 옵션 활성화
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Aspose.Cells SmartMarker에서 중첩 범위 옵션 활성화
url: /ko/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells SmartMarker에서 중첩 범위 옵션 활성화

Aspose.Cells SmartMarkerProcessor에서 **중첩 범위 옵션을 활성화**하는 방법이 궁금하셨나요? 이 기능을 활성화하면 주문 및 라인 항목과 같은 계층형 데이터를 문제 없이 처리할 수 있습니다.  

이 튜토리얼에서는 실제 시나리오를 통해 스마트 마커를 사용해 중첩 항목이 포함된 주문 목록을 Excel 템플릿에 채워 넣는 과정을 살펴봅니다. 튜토리얼을 마치면 완전한 워크북을 얻고, **SmartMarkerProcessor**에 대해 이해하게 되며, **중첩 범위 처리** 플래그가 왜 중요한지도 알게 됩니다.

다룰 내용:

* 마스터‑디테일 데이터를 흉내 내는 C# 익명 객체 준비  
* 프로세서에서 **중첩 범위** 플래그 켜기  
* 워크북에 프로세서를 실행하고 결과 확인  

특별한 프레임워크는 필요 없습니다—.NET 6+와 Aspose.Cells for .NET 라이브러리만 있으면 됩니다. 반복 행 안에 또 다른 반복 행을 처리하는 데 어려움을 겪어본 적이 있다면 이 가이드를 참고하세요.

---

## Excel 스마트 마커용 계층형 데이터 준비

먼저 부모‑자식 관계를 반영하는 데이터 소스가 필요합니다. 아래 예시는 두 개의 항목을 포함하는 하나의 주문을 나타내는 익명 객체를 생성합니다.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**왜 이런 형태인가?**  
스마트 마커는 속성 이름(`Orders`, `Items`)을 읽고 프로세서가 올바르게 구성되면 자동으로 중첩 범위를 생성합니다. 이를 Excel 템플릿이 반복할 작은 데이터베이스라고 생각하면 됩니다.

> **Pro tip:** 템플릿에 배치한 마커와 일치하는 의미 있는 속성 이름을 사용하세요(예: `&=Orders.Id&`, `&=Items.Name&`). 이름이 맞지 않으면 “데이터 없음” 오류가 흔히 발생합니다.

---

## SmartMarkerProcessor 구성 및 중첩 범위 활성화

이제 프로세서를 만들고 **NestedRange** 스위치를 켭니다. 이 한 줄은 Aspose.Cells에게 자식 컬렉션을 내부 테이블로 처리하도록 지시합니다.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**`NestedRange = true`가 실제로 하는 일은?**  
설정하면 프로세서는 각 자식 컬렉션마다 별도의 범위를 만들고 이를 부모 범위 안에 중첩합니다. 이 옵션이 없으면 최상위 컬렉션(`Orders`)만 렌더링되고 내부 `Items` 행은 무시됩니다.

> **Watch out:** 중첩 범위를 활성화했지만 템플릿에서 자식 범위를 표시하지 않으면(예: `&=Items.Start&` / `&=Items.End&` 사용) 프로세서가 `SmartMarkerException`을 발생시킵니다. 마커 구문을 항상 다시 확인하세요.

---

## 워크북 템플릿 로드 또는 생성

데모에서는 간단한 워크북을 즉석에서 생성하지만 실제 환경에서는 이미 스마트 마커가 포함된 기존 `.xlsx` 파일을 시작점으로 사용합니다.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

`&=Orders.Start&` / `&=Orders.End&` 마커에 주목하세요—이 마커들은 각 주문 블록의 시작과 끝을 프로세서에 알려 줍니다. 자식 `Items` 범위에도 동일한 패턴이 적용됩니다.

---

## 스마트 마커로 워크북 처리

데이터와 프로세서가 준비되었으니, 모든 것을 병합하는 한 줄 코드를 실행합니다.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

이 호출 이후 워크북은 다음과 같은 내용을 포함하게 됩니다:

| 주문 ID | 항목 이름 |
|----------|-----------|
| 1        | A         |
| 1        | B         |

결과를 디스크에 저장하거나 클라이언트로 스트리밍할 수 있습니다:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## 출력 확인 및 일반적인 함정 처리

### 예상 결과

`NestedRangeResult.xlsx` 파일을 열면 단일 주문 헤더 아래에 두 개의 행이 표시되고, 각 행에 항목 이름(`A`와 `B`)이 나타납니다. 주문 ID는 각 자식 행마다 반복됩니다—중첩 범위가 설계된 바로 그 동작입니다.

### 일반적인 문제

| 증상 | 가능한 원인 | 해결 방법 |
|---------|--------------|-----|
| 자식 행이 나타나지 않음 | `NestedRange`가 `false`로 남아 있음 | `processor.Options.NestedRange = true` 로 설정하십시오. |
| 마커가 일반 텍스트로 표시됨 | 마커 구문 오타 (`&=Orders.Start&` vs `&=Orders.Start`) | `&=`와 마지막 `&`가 모두 존재하는지 확인하십시오. |
| 각 주문마다 중복 행이 생성됨 | `&=Orders.End&` 마커가 누락됨 | 부모 범위를 제한하는 종료 마커를 추가하십시오. |

---

## 전체 작업 예제 (복사‑붙여넣기 가능)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

프로그램을 실행하고 생성된 파일을 열면 위 표와 동일하게 중첩 행이 정확히 채워진 것을 확인할 수 있습니다.

---

## 결론

여러분은 이제 Aspose.Cells SmartMarkerProcessor에서 **중첩 범위 옵션을 활성화**하는 방법을 배웠으며, 평면 Excel 템플릿을 강력한 마스터‑디테일 보고서 생성기로 변환할 수 있게 되었습니다. `processor.Options.NestedRange = true` 를 토글하면 라이브러리가 자동으로 자식 컬렉션에 대한 내부 테이블을 생성해 주어 수동 행 삽입 루프를 피할 수 있습니다.

다음 단계는? 두 번째 수준의 중첩(예: 주문 → 항목 → 부품)을 추가해 보거나, 생성된 행의 스타일을 실험하거나, 차트와 수식이 포함된 사전 디자인 템플릿으로 전환해 보세요. **Excel 스마트 마커**와 **중첩 범위 처리** 조합은 모든 자동화 보고 솔루션을 위한 견고한 기반이 됩니다.

질문이나 어려운 상황이 있나요? 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 작동 코드 예제와 단계별 설명을 포함하고 있어 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 탐색하는 데 도움이 됩니다.

- [Smart Markers를 사용한 중첩 객체 처리 Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Aspose.Cells for Java를 사용하여 중첩 데이터로 Excel 채우기: 종합 가이드](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Excel 중첩 데이터 채우기 Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}