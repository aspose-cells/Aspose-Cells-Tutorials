---
category: general
date: 2026-02-09
description: C#로 Excel에서 배열을 만드는 방법을 몇 분 안에 설명 – 순번 생성, COT 사용, 그리고 워크북을 XLSX로 저장하는
  방법을 배워보세요.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: ko
og_description: C#를 사용하여 Excel에서 배열을 만드는 방법을 단계별로 다루며, 시퀀스 번호 생성, COT 사용 및 워크북을 XLSX
  형식으로 저장하는 방법을 포함합니다.
og_title: C#로 Excel에서 배열 만들기 – 빠른 가이드
tags:
- C#
- Excel
- Aspose.Cells
title: C#로 Excel에서 배열 만들기 – 단계별 가이드
url: /ko/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 C#으로 배열 만들기 – 단계별 가이드

문서들을 뒤져보는 데 시간을 들이지 않고 **배열 만들기**를 C#으로 Excel에서 구현하는 방법이 궁금하셨나요? 혼자가 아닙니다. 많은 개발자들이 동적 스필 범위가 필요하거나, 빠른 삼각함수 값을 구하거나, 단순히 디스크에 깔끔한 XLSX 파일을 저장해야 할 때 벽에 부딪히곤 합니다. 이 튜토리얼에서는 그 문제를 바로 해결합니다—확장되는 배열 수식을 쓰고, 코탄젠트 계산을 삽입하며, 모든 것을 XLSX 파일로 저장하는 작은 워크북을 만드는 방법을 보여드립니다.

추가 트릭도 몇 가지 소개합니다: 순번 생성, `COT` 함수 마스터하기, 파일이 원하는 위치에 저장되도록 보장하기 등. 끝까지 읽으면 어떤 .NET 프로젝트에도 끼워넣을 수 있는 재사용 가능한 스니펫을 얻게 됩니다. 불필요한 설명은 없고, 바로 동작하는 코드만 제공합니다.

> **Pro tip:** 이 예제는 널리 사용되는 **Aspose.Cells** 라이브러리를 사용하지만, 개념은 다른 Excel 자동화 패키지(EPPlus, ClosedXML)에도 약간만 수정하면 적용할 수 있습니다.

---

## 필요한 사항

- **.NET 6** 이상 (코드는 .NET Framework 4.7+에서도 컴파일됩니다)  
- **Aspose.Cells for .NET** – NuGet에서 가져올 수 있습니다 (`Install-Package Aspose.Cells`)  
- 텍스트 편집기 또는 IDE (Visual Studio, Rider, VS Code…)  
- 출력 파일이 저장될 폴더에 대한 쓰기 권한  

그게 전부—추가 설정도 없고, COM 인터옵도 없으며, 깔끔한 관리 어셈블리만 있으면 됩니다.

---

## 1단계: Excel에서 배열 만들기 – 워크북 초기화

Excel 시트에서 **배열 만들기**를 시작하려면 먼저 워크북 객체를 생성해야 합니다. 워크북은 빈 캔버스와 같으며, 워크시트는 수식을 그릴 공간입니다.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

왜 매개변수 없이 `Workbook()`을 사용할까요? 기본 시트가 포함된 메모리 내 워크북을 바로 얻을 수 있어 빠른 프로그래밍 작업에 최적입니다. 기존 파일을 열어야 하면 파일 경로를 생성자에 전달하면 됩니다.

---

## 2단계: EXPAND와 SEQUENCE를 사용해 순번 생성

이제 시트가 준비됐으니 퍼즐의 **순번 생성** 부분을 해결해 보겠습니다. Excel의 새로운 동적 배열 함수(`SEQUENCE`, `EXPAND`)를 이용하면 3행 세로 리스트를 만들고 자동으로 3 × 5 범위에 스필할 수 있습니다.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**무슨 일이 일어나고 있나요?**  
- `SEQUENCE(3,1,1,1)` → 세로 배열 `{1;2;3}`을 생성합니다.  
- `EXPAND(...,5,1)` → 해당 3행 열을 5열로 확장하고, 남은 셀은 빈칸으로 채웁니다.  

결과 `output.xlsx`를 열면 **A1**부터 시작하는 3 × 5 블록이 보이며, 첫 번째 열에 1, 2, 3이 들어 있고 나머지 네 열은 비어 있습니다. 이 기술은 **배열 만들기**‑스타일 스필 범위를 수동으로 셀을 채우지 않고 구현하는 핵심 방법입니다.

---

