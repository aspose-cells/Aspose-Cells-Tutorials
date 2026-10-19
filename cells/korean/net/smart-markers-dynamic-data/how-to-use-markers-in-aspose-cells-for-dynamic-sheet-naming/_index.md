---
category: general
date: 2026-05-23
description: Aspose.Cells와 마커를 사용하여 동적 시트 이름 지정 Excel 자동화를 구현하는 방법. 스마트 마커, JSON 데이터
  바인딩 및 시트 생성을 몇 분 안에 배우세요.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: ko
og_description: Aspose.Cells에서 마커를 사용하여 동적 시트 이름을 가진 Excel 파일을 생성하는 방법. 전체 C# 예제와
  함께하는 단계별 완전 가이드.
og_title: 마커 사용 방법 – Aspose.Cells를 이용한 Excel 동적 시트 이름 지정
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells에서 마커를 사용하여 Excel 시트 이름을 동적으로 지정하는 방법
url: /ko/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells에서 마커를 사용하여 Excel에서 동적 시트 이름 지정하는 방법

정적 Excel 템플릿을 완전한 마스터‑디테일 워크북으로 바꾸기 위해 **마커 사용 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 특히 시트 이름이 JSON이나 데이터베이스에서 오는 데이터 값과 일치해야 할 때 *dynamic sheet naming excel* 기능이 필요해 벽에 부딪히곤 합니다.  

이 튜토리얼에서는 **마커 사용 방법**을 보여주는 완전하고 바로 실행 가능한 C# 예제를 단계별로 살펴보겠습니다. 여기서는 **Aspose.Cells** 스마트 마커와 JSON 데이터를 바인딩하고, 프로세서가 시트 이름을 실시간으로 변경하도록 합니다. 불필요한 내용 없이, Visual Studio에 바로 복사해 넣고 즉시 결과를 확인할 수 있는 정확한 코드를 제공합니다.

## 배울 내용

- **smart markers**의 개념과 마스터‑디테일 시나리오에 왜 완벽한지  
- 실제 시트 이름으로 나중에 교체될 워크북에 마커 태그를 삽입하는 방법  
- `DetailSheetNewName` 옵션을 사용하여 **dynamic sheet naming excel** 설정하기  
- JSON 데이터에 대해 `SmartMarkerProcessor`를 실행하여 여러 시트를 자동으로 생성하기  
- 출력을 검증하고 일반적인 함정을 피하기 위한 몇 가지 유용한 팁  

> **Prerequisites** – 최신 .NET 런타임(≥ .NET 6이면 충분), Aspose.Cells for .NET 라이브러리(무료 체험판을 Aspose에서 받을 수 있음), 그리고 C#에 대한 기본적인 이해가 필요합니다.  

---

![Aspose.Cells에서 마커 사용 예시](example.png "Aspose.Cells에서 마커 사용 예시")

## 마커를 사용하여 동적 시트 이름 만들기 (Step 1)

먼저 필요한 것은 템플릿 역할을 할 빈 워크북입니다. 실제 프로젝트에서는 이미 레이아웃, 서식 및 자리표시자 셀을 포함한 기존 `.xlsx` 파일에서 시작할 가능성이 높습니다. 명확성을 위해 모든 것을 프로그래밍 방식으로 생성하겠습니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*왜 중요한가*: `Worksheet` 객체는 **smart marker** 태그를 삽입할 위치입니다. 이 태그들을 JSON에서 가져온 실제 값으로 나중에 프로세서가 교체할 작은 자리표시자라고 생각하면 됩니다.

## 스마트 마커 태그 삽입 (Step 2)

이제 마커 태그를 셀에 직접 삽입합니다. `${...}` 구문은 Aspose.Cells에 “이것은 마커입니다”라고 알려줍니다. 예제에서는 마스터 시트 이름용 마커 하나와 디테일 시트 이름용 마커 하나, 총 두 개가 필요합니다.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – 마커 이름은 짧고 의미 있게 유지하세요; 이는 JSON 페이로드에서 사용할 키가 됩니다.

## JSON 데이터 준비 (Step 3)

프로세서는 JSON, `DataSet` 또는 일반 객체와 같이 표현 가능한 모든 데이터 소스와 함께 작동합니다. 여기에는 마스터‑디테일 컬렉션을 포함하는 최소 JSON 문자열이 있습니다. 각 주문이 `MasterSheetName`과 `DetailSheetName`을 모두 포함하고 있음을 확인하세요.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*왜 JSON인가?* 가볍고 사람이 읽기 쉬우며 웹 API와 잘 작동합니다. 이 데이터를 SQL 쿼리에서 가져와 `Newtonsoft.Json`으로 직렬화해도 무방합니다.

## SmartMarkerProcessor 초기화 (Step 4)

`SmartMarkerProcessor`는 워크북을 스캔하고 마커를 찾아 데이터 바인딩을 수행하는 엔진입니다. 인스턴스를 생성하는 코드는 한 줄입니다.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## 동적 시트 이름 정의 (Step 5)

