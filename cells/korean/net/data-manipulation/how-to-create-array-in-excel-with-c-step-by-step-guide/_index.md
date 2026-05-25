---
category: general
date: 2026-02-28
description: C#를 사용하여 Excel에서 배열을 만드는 방법. 숫자를 생성하고, 수식을 평가하며, Excel 워크북을 만들고, 몇 분
  안에 Excel 파일을 저장하는 방법을 배웁니다.
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: ko
og_description: C#를 사용하여 Excel에서 배열을 만드는 방법. 이 튜토리얼에서는 숫자를 생성하고, 수식을 평가하며, 워크북을 만들고
  파일을 저장하는 방법을 보여줍니다.
og_title: C#로 Excel에서 배열 만들기 – 완전 가이드
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: C#로 Excel에서 배열 만들기 – 단계별 가이드
url: /ko/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 로 Excel에서 배열 만들기 – 완전 프로그래밍 튜토리얼

Excel에서 **배열을 만들**는 방법을 C#으로 프로그래밍해서 구현해 본 적 있나요? 여러분만 그런 것이 아닙니다—개발자들은 수동으로 입력하지 않고 숫자 블록을 빠르게 생성하는 방법을 자주 찾습니다. 이 가이드에서는 **Excel 워크북을 생성**하고, **숫자를 생성하는 수식**을 삽입하고, **수식을 평가**한 뒤, **Excel 파일을 저장**하는 정확한 단계를 차근차근 살펴보겠습니다. 저장된 파일을 Excel에서 열어 결과를 확인할 수 있습니다.

우리는 Aspose.Cells 라이브러리를 사용할 것입니다. 이 라이브러리는 Excel이 설치되지 않아도 수식과 계산을 완벽히 제어할 수 있게 해줍니다. 다른 라이브러리를 선호한다면 API 호출만 교체하면 동일한 개념을 적용할 수 있습니다.

## 이 튜토리얼에서 다루는 내용

- 필요한 NuGet 패키지를 포함한 C# 프로젝트 설정  
- 새 워크북 만들기(즉, *create excel workbook* 단계)  
- `SEQUENCE`와 `WRAPCOLS`를 사용해 4 행 × 3 열 배열을 만드는 수식 작성  
- 엔진에 **수식을 평가**하도록 강제하여 배열이 실제 값으로 변환되게 하기  
- 워크북을 디스크에 저장(**save excel file**)하고 결과 확인  

