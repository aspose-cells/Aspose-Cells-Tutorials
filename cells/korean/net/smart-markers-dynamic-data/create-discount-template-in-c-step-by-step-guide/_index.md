---
category: general
date: 2026-02-14
description: 할인 템플릿을 빠르게 만들고, 스프레드시트에서 할인을 적용하는 방법, 템플릿에 데이터를 삽입하는 방법, 그리고 스마트 마커용
  변수 접두사를 정의하는 방법을 배우세요.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: ko
og_description: C#로 할인 템플릿 만들기. 스프레드시트에서 할인을 적용하고, 템플릿에 데이터를 주입하며, 스마트 마커용 변수 접두사를
  정의하는 방법을 배웁니다.
og_title: 할인 템플릿 만들기 – 전체 C# 워크스루
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: C#에서 할인 템플릿 만들기 – 단계별 가이드
url: /ko/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 할인 템플릿 만들기 – 전체 C# 워크스루

판매 보고서를 위해 **create discount template**이 필요했지만 숫자를 자동으로 스프레드시트에 넣는 방법을 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다. 이 튜토리얼에서는 **create discount template**을 정확히 만드는 방법, **apply discount in spreadsheet** 셀에 적용하는 방법, **inject data into template** 하는 방법, 그리고 스마트 마커를 위한 **define variable prefix**까지—모두 깔끔한 C# 코드로 보여드립니다.

문제를 먼저 정리한 뒤 바로 복사‑붙여넣기 할 수 있는 실용적인 솔루션으로 넘어갑니다. 끝까지 진행하면 인보이스, 가격표, 혹은 동적 할인이 필요한 모든 스프레드시트에 재사용 가능한 패턴을 갖게 됩니다.

---

## 배우게 될 내용

- 할인 인식을 하는 스프레드시트 템플릿을 설계하는 방법.
- 마커를 쉽게 찾을 수 있도록 사용자 정의 `VariablePrefix` / `VariableSuffix`를 구성하는 방법.
- 익명 객체(`discountData`)를 `SmartMarkerProcessor`에 전달하는 방법.
- 결과 수식(`=IF(#Discount#>0, A1*(1-#Discount#), A1)`)이 최종 가격을 자동으로 계산하는 방식.
- 0% 할인 행이나 다중 할인 단계와 같은 엣지 케이스를 처리하는 팁.

**Prerequisites** – 최신 .NET 런타임(≥ .NET 6), `SmartMarkerProcessor`를 제공하는 `Aspose.Cells`(또는 유사) 라이브러리에 대한 참조, 그리고 C# 구문에 대한 기본 이해. 별다른 전제조건은 없습니다.

---

## 1단계: 스프레드시트에서 할인 템플릿 만들기

먼저 새 워크북을 열거나 기존 워크북을 사용하고, 할인이 적용될 위치에 자리표시자를 배치합니다. 템플릿은 프로세서가 교체할 “스마트 마커”가 포함된 일반 Excel 파일이라고 생각하면 됩니다.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** 수식 안에 `#Discount#`를 삽입함으로써 프로세서에게 할인 값이 들어갈 정확한 위치를 알려줍니다. `SmartMarkerProcessor`는 나중에 제공하는 숫자로 `#Discount#`를 교체하고, 수식의 나머지 부분은 그대로 유지합니다.

---

## 2단계: 스마트 마커용 변수 접두사 정의

기본적으로 많은 라이브러리는 `${Variable}`이나 `{{Variable}}` 형태를 찾습니다. 여기서는 깔끔하고 사람이 읽기 쉬운 마커를 원하므로 **define variable prefix**와 suffix를 명시적으로 지정합니다.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** `#`를 사용하면 마커가 짧고 Excel 수식 입력줄에서 쉽게 눈에 띕니다. 기존 Excel 함수와 충돌을 피해야 할 경우 다른 쌍(예: `[[`와 `]]`)을 선택하면 됩니다.

---

## 3단계: SmartMarkerProcessor를 사용해 템플릿에 데이터 주입

이제 실제 할인 값을 전달합니다. 프로세서는 워크시트를 스캔하여 모든 `#Discount#`를 찾아 익명 객체에서 전달한 값으로 교체합니다.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

이 호출 이후 `B2` 셀의 수식은 다음과 같이 됩니다:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

워크북이 계산되면 `B2`는 **90**을 표시합니다. 즉, 원래 가격 100에 10 % 할인이 적용된 결과입니다.

**Why it works:** `StartSmartMarkerProcessing`은 모든 셀을 순회하면서 `#Discount#` 토큰을 찾아 숫자 값으로 대체합니다. 토큰이 `IF` 문 안에 있기 때문에 할인 값이 0일 경우에도 스프레드시트가 정상적으로 처리됩니다.

---

## 4단계: 스프레드시트에서 할인 적용 – 결과 확인

계산을 트리거하고 최종 가격을 콘솔에 출력해 봅시다. 이 단계는 **apply discount in spreadsheet** 워크플로가 성공했음을 증명합니다.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

`discountData.Discount`를 `0.25`로 바꾸고 프로세서를 다시 실행하면 출력이 자동으로 25 % 할인을 반영합니다—추가 코드는 필요하지 않습니다.

---

## 5단계: 엣지 케이스 및 다중 할인 처리

### 0% 할인 행

제품이 세일되지 않을 때도 있습니다. 앞서 넣은 `IF` 문이 이미 이 시나리오를 커버합니다: `#Discount#`가 `0`이면 원래 가격이 그대로 전달됩니다.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### 다중 할인 열

행마다 별도의 할인이 필요하면 각 행에 고유 마커를 부여합니다(e.g., `#Discount1#`, `#Discount2#`) 그리고 컬렉션을 전달합니다:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

프로세서는 마커를 순차적으로 매칭하므로 각 행에 올바른 값이 적용됩니다.

---

## 전체 작업 예제

아래는 위의 모든 단계를 포함한 완전한 복사‑가능 프로그램입니다. `Program.cs`로 저장하고 `Aspose.Cells`에 대한 참조를 추가한 뒤 실행하세요.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

실행하면 예상 숫자가 출력되고, `DiscountedPricing.xlsx` 파일이 생성됩니다. Excel에서 열어보면 수식이 이미 적용된 상태임을 확인할 수 있습니다.

---

## 결론

이제 **create discount template**, **apply discount in spreadsheet**, **inject data into template**, 그리고 스마트 마커를 위한 **define variable prefix**를 간결한 C# 몇 줄로 구현하는 방법을 알게 되었습니다. 이 패턴은 규모에 맞게 확장할 수 있습니다—익명 객체를 바꾸거나 컬렉션을 전달해 대량 업데이트를 수행하면 동일한 템플릿이 모든 할인 시나리오를 처리합니다.

다음 단계에 도전해 보세요:

- 할인과 함께 세금 계산을 추가하기.
- 할인 비율을 하드코딩하지 않고 데이터베이스에서 가져오기.
- 높은 할인이 적용된 행을 강조하는 조건부 서식 사용하기.

이러한 확장은 핵심 아이디어를 유지하면서 할인 템플릿의 활용도를 크게 높여줍니다.

질문이나 멋진 활용 사례가 있나요? 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}