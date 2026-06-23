---
category: general
date: 2026-04-07
description: 스프레드시트 셀에 사용자 정의 숫자 서식을 적용하고, C#로 셀 값을 내보낼 때 스프레드시트에서 숫자를 서식 지정하는 방법을
  배워보세요. 빠르고 완전한 가이드.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: ko
og_description: 스프레드시트 셀에 사용자 지정 숫자 형식을 적용하고 형식이 지정된 문자열로 내보냅니다. 스프레드시트에서 숫자를 형식화하고
  셀 값을 내보내는 방법을 알아보세요.
og_title: 사용자 지정 숫자 형식 적용 – 완전한 C# 내보내기 튜토리얼
tags:
- C#
- Spreadsheet
- Number Formatting
title: C# 스프레드시트 내보내기에서 사용자 정의 숫자 형식 적용 – 단계별 가이드
url: /ko/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# 스프레드시트 내보내기에서 사용자 정의 숫자 형식 적용 – 전체 튜토리얼

셀에 **사용자 정의 숫자 형식**을 적용하고 그 형식이 적용된 문자열을 스프레드시트에서 추출해야 했던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 개발자들이 원시 값이 반환되어 보기 좋은 로케일에 맞는 문자열이 나오지 않을 때 난관에 부딪히곤 합니다. 이 가이드에서는 스프레드시트 셀에서 숫자를 형식화하는 방법과 인기 있는 C# 스프레드시트 라이브러리를 사용해 셀 값을 형식이 적용된 문자열로 내보내는 방법을 정확히 보여드립니다.

이 과정을 마치면 모든 숫자 셀에 **사용자 정의 숫자 형식**을 적용하고 `ExportTable`로 결과를 내보내며 UI나 보고서에 표시하고자 하는 정확한 출력을 확인할 수 있습니다. 별도의 외부 문서는 필요 없습니다—모든 것이 여기 있습니다.

## 사전 요구 사항

- .NET 6.0 이상 (코드는 .NET Framework 4.7+에서도 동작합니다)
- `Workbook`, `Worksheet`, `ExportTableOptions`를 제공하는 스프레드시트 라이브러리에 대한 참조 (예: **Aspose.Cells** 또는 **GemBox.Spreadsheet**; 여기 보여지는 API는 Aspose.Cells와 일치합니다)
- 기본 C# 지식 — `Console.WriteLine`을 작성할 수 있다면 바로 시작할 수 있습니다

> **프로 팁:** 다른 라이브러리를 사용한다면 속성 이름은 보통 비슷합니다 (`NumberFormat`, `ExportAsString`). 해당 이름에 맞게 매핑하면 됩니다.

## 튜토리얼에서 다루는 내용

1. 워크북을 생성하고 첫 번째 워크시트를 선택하기.  
2. 셀에 숫자 값을 삽입하기.  
3. `ExportTableOptions`를 설정하여 **사용자 정의 숫자 형식**을 적용하고 문자열을 반환하도록 하기.  
4. 셀을 내보내고 형식이 적용된 결과를 출력하기.  
5. 예외 상황 처리 – 셀에 수식이나 null 값이 들어 있는 경우는 어떻게 할까?

시작해 봅시다.

