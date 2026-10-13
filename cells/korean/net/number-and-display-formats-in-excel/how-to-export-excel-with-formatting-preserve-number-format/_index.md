---
category: general
date: 2026-03-22
description: 서식이 적용된 Excel을 내보내고 숫자 형식을 유지하는 방법. Excel 범위를 변환하고, 수식 결과를 얻으며, Aspose.Cells를
  사용하여 서식이 적용된 Excel을 내보내는 방법을 배웁니다.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: ko
og_description: 서식이 포함된 Excel을 내보내고 숫자 서식을 유지하는 방법. Excel 범위를 변환하고 수식 결과를 얻으며 C#에서
  서식이 적용된 Excel을 내보내는 단계별 가이드.
og_title: 서식이 포함된 Excel 내보내기 방법 – 숫자 서식 유지
tags:
- C#
- Aspose.Cells
- Excel automation
title: 서식이 포함된 Excel 내보내기 방법 – 숫자 서식 유지
url: /ko/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 서식과 함께 내보내는 방법 – 숫자 서식 유지

워크북에서 보는 그대로 모든 셀의 모양을 유지하면서 **Excel을 내보내는 방법**을 궁금해 본 적 있나요? 보고서를 클라이언트에게 전달하거나, 그리드 컨트롤에 데이터를 공급하거나, 데이터베이스에 값을 저장해야 할 수도 있습니다. 대부분의 경우 숫자 서식이 사라지거나 수식이 원시 문자열로 변환되는 문제가 발생합니다.  

이 튜토리얼에서는 **숫자 서식 유지**, **Excel 범위를 `DataTable` 로 변환**, **수식 결과 가져오기**, 그리고 마지막으로 Aspose.Cells를 사용해 **서식이 적용된 Excel 내보내기**를 수행하는 완전한 C# 예제를 단계별로 살펴봅니다. 끝까지 따라오면 워크시트 참조만으로 어떤 프로젝트에든 삽입할 수 있는 단일 메서드를 얻게 됩니다.

> **빠른 미리보기:** 코드는 워크북을 생성하고 값과 수식을 기록한 뒤, Aspose.Cells에 셀을 서식이 적용된 문자열로 내보내도록 지시하고 `123.456 | 246.912` 를 출력합니다 – Excel에서 기대하는 그대로입니다.

---

## 필요 사항

- **Aspose.Cells for .NET** (무료 체험판으로 학습에 충분합니다)
- .NET 6.0 이상 (.NET Framework에서도 API는 동일합니다)
- 기본 C# 개발 환경 (Visual Studio, VS Code, Rider 등… 원하는 도구 선택)

Aspose.Cells 외에 추가 NuGet 패키지는 필요하지 않습니다. 아직 설치하지 않았다면 다음을 실행하세요:

```bash
dotnet add package Aspose.Cells
```

---

## 단계 1 – 워크북 생성 및 값 쓰기 (수식 포함)

먼저 새 워크북을 만들고 **A1**에 숫자 값을 입력합니다. 그런 다음 **B1**에 첫 번째 셀을 두 배로 곱하는 간단한 수식을 추가합니다. 이는 이후 **수식 결과 가져오기**를 시연하기 위한 준비 단계입니다.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**왜 중요한가:**  
- `PutValue`는 원시 숫자를 저장하고, `PutFormula`는 계산식을 저장합니다.  
- Aspose.Cells는 수식을 **활성** 상태로 유지하므로, 나중에 셀 값을 요청하면 실제로 `246.912` 를 얻으며, 문자열 `"=A1*2"` 가 반환되지 않습니다.

---

## 단계 2 – Aspose.Cells에 서식이 적용된 문자열로 값 내보내기

기본 설정으로 `ExportDataTable`을 호출하면 숫자 셀은 기본 `double` 값으로 반환됩니다. 이 경우 천 단위 구분 기호, 통화 기호, 사용자 지정 소수점 등 설정한 서식이 모두 사라집니다. `ExportTableOptions` 클래스를 사용하면 **숫자 서식 유지**와 **문자열로 내보내기**를 동시에 할 수 있습니다.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**핵심 포인트:** `ExportNumberFormat = true` 가 **숫자 서식 유지** 기능을 활성화하는 플래그입니다. 이를 설정하지 않으면 `"123.456"` 와 `"246.912"` 가 원시 숫자로 표시되어 코드에서는 괜찮아 보이지만, Excel과 동일한 서식을 기대하는 UI에 붙여넣을 때는 문제가 됩니다.

