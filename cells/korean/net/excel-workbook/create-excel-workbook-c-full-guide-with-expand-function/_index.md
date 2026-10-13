---
category: general
date: 2026-06-08
description: C#로 Excel 워크북을 단계별로 만들고, 동적 범위를 위한 Excel의 expand 함수 사용법을 배워보세요. .NET
  개발자에게 최적입니다.
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: ko
og_description: 명확한 예제와 함께 C#로 Excel 워크북을 만들고, Excel에서 Expand 함수를 사용해 동적 배열을 생성하는
  방법을 알아보세요.
og_title: Excel 워크북 만들기 C# – 완전 프로그래밍 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: C#로 Excel 워크북 만들기 – 확장 기능을 포함한 전체 가이드
url: /ko/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크북 C# 만들기 – 확장 함수 포함 전체 가이드

Excel 워크북을 **C#으로 만들** 때 COM 인터롭이나 XML을 직접 다루는 것이 번거롭다고 생각한 적 있나요? 여러분만 그런 것이 아닙니다. 많은 .NET 프로젝트에서 스프레드시트를 생성하고, 수식을 채워 넣은 뒤 비전문가에게 전달해야 할 때가 있습니다. 좋은 소식은? **Aspose.Cells** 같은 최신 라이브러리를 사용하면 전체 과정이 식은 죽 먹기라는 겁니다.

이 튜토리얼에서는 **Excel 워크북 C#을 만들고**, 몇 가지 수식을 삽입하며—특히 **Excel에서 expand 함수를 사용하는 방법**—파일을 저장해 바로 Excel에서 열 수 있는 완전 실행 가능한 예제를 단계별로 살펴봅니다. 끝까지 읽으면 *무엇을* 입력해야 하는지는 물론 *왜* 각 라인이 중요한지도 이해하게 되고, 어떤 프로젝트에도 복사해 넣을 수 있는 템플릿을 얻게 됩니다.

## 사전 준비

시작하기 전에 다음이 준비되어 있는지 확인하세요.

- .NET 6 SDK(또는 최신 .NET 버전) 설치
- NuGet을 지원하는 IDE(Visual Studio, VS Code, Rider 등)
- **Aspose.Cells** NuGet 패키지 – 코드에서 사용하는 `Workbook` 및 `Worksheet` 클래스를 제공합니다.
- C# 기본 지식; Excel 전용 경험은 필요 없습니다.

다 준비됐나요? 좋습니다—시작해 봅시다.

## 1단계: 프로젝트 생성 및 Aspose.Cells 추가

먼저 콘솔 앱을 만들고 라이브러리를 가져옵니다.

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** 기업 네트워크에 있다면 NuGet 프록시를 설정해야 할 수도 있습니다. Aspose.Cells 패키지는 가볍기 때문에 설치가 몇 초 안에 끝납니다.

이제 `Program.cs`를 엽니다. 기본 `Main` 메서드가 보일 텐데, 아래 스켈레톤으로 교체하세요.

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

`using Aspose.Cells;` 문은 스프레드시트 클래스를 현재 범위로 가져옵니다. 이를 빼면 컴파일러가 `Workbook`을 알 수 없다고 오류를 내므로, 나중에 문제를 피할 수 있습니다.

## 2단계: Excel 워크북 C# 만들고 첫 번째 워크시트에 접근하기

프로젝트가 준비되었으니 이제 **Excel 워크북 C#을 만들** 차례입니다. `Workbook` 생성자는 비어 있는 새 워크북을 반환하고, `Worksheets[0]` 인덱스는 기본 시트(이름은 “Sheet1”)를 반환합니다.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

왜 첫 번째 워크시트를 명시적으로 가져오는 걸까요? 많은 하위 API(예: 수식 설정)는 `Workbook`이 아니라 `Worksheet` 객체를 요구하기 때문입니다. 또한 코드를 읽는 사람에게도 명확해집니다.

## 3단계: Excel에서 Expand Function을 사용해 동적 범위 채우기

이제 쇼의 주인공, **Excel에서 expand 함수를 사용**합니다. `EXPAND` 함수(Excel 365 이상에서 사용 가능)는 원본 배열을 원하는 크기로 확장합니다. 예제에서는 `SEQUENCE(3)`으로 만든 3행 세로 배열을 5 × 5 블록으로 확장합니다.

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

무슨 일이 일어나나요?

1. `SEQUENCE(3)`은 세로 배열 `{1;2;3}`을 생성합니다.  
2. `EXPAND(...,5,5)`는 해당 배열을 5행 5열로 늘리라고 Excel에 지시합니다.  
3. 결과는 5 × 5 그리드이며, 처음 세 행은 1‑3이 열 전체에 반복되고, 나머지 두 행은 빈 셀입니다.

수식을 문자열 형태로 기록하기 때문에 Excel이 파일을 열 때 수식을 **실행**합니다. 즉, 워크북은 가볍게 유지되고, 원본 배열이 바뀌면 자동으로 결과가 업데이트됩니다.

> **Edge case:** 오래된 Excel 버전에서 `EXPAND`를 지원하지 않으면 셀에 `#NAME?`가 표시됩니다. 이를 방지하려면 `IFERROR`로 감싸면 되지만, 최신 환경에서는 그대로 사용해도 안전합니다.

