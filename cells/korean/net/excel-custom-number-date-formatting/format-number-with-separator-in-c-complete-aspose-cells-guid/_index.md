---
category: general
date: 2026-03-30
description: C#에서 Aspose.Cells를 사용하여 구분 기호가 있는 숫자 서식을 지정하는 방법을 배웁니다. 사용자 지정 숫자 서식
  설정, 천 단위 구분 기호 추가, 소수점 자리 서식 지정, 셀 서식 지정 방법을 포함합니다.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: ko
og_description: C#에서 구분자를 사용해 숫자 형식 지정하기. 이 가이드는 사용자 지정 숫자 형식 설정, 천 단위 구분자 추가, 소수점
  자리 형식 지정, 그리고 Aspose.Cells를 사용한 셀 서식 지정 방법을 보여줍니다.
og_title: C#에서 구분자를 사용한 숫자 서식 – Aspose.Cells 튜토리얼
tags:
- C#
- Aspose.Cells
- Number Formatting
title: C#에서 구분자를 사용한 숫자 서식 지정 – 완전한 Aspose.Cells 가이드
url: /ko/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 구분 기호를 사용한 숫자 서식 지정 – 완전한 Aspose.Cells 가이드

스프레드시트에서 **구분 기호가 있는 숫자 서식**을 적용해야 했지만 어떤 API 호출을 사용해야 할지 몰랐던 적이 있나요? 당신만 그런 것이 아닙니다—개발자들은 데이터를 내보낼 때 천 단위 구분 기호, 소수점 자리수, 사용자 정의 패턴을 끊임없이 다루고 있습니다.  

좋은 소식: Aspose.Cells가 이를 손쉽게 해결해 줍니다. 이번 튜토리얼에서는 **사용자 정의 숫자 서식 설정**, **천 단위 구분 기호 추가**, **소수점 자리수 서식 지정**, 그리고 **셀을 문자열로 포맷하는 방법**을 실제 예제로 단계별로 살펴봅니다. 끝까지 따라오면 .NET 프로젝트 어디에든 바로 넣어 실행할 수 있는 완성된 코드 조각을 얻을 수 있습니다.

## 이 가이드에서 다루는 내용

* 필요한 정확한 NuGet 패키지와 설치 방법.  
* 워크북을 생성하고, 숫자 값을 기록한 뒤, 사용자 정의 서식을 적용하는 단계별 코드.  
* `ExportTableOptions.ExportAsString`이 포맷된 값을 가져오는 권장 방법인 이유.  
* `ExportAsString`을 활성화하지 않거나 잘못된 서식 마스크를 사용하는 등 흔히 발생하는 실수.  
* 소수점 자리수나 구분 기호 스타일을 변경하고 싶을 때 서식 마스크를 조정하는 방법.

외부 문서 링크는 필요 없습니다; 여기서 바로 모든 것을 확인할 수 있습니다. 바로 시작해 보세요.

---

## 전제 조건

