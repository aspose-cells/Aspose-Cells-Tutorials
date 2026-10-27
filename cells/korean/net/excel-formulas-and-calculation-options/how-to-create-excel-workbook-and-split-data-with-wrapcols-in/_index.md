---
category: general
date: 2026-10-10
description: C#에서 Excel 워크북을 만들고 WRAPCOLS 함수를 사용하여 배열 데이터를 열로 나눕니다. 실행 가능한 코드와 함께
  완전한 단계별 가이드를 따라보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: ko
lastmod: 2026-10-10
og_description: C#에서 Excel 워크북을 생성하고 WRAPCOLS 함수를 적용하여 배열 데이터를 열로 분할합니다. 이 가이드는 전체
  코드를 보여주고 각 단계를 설명합니다.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: C#에서 Excel 워크북을 만들고 WRAPCOLS로 데이터를 분할하기
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#에서 Excel 워크북을 만들고 WRAPCOLS로 데이터를 분할하는 방법
url: /ko/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 WRAPCOLS를 사용하여 Excel 워크북을 만들고 데이터를 분할하는 방법

프로그래밍으로 **Excel 워크북을 만들** 필요가 있다면, 이 가이드는 정확히 어떻게 수행하는지와 `WRAPCOLS` 함수를 사용하여 열에 **배열 데이터를 분할**하는 방법을 보여줍니다. 완전하고 실행 가능한 예제를 제공하여 데이터가 세 열에 배분된 `.xlsx` 파일을 생성합니다.

이 튜토리얼은 필요한 모든 내용을 다룹니다: 필수 NuGet 패키지, 각 코드 라인, `WRAPCOLS` 수식이 동작하는 이유, 그리고 다양한 배열 크기나 열 개수에 맞게 솔루션을 적용하는 방법. 끝까지 진행하면 Excel 파일을 생성하는 모든 C# 프로젝트에 **use wrapcols function** 기술을 삽입할 수 있게 됩니다.

## 사전 요구 사항

시작하기 전에 다음이 설치되어 있는지 확인하세요:

* .NET 6.0 SDK 이상이 설치되어 있음  
* C# IDE (Visual Studio, VS Code, Rider 등)  
* **Aspose.Cells for .NET** NuGet 패키지 – 예제에서 사용되는 `Workbook` 클래스를 제공하는 라이브러리  

Office 설치가 필요하지 않습니다; Aspose.Cells는 `.xlsx` 파일을 직접 작성합니다.

## Step 1 – Excel 워크북 만들기

