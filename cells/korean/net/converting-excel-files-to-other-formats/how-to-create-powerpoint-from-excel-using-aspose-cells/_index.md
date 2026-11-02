---
category: general
date: 2026-09-18
description: Aspose.Cells를 사용해 Excel에서 PowerPoint를 생성합니다 – 피벗 테이블을 복사하고, 범위를 내보내며,
  몇 줄의 C# 코드만으로 PPTX로 저장합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: ko
lastmod: 2026-09-18
og_description: Excel에서 빠르게 PowerPoint를 만들세요. 피벗 테이블 복사, 범위 내보내기, 그리고 Aspose.Cells를
  사용해 워크북을 PPTX로 저장하는 방법을 배워보세요.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Aspose.Cells를 사용하여 Excel에서 PowerPoint 만들기 – 단계별 가이드
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Aspose.Cells를 사용하여 Excel에서 PowerPoint를 만드는 방법
url: /ko/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 Excel에서 PowerPoint 만들기

Excel에서 PowerPoint를 만들어야 할 경우, 이 가이드는 간결하고 끝‑까지 진행되는 솔루션을 보여줍니다. 피벗 테이블을 복사하고, 선택한 범위를 내보내며, 몇 줄의 C# 코드만으로 결과를 PPTX 파일로 저장하는 방법을 확인할 수 있습니다.

스프레드시트 데이터에서 직접 슬라이드 덱을 생성하면 보고서 작업 흐름을 늦추는 수동 복사‑붙여넣기 단계를 없앨 수 있습니다. 이 튜토리얼은 프로젝트 설정부터 최종 PPTX 파일까지 필요한 모든 내용을 다루며, 최신 Aspose.Cells for .NET과 함께 작동합니다.

## Prerequisites

시작하기 전에 다음이 준비되어 있는지 확인하세요:

* **Aspose.Cells for .NET** (버전 23.12 이상). NuGet을 통해 설치: `Install-Package Aspose.Cells`.
* **.NET 6+** 개발 환경 (Visual Studio 2022 또는 VS Code 사용 가능).
* 재사용하려는 데이터와 피벗 테이블이 포함된 Excel 워크북 (`Source.xlsx`).
* 출력 폴더에 대한 쓰기 권한.

추가 서드‑파티 라이브러리는 필요하지 않습니다.

## Excel에서 PowerPoint 만들기 – 단계별

이 과정은 아래 네 가지 논리적 단계로 구성되며, 이후에 볼 코드 예제와 직접 연결됩니다.

### Step 1: Load the source workbook and define the range

소스 데이터를 보유하고 있는 워크북을 로드하고, 정확한 범위를 정의해야 합니다. 정확한 범위를 선택하면 필요한 셀만 전송되어 결과 슬라이드가 가벼워집니다.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Why this matters:**  
`CreateRange`는 전체를 복사할 수 있는 `Range` 객체를 생성합니다. 범위를 `A1:G20`으로 제한하면 관련 없는 셀을 가져오지 않게 되어 PowerPoint 파일이 불필요하게 커지는 것을 방지합니다.

### Step 2: Prepare the destination workbook

Aspose.Cells는 PPTX 형식으로 저장할 때 PowerPoint 슬라이드를 워크북으로 취급합니다. 새 워크북을 만들면 복사된 범위를 위한 깨끗한 캔버스를 얻을 수 있습니다.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** 여러 슬라이드가 필요하면 추가 워크시트를 만든 뒤 각각을 별도의 PPTX 파일로 저장하면 됩니다.

### Step 3: Copy the range while preserving the pivot table

`CopyRange` 메서드는 `PasteOptions` 객체를 받습니다. `CopyPivotTables = true` 로 설정하면 Aspose.Cells가 피벗 테이블 구조를 그대로 유지하도록 지시합니다(렌더링된 값만 복사하지 않음).

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**How it works:**  
`CopyPivotTables`가 true이면 대상 시트가 소스 데이터와 피벗 캐시를 모두 받습니다. 따라서 피벗 테이블은 완전하게 기능을 유지하며, 소스 데이터가 변경될 경우 나중에 새로 고칠 수 있습니다.

### Step 4: Save the workbook as a PowerPoint file

마지막으로 워크북을 PPTX 형식으로 내보냅니다. `SaveFormat.Pptx` 플래그는 Aspose.Cells에게 워크시트를 PowerPoint 슬라이드로 기록하도록 지시합니다.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Result:**  
`CopyWithPivot.pptx`를 Microsoft PowerPoint(또는 호환 뷰어)에서 열면 복사된 범위와 함께 라이브 피벗 테이블이 포함된 단일 슬라이드가 표시됩니다. PowerPoint 내에서 피벗 테이블을 직접 상호작용할 수 있습니다.

## Full runnable example

아래는 새 콘솔 프로젝트에 붙여넣고 바로 실행할 수 있는 전체 프로그램입니다.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Expected output:**  
프로그램을 실행하면 “PowerPoint file created successfully.” 라는 메시지가 출력되고 `CopyWithPivot.pptx` 파일이 생성됩니다. PowerPoint에서 파일을 열면 복사된 Excel 범위가 원본 워크시트와 동일하게 표시되며, 슬라이드 내에서 새로 고칠 수 있는 활성 피벗 테이블이 포함됩니다.

## Common variations and edge cases

| Situation | What to change |
|-----------|----------------|
| **Multiple pivot tables** | 각 테이블마다 별도의 `Range` 객체를 정의하고 각각 `CopyRange`를 호출하거나, 동일한 데이터 소스를 공유한다면 전체 시트를 복사합니다. |
| **Large data sets** | 범위를 예를 들어 `"A1:Z5000"`처럼 확대합니다. `PasteOptions.CompressData = true`를 활성화하면 PPTX 크기를 줄일 수 있습니다. |
| **Different slide layouts** | PPTX로 저장한 뒤 PowerPoint에서 사용자 정의 레이아웃이나 테마를 적용합니다. 데이터는 그대로 편집 가능합니다. |
| **Saving to a stream** | 웹 API를 통해 PPTX를 반환해야 할 경우 `destinationWorkbook.Save(stream, SaveFormat.Pptx)`를 사용합니다. |
| **Preserving cell formatting** | `PasteOptions.PasteType = PasteType.All`을 설정하면 글꼴, 색상, 테두리 등 서식이 유지됩니다. |

**Pro tip:** `Save`를 호출하기 전에 대상 폴더가 존재하는지 항상 확인하세요. 폴더가 없으면 `Save`가 `DirectoryNotFoundException`을 발생시킵니다.

## Conclusion

이제 Aspose.Cells를 사용해 Excel에서 PowerPoint를 만들고, 피벗 테이블을 복사하며, 결과를 PPTX 파일로 내보내는 방법을 알게 되었습니다. 소스 워크북 로드, 범위 정의, `CopyPivotTables`와 함께 복사, PPTX로 저장하는 단계는 전체 워크플로우를 신뢰할 수 있게 해줍니다.

다음으로 **여러 워크시트를 PPTX로 내보내는 방법**이나 **여러 소스에서 데이터를 병합한 뒤 슬라이드 덱을 생성하는 방법**을 살펴보세요. 두 주제 모두 동일한 API를 기반으로 하며 복잡한 보고 파이프라인을 자동화하는 데 활용할 수 있습니다.

Happy coding, and enjoy turning your spreadsheets into polished presentations!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}