![사용자 정의 숫자 형식 적용 예시](https://example.com/image.png "사용자 정의 숫자 형식 적용")

## 단계 1 – 워크북을 생성하고 첫 번째 워크시트 가져오기

먼저 필요한 것은 워크북 객체입니다. 이를 Office 앱에서 여는 Excel 파일이라고 생각하면 됩니다. 워크북을 얻은 뒤 첫 번째 시트를 가져오세요—대부분의 튜토리얼이 여기서 시작하는 이유는 예제를 간결하게 유지할 수 있기 때문입니다.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**왜 중요한가:** 새 워크북은 깨끗한 상태를 제공하므로 이후에 적용할 사용자 정의 숫자 형식에 방해가 되는 숨겨진 서식이 없습니다.

## 단계 2 – 셀 B2에 숫자 값을 입력하기 (내보낼 셀)

이제 형식화할 대상이 필요합니다. **B2** 셀은 참조하기 쉽고 기본 A1 코너에서 충분히 떨어져 있어 실수로 덮어쓰는 일을 방지할 수 있는 편리한 위치입니다.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**값이 수식이라면?**  
나중에 원시 값을 수식(`=SUM(A1:A10)` 등)으로 교체하더라도, 내보내기 루틴은 다음 단계에서 적용한 숫자 형식을 그대로 적용합니다. 왜냐하면 서식은 셀에 붙어 있는 것이며, 값 유형에 따라 달라지지 않기 때문입니다.

## 단계 3 – 값을 형식이 적용된 문자열로 받기 위해 내보내기 옵션 구성하기

튜토리얼의 핵심입니다: 라이브러리에 내보내는 동안 **사용자 정의 숫자 형식**을 적용하도록 지시합니다. `NumberFormat` 문자열은 Excel의 “사용자 지정” 카테고리에서 사용하는 패턴과 동일합니다.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true`는 메서드가 원시 double 대신 `string`을 반환하도록 보장합니다.  
- `NumberFormat = "#,##0.00;(#,##0.00)"`는 Excel 패턴을 그대로 반영합니다: 천 단위 구분 기호로 콤마, 소수점 둘째 자리까지, 음수는 괄호로 표시합니다.

> **왜 사용자 정의 형식을 사용하나요?** 문화권 간 일관성을 보장합니다(예: 미국과 유럽의 숫자 구분자 차이) 그리고 회계용 괄호와 같은 비즈니스 특화 스타일을 삽입할 수 있습니다.

## 단계 4 – 구성된 옵션을 사용해 셀 내보내기

이제 실제로 워크시트에서 값을 추출하며, 라이브러리가 정의한 형식을 적용하는 무거운 작업을 수행하도록 합니다.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**예외 상황 – 빈 셀:** `B2`가 비어 있다면 `formattedResult`는 `null`이 됩니다. 출력하기 전에 간단한 null 체크로 이를 방지할 수 있습니다.

## 단계 5 – 형식이 적용된 문자열 표시하기

마지막으로 결과를 콘솔에 출력합니다. 실제 애플리케이션에서는 이 문자열을 PDF, 이메일, 혹은 UI 라벨에 전달할 수 있습니다.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**예상 출력**

```
1,234.56
```

원시 값을 `-9876.54`로 바꾸면 동일한 형식이 `(9,876.54)`를 반환합니다—많은 회계 보고서에서 요구하는 바로 그 형태입니다.

## 전체 실행 가능한 예제

아래는 새 콘솔 프로젝트에 복사‑붙여넣기 할 수 있는 전체 프로그램입니다. 스프레드시트 라이브러리에 맞는 NuGet 패키지를 추가했다면 그대로 컴파일되고 실행됩니다.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### 간단한 검증 체크

- **컴파일이 되나요?** 예—`Aspose.Cells`(또는 동등한) DLL이 참조되어 있는지 확인하면 됩니다.
- **다른 문화권에서도 동작하나요?** 형식 문자열은 문화권에 구애받지 않으며, 라이브러리는 제공된 패턴을 그대로 따릅니다. 로케일에 맞는 구분자가 필요하면 내보내기 전에 `CultureInfo` 처리를 앞에 추가하면 됩니다.

## 일반적인 질문 및 변형

### 다른 패턴을 사용해 **스프레드시트에서 숫자 형식 지정**하는 방법은?

`NumberFormat` 문자열을 교체하면 됩니다. 예를 들어, 소수점 한 자리까지 표시하는 퍼센트 형식은 다음과 같습니다:

```csharp
NumberFormat = "0.0%";
```

### 셀 값을 일반 텍스트가 아니라 HTML로 **내보내는 방법**이 필요하다면?

대부분의 라이브러리는 내보내기 유형을 받는 오버로드를 제공합니다. `ExportAsString = true`로 설정하고 `ExportHtml = true`(또는 유사 옵션)를 추가하면 됩니다. 원리는 동일합니다: 형식을 정의하고, 출력 형태를 선택합니다.

### 하나의 셀뿐 아니라 전체 범위에 형식을 적용할 수 있나요?

물론 가능합니다. `NumberFormat`을 `Style` 객체에 할당한 뒤 해당 스타일을 `Range`에 적용하면 됩니다. 내보내기 호출은 그대로이며, 자동으로 스타일을 인식합니다.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### 셀에 수식이 들어 있으면 어떻게 되나요?

내보내기 루틴은 먼저 수식을 계산한 뒤, 결과 숫자 값에 형식을 적용합니다. 추가 코드는 필요 없으며, 자동 계산을 비활성화한 경우 `Calculate`가 호출되었는지 확인하면 됩니다.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## 결론

이제 스프레드시트 셀에 **사용자 정의 숫자 형식**을 적용하고, **스프레드시트에서 숫자 형식 지정**을 수행하며, **셀 값을** 바로 표시 가능한 문자열로 **내보내는 방법**을 알게 되었습니다. 위의 간결한 코드 샘플은 워크북 생성부터 최종 출력까지 모든 단계를 포함하고 있어 바로 프로덕션 프로젝트에 삽입할 수 있습니다.

다음 도전에 준비가 되었나요? 이 기법을 날짜, 통화 기호, 조건부 서식 등 **숫자 셀 형식 지정**과 결합해 보세요. 혹은 여러 셀을 CSV로 내보내면서 각 셀의 사용자 정의 형식을 유지하는 방법을 탐구해 보세요. 가능성은 무한하며, 이 기본기를 통해 견고한 기반을 마련했습니다.

코딩을 즐기세요, 그리고 실험을 잊지 마세요—때로는 형식 문자열을 약간만 조정해도 최고의 해답이 떠오릅니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}