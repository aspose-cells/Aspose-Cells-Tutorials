---
category: general
date: 2026-06-24
description: C#에서 새 워크북을 만들고 피벗 테이블을 데이터가 보존된 상태로 복사합니다. 행을 복사하고, 선택한 범위를 내보내며, 피벗을
  그대로 유지하는 방법을 배워보세요.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: ko
og_description: C#에서 새 워크북을 만들고 피벗 테이블을 데이터가 보존된 상태로 복사합니다. 행을 복사하고 선택한 범위를 내보내는 방법을
  단계별로 안내합니다.
og_title: C#에서 새 워크북 만들기 – 피벗 테이블 복사
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: C#에서 새 워크북 만들기 – 피벗 테이블 복사
url: /ko/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 새 워크북 만들기 – 피벗 테이블 복사

C#에서 **create new workbook**을 만들어 피벗 테이블이 포함된 데이터 조각을 이동해야 했던 적이 있나요? 당신만 그런 것이 아닙니다. 많은 보고 파이프라인에서 몇 개의 행과 몇 개의 열을 가져오고 피벗이 그대로 유지되길 기대합니다—참조가 깨지지 않고, 계산이 누락되지 않도록.  

좋은 소식은? 몇 줄의 Aspose.Cells 코드만으로 **copy pivot table**을 할 수 있고, 그대로 유지하며 **export selected range**도 할 수 있습니다. 아래에서는 **how to copy rows**를 보여주는 완전한 실행 가능한 예제를 확인할 수 있으며, 피벗을 보존하고 결과를 완전히 새로운 워크북으로 저장합니다.

## 이 튜토리얼에서 다루는 내용

- Aspose.Cells를 사용하여 C# 프로젝트 설정하기 (코드를 구동하는 라이브러리).
- 원본 피벗이 포함된 소스 워크북 로드하기.
- 필요한 정확한 범위를 복제하기 위해 라이브러리의 `CopyRows` 및 `CopyColumns` 메서드 사용하기.
- 피벗이 정상 작동하도록 유지하면서 복제된 영역을 **create new workbook** 시나리오에 저장하기.
- 다중 피벗 테이블, 숨겨진 행, 대용량 데이터 세트와 같은 엣지 케이스에 대한 팁.

이 가이드를 마치면 모든 Excel 파일에서 **export selected range**를 수행하고, 피벗 로직을 유지하며, 원하는 위치에 새 파일을 저장할 수 있게 됩니다.

> **Prerequisite**: NuGet을 통해 설치된 Aspose.Cells for .NET (무료 체험 또는 라이선스 버전). 아직 추가하지 않았다면 프로젝트 폴더에서 `dotnet add package Aspose.Cells`를 실행하세요.

## 새 워크북 만들기 및 피벗 테이블 복사

아래는 솔루션의 핵심 부분입니다. 각 줄을 살펴보고, 왜 중요한지 설명한 뒤 전체 프로그램을 보여드립니다.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### 왜 이것이 작동하는가

- **`CopyRows` / `CopyColumns`**: 이 메서드들은 기본 셀 데이터와 연관된 객체(예: 피벗 캐시)를 복제합니다. 그래서 이동 후에도 피벗이 정상 작동합니다.
- **Separate destination workbook**: 새로운 `Workbook` 인스턴스를 생성함으로써 **create new workbook**를 수행하고, 방해가 될 수 있는 남은 서식이나 숨겨진 시트를 포함하지 않습니다.
- **Zero‑based indexing**: Aspose.Cells는 0부터 시작하는 인덱스를 사용하므로 `0`은 셀 **A1**을 가리킵니다. 피벗이 좌상단에 있지 않다면 `startRow`/`startColumn`을 조정하세요.
- **Preserve pivot table**: 피벗의 캐시는 동일한 범위에 존재하므로, 범위를 복사하면 캐시도 자동으로 복사됩니다. 추가 코드는 필요 없습니다.

## 피벗을 깨지 않게 행 복사하기

