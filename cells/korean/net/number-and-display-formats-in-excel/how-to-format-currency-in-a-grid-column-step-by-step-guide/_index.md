---
category: general
date: 2026-02-15
description: C#에서 열 번호 형식을 설정하고 사용자 지정 숫자 형식을 적용하여 통화를 빠르게 포맷하는 방법. 열 이름으로 열을 검색하고
  그리드 열 정렬을 설정하는 방법을 배웁니다.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: ko
og_description: C#를 사용하여 그리드 열에서 통화를 형식화하는 방법. 이 튜토리얼에서는 이름으로 열을 검색하고, 열 번호 형식을 설정하고,
  사용자 지정 숫자 형식을 적용하며, 그리드 열 정렬을 설정하는 방법을 보여줍니다.
og_title: 그리드 열에서 통화 형식 지정하기 – 완전 가이드
tags:
- C#
- GridFormatting
- UI
title: 그리드 열에서 통화 형식 지정 방법 – 단계별 가이드
url: /ko/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

string based on the user’s locale." => "**동적 문화권** – 사용자의 로케일에 따라 포맷 문자열을 전환합니다."

Second bullet incomplete: "**Conditional". Probably "Conditional formatting"? but incomplete. We'll translate as "**조건부**". Keep as is? Might be incomplete; we keep same text but translate "Conditional" to "조건부". So bullet: "- **Conditional" -> "- **조건부". Keep line as is.

Now closing shortcodes.

All good.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 그리드 열에서 통화 형식 지정 – 완전 프로그래밍 튜토리얼

그리드 열에서 **통화를 어떻게 포맷**해야 할지 머리를 쥐어뜯으며 고민해 본 적 있나요? 당신만 그런 것이 아닙니다. `1234.5` 같은 단순한 숫자를 바라보며 `$1,234.50` 형태로 자동 변환되길 바란다면, 보통은 몇 줄의 설정만으로 해결됩니다.  

이 가이드에서는 **열을 이름으로 가져오기**, **열의 숫자 형식 설정**, 그리고 일반적인 회계 레이아웃을 따르는 **사용자 정의 숫자 형식 적용**을 다룹니다. 또한 **그리드 열 정렬 설정**과 UI를 깔끔하게 보이게 하는 섬세한 테두리 추가도 함께 설명합니다.

> **TL;DR** – 끝까지 읽으면, 어떤 `GridJs`‑스타일 컨트롤에서도 원시 소수를 아름답게 포맷된 통화 값으로 변환하는 즉시 실행 가능한 코드 조각을 얻게 됩니다.

---

## 필요 사항

