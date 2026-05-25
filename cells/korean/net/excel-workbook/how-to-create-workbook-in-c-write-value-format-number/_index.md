---
category: general
date: 2026-03-01
description: C#에서 워크북을 빠르게 만드는 방법—셀에 값을 쓰고, 셀 숫자 형식을 설정하며, 간단한 단계로 셀 숫자를 포맷하는 방법을
  배워보세요.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: ko
og_description: C#에서 워크북을 만드는 방법은? 이 가이드는 셀에 값을 쓰고, 셀 숫자 형식을 설정하며, 몇 줄의 코드만으로 셀 숫자를
  포맷하는 방법을 보여줍니다.
og_title: C#에서 워크북 만들기 – 값 쓰기 및 숫자 서식 지정
tags:
- C#
- Aspose.Cells
- Excel Automation
title: C#에서 워크북 만들기 – 값 쓰기 및 숫자 서식 지정
url: /ko/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 워크북 만들기 – 값 쓰기 및 숫자 서식 지정

C#에서 워크북을 만드는 것은 Excel 파일을 즉석에서 생성해야 할 때 흔히 수행하는 작업입니다. 이 가이드에서는 셀에 값을 쓰고 셀의 숫자 서식을 지정하는 방법을 단계별로 안내하여 최종 시트가 깔끔하게 보이도록 합니다.

빈 스프레드시트를 보고 숫자가 너무 많은 소수점 이하까지 표시되는 경우를 겪어본 적이 있다면, 당신만 그런 것이 아닙니다. 워크북 객체 초기화부터 사용자 정의 숫자 서식 설정까지 모두 다루며, 나중에 마주칠 수 있는 몇 가지 엣지 케이스에 대한 팁도 제공하겠습니다.

## 배울 내용

- **새 `Workbook` 인스턴스 초기화**하기.  
- `PutValue` 메서드를 사용해 **셀에 값 쓰기**.  
- `Style` 객체로 **셀 숫자 서식 설정**하여 깔끔한 두 자리 소수점 표시 구현.  
- 셀을 다시 읽어보거나 Excel에서 파일을 열어 결과 확인하기.  

표준 Aspose.Cells(또는 유사 API) 외에 별도 라이브러리는 필요 없으며, 코드는 .NET 6+ 환경에서 추가 설정 없이 실행됩니다.

---

## 워크북 만들기 – 객체 초기화

먼저 워크시트를 담을 워크북 객체가 필요합니다. `Workbook`은 전체 Excel 파일을 의미하고, 각 `Worksheet`는 개별 탭을 의미합니다.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*왜 중요한가:* 워크북을 생성하면 이후 행, 열, 서식을 담을 내부 구조가 할당됩니다. 이 객체가 없으면 셀에 값을 쓸 곳이 없습니다.

> **프로 팁:** 기존 파일을 활용하려면 `new Workbook()` 대신 `new Workbook("template.xlsx")` 로 교체해 템플릿을 로드하고 스타일을 유지하세요.

## 셀에 값 쓰기

워크북이 준비되었으니 첫 번째 워크시트의 **A1** 셀에 숫자를 넣어봅시다.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*`PutValue` 사용 이유:* 이 메서드는 데이터 타입을 자동으로 감지하므로 직접 형변환하거나 변환할 필요가 없습니다. 또한 셀에 기존 스타일이 있으면 이를 그대로 유지해 나중에 **셀 숫자 서식 설정** 시 편리합니다.

### 빠른 확인

셀을 다시 읽어보면 원시 값이 표시됩니다:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

이는 서식이 적용되기 전의 숫자입니다.

## 셀 숫자 서식 지정

많은 소수점을 가진 원시 double 값을 그대로 표시하는 것은 사용자 친화적이지 않을 수 있습니다. 두 자리 소수점으로 제한해 보겠습니다.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

`Number` 속성은 Excel 내장 숫자 서식 ID와 매핑됩니다. `2`는 “소수점 두 자리 숫자”를 의미합니다. 다른 형식—예를 들어 통화나 날짜—이 필요하면 다른 ID 혹은 사용자 정의 서식 문자열을 사용하면 됩니다.

