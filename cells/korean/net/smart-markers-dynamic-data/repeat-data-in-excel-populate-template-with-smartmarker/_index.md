---
category: general
date: 2026-02-21
description: SmartMarker를 사용해 엑셀에서 데이터를 빠르게 반복하세요—엑셀 템플릿을 채우고 행을 손쉽게 반복하는 방법을 배워보세요.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: ko
og_description: SmartMarker를 사용하여 Excel에서 데이터를 반복합니다. Excel 템플릿을 채우고, 행을 반복하며, 스프레드시트를
  자동화하는 방법을 배워보세요.
og_title: Excel에서 데이터 반복 – SmartMarker로 템플릿 채우기
tags:
- excel
- csharp
- smartmarker
- automation
title: Excel에서 데이터 반복 – SmartMarker로 템플릿 채우기
url: /ko/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 데이터 반복 – SmartMarker로 템플릿 채우기

Excel에서 **데이터를 반복**해야 하는데 수작업 복사‑붙여넣기를 피하고 싶었던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 보고서 시나리오에서 항목 목록을 자동으로 행으로 확장해야 하는데, 손으로 일일이 처리하면 오류가 발생하기 쉽습니다.

핵심은 **GemBox.Spreadsheet** 라이브러리의 `SmartMarkerProcessor`를 사용하면 **한 줄의 C# 코드**만으로 Excel 템플릿을 채우고 컬렉션의 각 항목마다 행을 자동으로 반복할 수 있다는 점입니다. 이 가이드에서는 정확한 단계별 절차를 보여주고, 전체 코드를 제공하며, 각 부분이 왜 중요한지 설명합니다. 이를 통해 Excel에서 행을 반복하는 작업을 손쉽게 수행할 수 있습니다.

## 배울 내용

* 반복 작업을 구동하는 데이터 구조 정의 방법  
* 숨겨진 템플릿 시트를 포함한 워크북에 `SmartMarkerProcessor` 연결 방법  
* `${Repeat:Item}` 마커가 어떻게 자동으로 여러 행으로 확장되는지  
* 빈 컬렉션이나 사용자 정의 서식과 같은 엣지 케이스 처리 팁  

이 튜토리얼을 마치면 **데이터로 Excel을 채우는** 방법을 확장 가능하고 유지 보수가 쉬우며 모든 .NET 프로젝트에서 사용할 수 있게 됩니다.

---

## 사전 요구 사항

