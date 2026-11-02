---
category: general
date: 2026-06-27
description: C#에서 wrapcols와 wrap rows 엑셀을 사용하는 방법. C#으로 엑셀 워크북을 생성하고 단계별 예제로 엑셀 수식을
  다시 계산하는 방법을 배웁니다.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: ko
og_description: C#를 사용하여 Excel에서 wrapcols와 wrap rows를 사용하는 방법. 이 가이드는 C#로 Excel 워크북을
  만들고 몇 분 안에 Excel 수식을 다시 계산하는 방법을 보여줍니다.
og_title: C#에서 wrapcols 사용 방법 – 완전한 Excel 래핑 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: C#에서 wrapcols 사용 방법 – Excel WRAPROWS 및 수식 재계산 완전 가이드
url: /ko/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 wrapcols 사용 방법 – Excel WRAPROWS 및 수식 재계산 전체 가이드

긴 목록을 깔끔한 그리드로 변환해야 할 때 **wrapcols 사용 방법**이 궁금하셨나요? 수동 복사‑붙여넣기 방법을 시도해 보셨을 수도 있지만, 느리고 오류가 발생하기 쉬우며 정말 번거롭습니다. 좋은 소식은? Excel의 `WRAPCOLS`(및 형제 함수 `WRAPROWS`)가 무거운 작업을 대신해 주며, 이를 C# 코드에서 제어할 수 있다는 점입니다.

이 튜토리얼에서는 C#에서 Excel 워크북을 생성하고, `WRAPCOLS`와 `WRAPROWS`를 적용한 뒤, **excel 수식 재계산**을 수행해 래핑된 데이터가 즉시 표시되도록 하는 과정을 단계별로 살펴봅니다. 마지막에는 .NET 프로젝트에 바로 넣어 실행할 수 있는 완전한 코드 스니펫을 제공합니다.

## 배울 내용

- Aspose.Cells 라이브러리를 사용해 **create excel workbook c#** 하는 방법 (COM interop 필요 없음).  
- `WRAPCOLS` 함수의 정확한 구문과 `WRAPROWS`와의 차이점.  
- 함수를 삽입한 후 **recalculate excel formulas**가 반드시 필요한 이유와 효율적인 수행 방법.  
- `.xlsx` 파일로 결과를 확인할 수 있는 완전한 실행 예제.  

**전제 조건** – .NET 6+ (또는 .NET Framework 4.7+), Visual Studio 2022 혹은 선호하는 IDE, 그리고 Aspose.Cells for .NET NuGet 패키지가 필요합니다. Aspose.Cells가 처음이라면 걱정 마세요; 단계는 간단하고 자세히 설명됩니다.

---

## Step 1: 프로젝트 설정 및 Aspose.Cells 설치

먼저 새 콘솔 프로젝트를 생성합니다:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Visual Studio를 사용한다면 프로젝트를 마우스 오른쪽 버튼으로 클릭 → *Manage NuGet Packages* → **Aspose.Cells** 검색 후 설치하면 됩니다.

이 라이브러리를 통해 나머지 튜토리얼에서 사용할 `Workbook`, `Worksheet`, `Cell` 클래스를 얻을 수 있습니다.

## Step 2: Excel 워크북 생성 및 샘플 데이터 채우기

이제 워크북을 만들고 첫 번째 워크시트를 가져온 뒤, **A** 열과 **B** 열에 샘플 숫자를 채워 보겠습니다. 이 데이터는 이후 열과 행으로 래핑됩니다.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Why this matters:** 결정적인 데이터를 가지고 있으면 `WRAPCOLS`와 `WRAPROWS`가 기대한 대로 작동하는지 검증할 수 있습니다.

## Step 3: `WRAPCOLS` 함수 적용 – **how to use wrapcols**

`WRAPCOLS`는 1차원 범위를 받아 지정된 열 수만큼 가로로 펼치고, 필요에 따라 새로운 행을 자동으로 추가합니다. 다음은 **A1** 셀에 삽입할 정확한 수식입니다:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Explanation:** 두 번째 인수(`3`)는 Excel에 행당 세 개의 열을 만들도록 지시합니다. 따라서 처음 세 값(1, 2, 3)은 A1:C1에, 다음 세 값(4, 5, 6)은 A2:C2에, 나머지는 다음 행에 채워집니다.

