---
category: general
date: 2026-02-14
description: C#에서 마스터 데이터 객체를 생성하고 상세 시트를 손쉽게 만들 수 있습니다. 실용적인 코드 예제로 전체 SmartMarker
  워크플로우를 배워보세요.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: ko
og_description: C#에서 마스터 데이터 객체를 생성하고 SmartMarker로 상세 시트를 생성하세요. 바로 실행 가능한 솔루션을 위한
  자세한 튜토리얼을 따라보세요.
og_title: 마스터 데이터 객체 만들기 – 완전 가이드
tags:
- C#
- SmartMarker
- Excel Automation
title: 마스터 데이터 객체 생성 – 상세 시트 생성을 위한 단계별 가이드
url: /ko/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 마스터 데이터 객체 만들기 – 전체 튜토리얼

Excel 워크시트용 **create master data object**가 필요했지만 SmartMarker 디테일 시트에 연결하는 방법을 몰라 고민한 적이 있나요? 당신만 그런 것이 아닙니다. 많은 보고 시나리오에서 마스터 객체는 동적 디테일 시트를 구동하며, 연결을 올바르게 설정하는 것은 그림 없이 퍼즐을 맞추는 느낌일 수 있습니다.  

이 가이드에서는 전체 과정을 단계별로 살펴봅니다—마스터 데이터 객체를 구축하고, SmartMarker 옵션을 **generate detail sheet**하도록 구성하며, 마지막으로 프로세서를 실행합니다. 끝까지 진행하면 GrapeCity Documents for Excel (GcExcel) 라이브러리를 사용하는 모든 .NET 프로젝트에 붙여넣을 수 있는 실행 가능한 코드 조각을 얻게 됩니다.

## 필요 사항

- .NET 6+ (또는 .NET Framework 4.7.2)와 `GcExcel.dll`에 대한 참조가 포함된 환경
- 기본 C# 지식 (변수, 익명 타입, 객체 초기화자)
- `{{OrderId}}`와 같은 SmartMarker 태그 및 라인 아이템 테이블이 이미 포함된 Excel 워크북
- Visual Studio, Rider 또는 선호하는 기타 편집기

그게 전부입니다—핵심 GcExcel 배포 외에 추가 NuGet 패키지는 필요하지 않습니다.

## 1단계: 마스터 데이터 객체 만들기

먼저 해야 할 일은 SmartMarker 태그가 기대하는 구조를 반영하는 **create master data object**를 만드는 것입니다. 이를 작은 인‑메모리 보고 모델이라고 생각하면 됩니다.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

여기서 익명 타입을 사용하는 이유는? 전체 클래스를 선언하지 않고도 가벼운 컨테이너를 정의할 수 있어 빠른 데모나 구조가 변하지 않을 경우에 이상적이기 때문입니다. 나중에 재사용 가능한 모델이 필요하면 `var`를 적절한 POCO로 교체하면 됩니다.

> **Pro tip:** 속성 이름(`OrderId`, `Product`, `Quantity`)을 워크시트의 플레이스홀더와 동일하게 유지하세요; SmartMarker는 대소문자를 구분하지 않고 일치시킵니다.

## 2단계: SmartMarker 옵션을 구성하여 디테일 시트 생성