---

## 단계 3 – 내보낸 데이터 출력 (검증)

이제 `DataTable`에 서식이 적용된 문자열이 가득하므로, 콘솔에 내용을 덤프해 보겠습니다. 이를 통해 **수식 결과 가져오기**가 수식을 직접 평가하지 않아도 정상적으로 동작함을 확인할 수 있습니다.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

프로그램을 실행하면 다음과 같이 출력됩니다:

```
123.456 | 246.912
```

두 번째 열이 **수식 결과**를 보여주고, 수식 텍스트가 아니라는 점에 주목하세요. 이것이 **서식이 적용된 Excel 내보내기**를 할 때 필요한 정확한 동작입니다.

---

## 단계 4 – 큰 Excel 범위 변환 (선택 사항)

위 예제는 작은 `A1:B1` 영역만 다루지만, 실제 상황에서는 전체 테이블을 내보내야 할 때가 많습니다. 동일한 메서드는 어떤 직사각형 블록에도 적용할 수 있으며, `firstRow`, `firstColumn`, `totalRows`, `totalColumns` 인자를 적절히 조정하면 됩니다.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro tip:** 시트에 이미 헤더 행이 있다면 `includeColumnNames` 를 `true` 로 설정하세요. Aspose.Cells는 해당 범위의 첫 번째 행을 열 이름으로 사용하므로, 이후 `DataTable` 을 UI 그리드에 바인딩할 때 편리합니다.

---

## 단계 5 – 일반적인 함정 및 회피 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Numbers lose commas or currency symbols** | `ExportAsString` 이 `false` 이거나 `ExportNumberFormat` 이 누락됨 | `ExportAsString = true` **와** `ExportNumberFormat = true` 를 모두 설정합니다. |
| **Formula cells return the formula text** | 워크북이 자동 계산으로 설정되지 않은 경우 내보내기 전에 `CalculateFormula` 를 호출하지 않음 | 자동 계산을 활성화(`workbook.CalculateFormula()`)하거나 `ExportAsString` 을 사용해 강제로 평가하도록 합니다. |
| **Headers appear as data rows** | 범위에 헤더 행이 포함되어 있음에도 `includeColumnNames` 가 `false` 로 설정됨 | 첫 번째 행을 열 이름으로 취급하려면 `includeColumnNames = true` 로 설정합니다. |
| **Large ranges cause memory pressure** | 전체 시트를 한 번에 내보내면 메모리에 모두 로드됨 | 500행씩 등 작은 청크로 나누어 내보내고 필요 시 `DataTable` 을 병합합니다. |

---

## 단계 6 – 전체 작업 예제 (복사‑붙여넣기 준비)

아래는 `using` 구문부터 `Main` 메서드까지 포함한 전체 프로그램입니다. 콘솔 앱에 붙여넣고 **F5** 키를 눌러 실행하면 서식이 적용된 출력이 즉시 표시됩니다.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Expected output**

```
123.456 | 246.912

Press any key to exit...
```

이것이 **Excel을 내보내는 방법** 전체 흐름이며, 서식이 유지되고 수식 결과가 평가된 상태의 깔끔한 `DataTable` 을 어떤 .NET 소비자도 사용할 수 있게 제공합니다.

---

## 결론

우리는 **Excel을 내보내는 방법**에 대해 **숫자 서식 유지**, **Excel 범위를 `DataTable` 로 변환**, 그리고 **수식 결과 가져오기**를 별도 파싱 없이 수행하는 전체 과정을 다루었습니다. 핵심은 `ExportTableOptions` 설정이며, `ExportAsString` 과 `ExportNumberFormat` 을 `true` 로 지정하면 Aspose.Cells가 모든 복잡한 작업을 대신 처리합니다.

이제 다음과 같이 활용할 수 있습니다:

- `DataTable` 을 WPF `DataGrid` 나 ASP.NET MVC 뷰에 연결
- 정확한 시각적 표현을 유지하면서 CSV 파일로 저장
- 여러 시트 또는 동적 범위에 대해 동일한 접근 방식 확장

다양한 서식(통화, 백분율)과 더 큰 데이터 블록을 실험해 보세요. 문제가 발생하면 **일반적인 함정** 표를 다시 참고하십시오 – **서식이 적용된 Excel 내보내기** 시 가장 흔히 겪는 문제들을 정리했습니다.

행복한 코딩 되시길 바라며, 내보낸 스프레드시트가 원본만큼 깔끔하게 보이길 바랍니다!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}