여기서 **dynamic sheet naming excel**이 진정으로 빛을 발합니다. `DetailSheetNewName`을 설정하면 프로세서가 각 주문마다 새로운 디테일 시트를 만들고 `OrderId`를 기반으로 이름을 지정하도록 지시합니다. `${OrderId}` 자리표시자는 처리 중 현재 레코드에서 해결됩니다.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Watch out** – `${}` 구문을 빼먹으면 시트 이름이 실제로 “Detail_${OrderId}”가 되며, “Detail_1”, “Detail_2” 등으로 바뀌지 않습니다.

## JSON 적용 및 시트 생성 (Step 6)

이제 프로세서가 무거운 작업을 수행하도록 합니다. JSON을 읽고 마커를 교체하며 필요에 따라 새로운 워크시트를 생성합니다.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### 내부 동작 과정?

1. 프로세서는 `Orders` 배열을 읽습니다.  
2. 각 주문마다 **master sheet**를 (`${Orders.MasterSheetName}` 사용) 그리고 **detail sheet**를 (`DetailSheetNewName` 패턴 사용) 생성합니다.  
3. 셀 값은 해당 JSON 필드로 교체되어, 마스터 시트의 첫 번째 셀에 “Master_1”, “Master_2” 등이 들어갑니다.  

## 결과 저장 및 검증 (선택 사항)

마지막으로 워크북을 디스크에 저장합니다. Excel에서 파일을 열면 두 개의 마스터 시트(`Master_1`, `Master_2`)와 두 개의 동적으로 이름이 지정된 디테일 시트(`Detail_1`, `Detail_2`)를 확인할 수 있습니다.  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Expected output** – `output.xlsx`를 연 후 다음과 같이 보입니다:

- 시트 **Master_1**의 셀 A1 = “Master_1”.  
- 시트 **Detail_1**의 셀 A1 = “Detail_1”.  
- 시트 **Master_2**의 셀 A1 = “Master_2”.  
- 시트 **Detail_2**의 셀 A1 = “Detail_2”.  

이것이 **마커 사용 방법**을 통해 **Aspose.Cells 스마트 마커**와 **dynamic sheet naming excel**을 구현하는 전체 흐름입니다.

---

## 일반 질문 및 엣지 케이스

### 계층이 두 단계 이상 필요하면 어떻게 하나요?

새로 만든 디테일 시트 안에 마커를 중첩할 수 있습니다. 처리 전에 템플릿 시트에 추가 `${...}` 태그를 배치하면 됩니다. 프로세서는 각 레벨을 자동으로 연쇄 처리합니다.

### JSON 대신 DataTable을 사용할 수 있나요?

물론 가능합니다. `SmartMarkerProcessor`는 `DataSet`, `DataTable`, 그리고 사용자 정의 객체에 대한 오버로드를 제공합니다. 유일한 차이점은 `ApplyJson` 호출을 `ApplyDataSet(myDataSet)`으로 바꾸는 것입니다.

### 시트 생성 순서를 어떻게 제어하나요?

순서는 소스 컬렉션의 순서를 따릅니다. 사용자 정의 정렬이 필요하면, 프로세서에 전달하기 전에 JSON 배열(또는 DataTable)을 정렬하면 됩니다.

### 처리 후 템플릿 시트를 숨길 방법이 있나요?

예. `ApplyJson`을 호출하기 전에 `sm.Options.RemoveTemplateSheets = true;` 로 설정하면 됩니다. 원본 시트(인덱스 0)는 최종 워크북에서 제거됩니다.

---

## 전체 작업 예제 (모든 단계 결합)

아래는 새 C# 콘솔 프로젝트에 복사‑붙여넣기 할 수 있는 전체 프로그램입니다. `Aspose.Cells` NuGet 패키지를 참조했는지 확인하세요.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

프로그램을 실행하고 `output.xlsx`를 열면 앞서 설명한 대로 동적 시트가 표시됩니다.

---

## 마무리

우리는 방금 Aspose.Cells에서 **마커 사용 방법**을 다루어 일반 워크북을 **dynamic sheet naming excel**이 적용된 마스터‑디테일 솔루션으로 변환했습니다. 주요 요점은 다음과 같습니다:

1. 데이터가 표시될 위치에 `${...}` 스마트 마커를 배치합니다.  
2. JSON(또는 지원되는 다른 데이터 소스)를 `SmartMarkerProcessor`에 전달합니다.  
3. `DetailSheetNewName`을 사용하여 프로세서가 새 시트 이름을 실시간으로 지정하도록 합니다.  

여기서부터는 테이블 추가, 셀 스타일링, 차트 삽입 등 더 고급 시나리오를 탐색할 수 있습니다—모두 데이터에 의해 구동됩니다.

## 관련 튜토리얼

- [동적 Excel 보고서를 위한 Aspose.Cells 스마트 마커 C# 구현 방법](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Aspose.Cells .NET 스마트 마커를 사용한 동적 Excel 보고서 생성](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose.Cells .NET 마스터하기: 동적 Excel 보고서를 위한 스마트 마커 및 커스텀 레이블 구현](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}