이제 SmartMarker에 라인 아이템 테이블용 별도의 워크시트를 원한다는 것을 알려줍니다. 여기서 **generate detail sheet** 키워드가 사용됩니다.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName` 패턴은 런타임에 교체되는 중괄호 플레이스홀더를 사용합니다. 예시에서는 시트 이름이 `Order_1`이 됩니다. 이후 여러 주문을 반복하면 각 주문마다 별도의 탭이 생성되며, 이는 대부분의 회계 담당자가 기대하는 동작과 정확히 일치합니다.

## 3단계: SmartMarker 프로세서 실행

데이터와 옵션이 준비되었으므로, 마지막 단계는 대상 워크시트에 프로세서를 호출하는 것입니다.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

내부적으로 SmartMarker는 워크시트의 태그를 스캔하고 `orderData` 값을 삽입합니다. `DetailSheet`가 `true`이기 때문에 템플릿을 복제하여 `Order_1`이라는 새 시트를 만들고, 모든 라인 아이템이 디테일 영역에 표시되며 템플릿에서 적용한 모든 서식이 유지됩니다.

### 전체 작업 예제

아래는 템플릿 워크북(`Template.xlsx`)을 열고 세 단계를 실행한 뒤 결과를 `Result.xlsx`로 저장하는 독립 실행형 콘솔 프로그램입니다. 이를 새 콘솔 프로젝트에 복사‑붙여넣기하고 **F5**를 눌러 실행할 수 있습니다.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### 예상 출력

- **Result.xlsx**에 `Order_1`이라는 시트가 포함됩니다.
- `A1` 셀(또는 `{{OrderId}}`를 배치한 위치)에 이제 `1`이 표시됩니다.
- SmartMarker 블록에서 시작하는 테이블에 두 행이 나열됩니다:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

파일을 열면 템플릿에서 적용한 서식—테두리, 글꼴, 조건부 서식—이 모두 그대로 유지된 것을 확인할 수 있습니다.

## 일반적인 질문 및 엣지 케이스

### 여러 주문이 있는 경우는 어떻게 하나요?

마스터 객체를 컬렉션으로 감싸면 SmartMarker가 자동으로 반복 처리합니다:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

각 주문마다 자체 시트(`Order_1`, `Order_2`, …)가 생성됩니다. 프로세서는 외부 배열을 마스터 컬렉션으로 취급합니다.

### 시트 위치를 어떻게 제어하나요?

새 시트를 두 번째 탭 뒤에 배치하려면 `smartMarkerOptions.DetailSheetInsertIndex = 2;`를 설정하고, 이름이 지정된 시트 뒤에 삽입하려면 `DetailSheetInsertAfter = "Summary"`을 사용합니다.

### 특정 실행에서 디테일 시트를 비활성화할 수 있나요?

`DetailSheet = false;`로 간단히 전환하면 됩니다. 그러면 SmartMarker는 라인 아이템을 마스터 태그가 있는 동일한 시트에 기록합니다.

### 대용량 데이터 세트는 어떻게 처리하나요?

SmartMarker는 데이터를 효율적으로 스트리밍하지만, 수십만 행을 초과하면 Excel의 1,048,576 행 제한에 도달할 수 있습니다. 이 경우 데이터를 여러 마스터 레코드로 분할하거나 CSV로 내보내는 것을 고려하세요.

## 시각적 개요

![SmartMarker를 사용하여 마스터 데이터 객체를 만들고 디테일 시트를 생성하는 흐름을 보여주는 다이어그램](/images/smartmarker-flow.png)

*이 일러스트는 C# 마스터 객체 → SmartMarker 옵션 → 워크시트 처리 → 새로운 디테일 시트 흐름을 보여줍니다.*

## 결론

이제 C#에서 **create master data object**를 만드는 방법과 SmartMarker를 **generate detail sheet**하도록 자동으로 구성하는 방법을 알게 되었습니다. 데이터, 옵션, 프로세서의 3단계 패턴은 GcExcel을 활용한 대부분의 Excel 자동화 시나리오를 포괄합니다.  

다음 단계로 다음을 탐색할 수 있습니다:

- 각 디테일 시트에 헤더/푸터 데이터 추가
- 주문 상태에 따라 조건부 서식 적용
- `workbook.SaveAsPdf(...)`를 사용하여 생성된 워크북을 PDF로 내보내기

자유롭게 실험하고, 문제를 일으키고, 다시 합쳐 보세요. 이것이 워크시트 자동화를 마스터하는 가장 빠른 방법입니다. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}