- .NET 프로젝트 (C# 8.0 이상을 지원하는 버전이면 모두 가능 – Visual Studio 2022가 특히 좋습니다).  
- `Columns` 컬렉션을 제공하는 그리드 컴포넌트 (예제는 가상의 `GridJs` 클래스를 사용하지만, 개념은 DevExpress, Telerik, Syncfusion 그리드에도 적용됩니다).  
- C# 문법에 대한 기본적인 이해 – 고급 트릭은 필요 없습니다.

이미 준비되어 있다면 좋습니다. 없으면 콘솔 앱을 하나 만들면 됩니다; 그리드는 예시를 위해 모킹할 수 있습니다.

## 단계별 구현

각 단계마다 간결한 코드 블록과 해당 라인이 중요한 **이유**에 대한 짧은 설명, 그리고 흔히 발생하는 실수를 피하기 위한 팁을 확인할 수 있습니다.

### ## Step 1 – “Amount” 열을 이름으로 가져오기

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**왜 중요한가:**  
대부분의 그리드 API는 사전 형태의 인덱서를 통해 열을 노출합니다. 헤더 이름(`"Amount"`)으로 열을 가져오면 기본 데이터 소스를 건드리지 않고도 해당 열의 표시 방식을 조정할 수 있습니다.  

**프로 팁:**  
`null` 반환에 항상 대비하세요 – 열 이름 오타나 동적 스키마 변경으로 인해 런타임에 `NullReferenceException`이 발생할 수 있습니다.

### ## Step 2 – 사용자 정의 통화 마스크를 사용해 열 숫자 형식 설정

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**왜 중요한가:**  
포맷 문자열은 Excel 회계 형식 규칙을 따릅니다:

- `_(* #,##0.00_)` → 양수, 통화 기호 앞에 공백을 두고 오른쪽 정렬.  
- `_(* (#,##0.00)` → 음수는 괄호로 감싸짐.  
- `_(* \"-\"??_)` → 0 값은 대시(-)로 표시.  
- `_(@_)` → 텍스트 값은 그대로 유지.

**사용자 정의 숫자 형식 적용**을 사용하면 천 단위 구분자, 소수점 자리수, 통화 기호 위치 등을 완벽히 제어할 수 있습니다.  

**예외 상황:** 애플리케이션이 다른 로케일(예: USD 대신 Euro)을 사용해야 한다면, 앞 공백을 해당 기호로 교체하거나 데이터 소스에서 `CultureInfo` 기반 포맷을 사용하세요.

### ## Step 3 – 가독성을 위해 열 내용을 오른쪽 정렬

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**왜 중요한가:**  
통화 값은 소수점 기준으로 정렬될 때 스캔하기 쉽습니다. **그리드 열 정렬 설정**을 `Right`로 지정하면 스프레드시트와 동일한 방식으로 금액을 표시합니다.  

**주의점:** 일부 그리드는 사용자 정의 템플릿이 있는 셀의 정렬을 무시합니다. 정렬이 적용되지 않으면 해당 열이 커스텀 셀 렌더러를 사용하고 있지 않은지 확인하세요.

### ## Step 4 – 열 셀에 얇은 회색 테두리 추가

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**왜 중요한가:**  
섬세한 테두리는 특히 그리드에 교차 행 색상이 있을 때 “Amount” 열을 주변 열과 구분해 줍니다. 이는 데이터가 별도의 재무 수치를 나타낸다는 시각적 신호입니다.  

**팁:** 인쇄용으로 더 두꺼운 선이 필요하면 `BorderLineStyle`을 `Medium`으로 바꾸거나 `Color`를 `Color.Black`으로 설정하세요.

## 전체 작업 예제

`GridJs`‑스타일 컨트롤을 사용하는 WinForms 또는 WPF 프로젝트에 바로 넣을 수 있는 전체 코드 스니펫입니다. 예제는 포맷된 값을 콘솔에 출력하므로 UI 없이도 결과를 확인할 수 있습니다.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**예상 콘솔 출력**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

양수는 오른쪽 정렬되고, 음수는 괄호로 표시되며, 0은 대시(-)로 나타나는 것을 확인하세요 – 이는 사용자 정의 포맷 문자열이 지정한 대로 동작합니다.

## 자주 묻는 질문 및 예외 상황

| Question | Answer |
|----------|--------|
| *그리드가 다른 문화권(예: $ 대신 €)을 사용한다면 어떻게 해야 하나요?* | 포맷 문자열의 앞 공백을 원하는 기호로 교체하거나 데이터 소스가 `CultureInfo.CurrentCulture`를 사용해 미리 포맷된 문자열을 출력하도록 하세요. |
| *같은 포맷을 여러 열에 재사용할 수 있나요?* | 물론 가능합니다. 포맷 문자열을 상수(`const string CurrencyMask = "...";`)에 저장하고 통화가 필요한 곳에 할당하면 됩니다. |
| *열에 문자열 값이 포함되어 있으면 어떻게 되나요?* | 포맷 문자열은 숫자형에만 적용됩니다. 문자열은 그대로 통과하므로 마스크의 마지막 부분(`_(@_)`)이 존재해 비숫자 콘텐츠를 보존합니다. |
| *성능에 영향을 미치나요?* | 거의 없습니다. 포맷은 데이터 조회 시가 아니라 렌더링 시에 적용됩니다. 프레임당 수천 행을 렌더링하지 않는 한 속도 저하를 느끼지 못할 것입니다. |
| *인쇄용 보고서에서 테두리를 더 두껍게 하려면 어떻게 해야 하나요?* | `BorderLineStyle.Thin`을 `BorderLineStyle.Medium` 혹은 `BorderLineStyle.Thick`으로 교체하세요. 일부 라이브러리는 픽셀 단위 너비를 직접 지정할 수도 있습니다. |

## 마무리

시작부터 끝까지 그리드 열에서 **통화 형식 지정** 방법을 살펴보았습니다: 열을 이름으로 가져오고, 숫자 형식을 설정하고, 사용자 정의 숫자 포맷을 적용하고, 셀을 정렬하고, 세련된 테두리를 추가합니다. 전체 예제는 바로 실행 가능하며 기대할 수 있는 정확한 시각적 결과를 보여줍니다.

더 확장하고 싶다면 다음을 시도해 보세요:

- **동적 문화권** – 사용자의 로케일에 따라 포맷 문자열을 전환합니다.  
- **조건부

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}