* .NET 6.0 이상 (코드에 최신 C# 기능 사용)  
* **GemBox.Spreadsheet** NuGet 패키지 (무료 버전은 최대 150행 지원)  
* 숨겨진 시트 `HiddenTemplate`이 포함된 기본 Excel 템플릿 파일 (`Template.xlsx`)  
* C# 객체와 LINQ에 대한 기본 지식이 있으면 도움이 되지만 필수는 아닙니다.

---

## 1단계 – 반복 데이터 구조 정의

먼저 SmartMarker 엔진이 반복할 수 있는 데이터 소스가 필요합니다. 실제 애플리케이션에서는 보통 데이터베이스, API, CSV 파일 등에서 가져오게 됩니다. 여기서는 이해를 돕기 위해 `Item`이라는 단일 속성을 가진 익명 타입을 사용해 문자열 배열을 전달합니다.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **왜 중요한가:** Excel 템플릿 안의 `${Repeat:Item}` 마커는 `Item`이라는 속성을 찾습니다. 속성 이름을 바꾸면 마커도 동일하게 수정해야 합니다. 이 강한 결합 덕분에 템플릿과 코드가 항상 일치해 **Excel 템플릿을 채우는** 작업을 컬럼 이름을 추측하지 않아도 쉽게 할 수 있습니다.

### 흔히 쓰이는 변형

* **복합 객체:** 단순 문자열 배열 대신 객체 리스트(`new[] { new { Name = "A", Qty = 10 } }`)를 제공할 수 있습니다. 마커는 행을 반복하고 시트에서는 `${Item.Name}`·`${Item.Qty}`와 같이 참조합니다.  
* **빈 컬렉션:** `Item`이 비어 있으면 SmartMarker는 반복 블록을 그대로 제거하고 템플릿을 그대로 두어 선택적 섹션에 적합합니다.

---

## 2단계 – 숨겨진 템플릿 시트를 위한 SmartMarkerProcessor 생성

다음으로 워크북을 로드하고 `SmartMarkerProcessor` 인스턴스를 생성합니다. 숨겨진 템플릿 시트가 포함된 워크북을 지정하면 SmartMarker가 해당 시트를 복사해 보이는 시트로 만들고 반복 마커를 확장합니다.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **프로 팁:** 동일 파일에 여러 템플릿이 있는 경우 `processor.Process` 호출 시 소스 시트 이름을 지정하면 됩니다. 이렇게 하면 **Excel에서 행을 반복**해야 하는 보고서의 서로 다른 섹션에 각각 적용할 수 있습니다.

### 엣지 케이스 처리

* **템플릿 시트 누락:** 로드 코드를 try/catch 로 감싸고 명확한 오류를 로그에 남기세요. 파일 경로가 잘못됐을 때 무음 실패를 방지할 수 있습니다.  
* **대용량 데이터:** 수천 행을 처리할 경우 메모리에 모두 보관하기보다 (`processor.Save`) 파일 스트리밍 방식으로 출력하는 것을 고려하세요.

---

## 3단계 – 데이터 적용 및 `${Repeat:Item}` 마커 확장

이제 실제로 행을 반복하는 마법의 한 줄을 실행합니다. 1단계에서 만든 객체를 `processor.Process`에 전달하면 SmartMarker가 모든 `${Repeat:Item}` 마커를 찾아 각 요소마다 행을 복제하고 자리표시자를 실제 값으로 교체합니다.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### 기대 결과

`Result.xlsx`를 열면 숨겨진 템플릿 시트가 새 보이는 시트(기본 이름 `Sheet1`)로 복사됩니다. `${Repeat:Item}`이 있던 행이 세 번 나타나며 셀에는 각각 **A**, **B**, **C**가 표시됩니다.

| Item |
|------|
| A    |
| B    |
| C    |

추가로 `${Item.Price}`와 같은 컬럼을 넣으면 데이터 소스에서 자동으로 채워집니다.

---

## SmartMarker 없이 Excel에서 행을 반복하는 방법 (간단 비교)

| 접근 방식               | 코드 복잡도 | 유지 보수성 | 성능 |
|------------------------|------------|------------|------|
| 수동 복사‑붙여넣기      | 높음       | 낮음       | 낮음 |
| VBA 매크로              | 중간       | 중간       | 좋음 |
| **SmartMarkerProcessor**| 낮음       | 높음       | 매우 좋음 |

보시다시피 SmartMarker를 사용해 **Excel에서 데이터를 반복**하면 템플릿 디자인과 비즈니스 로직을 가장 깔끔하게 분리할 수 있습니다. 또한 언어에 구애받지 않아 Java, Python, JavaScript 라이브러리에서도 유사한 개념을 찾을 수 있습니다.

---

## 고급 팁 및 흔히 발생하는 실수

### 1. 반복 행 서식 지정

SmartMarker는 전체 행을 복사하므로 셀 스타일, 테두리, 조건부 서식까지 그대로 유지됩니다. 첫 번째 혹은 마지막 행에 다른 스타일이 필요하면 `${If:Item.IsFirst}`와 같은 추가 마커를 넣고 Excel 내부에서 조건식으로 처리하세요.

### 2. 대용량 데이터 처리

10 000행 이상을 다룰 때는 처리 전에 Excel 자동 계산을 비활성화합니다.

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

저장 후 다시 활성화하면 성능이 크게 향상됩니다.

### 3. 실제 데이터베이스에서 Excel 채우기

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

그 다음 템플릿에 `${Repeat:Order}`를 사용하면 모든 주문을 나열할 수 있습니다. 이 패턴은 Entity Framework에서 **데이터로 Excel을 채우는** 작업이 얼마나 쉬운지 보여줍니다.

### 4. 여러 반복 블록 사용

같은 시트 혹은 다른 시트에 여러 `${Repeat:...}` 마커를 배치할 수 있습니다. SmartMarker는 순차적으로 처리하므로 하나의 블록이 다른 블록의 출력에 의존하는 경우 순서가 중요합니다.

---

## 완전 실행 예제

아래 코드는 Visual Studio에 붙여넣고 바로 실행할 수 있는 독립형 콘솔 애플리케이션입니다. 세 단계 전체와 파일 저장까지 모두 보여줍니다.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**예상 출력:** `Result.xlsx`에 `${Repeat:Item}` 행이 세 번 나타나고 A, B, C가 표시됩니다. 수동 조정이 전혀 필요 없습니다.

---

## 결론

이제 **SmartMarkerProcessor**를 활용해 **Excel에서 데이터를 효율적으로 반복**하는 방법을 알게 되었습니다. 간단한 데이터 객체를 정의하고, 템플릿 워크북을 로드한 뒤 `Process`를 호출하면 **Excel 템플릿을 채우고**, **Excel에서 행을 반복**하며, 전반적인 작업 흐름을 크게 간소화할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}