## 4단계: 부가적으로 코탄젠트 수식 추가하기

수학 표현식을 추가하는 간단한 예제로 코탄젠트 수식을 넣어 보겠습니다. π/4의 코탄젠트는 정확히 `1`입니다.

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Excel의 `COT` 함수는 `SIN`이나 `COS`만큼 흔하지 않지만, 삼각함수 작업에 유용합니다. 워크북을 열면 **B1** 셀에 `1`이 표시됩니다.

## 5단계: 워크북 저장 및 결과 확인

아무리 멋진 작업이라도 파일을 저장하지 않으면 의미가 없습니다. `Save` 메서드는 메모리상의 워크북을 디스크에 기록합니다. 쓰기 권한이 있는 폴더를 선택하고 친절한 파일명을 지정하세요.

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

프로그램 실행:

```bash
dotnet run
```

콘솔에 저장 확인 메시지가 표시될 것입니다. `output.xlsx`를 Excel에서 열면 다음을 확인할 수 있습니다.

- **A1:E5** 셀에 확장된 시퀀스가 채워짐(첫 세 행은 1‑3이 반복, 4‑5행은 빈 셀)  
- **B1** 셀에 코탄젠트 수식 결과 `1` 표시

이것이 전체 흐름입니다: **excel workbook c# 만들기**, 수식 삽입, 사용 가능한 스프레드시트 생성.

![생성된 Excel 워크북의 확장된 배열과 코탄젠트 결과를 보여주는 스크린샷](/images/create-excel-workbook-csharp.png "excel 워크북 c# 예제")

*이미지 대체 텍스트: excel 워크북 c# – 채워진 스프레드시트 화면.*

## 6단계: 선택 사항 – 자동 열 너비 맞춤으로 깔끔하게 만들기

파일을 최종 사용자에게 배포한다면 자동 열 너비 맞춤을 적용해 보세요.

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

이 코드는 데이터가 들어 있는 모든 열을 순회하면서 가장 긴 내용에 맞게 너비를 조정합니다. 작은 터치지만, 숫자가 기본 열 너비보다 넓을 때 나타나는 “…###” 현상을 방지합니다.

## 7단계: 마무리 및 다음 단계

축하합니다! 이제 **excel workbook c# 만들기**와 **excel에서 expand 함수를 사용**하여 동적 배열을 생성하는 방법을 마스터했습니다. 코드는 의도적으로 최소화했으니 어떤 프로젝트에도 복사‑붙여넣기 할 수 있습니다. 개념은 다음과 같이 확장됩니다.

- **동적 데이터 소스:** `SEQUENCE(3)`을 다른 범위나 명명된 테이블로 교체  
- **조건부 서식:** `ws.Cells["A1:E5"].Style`을 사용해 값에 따라 색상 적용  
- **차트 및 그래픽:** Aspose.Cells는 차트, 이미지, 피벗 테이블까지 삽입 가능

자유롭게 실험해 보세요—`EXPAND` 차원을 바꾸거나 `FILTER`, `SORT`를 시도하고, 여러 수식을 체인처럼 연결해 보세요. 라이브러리가 OpenXML을 직접 다루지 않아도 모든 작업을 처리해 줍니다.

---

### 자주 묻는 질문

**Q: .NET Framework 4.8에서도 작동하나요?**  
A: 물론입니다. Aspose.Cells는 .NET Standard 2.0을 타깃으로 하며, .NET Core와 클래식 Framework 모두와 호환됩니다.

**Q: 시트를 보호하려면 어떻게 해야 하나요?**  
A: 저장하기 전에 `ws.Protect(ProtectionType.All, "yourPassword");`를 호출하면 됩니다.

**Q: 워크북을 `MemoryStream`에 직접 쓸 수 있나요?**  
A: 네. 웹 API에서 파일을 다운로드 형태로 반환할 때 `workbook.Save(stream, SaveFormat.Xlsx);`가 유용합니다.

---

## TL;DR

우리는 다음을 수행하는 **완전한 C# 콘솔 앱**을 만들었습니다.

1. **Aspose.Cells**를 사용해 **Excel 워크북 C# 만들기**.  
2. **Excel에서 EXPAND 함수**를 이용해 3‑행 배열을 5 × 5 블록으로 변환.  
3. 코탄젠트 수식(`COT(PI()/4)`) 추가.  
4. 파일 저장 및 필요 시 자동 열 너비 맞춤 적용.

이제 .NET에서 Excel 파일을 자동 생성하는 모든 작업에 튼튼한 기반을 갖추었습니다. 즐거운 코딩 되세요, 그리고 스프레드시트가 언제나 오류 없이 동작하길 바랍니다!

## 다음에 배울 내용은?

다음 튜토리얼들은 이번 가이드에서 사용한 기술을 확장하고, 추가 API 기능을 마스터하며, 프로젝트에 다양한 구현 방식을 적용할 수 있도록 돕습니다. 각각 완전한 코드 예제와 단계별 설명을 포함하고 있습니다.

- [Aspose.Cells .NET를 사용하여 Excel에서 워크북 범위 지정된 명명된 범위 만들기](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Aspose.Cells .NET (C# 가이드)로 Excel에서 유니온 범위 만들고 사용하기](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [Aspose.Cells .NET를 사용해 차트가 포함된 Excel 워크북 만들기 | 단계별 가이드](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}