---
category: general
date: 2026-03-27
description: C#에서 Aspose.Cells를 사용하여 피벗 테이블을 만드는 방법 – 데이터를 추가하고, 새로 고침을 활성화하며, 워크북을
  xlsx 형식으로 저장하는 한 번의 튜토리얼.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: ko
og_description: Aspose.Cells를 사용하여 C#에서 피벗 테이블을 만드는 방법. 이 가이드는 데이터를 추가하고, 새로 고침을 활성화하며,
  워크북을 xlsx 형식으로 저장하는 방법을 보여줍니다.
og_title: C#에서 피벗 테이블 만들기 – 완전 Aspose.Cells 튜토리얼
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#에서 피벗 테이블 만드는 방법 – Aspose.Cells를 활용한 완전 가이드
url: /ko/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#에서 피벗 테이블 만들기 – 완전한 Aspose.Cells 튜토리얼

COM interop과 씨름하지 않고 C#에서 **피벗 테이블을 만드는 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 많은 데이터 기반 애플리케이션에서 원시 판매 데이터를 깔끔한 요약으로 빠르게 전환해야 하는데, Aspose.Cells가 이를 손쉽게 해줍니다.  

이 튜토리얼에서는 모든 단계를 차근차근 살펴봅니다: 데이터 추가, 피벗 테이블 구축, 자동 새로 고침 활성화, 그리고 마지막으로 **save workbook as xlsx** 하여 사용자가 즉시 Excel에서 열 수 있도록 합니다. 끝까지 진행하면 바로 사용할 수 있는 `PivotRefresh.xlsx` 파일과 각 코드 라인이 왜 중요한지에 대한 확실한 이해를 얻게 됩니다.

## Prerequisites

- .NET 6+ (or .NET Framework 4.7.2 and later) – 최신 런타임이면 모두 동작합니다.  
- Aspose.Cells for .NET – NuGet(`Install-Package Aspose.Cells`)에서 가져올 수 있습니다.  
- C# 문법에 대한 기본적인 이해 – 깊은 Excel 지식은 필요 없습니다.

> **Pro tip:** 기업용 컴퓨터를 사용 중이라면 Aspose 라이선스가 적용되어 있는지 확인하세요. 그렇지 않으면 생성된 파일에 워터마크가 표시됩니다.

## Step 1 – How to Add Data to a New Workbook

피벗이 존재하려면 먼저 원본 테이블이 있어야 합니다. 새 워크북을 만들고 첫 번째 워크시트 이름을 *SalesData* 로 지정한 뒤, 실제 판매 데이터를 흉내낸 몇 개의 행을 삽입합니다.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Why this matters:**  
- `PutValue` 를 사용하면 셀 유형이 자동으로 설정되어 나중에 문자열과 숫자 형식 불일치에 신경 쓸 필요가 없습니다.  
- 1행에 헤더를 정의하면 피벗 엔진이 필드를 매핑할 때 참조할 대상이 생깁니다.

## Step 2 – Create a Worksheet that Will Host the Pivot Table

피벗 테이블은 자체 시트에 존재하므로 원본 데이터를 깔끔하게 유지하고 보고서를 정돈된 형태로 제공합니다.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **What if you already have a sheet?** 새 시트를 추가하는 대신 `workbook.Worksheets["MySheet"]` 와 같이 인덱스로 기존 시트를 참조하면 됩니다.

## Step 3 – Define the Source Range (How to Add Data → Define Range)

Aspose.Cells는 헤더와 데이터를 모두 포함하는 `CellArea` 혹은 범위 문자열이 필요합니다. 여기서는 최대 100행을 가정했으며, 필요에 따라 조정하세요.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Edge case:** 데이터 집합이 동적이라면 `salesDataSheet.Cells.MaxDataRow` 로 마지막 사용 행을 계산하고 그에 맞게 범위를 구성할 수 있습니다.

