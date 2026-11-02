---
category: general
date: 2026-10-10
description: C#를 사용하여 Excel 워크북에서 전체 행을 삭제하는 방법을 배웁니다. 이 단계별 가이드에서는 인덱스로 행을 삭제하고 Aspose.Cells를
  사용하여 인덱스로 행을 제거하는 방법도 다룹니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: ko
lastmod: 2026-10-10
og_description: C#를 사용하여 Excel 워크북에서 전체 행을 삭제합니다. 이 가이드를 따라 인덱스로 행을 삭제하고, 인덱스로 행을
  제거하며, 파일을 안전하게 저장하는 방법을 배워보세요.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: C#로 Excel에서 전체 행 삭제 – 완전한 프로그래밍 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: C#를 사용하여 Excel 파일에서 전체 행을 삭제하는 방법
url: /ko/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#를 사용하여 Excel 파일에서 전체 행 삭제

If you need to **delete entire row** in an Excel workbook, this guide shows you exactly how to do it with C#. Whether you are cleaning up imported data or building a reporting tool, the steps below let you remove a row by its index and save the result without losing other data.

Excel 워크북에서 **전체 행을 삭제**해야 하는 경우, 이 가이드는 C#로 정확히 수행하는 방법을 보여줍니다. 가져온 데이터를 정리하거나 보고 도구를 구축할 때, 아래 단계들을 통해 인덱스로 행을 제거하고 다른 데이터를 잃지 않으면서 결과를 저장할 수 있습니다.

You’ll also see how the same approach answers the question **how to delete row** by index, how to **remove row by index**, and why this works for **delete row excel** scenarios in C#.

또한 동일한 접근 방식이 인덱스로 **행을 삭제하는 방법**(how to delete row), **인덱스로 행을 제거하는 방법**(remove row by index)이라는 질문에 어떻게 답하는지, 그리고 C#에서 **delete row excel** 시나리오에 왜 적용되는지 확인할 수 있습니다.

## 사전 요구 사항

Before you start, make sure you have:

* .NET 6.0 이상 (코드는 .NET Framework 4.6+에서도 작동합니다)  
* The **Aspose.Cells for .NET** library (available via NuGet: `Install-Package Aspose.Cells`)  
* Basic familiarity with C# console or desktop projects  

추가적인 Excel 인터옵이나 COM 구성 요소가 필요하지 않아 솔루션이 가볍고 서버 측 실행에 안전합니다.

## 단계 1: 프로젝트 설정 및 네임스페이스 가져오기

Create a new console application (or add the code to an existing project) and add the required `using` directives:

새 콘솔 애플리케이션을 생성하고(또는 기존 프로젝트에 코드를 추가하고) 필요한 `using` 지시문을 추가합니다:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Why this matters*: Importing `Aspose.Cells` gives you access to `Workbook`, `Worksheet`, and the `DeleteRows` method that performs the actual row removal.

*Why this matters*: `Aspose.Cells`를 가져오면 `Workbook`, `Worksheet`, 그리고 실제 행 제거를 수행하는 `DeleteRows` 메서드에 접근할 수 있습니다.

## 단계 2: 워크북 로드 및 워크시트 선택

You must load the source file (`input.xlsx`) and obtain the worksheet you want to modify. The first worksheet is accessed with index `0`.

소스 파일(`input.xlsx`)을 로드하고 수정하려는 워크시트를 가져와야 합니다. 첫 번째 워크시트는 인덱스 `0`으로 접근합니다.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tip**: 특정 시트에서 작업해야 하는 경우, 인덱스를 시트 이름으로 교체하세요: `workbook.Worksheets["Data"]`.

## 단계 3: 0 기반 인덱스로 전체 행 삭제

Aspose.Cells uses zero‑based indexing, so the first row is `0`. To delete row 5 (the sixth visual row), call `DeleteRows` with `DeleteOptions.DeleteEntireRow`.

Aspose.Cells는 0 기반 인덱스를 사용하므로 첫 번째 행은 `0`입니다. 시각적으로 6번째 행인 row 5를 삭제하려면 `DeleteRows`에 `DeleteOptions.DeleteEntireRow`를 전달합니다.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*설명*:

* `ws.Cells[5, 0]`은 삭제하려는 행의 첫 번째 셀을 가리킵니다.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)`는 Aspose.Cells에 **1**개의 행을 제거하도록 지시하며, `DeleteEntireRow` 플래그는 **전체 행**이 사라지고 아래 행이 위로 이동하도록 보장합니다.

### 다른 시나리오에서 인덱스로 행 삭제 방법

* **연속된 여러 행 삭제** – 첫 번째 인수를 삭제하려는 행 수로 변경합니다:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **마지막 행 삭제** – `ws.Cells.MaxDataRow`를 사용하여 가장 아래에 데이터가 있는 행의 인덱스를 가져옵니다:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

These snippets answer the **remove row by index** requirement while keeping the code easy to read.

이 스니펫들은 코드를 읽기 쉽게 유지하면서 **remove row by index** 요구 사항을 충족합니다.

## 단계 4: 행이 제거된 워크북 저장

After the deletion, write the modified workbook back to disk. You can overwrite the original file or create a new one.

삭제 후, 수정된 워크북을 디스크에 다시 씁니다. 원본 파일을 덮어쓰거나 새 파일을 만들 수 있습니다.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

If you need to keep the original file unchanged, simply change the output path. The `Save` method supports many formats (`.xls`, `.csv`, `.pdf`, etc.) – just change the file extension.

원본 파일을 그대로 두어야 하면 출력 경로만 변경하면 됩니다. `Save` 메서드는 다양한 형식(`.xls`, `.csv`, `.pdf` 등)을 지원하므로 파일 확장자를 바꾸면 됩니다.

## 전체 작동 예제

Putting everything together, here is a complete, ready‑to‑run program:

모든 내용을 합치면, 다음은 완전하고 바로 실행 가능한 프로그램입니다:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**예상 출력**: After running the program, `output.xlsx` will contain all original rows except the one that started at visual row 6. All data below the removed row shifts up automatically, preserving formulas and formatting.

**예상 출력**: 프로그램을 실행하면 `output.xlsx`에 시각적으로 6번째 행에 해당하는 행을 제외한 모든 원본 행이 포함됩니다. 제거된 행 아래의 모든 데이터가 자동으로 위로 이동하여 수식과 서식이 유지됩니다.

## 일반적인 함정 및 회피 방법

| 문제 | 발생 원인 | 해결 방법 |
|-------|----------------|-----|
| **인덱스 범위 초과** | 존재하지 않는 행 인덱스를 삭제하려고 할 때 발생합니다(예: 200행 시트에서 `ws.Cells[1000,0]`). | `DeleteRows`를 호출하기 전에 `ws.Cells.MaxDataRow`를 사용하여 가장 높은 유효 인덱스를 확인합니다. |
| **부분 행 삭제** | `DeleteOptions.DeleteEntireRow`를 생략하면 셀 내용만 지워집니다. | 전체 행을 삭제해야 할 경우 항상 `DeleteOptions.DeleteEntireRow`를 전달하세요. |
| **예상치 못한 수식 변경** | 수식 범위에 포함된 행을 삭제하면 참조가 깨질 수 있습니다. | 워크북이 동적 범위에 의존한다면 삭제 후 수식을 다시 계산합니다(`workbook.CalculateFormula()`). |
| **읽기 전용 위치에 저장** | 폴더가 보호되어 있으면 `Save` 호출 시 예외가 발생합니다. | 대상 디렉터리가 쓰기 가능한지 확인하거나 적절한 권한으로 프로그램을 실행하세요. |

Addressing these concerns makes the solution robust for production use and satisfies the **delete row excel** and **delete row c#** queries.

이러한 문제들을 해결하면 솔루션이 프로덕션 환경에서도 견고해지고 **delete row excel** 및 **delete row c#** 질문에 답할 수 있습니다.

## 고급: 조건에 따라 행 삭제

Sometimes you need to remove rows that meet a certain criterion (e.g., rows where column A is empty). The following loop demonstrates a safe way to scan from bottom to top and delete matching rows:

때때로 특정 기준을 만족하는 행(예: A 열이 비어 있는 행)을 제거해야 할 때가 있습니다. 다음 루프는 아래에서 위로 스캔하면서 일치하는 행을 삭제하는 안전한 방법을 보여줍니다:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Scanning upward prevents the index shift problem that occurs when deleting rows while iterating forward.

위쪽으로 스캔하면 앞쪽으로 반복하면서 행을 삭제할 때 발생하는 인덱스 이동 문제를 방지할 수 있습니다.

## 결론

You now know how to **delete entire row** in an Excel workbook using C#. The guide covered:

이제 C#를 사용하여 Excel 워크북에서 **전체 행을 삭제**하는 방법을 알게 되었습니다. 가이드에서는 다음을 다루었습니다:

* 워크북 로드 및 워크시트 선택  
* `DeleteRows`와 `DeleteOptions.DeleteEntireRow`를 사용하여 인덱스로 **how to delete row** 수행  
* 수정된 파일을 안전하게 저장  
* 예외 상황 처리, 성능 팁, 조건부 삭제 예제  

With this knowledge you can confidently implement **remove row by index** functionality, automate data clean‑up, and integrate Excel manipulation into any C# application.

이 지식을 통해 **remove row by index** 기능을 자신 있게 구현하고, 데이터 정리를 자동화하며, Excel 조작을 모든 C# 애플리케이션에 통합할 수 있습니다.

**다음 단계**: 행 삽입, 범위 복사, 워크북을 PDF로 변환 등 다른 Aspose.Cells 기능을 탐색하세요—모두 방금 익힌 `Workbook` 및 `Worksheet` 객체를 기반으로 합니다. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료에는 완전한 코드 예제와 단계별 설명이 포함되어 있어 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움이 됩니다.

- [How to Delete an Excel Row Using Aspose.Cells .NET&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}