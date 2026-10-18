---
category: general
date: 2026-05-23
description: C#에서 엑셀 워크북을 만들고 동적 배열 수식을 위해 EXPAND 함수를 사용하는 방법을 배웁니다. 엑셀 파일을 작성하고 샘플
  데이터를 추가하는 단계별 튜토리얼.
draft: false
keywords:
- create excel workbook
- how to use expand
- dynamic array formula
- write excel file
- add sample data
language: ko
og_description: C#에서 엑셀 워크북을 만들고 동적 배열 수식을 위한 EXPAND 사용법을 마스터하세요. 엑셀 파일 작성, 샘플 데이터
  추가 및 스프레드시트 자동화를 배워보세요.
og_title: C#에서 Excel 워크북 만들기 – EXPAND 및 동적 배열 가이드
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to use expand for dynamic
    array formulas. Step-by-step tutorial to write excel file and add sample data.
  headline: Create Excel Workbook with C# – Complete Guide to Using EXPAND
  type: TechArticle
- description: Create excel workbook in C# and learn how to use expand for dynamic
    array formulas. Step-by-step tutorial to write excel file and add sample data.
  name: Create Excel Workbook with C# – Complete Guide to Using EXPAND
  steps:
  - name: '**Dynamic chart generation** – link the spilled range to a chart object
      for live dashboards.'
    text: '**Dynamic chart generation** – link the spilled range to a chart object
      for live dashboards.'
  - name: '**Conditional formatting** – apply rules to the expanded area to highlight
      outliers.'
    text: '**Conditional formatting** – apply rules to the expanded area to highlight
      outliers.'
  - name: '**Export to CSV** – Aspose.Cells can also `Save(..., SaveFormat.Csv)` if
      you need a plain‑text version.'
    text: '**Export to CSV** – Aspose.Cells can also `Save(..., SaveFormat.Csv)` if
      you need a plain‑text version.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C#로 Excel 워크북 만들기 – EXPAND 사용 완전 가이드
url: /ko/net/excel-workbook/create-excel-workbook-with-c-complete-guide-to-using-expand/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#로 Excel 워크북 만들기 – EXPAND 사용 완전 가이드

Ever wondered how to **create excel workbook** from scratch using C#? In this tutorial we'll show you exactly that, plus **how to use expand** to build a **dynamic array formula**. We'll also cover **write excel file** steps and **add sample data** so you can see the result instantly.  

C#를 사용해 처음부터 **create excel workbook** 하는 방법이 궁금하셨나요? 이 튜토리얼에서는 바로 그 방법과 **how to use expand** 로 **dynamic array formula** 를 만드는 방법을 보여드립니다. 또한 **write excel file** 단계와 **add sample data** 를 다루어 즉시 결과를 확인할 수 있습니다.  

If you’ve ever stared at a spreadsheet and thought, “There has to be a programmatic way to grow this range,” you’re in the right place. By the end, you’ll have a runnable console app that expands a range, fills it with values, and saves the file—all without opening Excel manually.

스프레드시트를 바라보며 “이 범위를 프로그래밍적으로 확장할 방법이 있어야 해” 라고 생각해 본 적이 있다면, 여기가 바로 맞는 곳입니다. 끝까지 읽으면, 범위를 확장하고 값을 채우며 파일을 저장하는 실행 가능한 콘솔 앱을 얻을 수 있습니다—Excel을 직접 열 필요 없이.

## 필요 사항

- .NET 6 (또는 최신 .NET 버전) – 코드는 .NET Framework에서도 작동합니다.  
- **Aspose.Cells for .NET** NuGet 패키지 – `Workbook`, `Worksheet`, 그리고 `EXPAND` 지원을 제공합니다.  
- 선호하는 IDE (Visual Studio, Rider, 또는 VS Code).  

추가적인 Excel 설치가 필요하지 않습니다; Aspose.Cells가 모든 작업을 메모리에서 처리합니다.