## Step 4 – How to Create Pivot – Insert the Pivot Table

이제 재미있는 부분입니다. 방금 정의한 범위에 연결된 피벗을 Aspose.Cells에 생성하도록 지시합니다.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

`=SalesData!A1:D100` 와 같은 수식 스타일 참조를 사용합니다. 이는 Excel에 직접 입력하는 구문과 동일해 API 사용이 직관적입니다.

## Step 5 – Configure Row, Column, and Data Fields (How to Add Data → Fields)

*Region* 을 행에, *Product* 를 열에, 그리고 *Units* 와 *Revenue* 를 합계로 배치합니다.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Why these indices?**  
Aspose.Cells는 열 인덱스를 0부터 시작하므로 `0` 은 *Region* 을 가리킵니다. `DataFields.Add` 메서드를 사용하면 필드 이름을 (예: “Sum of Units”) 바꾸고 집계 유형을 지정할 수 있습니다 – 숫자 데이터에는 `Sum` 이 가장 일반적입니다.

## Step 6 – How to Enable Refresh – Make the Pivot Auto‑Update on Open

원본 데이터가 나중에 변경되면 피벗도 자동으로 업데이트되길 원할 것입니다. 바로 `RefreshDataOnOpen` 옵션이 그 역할을 합니다.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Note:** 이 플래그는 워크북을 Excel에서 열 때만 작동합니다. Aspose.Cells 내부에서 재계산하려면 `pivotTable.RefreshData()` 를 직접 호출해야 합니다.

## Step 7 – Save Workbook as XLSX (How to Save Workbook as XLSX)

마지막으로 파일을 디스크에 저장합니다. `.xlsx` 형식은 현대적인 zip 기반 Excel 파일 형식으로 어디서든 호환됩니다.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

프로그램을 실행하면 실행 폴더에 **PivotRefresh.xlsx** 라는 파일이 생성됩니다. Excel에서 열면 *Region* 행, *Product* 열, 그리고 합계된 *Units* 와 *Revenue* 값이 깔끔하게 정렬된 피벗을 확인할 수 있습니다. 자동 새로 고침을 활성화했기 때문에 *SalesData* 시트를 수정하면 다음에 워크북을 열 때 피벗이 자동으로 업데이트됩니다.

### Expected Output

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(추가한 행에 따라 숫자는 달라질 수 있습니다.)*

---

## Common Questions & Variations

### What if I need multiple pivot tables?

**Step 4** 를 다른 이름과 위치로 반복하면 됩니다. `PivotTables.Add` 호출마다 새로운 인덱스가 반환되며, 이를 사용해 해당 테이블 객체를 가져올 수 있습니다.

### How do I change the aggregation to *Average* instead of *Sum*?

`DataFields.Add` 호출에서 `PivotTableDataAggregationType.Sum` 을 `PivotTableDataAggregationType.Average` 로 교체하면 됩니다.

### Can I style the pivot (fonts, colors)?

가능합니다. 피벗을 만든 뒤 `Style` 속성에 접근하거나 피벗이 포함된 범위에 셀 서식을 적용하면 됩니다. 예시:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Is it possible to add more rows after the workbook is saved?

물론입니다. `new Workbook("PivotRefresh.xlsx")` 로 파일을 로드하고 *SalesData* 시트에 행을 추가한 뒤 `pivotTable.RefreshData()` 를 호출하고 다시 저장하면 됩니다.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

파일을 저장하고 실행한 뒤 생성된 **PivotRefresh.xlsx** 를 열어 보세요 – 이제 **how to create pivot** in C# 를 완벽히 마스터했습니다.

---

## Wrapping Up

우리는 **how to create pivot** 테이블을 프로그래밍 방식으로 만드는 방법, **add data**, **enable refresh**, 그리고 Aspose.Cells를 사용해 **save workbook as xlsx** 하는 방법을 모두 다뤘습니다. The code

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}