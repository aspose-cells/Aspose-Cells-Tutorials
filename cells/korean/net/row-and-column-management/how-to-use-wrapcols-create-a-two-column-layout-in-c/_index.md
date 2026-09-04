---
category: general
date: 2026-02-15
description: C# 워크시트에서 WRAPCOLS를 사용하여 두 열 레이아웃을 만들고, 수식을 추가하며, 시퀀스 배열을 생성하는 단계별 가이드.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: ko
og_description: C# 워크시트에서 WRAPCOLS를 사용해 두 열 레이아웃을 만들고, 수식을 추가하며, 시퀀스 배열을 생성하는 방법 –
  완전 가이드.
og_title: 'WRAPCOLS 사용 방법: C#에서 두 열 레이아웃'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'WRAPCOLS 사용 방법: C#에서 두 열 레이아웃 만들기'
url: /ko/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# WRAPCOLS 사용 방법: C#에서 두 열 레이아웃 만들기

Excel 스타일 워크시트 안에서 빠른 두 열 보기가 필요할 때 **WRAPCOLS 사용 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 각 셀마다 루프를 작성하지 않고 생성된 목록을 깔끔한 열로 나누려 할 때 벽에 부딪칩니다. 좋은 소식은? `WRAPCOLS` 함수를 사용하면 `A1`에 단일 수식을 넣고 Excel(또는 호환 엔진)이 무거운 작업을 처리합니다.

이 튜토리얼에서는 **수식 추가 방법**을 살펴보고, **두 열 레이아웃 만들기**를 생성하며, **동적으로 열 만들기**와 **시퀀스 배열 생성** 값을 즉석에서 만드는 방법을 보여드립니다. 마지막까지 하면 프로젝트에 붙여넣고 실행하여 깔끔한 두 열 블록이 즉시 나타나는 완전 실행 가능한 C# 스니펫을 얻게 됩니다.

## 배울 내용

- `WRAPCOLS`의 목적과 수동 루프보다 더 나은 대안인 이유.  
- C#을 사용하여 워크시트 셀에 **수식 추가**하는 방법.  
- `SEQUENCE`로 시퀀스 배열을 생성하고 이를 `WRAPCOLS`에 전달하는 방법.  
- 수식이 즉시 계산되도록 시트를 다시 계산하는 팁.  
- 엣지 케이스 처리(예: 빈 워크시트, 사용자 정의 열 개수).

표준 Excel 처리 패키지를 제외하고 외부 라이브러리는 필요하지 않습니다 – 직관적인 API 때문에 **ClosedXML**을 사용할 것이지만, 이 개념은 EPPlus, SpreadsheetGear, 혹은 Google Sheets API에도 적용됩니다.

---

## 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET Core 및 .NET Framework에서 컴파일됩니다).  
- **ClosedXML** 참조 (`dotnet add package ClosedXML`).  
- 기본 C# 지식 – `using` 문과 객체 초기화에 익숙해야 합니다.

이미 워크북을 열어 두었다면 파일 생성 부분을 건너뛰고 바로 수식 섹션으로 이동할 수 있습니다.

## 단계 1: 워크시트 설정 (열 만들기 방법)

먼저 작업할 `Worksheet` 객체가 필요합니다. ClosedXML에서는 `XLWorkbook`에서 얻습니다. 아래 스니펫은 새 워크북을 만들고, *Demo*라는 시트를 추가한 뒤, 명확성을 위해 `worksheet`라는 참조를 가져옵니다.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **왜 이름을 바꾸나요?**  
> 변수 이름을 짧게 (`worksheet`) 유지하면 이후 코드를 읽기 쉬워지고, 특히 여러 작업을 체인할 때 유리합니다. 또한 대부분의 문서에서 보는 명명 스타일을 반영해 인지 부하를 줄여줍니다.

## 단계 2: 수식 작성 (수식 추가 및 시퀀스 배열 생성 방법)

이제 마법 같은 라인이 나옵니다. **A1** 셀에 두 가지 작업을 수행하는 수식을 넣겠습니다:

1. **시퀀스 배열 생성**: 6개의 숫자(`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **그 숫자를 두 열로 래핑** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **무슨 일이 일어나나요?**  
> `SEQUENCE(6)`은 수직 배열 `{1;2;3;4;5;6}`을 생성합니다. `WRAPCOLS`는 그 배열을 지정된 열 수(**2**)로 “래핑”합니다. 결과는 다음과 같은 3행 × 2열 블록입니다:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

두 번째 인수를 **3**으로 바꾸면 대신 세 열 레이아웃이 됩니다. 이것이 **동적으로 열 만들기**를 수동 루프 없이 수행하는 핵심입니다.

## 단계 3: 워크시트 재계산 (수식 평가 보장)

ClosedXML은 수식을 작성해도 자동으로 평가하지 않습니다. 평가를 강제하려면 워크북(또는 특정 워크시트)에서 `Calculate()`를 호출해야 합니다.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **프로 팁:** 큰 워크북을 다룰 때는 실제로 변경된 시트에만 `Calculate()`를 호출하세요. 메모리를 절약하고 처리 속도를 높입니다.

`WrapColsDemo.xlsx`를 열면 **A1:B3**에 두 열 레이아웃이 깔끔하게 채워진 것을 볼 수 있습니다. 행이나 열을 루프하는 추가 코드가 필요하지 않았으며 – `WRAPCOLS`가 모든 것을 처리했습니다.

## 단계 4: 출력 확인 (예상 결과)

프로그램을 실행한 후 생성된 파일을 열면 다음과 같이 표시됩니다:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

숫자가 세로로(즉, 모두 A 열에) 나타난다면, 수식을 설정한 **후에** `worksheet.Calculate()`를 호출했는지 다시 확인하세요. 일부 엔진은 `workbook.Calculate()`도 필요합니다; 위 스니펫은 ClosedXML 내장 평가기에 대해 작동합니다.

## 일반적인 변형 및 엣지 케이스

### 열 개수 변경하기

다른 행 개수로 **두 열 레이아웃 만들기**를 하려면 `SEQUENCE` 크기나 `WRAPCOLS`의 두 번째 인수를 조정하면 됩니다:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

이렇게 하면 4행 × 3열 블록(12개의 숫자를 세 열에 나눔)이 생성됩니다.

### 동적 열 개수 사용하기

열 개수가 변수에서 온다면 문자열 보간을 사용해 삽입하세요:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

이제 런타임에 맞게 조정되는 **수식 추가 방법**을 갖게 되었습니다.

### 빈 워크시트

워크시트가 비어 있어도 `Calculate()`는 작동합니다 – 수식이 A1부터 셀을 채웁니다. 하지만 나중에 출력 범위와 교차하는 행/열을 삭제하면 `#REF!` 오류가 나타날 수 있습니다. 이를 방지하려면 먼저 대상 범위를 지우세요:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### 호환성

`WRAPCOLS`와 `SEQUENCE`는 Office 365에서 도입된 Excel의 **동적 배열** 함수의 일부입니다. 오래된 Excel 버전을 대상으로 하면 해당 함수가 없으며 수동 루프가 필요합니다. ClosedXML의 평가기는 최신 Excel 동작을 그대로 반영하므로 최신 환경에서 안전합니다.

## 전체 작업 예제 (복사‑붙여넣기 준비)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**예상 결과:** *WrapColsDemo.xlsx*를 열면 앞서 설명한 대로 1‑6 숫자가 정렬된 깔끔한 두 열 레이아웃이 표시됩니다.

## 결론

우리는 **WRAPCOLS 사용 방법**을 통해 **두 열 레이아웃 만들기**를 다루었고, 프로그래밍 방식으로 **수식 추가 방법**을 시연했으며, `SEQUENCE`가 루프 없이 **시퀀스 배열 생성** 값을 제공하는 것을 확인했습니다. C#에서 Excel의 동적 배열 함수를 활용하면 코드를 간결하고 읽기 쉽고 유지 보수하기 쉬운 형태로 유지할 수 있습니다.

다음으로 탐색해 볼 수 있습니다:

- `ROWS` 또는 `COUNTA`를 사용한 **동적 행 개수 만들기**.  
- ClosedXML 스타일링 API를 이용한 **출력 스타일링**(테두리, 숫자 형식).  
- 레이아웃 구축 후 **CSV로 내보내기**를 통해 후속 처리.

한 번 시도해 보고, 열 개수를 조정해 보세요. 복잡한 스프레드시트를 얼마나 빠르게 프로토타이핑할 수 있는지 확인해 보세요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}