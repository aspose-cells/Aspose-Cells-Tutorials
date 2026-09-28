---
category: general
date: 2026-09-27
description: C#에서 Excel 테이블의 행을 삭제하는 방법을 단계별 가이드와 함께 배우고, Excel 워크북을 C#에서 빠르게 로드하는
  방법도 확인하세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: ko
lastmod: 2026-09-27
og_description: 명확한 예시와 함께 C#에서 Excel 테이블의 행을 삭제합니다. 이 튜토리얼에서는 C#으로 Excel 워크북을 로드하는
  방법과 일반적인 엣지 케이스를 처리하는 방법도 다룹니다.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: C#에서 Excel 테이블 행 삭제 – 완전한 코드 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: C#를 사용하여 Excel 테이블에서 행 삭제하는 방법
url: /ko/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 Excel 테이블 행 삭제 – 완전 프로그래밍 가이드

.xlsx 파일에서 **Excel 테이블의 행을 삭제**해야 하는 경우, 이 튜토리얼에서는 C#를 사용하여 정확히 수행하는 방법을 보여줍니다. Excel 워크북을 로드하고, 첫 번째 테이블에서 특정 행을 제거한 뒤 결과를 저장하는 간결하고 실행 가능한 예제를 확인할 수 있습니다. 이 접근 방식은 널리 사용되는 Aspose.Cells 라이브러리와 함께 작동하며 다른 .NET Excel API에도 적용할 수 있습니다.

테이블에서 행을 제거하는 것은 가져온 데이터를 정리하거나, 보고서 섹션을 다듬거나, 스프레드시트 업데이트를 자동화할 때 흔히 수행되는 작업입니다. 이 가이드를 끝까지 따라오면 **C#에서 Excel 워크북 로드**하고, 테이블(ListObject)을 찾은 뒤 원하는 행을 삭제하고, 수정된 파일을 디스크에 다시 쓸 수 있게 됩니다.

## 사전 요구 사항

* .NET 6.0 이상이 설치되어 있어야 합니다 (코드는 .NET Framework 4.7+에서도 작동합니다).
* **Aspose.Cells** NuGet 패키지에 대한 참조가 필요합니다 (또는 `Workbook`, `Worksheet`, `ListObject` 타입을 제공하는 호환 라이브러리).
* `input.xlsx` 라는 이름의 입력 파일을 프로젝트에서 참조할 수 있는 폴더에 배치합니다.
* C# 구문과 Visual Studio(또는 선호하는 IDE)에 대한 기본적인 이해가 필요합니다.

> **팁:** 오픈소스 대안을 선호한다면, 동일한 로직을 **ClosedXML**로 적용할 수 있습니다 – Aspose 전용 클래스를 `XLWorkbook`, `IXLWorksheet`, `IXLTable` 로 교체하면 됩니다.

## Step 1: C#에서 Excel 워크북 로드

첫 번째 작업은 소스 파일을 메모리로 읽는 것입니다. 일반적인 스프레드시트 크기에서는 워크북 로드가 비용이 적으며, 워크시트, 테이블 및 셀 값에 대한 전체 접근 권한을 제공합니다.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*왜 중요한가:* `Workbook`은 .xlsx 파일의 Open XML 구조를 파싱하여 `Worksheet` 객체 컬렉션을 노출합니다. 파일을 찾을 수 없으면 Aspose가 `FileNotFoundException`을 발생시키므로 경로가 올바른지 확인하세요.

## Step 2: 대상 워크시트 접근

대부분의 스프레드시트는 여러 시트를 포함합니다; 수정하려는 테이블이 있는 시트를 선택해야 합니다. 여기서는 첫 번째 시트(`Worksheets[0]`)를 사용합니다. 이는 간단한 파일에 안전한 기본값입니다.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*왜 중요한가:* `Worksheet`은 테이블(`ListObjects`)의 컨테이너입니다. 올바른 시트를 접근함으로써 무관한 데이터에 대한 실수로 인한 변경을 방지합니다.

## Step 3: Excel 테이블에서 행 삭제

Excel 테이블은 `ListObject` 객체로 표현됩니다. 시트의 첫 번째 테이블은 `ListObjects[0]`입니다. `DeleteRows(startIndex, rowCount)` 메서드는 워크시트의 절대 행 번호가 아니라 **테이블 데이터 영역을 기준**으로 행을 제거합니다.  

이 예제에서는 테이블의 두 번째와 세 번째 행을 삭제합니다(헤더가 행 0이므로 인덱스 1부터 시작).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### 테이블 이름이나 위치가 다르면 어떻게 하나요?

* **명명된 테이블:** 인덱스 대신 `ws.ListObjects["MyTableName"]`를 사용합니다.
* **다중 테이블:** `ws.ListObjects`를 순회하며 조건에 맞는 테이블을 선택합니다(예: 열 헤더 이름).
* **동적 행 수:** `ws.ListObjects[0].DataRange.RowCount`를 검사하여 런타임에 `rowCount`를 계산할 수 있습니다.

