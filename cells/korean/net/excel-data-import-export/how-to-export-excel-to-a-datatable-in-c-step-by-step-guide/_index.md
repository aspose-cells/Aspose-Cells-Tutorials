---
category: general
date: 2026-03-18
description: C#에서 특정 셀을 처리하고 Excel을 DataTable로 변환하며 숫자를 포맷하는 코드를 사용하여 Excel 데이터를 DataTable로
  내보내는 방법. 특정 셀 내보내기 및 기타 기능을 배워보세요.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: ko
og_description: C#에서 Excel 데이터를 DataTable로 내보내는 방법. 이 튜토리얼에서는 특정 셀을 내보내고, Excel을 DataTable로
  변환하며, 숫자를 쉽게 포맷하는 방법을 보여줍니다.
og_title: C#에서 Excel을 DataTable로 내보내는 방법 – 완전 가이드
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C#에서 Excel을 DataTable로 내보내는 방법 – 단계별 가이드
url: /ko/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel을 DataTable로 내보내는 방법 (C#) – 단계별 가이드

Excel 데이터를 서식 손실 없이 `DataTable`로 **내보내는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다—개발자들은 보고서 작성, 검증, 대량 삽입 작업 등을 위해 스프레드시트의 일부를 메모리로 가져와야 합니다. 좋은 소식은? 몇 줄의 C# 코드만으로 정확한 범위(예: *A1:F11*)를 내보내고, 모든 셀을 문자열로 처리하도록 강제하며, 사용자 정의 숫자 서식도 적용할 수 있다는 것입니다.

이 튜토리얼에서는 워크북 로드, **특정 셀 내보내기** 구성, 범위를 `DataTable`로 변환, 빈 행이나 로케일에 따라 달라지는 숫자와 같은 엣지 케이스 처리 등 알아야 할 모든 내용을 다룹니다. 끝까지 읽으면 프로덕션 코드에서 **excel to datatable c#** 시나리오에 사용할 수 있는 재사용 가능한 메서드를 얻게 됩니다.

> **전제 조건** – Aspose.Cells for .NET 라이브러리(또는 `ExportDataTable`을 제공하는 유사 API)가 필요합니다. 예제는 .NET 6+를 가정하지만, 개념은 이전 버전에도 적용됩니다.

---

## 배울 내용

- Aspose.Cells를 사용하여 **Excel을 DataTable로 변환**하는 방법.
- 모든 값을 문자열로 처리하면서 사용자 정의 범위(`excel range to datatable`)를 내보내기.
- 내보내기 시 두 자리 소수점 숫자 서식(`#,#00.00`) 적용하기.
- 일반적인 함정(null 행, 숨겨진 열)과 회피 방법.
- 바로 복사해서 실행할 수 있는 완전한 코드 샘플.

## 사전 요구 사항 및 설정

코드에 들어가기 전에 다음이 준비되어 있는지 확인하세요:

1. NuGet을 통해 **Aspose.Cells for .NET**을 설치:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. `input.xlsx`라는 Excel 파일을 참조 가능한 폴더에 배치합니다. 예: `YOUR_DIRECTORY/input.xlsx`.
3. .NET 6 이상을 타깃으로 하는 프로젝트(아래 `using` 문은 바로 사용할 수 있습니다).

> **전문가 팁:** 다른 라이브러리(예: EPPlus 또는 ClosedXML)를 사용하더라도 개념은 동일합니다—워크북을 로드하고, 범위를 선택한 뒤 `DataTable`을 반환하는 메서드를 호출하면 됩니다.

## 단계 1: 워크북 로드 및 첫 번째 워크시트 가져오기

먼저 Excel 파일을 나타내는 `Workbook` 객체가 필요합니다. 이를 얻으면 인덱스나 이름으로 원하는 워크시트에 접근할 수 있습니다.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**왜 중요한가:** 워크북을 미리 로드하면 내보낼 셀을 결정하기 전에 구조(숨겨진 시트, 보호 등)를 검사할 수 있습니다. 파일이 크면 `LoadOptions`를 사용해 필요한 부분만 스트리밍하는 것을 고려하세요.

## 단계 2: 내보내기 옵션 구성 – 모든 값을 문자열로 처리

데이터를 하위 처리(예: SQL에 대량 삽입)용으로 내보낼 때는 **일관된 문자열 표현**을 원할 때가 많습니다. 이렇게 하면 이후 타입 불일치 오류를 방지할 수 있습니다.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**설명:**  
- `ExportAsString = true`는 Aspose.Cells에 원본 셀 타입을 무시하고 포맷된 텍스트를 반환하도록 지시합니다.  
- `NumberFormat = "#,##0.00"`은 `1234.5`와 같은 숫자를 `"1,234.50"`으로 변환해 줍니다—재무 보고서에 유용합니다.

원본 데이터 타입이 필요하면 `ExportAsString`을 `false`로 설정하고 직접 변환하면 됩니다.

## 단계 3: 특정 범위(A1:F11)를 DataTable로 내보내기

이제 **특정 셀 내보내기**의 핵심 단계입니다. `ExportDataTable` 메서드는 시작/끝 행/열 인덱스(0부터 시작)와 헤더 포함 여부 플래그를 받습니다.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**결과:** 헤더를 포함해 11행, 6열(`A`‑`F`)을 가진 `DataTable`이 생성됩니다. 모든 값은 `exportOptions`에 지정된 문자열 형식으로 반환됩니다.

## 단계 4: 결과 확인 – 콘솔에 출력

다른 컴포넌트에 테이블을 전달하기 전에 출력 결과를 검증하는 것이 좋습니다.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

다음과 같은 결과가 표시될 것입니다:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

숫자 열이 두 자리 소수점으로 표시되는 것을 확인하세요. 우리가 지정한 대로입니다.

## 전체 작동 예제 (복사‑붙여넣기 준비 완료)

아래는 모든 과정을 하나로 묶은 완전한 프로그램입니다. 새 콘솔 프로젝트에 붙여넣고 파일 경로만 수정한 뒤 실행하면—추가 설정이 필요 없습니다.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**코드에서 얻을 수 있는 주요 포인트:**

- `ExportTableOptions` 객체는 재사용 가능하며, 여러 범위를 내보낼 때 여러 `ExportDataTable` 호출에 전달할 수 있습니다.
- 인덱스는 **0**부터 시작하므로 `A1`은 `(0,0)`에 해당합니다.
- `includeColumnNames`를 `true`로 설정하면 첫 번째 행이 자동으로 컬럼 헤더로 사용됩니다—하위 `DataTable` 작업에 유용합니다.

## 엣지 케이스 처리 및 흔한 질문

### 워크시트에 숨겨진 행이나 열이 있으면 어떻게 하나요?

Aspose.Cells는 기본적으로 가시성을 존중합니다. 숨겨진 데이터를 내보내려면 `exportOptions.ExportHiddenRows = true`와 `ExportHiddenColumns = true`를 설정하세요.

### Excel 파일에 수식이 포함되어 있는데, 계산된 값이 나오나요?

예. 기본적으로 `ExportDataTable`은 **표시된 값**(수식 결과)을 반환합니다. 원본 수식 텍스트가 필요하면 `exportOptions.ExportFormulas = true`로 설정하세요.

### 완전히 빈 행은 어떻게 건너뛰나요?

내보낸 후 `DataTable`을 정리할 수 있습니다:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### 비연속 범위(예: A1:B5와 D1:E5)를 내보낼 수 있나요?

Aspose.Cells는 단일 호출에서 비연속 범위를 지원하지 않습니다. 대신 각 블록을 별도로 내보낸 뒤 결과 `DataTable`을 수동으로 병합해야 합니다.

## 성능 팁

- 여러 번 내보낼 때는 **`ExportTableOptions`를 재사용**하세요; 매번 새 인스턴스를 만들면 오버헤드는 미미하지만 코드가 복잡해집니다.
- `LoadOptions`를 사용해 **대용량 파일을 스트리밍**하면 전체 워크북을 메모리에 로드하는 것을 피할 수 있습니다.
- 빠른 CSV 내보내기만 필요하다면 **`DataTable` 사용을 피**하세요—`ExportDataTable`은 편리하지만 대규모 시트에서는 메모리 효율이 떨어집니다.

## 결론

우리는 **Excel 데이터를 `DataTable`로 내보내는 방법**을 서식 제어, 특정 셀 범위 처리, 모든 값을 문자열로 받도록 보장하는 과정을 살펴보았습니다. 전체 예제는 **convert excel to datatable**, **export specific cells**, 혹은 **excel range to datatable**와 같은 시나리오에 적용할 수 있는 깔끔하고 프로덕션 수준의 접근 방식을 보여줍니다.

범위를 바꾸거나 `ExportAsString`을 토글하거나 `DataTable`을 바로 Entity Framework에 전달해 대량 삽입을 시도해 보세요. 탄탄한 기반만 있으면 가능성은 무한합니다.

### 다음 단계 및 관련 주제

- **DataTable을 Excel로 다시 가져오기** – `ImportDataTable`을 사용한 역작업을 배웁니다.
- **DataTable을 SQL Server에 대량 삽입** – `SqlBulkCopy`를 이용해 초고속 로드를 수행합니다.
- **EPPlus 또는 ClosedXML 사용** – 대체 라이브러리로 동일 작업을 수행하는 방법을 살펴봅니다.
- **내보내기 시 셀 서식 지정** – 날짜 형식, 사용자 정의 문화 설정 등 `ExportTableOptions`를 더 탐색합니다.

질문이나 다른 사용 사례가 있나요? 댓글을 남겨 주세요. 계속 이야기를 이어가요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}