| 요구 사항 | 이유 |
|-------------|--------|
| .NET 6.0 이상 | Aspose.Cells 23.10+은 .NET Standard 2.0+을 대상으로 하므로 .NET 6은 안전하고 최신 버전입니다. |
| Visual Studio 2022 (또는 any C# IDE) | 디버깅과 패키지 관리를 손쉽게 해 줍니다. |
| Aspose.Cells for .NET NuGet 패키지 | 우리가 사용할 `Workbook`, `Worksheet`, `ExportTableOptions` 클래스를 제공합니다. |

패키지는 Package Manager Console을 통해 설치할 수 있습니다:

```powershell
Install-Package Aspose.Cells
```

이것으로 끝—추가 DLL이나 COM 인터옵이 필요 없으며, NuGet 참조 하나만 있으면 됩니다.

---

## 1단계: 새 워크북 초기화 (셀 서식 지정 방법)

먼저 새로운 `Workbook` 인스턴스를 생성합니다. 이는 데이터를 받을 준비가 된 빈 Excel 파일과 같습니다.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **왜 중요한가:** `Workbook`은 Aspose.Cells에서 모든 작업의 진입점입니다. 첫 번째 워크시트(`Worksheets[0]`)를 가져오면 시트 이름을 지정하지 않아도 깨끗한 캔버스를 얻을 수 있습니다.

---

## 2단계: 대상 셀에 숫자 값 쓰기

다음으로 **A1** 셀에 원시 숫자를 입력합니다. 아직 서식이 적용되지 않은 상태이며, 단순히 `double` 값입니다.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **프로 팁:** 나중에 숫자 서식을 적용하려면 `PutString` 대신 `PutValue`를 사용하세요. 이렇게 하면 기본 데이터 형식이 유지되어 Excel 호환 계산이 가능합니다.

---

## 3단계: 사용자 정의 숫자 서식 설정 (천 단위 구분 기호 및 소수점 자리수 지정)

이제 튜토리얼의 핵심인 서식 마스크를 정의합니다. 마스크 `#,##0.00`은 다음 세 가지 역할을 합니다:

1. **`#,##0`** – 기본적으로 쉼표(,)를 천 단위 구분 기호로 추가합니다.  
2. **`.00`** – 정확히 두 자리 소수점을 강제합니다.  

다른 소수점 자리수가 필요하면 소수점 뒤의 `0` 개수를 변경하면 됩니다.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **`ExportAsString`을 사용하는 이유:** 기본적으로 `ExportString`은 원시 값을 반환합니다. `ExportAsString = true`로 설정하면 API가 `NumberFormat` 마스크를 적용한 뒤 텍스트로 변환합니다. 이는 보고서, JSON 페이로드, UI 표시 등에서 정확한 문자열 표현이 필요할 때 필수입니다.

---

## 4단계: 포맷된 텍스트 내보내기 (셀 서식 지정 방법)

옵션을 준비했으면 같은 셀에 `ExportString`을 호출합니다. 이 메서드는 방금 정의한 마스크를 적용해 깔끔한 문자열을 반환합니다.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

프로그램을 실행하면 콘솔에 **`12,345.68`**이 출력됩니다—우리가 지정한 그대로의 형식입니다.

> **예외 상황:** 원본 숫자에 소수점 이하가 두 자리보다 많으면 마스크가 반올림합니다. 반올림 대신 절삭이 필요하면 `PutValue` 호출 전에 `Math.Truncate`로 값을 미리 처리해야 합니다.

---

## 5단계: 서식 미세 조정 – 일반적인 변형

### 5.1 소수점 정밀도 변경

소수점 세 자리수가 필요하신가요? 마스크만 다음과 같이 바꾸면 됩니다:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 다른 천 단위 구분 기호 사용

일부 지역에서는 공백이나 마침표를 선호합니다. 문자 자체를 직접 삽입할 수 있습니다:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

또는 워크북의 문화권 설정을 활용하세요:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 접두사 또는 접미사 (통화, 퍼센트)

마스크에 달러 기호나 퍼센트 기호를 바로 추가합니다:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **주의:** 마스크는 대소문자를 구분합니다. `$`와 `%`는 리터럴 기호이며, 기본 숫자 값에는 영향을 주지 않습니다.

---

## 6단계: 전체 작업 예제 (복사‑붙여넣기 가능)

아래는 새 콘솔 앱에 복사해 넣을 수 있는 완전한 프로그램입니다. 모든 단계, 주석, 최종 출력 검증이 포함되어 있습니다.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

프로그램을 실행(`dotnet run`을 터미널에서 입력하거나 Visual Studio에서 F5)하면 위와 동일하게 포맷된 숫자가 출력됩니다.

---

## 자주 묻는 질문 (FAQ)

**Q: 오래된 Excel 버전에서도 작동하나요?**  
A: 네. 서식 마스크는 Excel 고유의 숫자 서식 구문을 따르므로 `#,##0.00`을 이해하는 모든 버전에서 동일한 문자열을 표시합니다.

**Q: 여러 셀 범위에 서식을 적용하려면 어떻게 해야 하나요?**  
A: 원하는 범위를 순회하면서 각 셀에 동일한 `ExportTableOptions`를 적용하거나, 범위에 `Style.Custom` 속성을 설정한 뒤 단일 셀에 `ExportString`을 호출하면 됩니다.

**Q: 이러한 서식을 적용한 상태로 CSV에 직접 내보낼 수 있나요?**  
A: 물론 가능합니다. 각 셀에 서식을 지정한 뒤 `Workbook.Save("output.csv", SaveFormat.CSV);`를 사용하면 Aspose.Cells가 셀 `Style`을 존중하여 CSV를 생성합니다.

---

## 결론

우리는 C#에서 Aspose.Cells를 사용해 **구분 기호가 있는 숫자 서식**을 적용하는 방법을 살펴보았습니다. 여기에는 **사용자 정의 숫자 서식 설정**, **천 단위 구분 기호 추가**, **소수점 자리수 지정**, 그리고 문자열 내보내기를 위한 **셀 서식 지정 방법**이 모두 포함됩니다. 코드는 완전히 독립적이며 .NET 6+에서 동작하고, 어떤 지역이나 정밀도 요구에도 쉽게 적용할 수 있습니다.

다음 단계로 살펴볼 내용:

* 날짜와 시간에도 동일한 기법 적용 (`NumberFormat = "dd‑MMM‑yyyy"`).  
* 각 열마다 다른 마스크가 필요한 대량 내보내기 자동화.  
* Aspose.Words와 연계해 포맷된 문자열을 PDF 보고서에 삽입.

시도해 보시고 팀 내 스프레드시트 서식 담당자로 빠르게 자리매김하세요. Happy coding!   (Image: ![Aspose.Cells에서 구분 기호가 포함된 형식화된 숫자 스크린샷](image-placeholder.png){alt="Aspose.Cells 출력에 표시된 구분 기호가 포함된 형식화된 숫자"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}