튜토리얼을 마치면 다음과 같은 Excel 시트를 생성하는 실행 가능한 프로그램을 얻게 됩니다:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![How to create array in Excel – resulting sheet after running the C# code](image.png)

*(이미지 alt 텍스트에는 주요 키워드 “how to create array”가 포함되어 SEO에 도움이 됩니다.)*

---

## 사전 요구 사항

- .NET 6.0 SDK 이상(코드는 .NET Framework 4.6+에서도 동작)  
- Visual Studio 2022 또는 선호하는 편집기  
- NuGet 패키지 **Aspose.Cells**(무료 체험판 제공)  

Excel을 별도로 설치할 필요가 없습니다. Aspose.Cells가 내부에 계산 엔진을 포함하고 있기 때문입니다.

---

## 1단계: 프로젝트 설정 및 Aspose.Cells 가져오기

먼저 콘솔 앱을 만들고 라이브러리를 추가합니다:

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

이제 **Program.cs**를 열고 네임스페이스를 추가합니다:

```csharp
using Aspose.Cells;
```

*왜 중요한가*: `Aspose.Cells`를 가져오면 **create excel workbook**과 수식 작업에 필요한 `Workbook`, `Worksheet`, 계산 클래스들을 사용할 수 있습니다.

---

## 2단계: 워크북 및 대상 워크시트 만들기

새 워크북 객체가 필요합니다. 첫 번째 워크시트(`Worksheets[0]`)에 배열을 배치합니다.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*설명*: `Workbook` 클래스는 전체 Excel 파일을 나타냅니다. 기본적으로 하나의 시트를 포함하고 있어 간단한 데모에 적합합니다. 시트를 더 추가하려면 나중에 `workbook.Worksheets.Add()`를 호출하면 됩니다.

---

## 3단계: **숫자를 생성**하고 배열을 만드는 수식 작성

Excel의 동적 배열 함수(`SEQUENCE`와 `WRAPCOLS`)를 사용하면 하나의 수식으로 값 블록을 만들 수 있습니다. 다음 문자열을 셀에 할당합니다:

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*왜 동작하는가*:  
- `SEQUENCE(12,1,1,1)`은 1‑12까지의 수를 세로 목록으로 반환합니다.  
- `WRAPCOLS(...,3)`은 그 목록을 3열로 가로 채워 자동으로 다음 행으로 넘깁니다.  

Excel에서 워크북을 **수식을 평가하지 않은** 상태로 열면 `A1`에 수식 텍스트만 보입니다. 다음 단계에서 계산을 강제합니다.

---

## 4단계: **수식을 평가**하여 배열을 실제 값으로 만들기

Aspose.Cells는 쓰기 시 자동으로 수식을 재계산하지 않으므로, 계산 엔진을 명시적으로 호출합니다:

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*무슨 일이 일어나는가*: `Calculate()`는 수식이 들어 있는 모든 셀을 순회하면서 결과를 계산하고 값을 다시 씁니다. 이것이 튜토리얼의 **how to evaluate formula** 부분입니다. 이 호출 이후 셀 A1:C4에는 1‑12가 채워져, 원래 Excel의 스필과 동일한 결과가 됩니다.

---

## 5단계: **Excel 파일 저장** 및 결과 확인

마지막으로 워크북을 디스크에 저장합니다:

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`output.xlsx`를 Excel에서 열면 우리가 만든 4 × 3 배열이 보일 것입니다. Excel 365/2019 이전 버전에서는 동적 배열 함수가 인식되지 않지만, Aspose.Cells가 이미 평가된 값을 기록하므로 파일은 그대로 사용할 수 있습니다.

*팁*: 특정 포맷을 강제하려면 `SaveFormat.Xlsx`를 사용하세요. 예: `workbook.Save(outputPath, SaveFormat.Xlsx);`.

---

## 전체 작업 예제 (복사‑붙여넣기 바로 사용)

아래는 완전한 프로그램 코드입니다. **Program.cs**에 붙여넣고 `dotnet run`을 실행하면 프로젝트 폴더에 `output.xlsx`가 생성됩니다.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**예상 콘솔 출력**:

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

파일을 열면 앞서 보여드린 대로 1‑12가 정확히 배열된 것을 확인할 수 있습니다.

---

## 변형 및 엣지 케이스

### 1. 동적 배열을 지원하지 않는 구버전 Excel  
사용자가 Excel 2016 이하를 사용한다면 `SEQUENCE`와 `WRAPCOLS`가 존재하지 않습니다. 이 경우 C#에서 직접 숫자를 생성해 쓰는 방법이 있습니다:

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

이 수동 루프는 동일한 결과를 만들지만 코드가 더 길어집니다. **숫자를 생성하는 방법**이라는 개념은 동일합니다.

### 2. 배열 크기 변경하기  
5 × 5 그리드, 즉 1‑25 숫자를 원한다면 `SEQUENCE` 인수와 `WRAPCOLS` 열 개수를 조정하면 됩니다:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. 재사용을 위한 이름 정의 사용  
스필된 범위에 이름을 지정해 다른 수식에서 재사용할 수 있습니다:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

이제 다른 시트에서도 `MyArray`를 직접 참조할 수 있습니다.

---

## 흔히 겪는 문제와 해결 방법

| 문제 | 발생 원인 | 해결 방법 |
|---|---|---|
| **수식이 스필되지 않음** | `Calculate()`를 호출하지 않았거나 수식 설정 전에 호출함 | 수식 할당 **후** 반드시 `workbook.Calculate()`를 호출 |
| **파일은 저장됐지만 내용이 비어 있음** | 실수로 `SaveFormat.Csv` 사용 | `SaveFormat.Xlsx`를 사용하거나 포맷 지정 없이 저장 |
| **동적 배열** |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}