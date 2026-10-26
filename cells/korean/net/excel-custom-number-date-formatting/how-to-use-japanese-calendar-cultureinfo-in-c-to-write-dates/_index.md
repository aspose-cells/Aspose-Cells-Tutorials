---
category: general
date: 2026-10-26
description: C#에서 일본 달력 CultureInfo를 사용하여 연호 날짜를 파싱하고 NPOI로 Excel 워크시트에 삽입하는 방법을 배웁니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: ko
lastmod: 2026-10-26
og_description: C#에서 일본 달력 CultureInfo를 사용해 레이와 연호 날짜를 파싱하고 Excel 워크시트에 기록합니다. 완전하고
  실행 가능한 코드와 설명을 포함합니다.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: C#에서 일본 달력 CultureInfo 사용 – 전체 Excel 예제
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: C#에서 일본식 달력 CultureInfo를 이용해 Excel에 날짜를 쓰는 방법
url: /ko/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 일본 달력 CultureInfo를 사용해 날짜를 Excel에 쓰는 방법

날짜를 다룰 때 **일본 달력 CultureInfo**를 사용해야 하는 경우, 이 가이드는 정확한 방법을 보여줍니다. 일본 연호(예: *Reiwa 2/5/1*)가 포함된 날짜 문자열을 파싱하고, 결과 `DateTime`을 NPOI 라이브러리를 사용해 Excel 워크시트의 첫 번째 셀에 쓰는 방법을 배웁니다.

올바른 `CultureInfo` 없이 연호 기반 날짜를 파싱하면 `FormatException`이 발생하거나 월/일 값이 잘못될 수 있습니다. `CultureInfo`를 일본 달력으로 설정하면 .NET 런타임이 연호를 올바르게 해석하고, Excel에 저장되는 값이 원래 일본 표기와 일치하도록 보장합니다.

이 튜토리얼에서 배우게 될 내용:

* 일본 달력을 사용하는 `CultureInfo` 객체 만들기
* `DateTime.Parse`로 일본 연호 날짜 문자열 파싱
* 파싱된 `DateTime`을 NPOI 워크시트 셀에 삽입
* 전체 실행 가능한 프로그램과 예상 출력 보기

> **Prerequisites** – .NET 6.0+ (또는 .NET Core 3.1+), **NPOI** NuGet 패키지, 그리고 C#와 Excel 파일 처리에 대한 기본 이해

---

## What you’ll need

| Item | Reason |
|------|--------|
| **.NET SDK** (6.0 이상) | `CultureInfo`를 위한 런타임 및 라이브러리를 제공합니다. |
| **NPOI** (`NPOI` NuGet 패키지) | Office가 설치되지 않은 환경에서도 Excel 파일을 생성·조작할 수 있게 해줍니다. |
| **Visual Studio Code**, **Visual Studio**, 또는 기타 C# IDE | 샘플을 컴파일하고 실행하기 위해 필요합니다. |
| **Japanese era date string** (예: `"Reiwa 2/5/1"`) | 일본 달력 사용을 시연합니다. |

---

## Step 1: Install NPOI

프로젝트 폴더에서 터미널을 열고 다음을 실행합니다:

```bash
dotnet add package NPOI --version 2.6.1
```

이 패키지는 이후에 사용할 `IWorkbook`, `ISheet`, `ICell` 타입을 제공합니다.

---

## Step 2: Create a CultureInfo that uses the Japanese calendar

일본 달력은 연호 기반 달력입니다. `ja-JP` 로케일의 *Japanese* 변형을 요청하고, `Calendar`를 명시적으로 `JapaneseCalendar`로 설정해야 합니다.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – 기본 `ja-JP` 문화권은 그레고리안 달력을 사용합니다. `Calendar` 속성을 재할당하면 *Reiwa*와 같은 연호 이름이 파싱 시 인식됩니다.

---

## Step 3: Parse a Japanese era date string