## 3단계: COT 사용법 – 삼각함수 공식 추가

또한 Excel 수식 안에서 **cot 사용법**에 대해 궁금하다면, `COT` 함수는 라디안으로 표현된 각도의 코탄젠트를 손쉽게 구할 수 있는 방법입니다. `cot(π/4)`를 계산해 보겠습니다. 결과는 **1**이 되어야 합니다.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

`PI()`를 사용해 180°의 라디안 값을 얻고, 이를 4로 나누어 45°를 만들었습니다. Excel이 무거운 연산을 처리하고, 워크북을 열면 셀 **B1**에 `1`이 표시됩니다. 이는 별도의 수학 라이브러리를 도입하지 않고도 **cot 사용법**을 활용해 빠른 엔지니어링·재무 계산을 할 수 있음을 보여줍니다.

---

## 4단계: 워크북을 XLSX로 저장 – 파일 영구 저장

배열을 만들고 수식을 삽입하는 재미가 파일을 디스크에 쓰지 않으면 무의미합니다. 아래는 Aspose.Cells를 사용해 **워크북을 XLSX로 저장**하는 가장 간단한 방법입니다.

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

왜 `SaveFormat.Xlsx`를 지정할까요? 최신 OpenXML 형식을 보장해 Excel, LibreOffice, Google Sheets 등 어디서든 읽을 수 있습니다. 오래된 `.xls` 파일이 필요하면 열거형만 바꾸면 됩니다.

---

## 전체 작업 예제 (모든 단계 결합)

아래는 완전한 실행 가능한 프로그램입니다. 콘솔 프로젝트에 복사·붙여넣기하고, Aspose.Cells NuGet 패키지를 복원한 뒤 **F5**를 눌러 실행하세요.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**예상 결과**는 `output.xlsx`를 열었을 때 다음과 같습니다:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- 열 A는 `SEQUENCE`로 생성된 1‑3 번호를 보여줍니다.  
- 열 B는 `COT` 수식에서 나온 **1** 값을 포함합니다.  
- 열 C‑E는 비어 있어 `EXPAND`의 패딩 효과를 나타냅니다.

---

## 일반적인 질문 및 엣지 케이스

### 행이나 열이 더 필요하면 어떻게 하나요?

`SEQUENCE`와 `EXPAND` 인자를 조정하면 됩니다.  
- `SEQUENCE(10,2,5,2)`는 5부터 시작해 2씩 증가하는 10행 × 2열 행렬을 반환합니다.  
- `EXPAND(...,10,5)`는 결과를 10열 × 5행으로 패딩합니다.

### 구버전 Excel에서도 작동하나요?

동적 배열 함수(`SEQUENCE`, `EXPAND`)는 Excel 365 또는 2019 이상이 필요합니다. 레거시 파일의 경우 고전 수식을 사용하거나 `Cells[row, col].PutValue(value)`로 직접 값을 기록하면 됩니다.

### R1C1 스타일로 수식을 작성할 수 있나요?

물론 가능합니다. `A1`을 `Cells[0, 0]`으로 교체하고 `FormulaR1C1` 속성을 사용하세요:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### 문화별 소수 구분자에 대해서는?

Aspose.Cells는 워크북의 로케일을 따릅니다. 특정 문화가 필요하면 수식 작성 전에 `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");`를 설정하세요.

---

## 시각적 요약

![C#을 사용하여 Excel에서 배열 만들기](/images/how-to-create-array-excel-csharp.png "C#을 사용하여 Excel에서 배열 만들기")

*스크린샷은 최종 스필 범위와 코탄젠트 결과를 보여줍니다.*

---

## 결론

이제 **Excel에서 C#으로 배열 만들기**, 순번 생성, `COT` 함수 활용, 그리고 **워크북을 XLSX로 저장**까지 한 번에 구현하는 방법을 알게 되었습니다. 핵심 포인트는:

1. `Workbook` 및 `Worksheet` 객체를 사용해 Excel 자동화를 시작합니다.  
2. 동적 배열 함수(`SEQUENCE`, `EXPAND`)를 활용해 유연한 스필 범위를 만듭니다.  
3. 별도 라이브러리 없이 `COT` 같은 삼각함수를 삽입해 빠른 수학 계산을 수행합니다.  
4. `SaveFormat.Xlsx`로 결과를 저장해 모든 환경에서 읽을 수 있는 파일을 생성합니다.

다음 단계가 준비되셨나요? `COT(PI()/4)`를 다른 각도로 바꿔 보세요.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}