## Step 4: `WRAPROWS` 함수 적용 – wrap rows excel

`WRAPROWS`는 반대 작업을 수행합니다: 세로 범위를 받아 지정된 행 수만큼 열에 배치합니다. 이 수식을 **B1**에 넣겠습니다:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Explanation:** 열당 `2` 행을 지정하면 값 “A, B”는 B1:B2에, “C, D”는 C1:C2에 배치되는 식입니다. 함수는 시트를 자동으로 가로로 확장합니다.

## Step 5: 모든 수식 재계산 – **recalculate excel formulas**

프로그램matically 수식을 설정하면 Excel은 워크북을 열 때까지 혹은 라이브러리에 명시적으로 계산을 요청하기 전까지 결과를 계산하지 않습니다. 여기서 **recalculate excel formulas**가 필요합니다:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Why you need this:** `CalculateFormula()`를 호출하지 않으면 파일을 열었을 때 셀에 `=WRAPCOLS(...)` 텍스트가 그대로 표시되어 튜토리얼의 목적이 무색해집니다.

## Step 6: 워크북 저장 및 결과 확인

마지막으로 워크북을 디스크에 저장합니다. 생성된 파일을 Excel에서 열어 래핑된 레이아웃을 확인하세요.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Expected Result

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Columns A‑C**는 `WRAPCOLS` 호출에 의해 (행당 세 열) 채워집니다.  
- **Rows B‑I**는 `WRAPROWS` 호출에 의해 (열당 두 행) 채워집니다.  

`output.xlsx`를 열면 위와 동일한 레이아웃을 확인할 수 있습니다. 숫자가 맞지 않으면 수식 문자열을 다시 확인하고 `CalculateFormula()` 호출 여부를 점검하세요.

---

## Common Questions & Edge Cases

### What if the source range is empty?
Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting in a blank cell. It’s safe to call the functions even when you’re not sure about data presence.

### Can I wrap more than one range at a time?
Yes—just place additional formulas in other cells. Each formula works independently, so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.

### How does this differ from a simple copy‑paste transpose?
`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20 items and ask for 3 columns, the function creates the necessary number of rows (7 in this case) without you calculating the dimensions manually.

### Does the library support dynamic array formulas (Excel 365)?
Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS` and `WRAPROWS`. The calculation engine will spill the results just like native Excel.

### What about performance on large datasets?
For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`) or disabling automatic calculation while you insert formulas, then re‑enable it before saving.

---

## Full Source Code (Ready to Run)

Below is the complete program—copy it into `Program.cs` and hit **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Conclusion

You now know **how to use wrapcols** (and its counterpart `WRAPROWS`) from C# to reshape data in an Excel sheet, and you understand why **recalculate excel formulas** is a mandatory step. This pattern—*create excel workbook c# → insert WRAP functions → recalculate*—is a solid foundation for any reporting or data‑presentation task that requires dynamic column or row layouts.

What’s next? Try experimenting with:

- Different column/row counts (`WRAPCOLS(..., 5)` or `WRAPROWS(..., 4)`).  
- Combining `WRAPCOLS` with other dynamic array functions like `FILTER` or `SORT`.  
- Exporting the workbook to PDF with `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Feel free to tweak the sample, add styling, or integrate it into a larger automation pipeline. If you hit any snags, drop a comment below—happy coding!

![wrapcols와 wraprows가 단일 열을 그리드로 변환하는 과정을 보여주는 다이어그램 – how to use wrapcols 예시](wrapcols-wraprows-diagram.png "how to use wrapcols 예시")


## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 기반으로 하여 관련 주제를 심도 있게 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 제공하므로 API 기능을 마스터하고 프로젝트에 다양한 구현 방식을 적용하는 데 도움이 됩니다.

- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Hide Rows and Columns in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}