`CultureInfo`가 설정되었으니, 이제 연호가 포함된 문자열을 안전하게 파싱할 수 있습니다.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse` 메서드는 *Reiwa 2*를 그레고리안 연도 2020년, 5월, 1일로 해석합니다.

### Edge case: handling invalid eras

사용자가 지원되지 않는 연호(예: 헤이세이 시대가 끝난 뒤의 `"Heisei 31/4/30"`)를 제공하면 `DateTime.Parse`가 `FormatException`을 발생시킵니다. 친절한 오류 메시지를 제공하려면 try‑catch 블록으로 감싸세요:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Step 4: Write the parsed DateTime into an Excel worksheet

`DateTime` 객체가 준비되면 Excel 셀에 저장할 수 있습니다. NPOI는 `DateTime` 값을 자동으로 Excel 날짜 형식으로 변환합니다.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Result** – *JapaneseEraDate.xlsx*를 열면 셀 A1에 **2020‑05‑01** 날짜가 표시됩니다.

### Why use NPOI?

*Works on any platform* (Windows, Linux, macOS) and does **not** require Microsoft Office. This makes the solution suitable for CI pipelines, Docker containers, or server‑side processing.

---

## Step 5: Full, runnable program

모든 내용을 하나로 모은 완전한 콘솔 애플리케이션 예제는 다음과 같습니다:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**How to run**

```bash
dotnet run
```

실행 후 프로젝트 폴더에 `JapaneseEraDate.xlsx` 파일이 생성되며, 올바르게 파싱된 날짜가 들어 있습니다.

---

## Common pitfalls and best‑practice tips

| Pitfall | Fix / Recommendation |
|---------|----------------------|
| `japaneseCulture.DateTimeFormat.Calendar` 설정을 잊음 | `JapaneseCalendar` 인스턴스를 항상 할당하세요; 그렇지 않으면 연호가 인식되지 않습니다. |
| 커스텀 `CultureInfo` 없이 `DateTime.TryParse` 사용 | `TryParse`에도 동일한 `japaneseCulture`를 전달해 동작을 일관되게 유지하세요. |
| Excel이 연호 이름을 표시할 것으로 기대 | Excel 기본 날짜 형식은 그레고리안만 지원합니다. 연호를 표시하려면 원본 문자열을 별도 열에 저장하거나 사용자 정의 텍스트 형식을 만들세요. |
| `FileStream`을 닫지 않음 | 예시와 같이 `using` 블록을 사용해 파일 핸들을 즉시 해제하세요. |
| 스레드 간 `CultureInfo` 객체 혼용 | `CultureInfo`는 읽기 전용 작업에 대해 스레드‑안전하지만, 초기 설정 후 `Calendar` 속성을 변경하지 않도록 하세요. |

---

## Conclusion

이제 C#에서 **일본 달력 CultureInfo**를 사용해 일본 연호 날짜를 정확히 파싱하고, NPOI를 통해 Excel 워크시트에 `DateTime`을 기록하는 방법을 알게 되었습니다. 전체 예제는 구성, 파싱, 오류 처리, Excel 출력까지 다루며, 국제화된 보고서나 데이터 교환 시 견고한 기반을 제공합니다.

다음 단계로 고려해 볼 내용:

* **커스텀 텍스트 형식으로 날짜 포맷**하여 Excel 안에 연호 이름을 유지하기
* **Excel에서 날짜 읽기** – `cell.DateCellValue`를 사용하면서 일본 달력을 고려하기
* **다른 연호 기반 달력**(예: 태국 불교 달력)에도 동일한 기법 적용 – `JapaneseCalendar`를 해당 `Calendar` 서브클래스로 교체하기

다양한 연호 문자열, 대용량 데이터 세트, 혹은 ASP.NET Core API와 결합해 실시간 Excel 보고서를 생성하는 등 여러 시나리오를 실험해 보세요. Happy coding!

## What Should You Learn Next?

다음 튜토리얼들은 이 가이드에서 다룬 기술을 확장하고, 추가 API 기능을 마스터하며, 프로젝트에 적용할 수 있는 대안 구현 방법을 제공합니다.

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}