## Excel 워크북 만들기 – 프로젝트 설정

시작하려면 새 콘솔 프로젝트를 만들고 Aspose.Cells 라이브러리를 가져옵니다:

```bash
dotnet new console -n ExcelExpandDemo
cd ExcelExpandDemo
dotnet add package Aspose.Cells
```

이제 `Program.cs`를 엽니다. 첫 번째로 **create excel workbook** 하고 기본 워크시트를 가져옵니다:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();               // <-- create excel workbook
        Worksheet ws = wb.Worksheets[0];

        // (Optional) Add sample data so we have something to expand
        ws.Cells["A1"].PutValue(10);
        ws.Cells["A2"].PutValue(20);
        ws.Cells["A3"].PutValue(30);
```

> **왜 중요한가:** `Workbook`은 Excel 파일을 나타내는 최상위 객체입니다. 이를 인스턴스화하는 것이 **create excel workbook** 의 첫 단계이며, 이것 없이는 워크시트, 수식 등을 추가할 수 없습니다.  
> **프로 팁:** 이미 템플릿 파일이 있다면 `new Workbook()`을 `new Workbook("template.xlsx")`로 교체하면 기존 내용 위에 **add sample data** 를 계속 추가할 수 있습니다.

## 동적 배열 수식에 EXPAND 사용 방법

`EXPAND` 함수에 진정한 마법이 있습니다. 이 함수는 소스 범위를 받아 지정한 행과 열 수에 따라 더 큰 배열을 반환합니다. 프로그래밍으로 제어할 수 있는 Excel의 내장 “fill down”이라고 생각하면 됩니다.

```csharp
        // Step 2: Apply the EXPAND formula to cell A1
        // Syntax: =EXPAND(source, rows, columns)
        ws.Cells["A1"].Formula = "=EXPAND(A1:A3,5,1)";

        // Step 3: Force calculation so the expanded values appear
        wb.CalculateFormula();
```

> **무슨 일이 일어나고 있나요?**  
> * `A1:A3`은 이미 세 개의 숫자를 포함하고 있는 소스 범위입니다.  
> * `5`는 `EXPAND`가 **5행**을 생성하도록 지정합니다; 추가된 두 행은 기본적으로 마지막 값(30)을 반복합니다.  
> * `1`은 열 개수를 **1**로 유지하므로 열 A에 머무릅니다.  
> **예외 상황:** 소스 범위가 요청된 크기보다 크면 Excel이 초과 부분을 잘라냅니다. 이는 스필 범위를 제한하고 싶을 때 유용합니다.  
> **대안:** 행이나 열에 `0`을 전달하면 Excel이 자동으로 결정합니다. 예를 들어 `=EXPAND(A1:A3,0,2)`는 원래 행 수를 유지하면서 두 열로 스필됩니다.

## 워크시트에 샘플 데이터 추가

이미 몇 개의 숫자를 넣었지만, 더 현실적인 시나리오를 보여드리겠습니다: 리스트에서 데이터를 가져와 확장하는 예시입니다.

```csharp
        // Imagine we fetched these from a database
        int[] sales = { 150, 275, 320, 410 };
        for (int i = 0; i < sales.Length; i++)
        {
            ws.Cells[i, 1].PutValue(sales[i]); // Column B gets the raw sales numbers
        }

        // Now expand the sales column to a summary table with 8 rows
        ws.Cells["B1"].Formula = "=EXPAND(B1:B4,8,1)";
        wb.CalculateFormula();
```

> **왜 추가하나요?** 추가 데이터를 넣으면 소스가 커질 때 **dynamic array formula** 가 어떻게 동작하는지 확인할 수 있습니다. 또한 실제 ETL 파이프라인에서 반복할 **add sample data** 패턴을 보여줍니다.

## Excel 파일 쓰기 및 출력 확인

워크북이 준비되면, 디스크에 **write excel file** 합니다. Aspose.Cells는 다양한 형식을 지원하지만 여기서는 클래식 `.xlsx` 형식을 사용합니다.

```csharp
        // Step 4: Save the workbook – this writes the Excel file
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "ExpandedWorkbook.xlsx");
        wb.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **예상 결과:**  