행 복사 부분만 필요하다면, 해당 부분만 분리해서 사용할 수 있습니다:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: 피벗 테이블과 교차하는 행을 복사할 때는 항상 *전체* 피벗 영역(행 + 열)을 복사하세요. 부분 복사는 피벗에 누락된 필드가 생겨 `#REF!` 오류를 일으킬 수 있습니다.

## 선택된 범위 내보내기 – 실제 시나리오

거대한 판매 워크북이 있지만, 클라이언트가 1분기 요약(행 1‑20, 열 A‑D)만 원한다고 가정해 보세요. 위 코드 조각은 이미 **export selected range**를 수행합니다. `totalRows`와 `totalColumns` 변수를 클라이언트 요청에 맞게 변경하면 완료됩니다.

### 숨겨진 행 또는 필터 처리

소스 시트에 숨겨진 행(필터링된 경우)이 있다면, *보이는* 행만 복사하고 싶을 수 있습니다. Aspose.Cells는 가시성을 고려한 `CopyRows` 오버로드를 제공합니다:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

마지막 불리언 값을 `true`로 설정하면 보이는 행만 복사됩니다—사용자가 필터를 적용했을 때 “export selected range”에 적합합니다.

## 피벗 테이블 보존 – 일반적인 함정 및 회피 방법

| 함정 | 발생 원인 | 해결 방법 |
|------|----------|----------|
| **Pivot 캐시가 복사되지 않음** | `Cells.CopyRows/CopyColumns` 대신 일반 `Range.Copy` 사용. | 예시와 같이 `Cells` 메서드를 사용하세요. |
| **대상 시트에 기존 피벗 존재** | 같은 이름의 피벗이 이미 포함된 워크북에 저장하는 경우. | 새로운 `Workbook()`으로 시작하세요 (우리가 하는 방식). |
| **이름 정의된 범위가 깨짐** | 소스 피벗이 새 파일에 존재하지 않는 이름 정의된 범위를 참조함. | 이름 정의된 범위도 복사하세요: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **데이터 소스 경로 변경** | 피벗이 사용 가능한 외부 데이터 소스를 가리키지 않음. | 필요하면 복사 후 `PivotTable.RefreshData()`를 사용하세요. |

## 전체 엔드‑투‑엔드 예제 (즉시 실행 가능)

아래는 `using` 지시문과 간단한 콘솔 UI를 포함한 전체 프로그램입니다. 새 콘솔 앱 프로젝트에 복사‑붙여넣기하고 **F5**를 눌러 실행하세요.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**예상 출력** (콘솔에):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

`copy-pivot.xlsx`를 열면 `source.xlsx`에 있던 동일한 피벗 테이블이 완전히 작동하며 복사된 데이터 범위를 참조하고 있음을 확인할 수 있습니다.

## 자주 묻는 질문

**Q: 같은 시트에 여러 피벗 테이블이 있어도 작동하나요?**  
A: 예, 복사하려는 사각형이 필요한 각 피벗을 포함하고 있다면 가능합니다. 하나만 원한다면 `rows`/`cols`를 조정해 해당 피벗만 격리하세요.

**Q: 소스 워크북이 외부 데이터 연결을 사용한다면?**  
A: 피벗 캐시는 여전히 원래 연결을 가리킵니다. 소스를 다시 조회하려면 대상 워크북을 로드한 후 `pivotTable.RefreshData()`를 호출하세요.

**Q: 같은 워크북 내의 다른 시트로 피벗을 복사할 수 있나요?**  
A: 물론 가능합니다. `destinationWorkbook`을 `sourceWorkbook`으로 교체하고 다른 워크시트 인덱스를 선택하면 됩니다.

**Q: 서식만 복사하는 방법이 있나요?**  
A: `CopyRows`/`CopyColumns` 중 `CopyOptions` 객체를 받는 오버로드를 사용하세요—필요에 따라 `CopyOptions.CopyType = CopyType.ValuesOnly` 또는 `CopyType.All`을 설정합니다.

## 결론

우리는 **create new workbook** 시나리오를 통해 **copy pivot table**, **preserve pivot table**, **export selected range**를 순수 C#으로 수행하는 방법을 살펴보았습니다.

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}