### 경계 상황 처리

| 상황                                   | 권장 코드 변경                                                |
|----------------------------------------|--------------------------------------------------------------|
| 테이블이 비어 있거나 행이 부족한 경우   | 삭제하기 전에 `ws.ListObjects[0].DataRange.RowCount`를 확인합니다. |
| 삭제하려는 행 수가 테이블 크기를 초과하는 경우 | `rowCount`를 `DataRange.RowCount - startIndex`로 제한합니다. |
| 조건에 따라 행을 삭제해야 하는 경우(예: C 열의 값) | `DataRange.Rows`를 순회하며 일치하는 인덱스를 수집한 뒤 인덱스를 안정적으로 유지하기 위해 역순으로 삭제합니다. |

## Step 4: 수정된 워크북 저장

삭제가 끝난 후, 워크북을 새 파일에 기록합니다(또는 원본을 덮어쓰고 싶다면 그렇게 할 수도 있습니다). 저장하면 업데이트된 테이블을 반영하는 새로운 .xlsx 파일이 생성됩니다.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*왜 중요한가:* `Save`는 메모리 상의 표현을 디스크에 직렬화합니다. 원본 파일을 보존해야 한다면 항상 다른 경로에 기록하세요.

## 전체 실행 가능한 예제

모든 단계를 합치면 복사·붙여넣기·실행이 가능한 독립형 프로그램이 됩니다.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**예상 출력** (콘솔):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

`output.xlsx`를 열면 첫 번째 테이블에서 삭제한 행이 사라지고, 헤더 행은 그대로 유지됩니다.

## 일반적인 질문 및 변형

### 워크북의 **모든** 테이블에서 행을 삭제하려면?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### **셀 값**을 기준으로 행을 삭제할 수 있나요?

예. `DataRange`를 스캔하여 일치하는 셀을 찾고, 해당 0 기반 인덱스를 수집한 뒤 내림차순으로 삭제합니다:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### **서식 유지**가 필요하면 어떻게 하나요?

`DeleteRows`는 테이블에서 전체 행을 제거하지만, 남은 행에 대해서는 테이블 스타일을 유지합니다. 삭제하려는 행에 특정 서식을 유지해야 한다면, 삭제 전에 해당 서식을 다른 행에 복사하세요.

### **.xls**(Excel 97‑2003) 파일에서도 작동하나요?

예. Aspose.Cells는 파일 형식을 자동으로 감지하므로 동일한 코드가 `.xls`에서도 작동합니다. `Workbook` 생성자에서 파일 확장자를 `.xls`로 바꾸기만 하면 됩니다.

## 성능 팁

* **배치 삭제:** 여러 행을 하나씩 삭제하면 느릴 수 있습니다. 가능하면 단일 `DeleteRows(start, count)` 호출을 사용하세요.
* **UI 스레드 차단 방지:** 데스크톱 앱에 통합할 경우, 워크북 조작을 백그라운드 스레드에서 실행해 UI가 응답하도록 유지하세요.
* **적절한 해제:** Aspose.Cells는 관리 메모리를 사용하지만, 큰 파일을 다룰 때는 `Workbook`을 `using` 블록으로 감싸서 리소스를 즉시 해제하세요.

## 결론

이제 C#를 사용하여 **Excel 테이블의 행을 삭제**하는 완전하고 프로덕션 수준의 예제가 준비되었습니다. 이 가이드는 **C#에서 Excel 워크북 로드**, 원하는 `ListObject` 찾기, 안전하게 행 삭제, 그리고 업데이트된 파일 저장 방법을 다루었습니다. 경계 상황 처리와 성능 조언을 포함했으므로 조건부 삭제, 다중 테이블, 또는 대체 .NET Excel 라이브러리와 같은 복잡한 시나리오에도 이 패턴을 적용할 수 있습니다.

### 다음 단계

* 완전한 오픈소스 스택을 원한다면 **ClosedXML** 또는 **EPPlus**를 탐색해 보세요.
* 행 삭제를 **데이터 검증**과 결합하여 데이터베이스에 가져오기 전에 스프레드시트를 정리하세요.
* `Directory.GetFiles`와 루프를 사용해 워크북 폴더 전체에 대해 자동화하세요.

다양한 행 범위, 테이블 이름 및 조건부 로직을 자유롭게 실험해 보세요. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 동작 코드 예제를 제공하여 추가 API 기능을 숙달하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Excel 파일 로드 C# – 행 삭제 및 특정 행 제거 방법](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Aspose.Cells for .NET를 사용한 Excel 행 삽입 및 삭제 방법: 종합 가이드](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Aspose.Cells .NET를 사용한 Excel 빈 행 삭제 방법 – 데이터 정리](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}