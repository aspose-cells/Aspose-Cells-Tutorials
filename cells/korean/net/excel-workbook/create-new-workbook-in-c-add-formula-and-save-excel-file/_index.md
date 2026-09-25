---
category: general
date: 2026-02-23
description: C#로 프로그래밍하여 새 워크북을 만들고 셀에 수식을 추가합니다. EXPAND 사용 방법을 배우고, Excel 워크북을 손쉽게
  저장하세요.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: ko
og_description: C#로 프로그래밍하여 새 워크북을 만들고, 셀에 수식을 추가한 뒤 EXPAND 사용법을 배우며, 몇 초 만에 Excel
  워크북을 저장하세요.
og_title: C#에서 새 워크북 만들기 – 수식 추가 및 엑셀 파일 저장
tags:
- C#
- Excel Automation
- Aspose.Cells
title: C#에서 새 워크북 만들기 – 수식 추가 및 엑셀 파일 저장
url: /ko/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 새 워크북 만들기 – 수식 추가 및 Excel 파일 저장

코드만으로 **create new workbook** 객체를 만들고 Excel을 전혀 열지 않아도 된다고 생각해 본 적 있나요? 여러분만 그런 것이 아닙니다. 보고서, 내보내기, 혹은 빠른 데이터 덤프를 위해 스프레드시트를 즉석에서 생성해야 할 때 많은 개발자들이 난관에 봉착합니다.  

좋은 소식은? 이 가이드에서는 **create new workbook**을 정확히 만드는 방법, **add formula to cell**을 삽입하는 방법, 그리고 몇 줄의 C# 코드만으로 **save excel workbook**하는 방법을 보여드립니다. 또한 **how to use expand**를 활용해 수동 복사 없이 동적 배열을 생성하는 방법도 살펴봅니다. 끝까지 읽으면 **create excel file programmatically**하고 이를 사용자나 다운스트림 서비스에 전달할 수 있게 됩니다.

## Prerequisites

- .NET 6.0 이상 (최근 .NET 런타임이면 모두 가능)
- Aspose.Cells for .NET (무료 체험판 또는 정식 라이선스) – 아래에서 사용하는 `Workbook` 및 `Worksheet` 클래스를 제공합니다.
- C# 문법에 대한 기본 이해 – 깊은 Excel 지식은 필요 없습니다.

이미 준비되어 있다면 좋습니다! 아직이라면 NuGet에서 Aspose.Cells를 가져오세요 (`Install-Package Aspose.Cells`). 이제 시작할 준비가 되었습니다.

---

## Step 1: Create New Workbook – The Foundation

먼저 새 워크북 객체를 인스턴스화해야 합니다. 이는 완전히 비어 있는 새 Excel 파일을 여는 것과 같습니다.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Why this matters:** `Workbook` 클래스는 모든 Excel 조작의 진입점입니다. 새 인스턴스를 만들면 파일 시스템에 접근하지 않고도 시트, 스타일, 수식 등을 위한 메모리를 할당합니다.

---

## Step 2: Access the First Worksheet

새 워크북마다 기본 워크시트가 하나 포함되어 있습니다(*Sheet1*). 데이터를 넣고 수식을 적용하려면 이 워크시트를 가져와야 합니다.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** 여러 시트가 필요하면 `workbook.Worksheets.Add("MySheet")`를 호출하고 반환된 `Worksheet` 객체를 사용하면 됩니다.

---

## Step 3: Add Formula to Cell – Using EXPAND

이제 재미있는 부분, 수식 삽입입니다. `EXPAND` 함수는 정적 배열을 더 큰 자동 채워진 범위로 바꾸고 싶을 때 완벽합니다.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### How the EXPAND Formula Works

| Argument | Meaning |
|----------|---------|
| `{1,2,3}` | 소스 배열 (가로로 나열된 세 개 숫자) |
| `5`       | 결과에 원하는 행 수 |
| `1`       | 원하는 열 수 (세로 배열을 유지하려면 1) |

Excel이 이를 평가하면 **세로** 목록이 생성됩니다.

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Why use EXPAND?** 수동 복사나 VBA 루프가 필요 없게 해 줍니다. 함수가 데이터를 동적으로 재구성하므로 스프레드시트를 더 견고하고 유지보수가 쉬워집니다.

---

## Step 4: Save Excel Workbook – Persist the Result

수식이 삽입되었으니 마지막 단계는 워크북을 디스크에 저장하는 것입니다. 쓰기 권한이 있는 폴더라면 어디든 선택할 수 있습니다.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **What you’ll see:** `ExpandFormula.xlsx` 파일을 Excel에서 열면 셀 `A1`에 확장된 배열이 표시됩니다. 수식 자체는 셀에 남아 있으므로 소스 배열을 편집하면 출력이 자동으로 업데이트됩니다.

---

## Optional: Verify the Output Programmatically

Excel을 직접 열고 싶지 않다면 값을 다시 읽어와서 기대한 대로인지 확인할 수 있습니다.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

위 코드를 실행하면 다음과 같이 출력됩니다:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I use EXPAND with a larger source array?** | Absolutely. Just change `{1,2,3}` to any constant or cell range, e.g., `EXPAND(A1:C1,10,1)`. |
| **What if I need a horizontal result?** | Swap the row/column arguments: `EXPAND({1,2,3},1,5)` will produce a 1‑row, 5‑column spread. |
| **Will this work on older Excel versions?** | `EXPAND` is available starting with Excel 365/2021. For older versions, you’d need to simulate the array with `INDEX`/`SEQUENCE`. |
| **Do I need to call `workbook.CalculateFormula()`?** | No. Aspose.Cells automatically evaluates formulas on save, so the values appear immediately. |
| **How to add more than one sheet before saving?** | Call `workbook.Worksheets.Add("SecondSheet")` and repeat the cell‑manipulation steps on the new worksheet. |

---

## Full Working Example

아래는 완전한 실행 가능한 프로그램 예시입니다. 콘솔 앱에 복사‑붙여넣기하고 출력 경로만 조정한 뒤 **F5**를 눌러 실행하세요.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Expected output in the console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

생성된 파일을 열면 **A** 열에 동일한 숫자가 채워진 것을 확인할 수 있습니다.

---

## Visual Summary

![새 워크북 예시](create-new-workbook.png "C#에서 새 워크북을 만들고 EXPAND 결과를 보여주는 스크린샷")

*이미지는 EXPAND 결과가 적용된 새 워크북을 보여줍니다.*

---

## Conclusion

이제 **create new workbook**, **add formula to cell**, **save excel workbook**을 C#으로 수행하는 방법을 알게 되었습니다. **how to use expand**를 마스터하면 수동 작업 없이 동적 배열을 생성할 수 있으며, 전체 프로세스를 통해 **create excel file programmatically**하여 다양한 자동화 시나리오에 활용할 수 있습니다.

다음 단계는? 상수 배열을 범위 참조로 바꾸어 보거나, `EXPAND` 차원을 다양하게 실험해 보세요. 여러 시트에 걸쳐 수식을 연결하거나 차트, 스타일, 피벗 테이블까지 동일한 패턴을 적용할 수 있습니다—계속 탐구해 보세요.

문제가 발생하면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되시고, 프로그래밍 Excel의 힘을 만끽하세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}