### 대안: 사용자 정의 서식 문자열

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*사용자 정의 스타일을 선택하는 이유:* 내장 ID가 지역 설정을 충분히 커버하지 못할 때 전체 제어가 가능합니다.

## 출력 확인 (선택 사항이지만 권장)

스타일을 적용한 뒤 워크북을 저장하고 Excel에서 열어 모양을 확인할 수 있습니다.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

셀 A1에 **123.46**이 표시될 것이며, 이는 우리가 지정한 두 자리 소수점 서식 덕분입니다.

---

### 전체 작업 예제

모두 합치면 콘솔 앱에 복사·붙여넣기 할 수 있는 독립 실행형 프로그램이 됩니다.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**프로그램 실행 시 예상 출력:**

```
Cell A1 shows: 123.46
```

`FormattedWorkbook.xlsx` 파일을 Excel에서 열면 동일한 서식이 적용된 값을 확인할 수 있습니다.

---

## 일반적인 변형 및 엣지 케이스

### 1. 다양한 숫자 서식

| 목표 | 서식 ID | 코드 스니펫 |
|------|-----------|--------------|
| 통화 (소수점 두 자리) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| 백분율 (소수점 없음) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| 과학적 표기법 | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

내장 ID가 맞지 않을 경우 앞서 소개한 사용자 정의 문자열을 사용하세요.

### 2. 문화권별 소수점 구분자

일부 로케일은 소수점에 콤마를 사용합니다. 문화권에 맞는 서식을 강제할 수 있습니다:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. 숫자가 아닌 텍스트 쓰기

문자열을 셀에 **쓰기**하려면 `PutValue`에 문자열을 전달하면 됩니다:

```csharp
cellA1.PutValue("Total Revenue");
```

숫자 서식은 필요 없지만 폰트 스타일은 여전히 적용할 수 있습니다.

### 4. 대용량 데이터셋

수천 행을 채우는 경우 `PutValue`를 반복하기보다 `Cells.ImportArray` 같은 배치 삽입이 더 빠릅니다. 서식 적용 방식은 동일하며, 범위에 스타일을 적용하면 됩니다:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## 자주 묻는 질문

**Q: .NET Core에서도 작동하나요?**  
A: 물론입니다. Aspose.Cells는 .NET Standard 2.0 이상을 지원하므로 .NET 5, .NET 6, .NET 7 등에서도 별도 변경 없이 사용할 수 있습니다.

**Q: 소수점 두 자리보다 더 많이 표시하려면 어떻게 하나요?**  
A: `Number` 속성을 해당하는 내장 ID(예: 세 자리 소수점은 `3`)로 바꾸거나, 사용자 정의 서식 문자열(`"#,##0.000"` 등)을 조정하면 됩니다.

**Q: 전체 열에 한 번에 서식을 적용할 수 있나요?**  
A: 가능합니다. `Cells["A:A"]` 로 전체 열을 가져온 뒤 `SetStyle`을 호출하면 됩니다.

---

## 결론

이제 C#에서 **워크북 만들기**, **셀에 값 쓰기**, **셀 숫자 서식 지정** 방법을 알게 되었습니다. 이 기본기를 마스터하면 최소한의 노력으로 전문적인 Excel 보고서, 청구서, 데이터 내보내기를 손쉽게 생성할 수 있습니다.

다음 단계로는 날짜, 백분율, 조건부 서식 등 **셀 숫자 서식**을 확장해 보세요—모두 이번에 다룬 원리를 기반으로 합니다. Aspose.Cells 문서를 참고해 더 다양한 스타일 옵션을 탐색하거나, 여러 워크시트를 하나의 워크북에 결합해 풍부한 보고서를 만들어 보세요.

코딩 즐겁게, 그리고 잘 서식화된 스프레드시트가 얼마나 큰 가치를 제공하는지 기억하세요.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}