첫 번째 작업은 새 워크북 객체를 인스턴스화하고 첫 번째 워크시트에 대한 참조를 얻는 것입니다. 이 단계는 이후 모든 조작의 기반이 됩니다.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook`은 전체 파일을 나타내고, `Worksheet`는 단일 시트를 나타냅니다. 워크북을 메모리에서 생성하면 명시적으로 저장할 때까지 디스크 I/O를 피할 수 있습니다.

## Step 2 – WRAPCOLS를 적용하여 배열 열을 분할하기

이제 `WRAPCOLS`를 사용하는 수식을 셀 **A1**에 입력합니다. 이 함수는 두 개의 인수를 받습니다: 원본 배열과 배열을 감싸서 배치할 열 개수.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**왜 동작하는가:** `WRAPCOLS`는 평면 배열 `{1,2,3,4,5,6}`을 받아 워크시트를 행‑단위로 채우며, 행당 세 개의 열을 생성합니다. 첫 번째 인수는 任意의 Excel 배열 리터럴, 이름이 지정된 범위, 또는 동적 배열 수식이 될 수 있습니다. 두 번째 인수(`3`)는 Excel에 다음 행으로 이동하기 전에 생성할 열 수를 알려줍니다.

### 다양한 데이터 유형으로 함수 사용하기

`WRAPCOLS` 함수는 숫자에만 제한되지 않습니다. 텍스트 값, 날짜, 혹은 혼합 유형도 분할할 수 있습니다:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

원본 배열에 문자열이 포함되면 Excel은 결과를 자동으로 텍스트 셀로 처리합니다. 이러한 유연성 덕분에 **excel formula split data**를 보고서, 대시보드, 또는 데이터 마이그레이션 작업에 활용할 수 있습니다.

## Step 3 – 수식을 계산하여 워크시트에 값 채우기

수식은 워크북에 평가를 요청하기 전까지 문자열로 저장됩니다. `CalculateFormula`를 호출하면 평가가 강제되고 결과가 셀에 기록됩니다.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

이 호출이 없으면 저장된 파일에는 계산된 값이 아니라 수식 텍스트만 포함됩니다. 이 메서드는 전체 워크북에 적용되므로 다른 위치에 추가 수식을 배치해도 한 번의 호출로 모두 해결됩니다.

## Step 4 – 워크북을 저장하여 결과 확인

마지막으로 워크북을 디스크에 기록합니다. 쓰기 권한이 있는 폴더를 선택하고 파일에 명확한 이름을 지정하세요.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

`output.xlsx`를 Excel(또는 호환 뷰어)에서 열면 다음과 같이 표시됩니다:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

혼합 유형 예제를 사용했다면, 3‑4행에 텍스트와 숫자가 각각 들어가게 됩니다.

## 고급 변형 및 엣지 케이스 처리

### 런타임 시 가변 열 개수

필요한 열 개수는 종종 사용자 입력에 따라 달라집니다. 수식 문자열을 동적으로 구성할 수 있습니다:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### 대형 배열 및 성능

`WRAPCOLS`는 수천 개 요소를 처리할 수 있지만, 단일 셀에서 매우 큰 배열을 평가하면 계산 시간이 늘어날 수 있습니다. 속도가 느려지는 것을 발견하면:

* 원본 배열을 더 작은 청크로 나누어 각각 별도의 시작 셀에 기록합니다.  
* `WorkbookSettings`를 사용하여 다중 스레드 계산을 활성화합니다:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### 빈 셀 처리

원본 배열에 빈 문자열(`""`)이나 `NULL` 값이 포함되어 있으면 `WRAPCOLS`는 빈 셀을 삽입하여 열 레이아웃을 유지합니다. 이 동작은 이후 데이터 입력을 위한 자리표시자 열이 필요할 때 유용합니다.

### 리터럴 대신 이름이 지정된 범위 사용

유지 보수를 위해 원본 데이터를 보유하는 이름이 지정된 범위를 정의하고 이를 참조합니다:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

이제 수식은 워크시트 자체에서 데이터를 읽어와, 동적 보고 시나리오에서 **how to use wrapcols**를 가능하게 합니다.

## 일반적인 함정 및 전문가 팁

* **두 번째 인수를 생략하지 마세요.** 열 개수가 없는 `WRAPCOLS(array)`는 단일 열을 반환하므로 데이터를 분할하는 목적에 맞지 않습니다.  
* **배열 차원을 혼합하지 마세요.** 원본 배열은 1차원이어야 하며, 2차원 배열(예: `{ {1,2},{3,4} }`)을 제공하면 `#VALUE!` 오류가 발생합니다.  
* **계산 후 저장하세요.** `CalculateFormula` 전에 `wb.Save`를 호출하면 파일에 수식 텍스트만 포함됩니다.  
* **파일 권한을 확인하세요.** 제한된 환경(예: ASP.NET)에서 실행할 때 프로세스 ID가 대상 폴더에 쓸 수 있는지 확인합니다.  

## 전체 작동 예제

아래는 복사·붙여넣기·실행할 수 있는 전체 프로그램입니다. 모든 import, 오류 처리 및 주석이 포함되어 있습니다.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

프로그램을 실행하면 `WRAPCOLS` 함수를 사용한 **excel formula split data**를 보여주는 세 개의 구역이 포함된 `output.xlsx`가 생성됩니다.

## 결론

이제 C#에서 **Excel 워크북** 파일을 만드는 방법과 **use wrapcols function**을 사용해 **배열 열을 효율적으로 분할**하는 방법을 알게 되었습니다. 주요 단계인 `Workbook` 인스턴스화, `WRAPCOLS` 수식 삽입, 계산, 저장은 열에 데이터를 배분해야 하는 모든 자동화 작업에 재사용 가능한 패턴을 제공합니다.

여기서부터는 다음을 할 수 있습니다:

* `WRAPCOLS`를 `FILTER` 또는 `SORT`와 같은 다른 동적 배열 함수와 결합합니다.  
* 데이터베이스에서 대량 데이터를 내보내고 Excel이 레이아웃을 자동으로 처리하도록 합니다.  
* UI 컨트롤을 통해 열 개수를 선택하는 사용자 주도 보고서를 구축합니다.

다양한 배열 소스, 열 개수 및 추가 수식을 실험하여 이 기반을 확장해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 전체 작동 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}