> - 셀 **A1:A5**는 `10, 20, 30, 30, 30`을 포함합니다.  
> - 셀 **B1:B8**는 `150, 275, 320, 410, 410, 410, 410, 410`을 포함합니다.  

Excel에서 파일을 열면 수식이 지정한 대로 스필된 범위를 정확히 확인할 수 있습니다. 수동으로 드래그할 필요가 없습니다.

![Excel 워크북에서 확장된 범위의 스크린샷](/images/expanded-range.png "create excel workbook 예시")

*이미지 대체 텍스트:* **create excel workbook** – EXPAND 사용 후 확장된 범위를 보여주는 스크린샷.

## 흔히 발생하는 문제와 팁

- **Formula recalculation:** 수식 설정 후 소스 셀을 수정하면 `wb.CalculateFormula()`를 다시 호출해야 합니다. 그렇지 않으면 스필 영역이 오래된 상태로 남습니다.
- **Zero‑based vs A1 notation:** Aspose.Cells는 `ws.Cells[0,0]` 또는 `ws.Cells["A1"]` 중 하나를 사용할 수 있습니다. 혼용하면 혼란스러우니 한 가지 스타일을 선택해 일관되게 사용하세요.
- **Performance:** 큰 시트의 경우 전체 워크북에 `CalculateFormula`를 호출하면 비용이 많이 들 수 있습니다. 범위를 제한하려면 `ws.CalculateFormula()`를 사용하세요.
- **Version compatibility:** `EXPAND`는 Excel 365에서 도입되었습니다. 이전 Excel 버전에서는 `#NAME?` 오류가 표시됩니다. 하위 호환성이 필요하면 `OFFSET`이나 수동 루프 사용을 고려하세요.

## 다음 단계 – 솔루션 확장

이제 **create excel workbook**, **how to use expand**, 그리고 **write excel file** 방법을 알았으니 다음을 탐색할 수 있습니다:

1. **Dynamic chart generation** – 스필된 범위를 차트 객체에 연결하여 실시간 대시보드를 만들 수 있습니다.  
2. **Conditional formatting** – 확장된 영역에 규칙을 적용해 이상치를 강조합니다.  
3. **Export to CSV** – 필요에 따라 Aspose.Cells는 `Save(..., SaveFormat.Csv)` 로 CSV 형식도 저장할 수 있습니다.  

이들 각각은 방금 설정한 **dynamic array formula** 기반 위에 구축됩니다.

---

## 결론

이 가이드에서는 C#로 **create excel workbook** 하는 전체 과정을 살펴보고, **how to use expand** 로 **dynamic array formula** 를 구현하며, **add sample data** 를 추가하고 마지막으로 **write excel file** 로 디스크에 저장하는 방법을 시연했습니다. 코드는 독립적이며 `dotnet run` 한 번으로 실행되고 즉시 열어볼 수 있는 검증 가능한 스프레드시트를 생성합니다.

행/열 수를 자유롭게 조정하고, 샘플 데이터 소스를 교체하거나 여러 `EXPAND` 호출을 연결해 보세요. 프로그래밍으로 Excel을 생성하고 최신 배열 함수를 결합하면 가능성은 무한합니다.

질문이 있거나 멋진 사용 사례를 공유하고 싶다면 아래에 댓글을 남겨 주세요. 즐거운 코딩 되세요!

## 관련 튜토리얼

- [Excel 자동화: Aspose.Cells for .NET를 사용해 워크북 만들기 및 ListBox 추가](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Aspose.Cells for .NET를 사용해 Excel에서 체크박스 만들기 | 데이터 검증 튜토리얼](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Aspose.Cells .NET를 사용해 Excel에서 워크북 범위 지정된 이름 범위 만들기](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}