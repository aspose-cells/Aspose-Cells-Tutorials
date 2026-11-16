---
category: general
date: 2026-11-16
description: Aspose.Cells, 동적 배열 함수 및 람다 리듀서를 사용하여 Excel에서 배열을 확장하는 방법을 배우고, C#에서
  Excel 파일을 작성합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: ko
lastmod: 2026-11-16
og_description: Aspose.Cells와 동적 배열 함수, 람다 리듀서를 사용하여 Excel에서 배열을 확장하는 방법. Excel 파일을
  작성하는 전체 C# 예제를 따라보세요.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Aspose.Cells를 사용하여 Excel에서 배열을 확장하는 방법 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells를 사용하여 Excel에서 배열 확장하는 방법
url: /ko/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 Excel에서 배열 확장하기

C#에서 Excel 워크시트에 **배열을 확장하는 방법**이 필요하다면, 이 튜토리얼이 정확한 단계를 보여줍니다. Excel 워크북을 생성하고, `EXPAND`와 `REDUCE` 같은 동적 배열 함수를 사용하며, **lambda** 누산기를 적용하고, 마지막으로 **Excel 파일을** 디스크에 **쓰기**합니다. 이 방법은 Aspose.Cells 23.10 이상에서 작동하며, 별도의 Excel 설치가 필요하지 않습니다.

이 가이드를 끝까지 따라 하면, 프로그래밍 환경에서 동적 배열 수식의 강력함을 보여주는 `ExpandReduceDemo.xlsx` 파일을 완전히 동작하도록 만들 수 있습니다.

## 준비 사항

- .NET 6.0 (또는 Aspose.Cells에서 지원하는 모든 .NET 버전)
- Aspose.Cells for .NET 패키지 (`dotnet add package Aspose.Cells`)
- 코드 편집기 또는 IDE (Visual Studio, VS Code, Rider 등)

Aspose.Cells가 파일 형식을 내부적으로 처리하므로 추가적인 COM 인터옵이나 Office 설치가 필요하지 않습니다.

## 1단계: Excel 워크북 만들기

첫 번째 작업은 메모리 내에서 **Excel 워크북을 생성**하는 것입니다. Aspose.Cells는 전체 XLSX 파일을 나타내는 `Workbook` 클래스를 제공합니다.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **왜 중요한가:** `Workbook`을 인스턴스화하면 깨끗한 캔버스를 얻게 됩니다. 기본 워크시트가 이미 준비되어 있으므로, 여러 시트를 원하지 않는 한 수동으로 추가할 필요가 없습니다.

## 2단계: 수직 배열 상수 삽입

Excel의 동적 배열 엔진은 리터럴 배열 상수와 함께 작동할 수 있습니다. 여기서는 수직 배열 `{1;2;3;4;5}`를 셀 **A1**에 배치합니다.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **팁:** 세미콜론(`;`)은 상수에서 행을 구분하고, 콤마(`,`)는 열을 구분합니다. 이는 Excel 자체 구문과 동일합니다.

## 3단계: 배열을 매트릭스로 확장

이제 핵심 질문인 **배열을 확장하는 방법**에 답합니다—`EXPAND` 함수를 사용합니다. 이 수식은 단일 열 배열을 5행 × 2열 매트릭스로 확장하며, **B1**부터 시작합니다.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **왜 EXPAND인가?** `EXPAND(source, rows, cols)`는 지정된 크기로 소스 범위를 강제로 차지하게 하며, 필요에 따라 빈 셀로 채웁니다. 단일 배열에서 더 큰 매트릭스를 생성하는 가장 가독성 높은 방법입니다.

## 4단계: lambda 누산기로 매트릭스 축소

`REDUCE` 함수는 범위를 순회하면서 **lambda** 식을 사용해 값을 누적합니다. 여기서는 각 열 값을 하나의 열로 합산하여 결과를 **D1**에 배치합니다.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **lambda 사용법:** `LAMBDA(acc, val, acc+val)`은 현재 누산기(`acc`)와 다음 셀 값(`val`)을 받아 새로운 누산기 값을 반환합니다. 이는 누적 합계를 수행합니다. 이 예제는 코드에서 Excel 수식으로 **lambda를 사용하는 방법**을 보여줍니다.

## 5단계: 수식 계산하여 결과 표시

Aspose.Cells는 수식을 설정할 때 자동으로 계산하지 않습니다. `CalculateFormula`를 호출하면 워크북의 모든 수식이 계산됩니다.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **참고:** 생성된 파일을 Excel에서 열면 값이 이미 표시됩니다. 이는 미리 계산되었기 때문입니다.

## 6단계: Excel 파일을 디스크에 쓰기

마지막으로 `Save` 메서드를 사용해 **Excel 파일을 쓰기**합니다. 쓰기 권한이 있는 폴더를 선택하세요.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 예상 결과

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **열 B**와 **열 C**는 `EXPAND`에 의해 생성된 5 × 2 매트릭스를 포함합니다.
- **셀 D1**은 `REDUCE` + **lambda** 수식으로 계산된 `15`(전체 합계)를 보여줍니다.

## 일반적인 질문 및 엣지 케이스

- **소스가 제공하는 열보다 더 많은 열로 확장할 수 있나요?**  
  네. `EXPAND`는 누락된 열을 빈 셀로 채워서 패딩합니다. 행도 동일하게 동작합니다.

- **소스 배열이 가로(`{1,2,3,4,5}`)인 경우는?**  
  `EXPAND`는 이를 단일 행으로 취급합니다. 여전히 행과 열을 지정해 원하는 형태로 재구성할 수 있습니다.

- **`REDUCE`가 비숫자 데이터에도 작동하나요?**  
  lambda가 누산기 타입과 호환되는 값을 반환해야 합니다. 텍스트 연결을 원한다면 `LAMBDA(acc, val, acc & val)`와 같이 사용할 수 있습니다.

- **모든 변경마다 `CalculateFormula`를 호출해야 하나요?**  
  저장 전에 계산된 값이 필요할 때만 호출하면 됩니다. 생략하면 Excel이 파일을 열 때 자동으로 재계산합니다.

## 전문가 팁

- **성능:** 큰 워크북에서는 모든 수식을 설정한 뒤 한 번만 `workbook.CalculateFormula`를 호출하세요. 셀마다 호출하면 비효율적입니다.
- **버전 호환성:** `EXPAND`와 `REDUCE`는 Excel 365 이상에서 제공됩니다. Aspose.Cells는 계산 엔진이 내장돼 있기 때문에 대상 Excel 버전과 무관하게 구현됩니다.
- **수식 디버깅:** `sheet.Cells["B1"].Formula`를 사용해 설정한 수식 문자열을 읽어보세요. 동적으로 수식을 만들 때 유용합니다.

## 결론

이제 Aspose.Cells를 사용해 Excel에서 **배열을 확장하는 방법**, **동적 배열 함수** 활용, `REDUCE`와 **lambda** 적용, 그리고 C#에서 **Excel 파일을 쓰는 방법**을 알게 되었습니다. 이 엔드‑투‑엔드 예제는 매트릭스 전치, 누적 합계, 사용자 정의 집계 등 보다 복잡한 데이터 변환에도 적용할 수 있습니다.

---

*다음 단계:*  
- `FILTER`, `SORT`, `UNIQUE`와 같은 다른 동적 함수 탐색하기.  
- 여러 `LAMBDA` 식을 결합해 재사용 가능한 사용자 정의 함수를 만들기.  
- 워크북 생성을 ASP.NET Core API에 통합해 실시간 보고서를 생성하기.

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하며, 추가 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}